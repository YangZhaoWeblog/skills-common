# Codex 调用

以下是 Bash 数组示例：主控先按调用方指定的 executor 设置 cli 数组，包含已核实的可执行文件与转发前缀；原生入口无前缀，包装器可能要求独立的 --。cwd、model、effort、run_dir、session_id 均来自本次选择和运行记录，不执行配置文本。task.txt 已含角色正文、项目规则入口与任务；使用 stdin 避免命令插值。

## 启动与恢复

```bash
umask 077
cd "$cwd" || exit 1
"${cli[@]}" exec --json --sandbox workspace-write --model "$model" \
  -c "model_reasoning_effort=\"$effort\"" - \
  < "$run_dir/task.txt" > "$run_dir/events.jsonl" 2> "$run_dir/stderr.log"
```

只读任务将 sandbox 改为 read-only；授权工作目录不是 Git 仓库时，初始 `exec` 和每次 `resume` 都须显式加 `--skip-git-repo-check`；Git 仓库不加此参数。写权限只用于已批准范围；不要默认用 danger-full-access。

```bash
"${cli[@]}" exec --sandbox workspace-write resume "$session_id" --json \
  --model "$model" -c "model_reasoning_effort=\"$effort\"" - \
  < "$run_dir/followup.txt" > "$run_dir/resume.jsonl" 2> "$run_dir/resume.stderr"
```

恢复时仍在原 cwd；sandbox 放在 resume 前，模型、effort 显式重传。不用 --ephemeral，否则无法依赖持久会话恢复。

## 运行中反馈：app-server 双向连接

预计长任务会收到追加意见时，可在主控的执行工具能**同时持有 stdin/stdout 和运行句柄**的前提下，用原生 app-server 保持连接。先按本次调用核对 `codex app-server --help` 和包装器转发；`--listen stdio://` 必须接到可双向读写的句柄。单纯把 stdout/stderr 重定向到文件而不持有 stdin，不能发送反馈。下例中的尖括号是占位符，发送前须用本次调用的 cwd、model、effort 及已授权的 approvalPolicy、sandbox 替换为合法 JSON 值；不据此改变角色或授权。

```bash
cd "$cwd" || exit 1
"${cli[@]}" app-server --listen stdio://
```

在同一 stdin/stdout 连接上按 JSON-RPC 行协议**顺序**交互：发送 `initialize` 后先等成功响应，再发 `initialized`；随后每个请求都等匹配的响应 ID，并从响应读取 thread／turn ID，再发送下一请求。不要一次性盲发以下多行。按本机原生 schema 核对方法与参数；若所用实验方法要求实验 API，在 initialize 参数中声明 `capabilities.experimentalApi: true`。

```json
{"id":1,"method":"initialize","params":{"clientInfo":{"name":"external-agent","title":"External Agent","version":"1.0"}}}
```

等待 `id:1` 成功响应，再发通知：

```json
{"method":"initialized","params":{}}
```

随后依次请求；每次等对应 `id` 的响应。`thread/start` 的响应提供后续使用的 thread ID：

```json
{"id":2,"method":"thread/start","params":{"cwd":"<cwd>","model":"<model>","approvalPolicy":"<approvalPolicy>","sandbox":"<sandbox>"}}
```

收到 thread ID 后，启动 turn 并保存响应中的活动 turn ID：

```json
{"id":3,"method":"turn/start","params":{"threadId":"<threadId from response>","input":[{"type":"text","text":"<task prompt; require an explicit ACK <feedback ID> and handling result for each later feedback; do not repeat completed work>"}],"effort":"<effort>"}}
```

`turn/start` 继承 `thread/start` 的 approvalPolicy 与 sandbox；本例不设置 turn 级权限覆写。

保存 `thread/start` 返回的 thread ID 和 `turn/start` 返回的活动 turn ID。运行中追加带编号的意见：

```json
{"id":4,"method":"turn/steer","params":{"threadId":"<threadId>","expectedTurnId":"<activeTurnId>","input":[{"type":"text","text":"Feedback F001: <feedback>. Explicitly reply ACK F001 and report how you handled it; do not repeat completed work."}]}}
```

RPC 成功响应只证明请求被接受；继续读同一连接的事件，直到 Agent 对 F001 明确 ACK／给出处理结果，并等待该轮终态。`turn/steer` 不会撤销已启动的工具命令，仍须核对其结果。若返回 `no active turn to steer`，先查询线程状态，再在同一线程用 `turn/start` 开新轮。`expectedTurnId` 失效或其他错误时也先查当前状态再决定动作，禁止盲目重发。可用以下 `thread/read` 查询当前状态与轮次；`includeTurns:true` 返回 turns，按其 ID 和状态确认是否仍有活动轮次：

```json
{"id":5,"method":"thread/read","params":{"threadId":"<threadId>","includeTurns":true}}
```

线程状态为持久时，`thread/queue/add` 可在当前轮结束后启动后续轮，须按当前原生 schema 核对是否需启用 experimental API；保持连接并等待每轮的 ACK／结果。ephemeral thread 不支持 queued submissions。排队成功本身不是已收到或已处理的证明。

若执行句柄无法双向通信，改用任务中约定的固定文件检查点，或在进程结束后按上节用明确 thread ID resume；检查点只读新增／未处理的编号反馈，文件更新不会唤醒 Agent。原 `exec`／`resume` 流程仍适用于批任务。

## 输出与停止

### 批量 `exec --json`

JSONL 中的 `thread.started`、`turn.completed`、`turn.failed` 是 exec 事件名；`thread.started` 提供 thread ID。核对最终事件、退出状态、stderr、公开回复和交付。完整 JSONL 留本机，默认不把推理内容读回主控。

### 持续 app-server 连接

JSON-RPC 通知名使用斜线：`thread/started`、`turn/started`、`turn/completed`。从 `turn/completed` 读取 `params.turn.status`：`completed` 才是成功终态，`failed` 和 `interrupted` 是非成功终态，`inProgress` 仍须等待。若 `error` 标有 `willRetry:true`，它不是最终失败；继续收事件直到轮次终态。持续连接按事件等待而非高频轮询。将反馈编号与 ACK／处理结果对应记录；终态无 ACK 时，先查公开回复和线程状态；仍无法确认则标为未确认，在原线程只发一次收件／处理核对，不重复业务。核对轮次终态后仍无确认则报告未确认，不无限等待或盲目重投。长日志只读新增或未处理片段。

任务正常收尾时，确认所有反馈已处理且线程没有活动 turn，再关闭本次连接并等待其进程退出。用户要求停止时，使用本次 `threadId` 和当前 `turnId` 调用 `turn/interrupt`，等待实际终态并核对本次所属子进程。`turn/completed` 的状态为 `interrupted` 才记录为已中断；若取消与正常完成／失败竞争，查询并记录实际终态，不强等中断、不伪造取消成功。关闭连接本身不证明 turn 已停止。若状态或子进程无法确认，暂停冲突写入并报告未知。

批量 `exec` 前台取消使用持有的执行句柄并等待退出，核对本次所属子进程；不要按名称杀所有 Codex 进程。

依据：[官方 app-server 文档](https://developers.openai.com/codex/app-server)（包含 turn/steer 与 thread/read）；[非交互说明](https://developers.openai.com/codex/noninteractive)。参数以本机原生 app-server schema 和 CLI 帮助为准。

## 验证边界

本机核对版本：tcodex 0.1.4／Codex 0.154.0。单次核验确认此组合支持 app-server steer、持久线程排队后续轮次、固定文件检查点及明确 thread ID resume；不证明全部包装器、模型、权限组合或运行环境均支持，也未形成性能结论。升级或改变授权参数后，先做对应的小任务验证。
