# CodeBuddy 调用

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

## 输出与停止

从 system/init 等事件取得 session_id；result 的 subtype、is_error 与最终文本共同判断本轮结果。result/success 也可能只是模型正常报告了工具拒绝，必须检查真实交付。

以上前台调用使用主控执行句柄停止并等待，核对本次子进程。若另选原生后台模式，先查本机 --bg、logs、stop 帮助，记录后台任务 ID；不要把前台 --print 与后台模式想当然混用。本方案未依赖后台服务。

依据：[官方说明](https://www.codebuddy.cn/docs/cli/cli-reference)；参数以本机 --help 为准。

## 验证边界

本机核对版本：2.171.0。已有隔离读写、明确会话 ID 恢复与前台调用取消证据；不是所有模型、操作系统或权限组合的兼容承诺。升级或改变授权参数后，先做对应的小任务验证。

隔离验证使用了 --setting-sources ''、--strict-mcp-config 和空 mcpServers 配置；写任务使用 acceptEdits。实测 dontAsk 下即使传入 --allowedTools Read,Write，仍可能拒绝 Write。--tools 也不能仅凭 init 列表证明工具限制生效；严格只读任务应使用经验证的权限隔离，未验证时报告限制，不把 Prompt 当沙箱。

前台取消实测可能仍返回退出码 0；保留取消操作及停止证据，不据此宣布任务成功。
