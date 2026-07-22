---
name: td-logic-writer
description: Write or revise concise, logical, no-fluff judgment-system articles for personal knowledge work. Use when the user wants to turn messy notes into a reusable judgment framework, concept boundary article, project cognition article, decision research note, or personal strategy article across technical, career, health/beauty, relationship, life-decision, or similar domains. Direct invocation is allowed when explicitly named; otherwise prefer td-logic-writing-flow to route broader Obsidian/MyDigitalGarden writing tasks. Do not use for atomic notes, MOC maps, deep-learn/light-learn lessons, DAG learning paths, casual idea capture, or formal technical reports/plans handled by tech-doc-writer.
---

# TD Logic Writer

把混乱材料写成未来自己可复用的判断系统。文章的目标不是“讲完知识”，而是让读者下次更会判断、选择、负责、止损。

## Read First

写作、重写、大改时读取：

- [style-rules.md](references/style-rules.md)
- [writing-workflow.md](references/writing-workflow.md)
- [review-checklist.md](references/review-checklist.md)

只做快速审查时先读 [review-checklist.md](references/review-checklist.md)，必要时再读另外两份。

## Boundary

Use this skill when the article is doing sensemaking: turning facts, options, concepts, risks, or lived experience into a reusable judgment model.

典型对象：

- 概念边界文：讲清对象、关系、映射、误区。
- 项目认知文：讲清负责一个系统必须理解什么。
- 判断标准文：把“合格/优秀/不合格”压成可自检标准。
- 决策型调研文：把复杂选项压成原则、排序、执行路径。
- 个人策略文：医美、两性、职业、生活决策等，只要目标是形成判断框架。

不要用于：

- 原子笔记：只定义一个概念或关系。
- MOC / 知识地图：组织链接和知识网络。
- deep-learn / light-learn / DAG：学习型内容生产链路。
- 普通产品灵感：除非用户要升级成策略或判断文。
- 正式技术方案、报告、调研、测试报告：交给 **tech-doc-writer**。

拿不准时问一句：这篇文章是不是为了帮助未来的自己判断、选择、负责、止损？是，就使用本 skill；不是，转给更合适的写作链路。

## Core Rules

- 背景为先：先说明这篇文章解决什么混乱、边界或判断问题，再进入术语。
- 结构先于句子：先修标题链和章节职责，再润色文字。
- 标题链必须递进：后文依赖前文，不做百科式平铺。
- 一级标题不超过 8 个；超过说明范围过大，要拆文或压缩。
- 每节只回答一个问题；两个问题就拆，重复问题就合并。
- 保留用户原文里准确、有辨识度的人话；只删噪音，不磨成礼貌模板。
- 把用户纠正当作后续写作约束：术语、事实、范围、风格一经确认就全局传播，不重复犯错或反复确认。
- 重要概念、字段、路径和关键判断统一用加粗；可执行代码只放代码块。
- 图、表、文字要分工：文字写判断和后果，表格写稳定比较，图写关系、层级、流向、映射、边界。
- 如果图已经表达关系，正文只留一行锚点；不要重复解释。
- 正文做无损压缩：中心判断留正文，决策证据和长讨论移到旁路记录；不要靠直接删除细节制造“简洁”。
- 不写默认总结。总结只有在它产生新判断或行动清单时才保留。
- Obsidian 文件名已经是页面标题时，不要在正文重复总标题。
- 不默认创建“一句话结论”章节；需要提前显性化主线时，用开场短段，不新增格式化标题。

## Output Behavior

- 用户还在讨论方向时，只给判断、取舍和下一步，不直接写完整文章。
- 用户要骨架时，只给标题链和每节回答的问题，不填正文。
- 用户要重写或大改时，先读现文和用户改动，保留好句子，再重构。
- 长任务维护最小纠正记录；正式文章不承载完整问答历史。
- 用户明确只改局部时，不顺手重写整篇。
- Obsidian 文章要保留 wikilink、frontmatter、图片嵌入、附件路径。
- 事实不确定时标注为假设；技术/项目事实要从代码、proto、DB、旧文档或用户材料验证。
