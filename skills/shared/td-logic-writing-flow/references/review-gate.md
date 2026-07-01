# Review Gate

用独立 reviewer 检查成文质量。目标不是再写一遍，而是发现 writer 自己看不见的问题。

## 触发条件

默认触发独立审查：

- 新写、重写、大改。
- 带图文章。
- 技术事实、项目认知、健康/医美、财务、两性策略、职业判断等高影响文章。
- 用户明确要求 review、审查、把关。
- writer 自审发现标题链、事实来源、视觉结构不稳。

不强制触发：

- 错别字、小句润色、局部压缩。
- 用户明确要求只做快速改动。

## Reviewer 输入原则

Reviewer 只看审查所需的最小上下文。不要把完整聊天历史交给 reviewer。

给 reviewer：

- `review-packet.md`
- `article.md` 或文章路径
- `td-logic-writer/references/review-checklist.md`
- 带图时附上 visual QA checklist 或图片路径

不要给 reviewer：

- writer 的中间推理。
- 完整聊天记录。
- 用户情绪反馈。
- 预期答案。
- writer 对文章的自我辩护。

## 临时文件

默认使用临时目录，不写进 Obsidian：

```text
/tmp/td-logic-review/<slug>/
  review-packet.md
  article.md
  review-report.md
```

`<slug>` 使用文章名或任务名的安全短名。用户明确要求留痕时，才把 report 保存到 vault。

## Writing Review Packet

`review-packet.md` 必须足够让 reviewer 独立判断：

```markdown
# Writing Review Packet

## Article Goal
[这篇文章要解决什么判断问题]

## Reader
[默认：未来的自己；如果公开发布或给团队看，写清楚]

## Writing Constraints
- Obsidian 文件名已经是标题，不重复总 H1。
- 不默认加“一句话结论”“核心摘要”“总结”章节。
- 领域概念用加粗，如 **TenantID**；代码字段用反引号，如 `sid`。
- 标题链要递进；每节只回答一个问题。
- 不写 AI 总结，不把文章写成百科、SOP、培训材料。

## Fact Sources
- [文章本身]
- [必要代码、proto、DB、旧文档、截图、图片路径、用户确认事实]
- [未知但不阻塞的假设]

## Article
[文章路径，或粘贴正文]

## Review Criteria
- td-logic-writer/references/review-checklist.md
- 带图时检查 visual QA
```

## Reviewer Prompt

Spawn reviewer 时使用这种任务，不夹带结论：

```text
You are an independent article reviewer. Do not edit files.

Read:
- /tmp/td-logic-review/<slug>/review-packet.md
- /tmp/td-logic-review/<slug>/article.md
- /path/to/td-logic-writer/references/review-checklist.md

Write only:
- /tmp/td-logic-review/<slug>/review-report.md

Judge the article against the packet and checklist. Do not use prior chat context. Do not infer hidden intent.
```

## Review Report

`review-report.md` 使用固定格式：

```markdown
# Review Report

## Verdict
pass | minor | structural | factual | visual | blocked

## Findings
- [severity] [位置] [问题] [为什么影响判断/阅读/事实准确性]

## Required Fixes
- [必须改什么]

## Optional Improvements
- [可改可不改]

## Residual Risk
[仍不确定或需要用户确认的点；没有写“无”]
```

## 结论分级

| Verdict | 含义 | 处理 |
| --- | --- | --- |
| `pass` | 可交付 | 汇报通过和剩余风险 |
| `minor` | 小问题 | writer 直接修，不必退回骨架 |
| `structural` | 标题链、章节职责、文章任务错误 | 退回骨架，不继续润色 |
| `factual` | 事实来源不足或疑似错误 | 暂停写作，查证或问用户 |
| `visual` | 图文重复、图过大、PPT 化、割裂 | 重画、缩图、删重复文字 |
| `blocked` | 目标、读者、事实或边界不清 | 停止，向用户汇报阻塞点 |

## 两轮熔断

最多两轮：

```text
writer 写完
→ reviewer 审
→ writer 修
→ reviewer 复审一次
→ 仍非 pass/minor：熔断
```

熔断后不要继续硬改。输出：

- 当前 verdict。
- 卡点类型。
- reviewer 的关键发现。
- 需要用户确认的问题或需要查证的事实。

## Writer 修复规则

- 小问题：直接修文章。
- 结构问题：先改骨架，再改正文。
- 事实问题：先验证事实，不用文字绕过。
- 视觉问题：先改图文分工，再改段落。
- reviewer 只负责判定；writer 负责修复。
