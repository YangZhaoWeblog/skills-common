# DeepSeek Harness（DSH）调用

Bash 示例中的 cli 是调用方指定的 executor 对应的命令及已核实转发前缀数组，原生入口为 dsh。其余变量由主控设置；task.txt 包含角色正文、项目规则入口与任务。

## 模型、权限与凭据

先核对本机 `dsh --version`、`dsh --profile headless --help`。headless 的模型和 effort 通过 `--patch` 配置，不能传 `--model`、`--effort`。在仓库外私有 run_dir 中，用结构化写入工具或 YAML/JSON 序列化器生成 invocation.yaml；以下为结构示意，值来自本次已明确的选择：

```yaml
- id: agent-default-model
  config:
    provider: <provider>
    model: <model>
    reasoningEffort: <effort>
```

DSH patch 替换整段 config，三个字段须一起填写。官方 Flash 1017 的模型 ID 为 `deepseek-flash`；官方路由支持 `off`、`low`、`high`、`max`，`medium` 不可直接映射。只核对本次选择块，不输出完整配置或凭据。

`permission_mode` 按任务选择 `read-only` 或 `workspace-write`，通过 `DSH_PERMISSION_MODE` 传入。已有 patch 可能覆盖权限配置，须核对冲突和实际隔离效果。

凭据按可用的官方入口选择，保持用户指定的模型和 effort：

- **API Key**：provider 为 `deepseek-official`，由 `DEEPSEEK_API_KEY` 或已配置的 credentials 服务提供凭据；缺失时报告 `MISSING_CREDENTIAL`。
- **Desktop 登录账号**：provider 为 `deepseek-account`。headless 默认关闭账号组件；复用已有登录时，在 invocation.yaml 追加下方覆盖。已有配置显式禁用凭据时，先核对其原因和本次授权。未登录返回 `ACCOUNT_SIGN_IN_REQUIRED`；账号 token 不等于 API Key。

```yaml
- id: credentials
  disabled: false
- id: authorization
  disabled: false
- id: deepseek-account
  disabled: false
```

覆盖只用于本次调用，不改长期配置；组件自行读取已有凭据，无需复制或输出 token。

## 启动与恢复

```bash
umask 077
cd "$cwd" || exit 1
DSH_PERMISSION_MODE="$permission_mode" "${cli[@]}" --profile headless \
  --patch "$run_dir/invocation.yaml" --json - \
  < "$run_dir/task.txt" > "$run_dir/events.jsonl" 2> "$run_dir/stderr.log"
```

`-` 从 stdin 读取任务。

```bash
DSH_PERMISSION_MODE="$permission_mode" "${cli[@]}" --profile headless \
  --patch "$run_dir/invocation.yaml" --json --session-id "$session_id" - \
  < "$run_dir/followup.txt" > "$run_dir/resume.jsonl" 2> "$run_dir/resume.stderr"
```

恢复时回到原 cwd，重传模型、effort、凭据路由和权限设置。`session.cwd` 是规范化路径，可核对符号链接差异。`--session-id` 拒绝未知 ID、不同 cwd、带 Agent preset、子 Agent 或 fork 来源的会话；本流程仅恢复主控自己启动且已停止执行的 headless 会话。

## 输出与停止

`--json` 输出逐行事件，但本机账号路由会在 stdout 混入 `[llm-deepseek-account] model listing ...` 普通日志。保留原始输出，逐行尝试 JSON 解析；已知普通日志单独归档，其他无法解析的行标为诊断，缺少必要事件时判为未验证，不能静默当成功。

- `session.sessionId` 是恢复标识；`tool_call`、`tool_result` 是工具证据。
- `status` 中 `phase=turn_end` 的 `reason.kind=completed`、`final` 与正常退出共同证明本轮正常结束；`final` 本身不表示成功。`error` 或错误终态须检查。
- 流中可能含 `thinking`；默认仅提取 session、终态、最终文本及必要工具错误。
- 工具拒绝后模型仍可能正常结束并退出 0；bash 的 `tool_result.status=completed` 也可能包含命令退出码 1。核对工具结果中的错误、真实文件与任务 AC，不能只看事件 status 或模型自述。

前台调用通过持有的执行句柄停止，等待退出并核对所属子进程。**SIGTERM 停止可能退出 0**，应记录为主控取消；不能据此当作任务完成。

依据：[官方 CLI 说明](https://github.com/deepseek-ai/deepseek-harness/blob/master/apps/cli/README.zh.md)、[CLI 行为参考](https://github.com/deepseek-ai/deepseek-harness/blob/master/apps/cli/reference/README.zh.md)、[官方模型 ID](https://api-docs.deepseek.com/quick_start/pricing/)。在线文档与安装版可能不同，以本机帮助、打包实现及实际验证为准。

## 验证边界

本机核对版本：0.2.1-rc.3。已用 `deepseek-flash` / `high`、Desktop 账号路由及本次覆盖配置验证：stdin 派发、JSON 事件、隔离目录读写、精确会话 ID 恢复、未知 ID 与错误 cwd 拒绝、文件工具和 bash 的只读写入拒绝、前台 SIGTERM 后父子进程退出。独立只读核验已复查原始日志和文件产物。

模型与 effort 证据为显式请求配置，JSON 事件没有对应服务端回执。API Key 路由本轮只观察到缺失凭据错误，未验证其成功调用；Windows、其他模型、升级权限、其他沙箱后端与其他版本不在本次验证范围。升级或改变路由、权限后，先做对应小任务验证。
