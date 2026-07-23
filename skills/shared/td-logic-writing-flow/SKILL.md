---
name: td-logic-writing-flow
description: Route and control MyDigitalGarden/Obsidian writing tasks with a logic-first, concise, no-fluff workflow. Use when the user asks to write, rewrite, restructure, polish, de-AI, outline, review, or continue an Obsidian article or personal knowledge note, especially when deciding whether the task belongs to td-logic-writer, knowledge-illustrator, imagegen, tech-doc-writer, atomic notes, MOC, deep-learn/light-learn, DAG, or casual idea capture. It enforces stage control, skeleton-first gates for new/rewrite/large edits, visual QA for illustrated articles, independent Review Gate for substantial/high-impact articles, and routing back to the right skill instead of blindly generating a full article.
---

# TD Logic Writing Flow

这是路由器，不是另一个 writer。先识别文章任务，再进入对应链路。

## 阶段

| 阶段 | 产物 |
| --- | --- |
| 讨论 | 目标、边界、取舍 |
| 骨架 | 标题链和每节问题 |
| 成文 | 按确认骨架写正文 |
| 修改 | 读取当前文和用户改动后局部或整体修改 |
| 复盘 | 可复用的正反模式 |
| 审查 | 独立 Review 结论 |

新写、重写、大改默认先给骨架；用户明确要求直接写时，仍先用短段说明任务和骨架方向。

## 路由

| 任务 | 去向 |
| --- | --- |
| 判断框架、概念边界、项目认知、个人策略 | **td-logic-writer** |
| 健康、财务、消费等风险 / 证据型个人决策 | **td-logic-writer** 的证据型决策骨架 |
| 正式方案、报告、调研、测试报告、操作手册 | **tech-doc-writer** |
| 原子笔记、MOC、学习链路、普通灵感 | 对应专用链路 |
| 正式技术文档的状态、时序、ER 图 | **tech-doc-writer** |
| 个人文章的精确关系、流程、层级、边界、映射图 | **knowledge-illustrator** |
| 封面、场景、插画等位图资产 | **imagegen** |

## 工作规则

- 先读当前文件、用户修改、截图、链接和参考样本；当前版本优先于历史讨论。
- 用户确认的术语、事实、范围和风格要传播到后续产物。
- 用户仍在讨论时只给判断、取舍和下一步，不提前写完整文章。
- 新写、重写或大改先明确文章契约：读者、真实问题、默认选择或根定义、什么会改变它、非目标。
- 骨架阶段为每节标注 **读者任务 → 主载体**；表格只用于真实横向比较，具体判定交给对应 writer。
- 标题、表、图和文字必须形成单一路径；页面割裂时先修视觉中心、分块和密度。
- 不把用户好句子改成无辨识度的 AI 书面语；不为完整感扩项。
- 名称性信息用 **加粗**；可执行代码仅用代码块。
- 路由器不复述 writer 的细节规则；判断账本、证据位置和无损压缩由对应 writer 负责。

## 图与审查

正式技术文档的状态、时序和 ER 图由 **tech-doc-writer** 使用 Mermaid、DBML 等可编辑格式。需要自定义布局或文章配图时，调用 **knowledge-illustrator**。精确关系不用生成式位图。

个人文章的新写、重写、大改、高影响或带图任务，读取 [review-gate.md](references/review-gate.md) 并启动独立 reviewer；带图再读 [visual-checklist.md](references/visual-checklist.md)。正式技术文档只使用 **tech-doc-writer** 的 Review Gate。小改仍需自审。

## 复盘

最终认可成品是正向样本，用户删除或否定的内容是负向样本。只把跨项目规律写回公共 Skill；项目事实和一次性约定留在项目材料。
