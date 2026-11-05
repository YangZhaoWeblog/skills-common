# Claude Code 调用

Bash 示例中的 cli 是调用方指定的 executor 对应的可执行文件及已核实转发前缀数组；包装器转发用独立参数，不能把整条命令当成一个字符串。cwd、model、effort、run_dir 与 session_id 由主控设置。task.txt 包含角色正文和项目规则入口，不依赖 --agent 自动发现项目角色。

## 启动与恢复

```bash
umask 077
cd "$cwd" || exit 1
"${cli[@]}" -p --model "$model" --effort "$effort" \
  --output-format stream-json --verbose --permission-mode acceptEdits \
  < "$run_dir/task.txt" > "$run_dir/events.jsonl" 2> "$run_dir/stderr.log"
```

acceptEdits 仅用于获准文件修改，不等于授权全部 shell 命令。按任务限制工具并明确批准必要命令；非交互模式无法弹出审批时可能拒绝工具。不要以 bypassPermissions 或全局跳过权限解决拒绝。

```bash
"${cli[@]}" -p --resume "$session_id" --model "$model" --effort "$effort" \
  --output-format stream-json --verbose --permission-mode acceptEdits \
  < "$run_dir/followup.txt" > "$run_dir/resume.jsonl" 2> "$run_dir/resume.stderr"
```

恢复时重传已核实的工具/权限参数，保持原 cwd。只读任务按当前 CLI 能力禁用写工具或限定读取工具；纯文本任务可禁用所有工具，但须核对实际生效。保留会话存储，不用 --no-session-persistence、--continue 或 --fork-session 代替明确恢复。

## 运行中反馈：先核对持续输入

Claude Agent SDK 的[官方 streaming 与 single-mode 指南](https://code.claude.com/docs/en/agent-sdk/streaming-vs-single-mode)建议：长任务需要中途追加输入时使用持续 streaming input。该建议不证明本机 `tclaude` 包装器支持相同能力。首次使用或包装器升级后，先核对当前 `tclaude --help`、`--input-format stream-json` 的参数转发，以及执行句柄能否在进程运行时持续写 stdin；再用无工具、只读的小任务验证追加输入能被收到并按编号回复。按帮助和官方协议使用其要求的输入帧，不套用 Codex app-server 的方法或 JSON 格式。

如果参数、stdin 持有或反馈送达任一项未核实，使用上节已知的 `-p` 与明确 `--resume` 流程作为后续反馈入口，或安排固定文件检查点。等待对应编号的明确 ACK／处理结果；提交或排队成功不代表 Agent 已收到。文件更新不会唤醒 Agent，任务结束后需显式恢复。

仅从 stdin 接收 `stream-json` 时，使用持续打开的管道。裸 PTY 可能被 `--print` 判断为没有输入，PTY 行缓冲还可能截断较长的 JSON；短 `Hello` 成功不能证明真实任务能完整送达。主控工具若只能持有 PTY，在本次专属 PTY 关闭行缓冲和回显，通过输入桥接接入 CLI 管道，并核对实际任务长度、多字节文本的编号回执。正常收尾关闭本次输入端并等待退出，不因某轮 `result/success` 就认为整个会话已结束；不停止共享网关。

## 输出与停止

从 system/init 等事件取得 session_id；result 的 subtype、is_error 与最终文本共同判断本轮结果。result/success 也可能只是模型正常报告了工具拒绝，必须检查真实交付。

以上前台调用使用主控执行句柄停止并等待，核对本次子进程。若另选原生后台模式，先查本机 --bg、logs、stop 帮助，记录后台任务 ID；不要把前台 --print 与后台模式想当然混用。本方案未依赖后台服务。

依据：[官方说明](https://code.claude.com/docs/en/headless)；参数以本机 --help 为准。

## 验证边界

本机核对版本：2.1.295。已有隔离读写、明确会话 ID 恢复与前台调用取消证据；不是所有模型、操作系统或权限组合的兼容承诺。升级或改变授权参数后，先做对应的小任务验证。

隔离验证使用了 --bare、--setting-sources ''、--strict-mcp-config 和空 mcpServers 配置，以及 Read,Edit,Write 工具集合。--bare 会跳过 CLAUDE.md 自动发现与部分用户设施，使用时必须显式给出角色及项目规则；不要未经判断作为普通项目的默认。仅设置 --allowedTools 并不证明工具可用，检查 init 中的工具和实际调用结果。
