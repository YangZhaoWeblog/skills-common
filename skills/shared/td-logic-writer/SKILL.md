---
name: td-logic-writer
description: Write or revise concise, evidence-aware judgment articles for personal knowledge work. Use when the user wants to turn messy notes into a reusable concept boundary, project cognition, judgment standard, decision research note, or personal strategy across technical, career, health/beauty, relationship, life-decision, or similar domains. Direct invocation is allowed when explicitly named; otherwise prefer td-logic-writing-flow to route broader Obsidian/MyDigitalGarden writing tasks. Do not use for atomic notes, MOC maps, deep-learn/light-learn lessons, DAG learning paths, casual idea capture, or formal technical reports/plans handled by tech-doc-writer.
---

# TD Logic Writer

把混乱材料压成未来可复用的判断。目标不是讲完知识，而是让读者知道默认怎么选、什么会改变选择、下一步做什么。

## Read First

写作、重写、大改时读取：

- [style-rules.md](references/style-rules.md)
- [writing-workflow.md](references/writing-workflow.md)
- [review-checklist.md](references/review-checklist.md)
- [progression-modes.md](references/progression-modes.md)
- [current-content-integrity.md](references/current-content-integrity.md)

只做快速审查时先读 [review-checklist.md](references/review-checklist.md)，必要时再读另外两份。

## Boundary

Use this skill when the article is doing sensemaking: turning facts, options, concepts, risks, or lived experience into a reusable judgment model.

典型对象：

- 概念边界文：讲清对象、关系、映射、误区。
- 项目认知文：讲清负责一个系统必须理解什么。
- 判断标准文：把“合格/优秀/不合格”压成可自检标准。
- 决策型调研文：把复杂选项压成原则、排序、执行路径。
- 个人策略文：医美、两性、职业、生活决策等，只要目标是形成判断框架。
- 个人系统/决策文档：让未来的自己或会议参与者按同一原则运行时间、注意力、任务、资金或其他个人资源。

不要用于：

- 原子笔记：只定义一个概念或关系。
- MOC / 知识地图：组织链接和知识网络。
- deep-learn / light-learn / DAG：学习型内容生产链路。
- 普通产品灵感：除非用户要升级成策略或判断文。
- 正式技术方案、报告、调研、测试报告：交给 **tech-doc-writer**。

拿不准时问一句：这篇文章是不是为了帮助未来的自己判断、选择、负责、止损？是，就使用本 skill；不是，转给更合适的写作链路。

## 先选文章类型

不要把所有文章套进同一条标题链。

| 类型 | 读者最后要获得什么 |
| --- | --- |
| 概念边界 | 定义、边界、容易混淆的对象与使用后果 |
| 项目认知 | 责任边界、关键关系与负责人的判断点 |
| 判断标准 | 可复用的判断条件、反例与动作 |
| 证据型决策 | 默认选择、改变选择的条件、候选结论与停止条件 |
| 个人系统/决策文档 | 核心损失、根原则、判断流程、动作边界与反馈机制 |

具体骨架、证据位置和压缩步骤见 [writing-workflow.md](references/writing-workflow.md)。

## Core Rules

- 先写文章契约：读者、真实问题、默认选择或根定义、什么会改变它；不服务这些项的信息不进正文。
- 个人系统/决策文档要写清核心对象、关系和规则依据；涉及稀缺资源或持续承诺时，再说明容量边界与超载处理。
- 文件名必须准确覆盖全文的核心对象和范围；如果正文同时处理多个层次，不要用其中一个工具名、分类器或局部规则命名整篇文章。
- 复杂文章先确定阅读组织方式，如推导、比较、逐层理解、案例验证或并列查阅；按实际对象与读者任务组织，不固定四选一。
- 结构先于句子：先修标题链和章节职责，再润色文字。
- 标题链按对象关系和阅读依赖排序，同级标题保持相称的抽象层级；允许必要的并列分类，不强制逐节因果。中文线性长文、判断文章和项目认知文章的一级标题默认使用 `一、二、三、四` 编号，非线性内容、短笔记、局部小改或已有稳定格式不强制重排。
- 定义/决策型标题优先使用准确、精练、对象明确的词组；故事型可口语或悬念，操作手册可用动作。标题链呈现结构，不必复述结论，不设字数硬限；正反 schema 见 [style-rules.md](references/style-rules.md)。
- 文件名提供文章身份，一级标题呈现对象、层次和逻辑顺序；两者范围不一致时，回到骨架检查命名或组织。
- 标题层级连续；不要从一级标题直接跳到三级标题。
- 一级标题超过 8 个时检查范围、重复与导航负担；章节数是检查信号，不是拆文或删节的硬限。
- 每节只回答一个判断问题；同一结论的不同解释不要拆成多个章节。
- 一条关键判断只设一个主载体。其他位置重复时，必须新增条件、例外、证据或动作。
- 每段应承担必要的定义、关系、判断、条件、证据、例外或动作；无信息贡献的重复内容合并、移旁路或删除。
- 保留用户原文里准确、有辨识度的人话；只删噪音，不磨成礼貌模板。
- 把用户纠正当作后续写作约束：术语、事实、范围、风格一经确认就全局传播，不重复犯错或反复确认。
- 当前成品以当前任务和已确认范围为准，不补回无关删改旁白；必要的真实对比、历史证据和用户要求的变更记录按 [current-content-integrity.md](references/current-content-integrity.md) 保留，不要求每句导向动作。
- 标题呈现结构，加粗呈现关键判断；概念、字段、路径和边界可作为辅助锚点。读者只扫标题和加粗内容，也应能复述文章主线。可执行代码只放代码块。
- 先按读者任务选载体：同类对象的横向比较用表格；顺序用步骤或流程；规则和门槛用短段或清单；概念分类用小标题和判断句；关系、层级、流向、映射用图。表格不是压缩段落或制造视觉中心的默认工具。
- 图或表已经给出结论，正文只留理由、例外或后果；不要逐行复述。
- 正文做无损压缩：中心判断和改变选择的证据留正文，长证据与历史讨论移到旁路记录；不要靠直接删除细节制造“简洁”。
- 保留事实不等于保留原句；压缩时不得把“本次证据 / 某研究 / 已核实范围”扩大成“全部现有 / 普遍事实”，也不得把“不能支持”写强成“证明”或“排除”。
- 用户要求去重或压缩时，必须实际合并、移位或删除重复载体；只换标题和语序不算完成。
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
- 事实不确定时标注为假设；健康、财务等高影响决策保留来源、不确定性和个人约束，不装成专业诊断。
