---
name: td-logic-writing-flow
description: Route and control MyDigitalGarden/Obsidian writing tasks with a logic-first, concise, no-fluff workflow. Use when the user asks to write, rewrite, restructure, polish, de-AI, outline, review, or continue an Obsidian article or personal knowledge note, especially when deciding whether the task belongs to td-logic-writer, knowledge-illustrator, imagegen, tech-doc-writer, atomic notes, MOC, deep-learn/light-learn, DAG, or casual idea capture. It enforces stage control, skeleton-first gates for new/rewrite/large edits, visual QA for illustrated articles, independent Review Gate for substantial/high-impact articles, and routing back to the right skill instead of blindly generating a full article.
---

# TD Logic Writing Flow

写作总控，不是另一个 writer。先判断任务属于哪条生产链路，再决定是否调用 `td-logic-writer`、`knowledge-illustrator`、`imagegen`、`tech-doc-writer` 或其他知识类 skill。

## Core Question

拿不准时回到这一句：

**这篇文章是不是为了帮助未来的自己判断、选择、负责、止损？**

是：进入 `td-logic-writer`。

否：按文章真实任务分流，不要硬写成判断文。

## Stage Control

先判断当前阶段，再行动：

| 阶段 | 行为 |
| --- | --- |
| 讨论 | 只澄清边界、目标、读者和取舍，不写完整文章 |
| 骨架 | 只给标题链和每节回答的问题 |
| 成文 | 按确认后的骨架写正文 |
| 修改 | 先读现文和用户改动，再局部或整体修改 |
| 复盘 | 提取正反模式，反哺 skill 或写作规则 |
| 审查 | 用最小上下文 Review Gate 做独立审查 |

新写、重写、大改默认先给标题链。用户明确说“直接写”时可以跳过确认，但仍先用 3-5 行说明判断出的文章任务和骨架方向。

Obsidian 文件名通常已经是页面标题。给骨架时不要再生成文章总 H1，也不要默认添加“一句话结论”章节；如果需要先给主线，用正文开场短段承载，然后从一级章节标题开始。

## Routing

| 任务 | 去向 |
| --- | --- |
| 判断系统型文章：概念边界、项目认知、判断标准、决策调研、个人策略 | `td-logic-writer` |
| 正式技术方案、报告、调研报告、测试报告、操作手册 | `tech-doc-writer` |
| 原子笔记：单一概念定义、上下位关系、短连接 | 原子笔记链路，不走 writer |
| MOC / 知识地图 | MOC 链路，不走 writer |
| deep-learn / light-learn / DAG 系列 | 对应学习内容链路，不走 writer |
| 精确关系图、流程图、层级图、边界图、映射图 | `knowledge-illustrator` |
| 封面、氛围图、真实场景、bitmap visual asset | Codex system `imagegen` |
| 普通灵感记录 | 轻量整理即可，除非用户要求升级成策略/判断文 |

## Interaction Rules

- 不在用户还在讨论时提前生成完整文章。
- 不把“骨架”写成正文。
- 不把 Obsidian 文件名重复成正文标题。
- 不把“一句话结论”当默认章节；结论先行只适用于需要它的文档，不是个人知识文章的固定格式。
- 输出骨架、评审意见或正文片段时，领域概念用加粗，如 **TenantID**、**SID + OrgID**；只有代码字段、命令、路径用反引号，如 `sid`、`orgId`。
- 不为了显得完整而扩展范围。
- 不把已有好句子改成更平但更像 AI 的表达。
- 如果用户给了现文、截图、链接或 Obsidian URI，先读再判断。
- 如果用户用截图反馈“割裂、不舒服、不好看”，优先判断视觉中心、分块、密度和载体选择；不要先润色句子。
- 如果事实会影响核心判断，先验证；不能验证时标注假设或向用户确认。

## Diagram Routing

精确关系、流程、边界、映射图默认交给 `knowledge-illustrator`。这些图需要 deterministic structure，不要用 `imagegen` 猜。

`imagegen` 只用于 bitmap 类视觉资产：封面、氛围、实物感场景、插画、照片风格图。当前 Codex 环境里它是系统 skill，默认走内置 `image_gen`；只有 CLI/API fallback 才需要 `OPENAI_API_KEY`。

配图前先说明图要表达什么。配图后检查文字是否能瘦身。

## Visual QA

带图文章必须做视觉检查：

- 图是否重复了章节标题？
- 图是否重复了前后段落？
- 图是否过大，像 PPT 截图而不是文章内嵌图？
- 图是否抢走正文注意力？
- 图和它支撑的文字是否在同一认知区域？
- 图能表达的关系，正文是否已经删掉或压缩？
- 大章节之间是否需要 `---` 减少割裂感？

不能截图或预览时，也要按以上 checklist 自检。

## Review Gate

新写、重写、大改、高影响文章或带图文章完成后，读取 [review-gate.md](references/review-gate.md)，按其中的 `Writing Review Packet` 启动独立 reviewer。

独立性来自最小上下文，不来自 reviewer skill。reviewer 只读 packet、article、checklist，不读完整聊天，不看 writer 中间推理，不直接改原文。

小改、错别字、局部压缩不强制独立审查；仍要做 writer 自审。

## Boundary With Other Writing Skills

`tech-doc-writer` 服务正式决策：方案、报告、调研、测试报告、操作手册。

`td-logic-writer` 服务个人理解和复用：判断框架、概念边界、项目认知、个人策略。

不要把正式报告写成个人判断文，也不要把个人判断文写成正式方案。
