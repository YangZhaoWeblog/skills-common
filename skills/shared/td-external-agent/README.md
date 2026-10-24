# td-external-agent

在当前 **Codex** 或 **Claude Code** 会话中，可以通过 **CodeBuddy、tcodex 或 tclaude** 调用另一个独立 Agent。

例如，在 **Codex** 会话里通过 **tclaude** 启动独立 **Agent**，并让它使用 **Opus 5.5、DeepSeek-V4.1-Flash-1017** 等模型。

## 一、快速开始

1.1 **把外部 Agent 当 Coder**

```shell
$td-external-agent

用〈tcodex〉作为 Coder，按已批准的 Plan 编码并补测试，完成后报告。
模型用〈模型 ID〉，effort 用〈High〉。
```

1.2 **让另一个 Agent 独立审查**

```shell
$td-external-agent

用  {tclaude cli}  作为独立 review, 审阅本次需求代码, 完成后报告结果
+ 模型用 {模型 ID}
+ effort 用 {high}
```

派发前要明确 `<CLI, Model, Effort>` 三项；缺少任何一项，Skill 会先问你。

## 二、保存为项目角色

使用外部 Agent 后，可以把这次调用保存为项目角色，之后从项目入口直接复用。

> skill: 要把这次调用保存为项目里的 Coder 吗？我会一并添加角色配置和调用入口，记录 tcodex、〈模型 ID〉和 High，之后可直接复用。

**保存前，先展示要修改的文件和内容，得到你同意后再写入。**

不想保存就跳过，本次对话不再问。
