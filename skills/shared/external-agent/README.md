# External Agent

让主 Agent 通过 **Codex、Claude Code 或 CodeBuddy CLI** 执行任务，跟进结果、恢复会话或停止调用。支持独立使用，不依赖 Harness，也不限编码任务。

## 一、调用

准备好已安装、已登录的 CLI，然后告诉主 Agent：

> $external-agent 用 CodeBuddy 整理当前项目的公开 API，只读。模型用〈模型 ID〉，effort 用 medium。

替换模型 ID 即可。**CLI、模型、effort 缺什么问什么，不擅自默认。** 也可让主 Agent 读取已有角色配置；本次明确指令优先。操作范围由主 Agent 按任务和已有授权确定。

## 二、保存与续用

执行后可选择固化为角色 Agent。**先看具体改动，批准后才保存配置和入口**；下次从入口读取，无需重填参数。不保存就不写；拒绝后，本次会话不再提醒，已固化的调用也不重复提示。

继续任务时指定原会话，Agent 先检查已有产物，避免重复或覆盖修改。任务完成以实际验收为准；停止未确认时暂停冲突写入。

## 三、执行说明

[执行规则](SKILL.md) · [Codex](references/codex.md) · [Claude Code](references/claude.md) · [CodeBuddy](references/codebuddy.md)

调用方法与验证范围见对应平台说明。保存角色配置不授予后续任务写权限。
