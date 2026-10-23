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

只读任务将 sandbox 改为 read-only；非 Git 的已授权隔离目录可加 --skip-git-repo-check。写权限只用于已批准范围；不要默认用 danger-full-access。

```bash
"${cli[@]}" exec --sandbox workspace-write resume "$session_id" --json \
  --model "$model" -c "model_reasoning_effort=\"$effort\"" - \
  < "$run_dir/followup.txt" > "$run_dir/resume.jsonl" 2> "$run_dir/resume.stderr"
```

恢复时仍在原 cwd；sandbox 放在 resume 前，模型、effort 显式重传。不用 --ephemeral，否则无法依赖持久会话恢复。

## 输出与停止

thread.started 的 thread_id 是恢复标识；item 事件包含工具和公开回复；turn.completed 是成功轮次终态，turn.failed 或 error 要检查。成功还需进程退出及产物验收。完整 JSONL 留本机，默认不把推理内容读回主控。

这些示例是前台 exec，由主控保存执行工具的句柄并等待。取消使用该句柄，等待退出并核对本次所属子进程；不要按名称杀所有 Codex 进程。

依据：[官方非交互说明](https://developers.openai.com/codex/noninteractive)；参数以本机 exec --help、exec resume --help 为准。

## 验证边界

本机核对版本：0.154.0。已有隔离读写、明确会话 ID 恢复与前台调用取消证据；不是所有模型、操作系统或权限组合的兼容承诺。升级或改变授权参数后，先做对应的小任务验证。
