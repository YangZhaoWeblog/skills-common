---
name: td-logic-writing-flow
description: Route and control MyDigitalGarden/Obsidian writing tasks with a logic-first, concise, no-fluff workflow. Use when the user asks to write, rewrite, restructure, polish, de-AI, outline, review, or continue an Obsidian article or personal knowledge note, especially when deciding whether the task belongs to td-logic-writer, knowledge-illustrator, imagegen, tech-doc-writer, atomic notes, MOC, deep-learn/light-learn, DAG, or casual idea capture. It enforces stage control, skeleton-first gates for new/rewrite/large edits, visual QA for illustrated articles, a mandatory independent Review Gate for substantial/high-impact articles, and routing back to the right skill instead of blindly generating a full article.
---

# TD Logic Writing Flow

这是路由器，不是另一个 writer。先识别文档类型和主推进模式，再进入对应链路。

## 阶段

| 阶段 | 产物 |
| --- | --- |
| 讨论 | 目标、边界、取舍 |
| 骨架 | 标题链和每节问题 |
| 成文 | 按确认骨架写正文 |
| 修改 | 读取当前文和用户改动后局部或整体修改 |
| 复盘 | 可复用的正反模式 |
| 审查 | 独立 Review 结论；未完成则不可交付 |

新写、重写、大改默认先给骨架；用户明确要求直接写时，仍先用短段说明任务和骨架方向。

## 双重定型

写作前必须同时确定：

- **文档类型：** 写给别人理解的文章、个人系统/决策文档，还是正式团队技术文档。
- **主推进模式：** 收窄选择空间、根原则推导系统、逐层建立理解，或案例验证判断。

每节都必须改变读者状态：缩小候选、解决疑问、升级模型、验证判断、澄清边界或确定下一步。只增加同层信息的章节不是推进，应合并、移位或删除。详见 [progression-modes.md](../td-logic-writer/references/progression-modes.md)。

## 硬性审查闸门

- 新写、重写、大改、高影响或带图的个人文章，必须在最终写入目标文件或交付前完成独立 Review；这不是建议，也不能用作者自审替代。
- 在 Review `pass` 之前，不得创建、覆盖或修改最终目标路径；候选稿只能写入明确标记的 draft/temp 路径。`pass` 后才能提升到目标路径，并重新读取最终文件验证内容一致。
- 独立 Review 必须由独立 reviewer 调用或隔离的评审上下文完成。作者再次阅读、同一上下文切换成“审查者口吻”、或依据 checklist 自查，都不算独立 Review。
- 触发 Review Gate 时必须生成不可变的 `gate_id`，绑定规范化绝对路径、解析后的真实路径或文件身份；换会话、换任务名、移动或改名都不能重置它。缺少或丢失 `gate_id` 时状态为 `blocked`。
- Review 结果必须可复核地记录：`gate_id`、规范化目标路径或文章身份、候选版本的 SHA-256、系统生成的 reviewer 调用 ID、原始返回结果或隔离会话 ID/审计记录、Review 包范围、结论、复审轮次和剩余风险。reviewer 必须实际收到并审查该 SHA-256 对应的版本；不能用手写 reviewer 名称、未定义的“隔离证据”或旧版本结论代替。
- `pass` 才能交付；`minor`、`structural`、`factual` 或 `visual` 都必须先修复，再由独立 reviewer 复核最终版本。提升到最终目标路径后，必须重新计算最终文件 SHA-256，并与 reviewer 审查的候选版本一致；路径身份或哈希不一致时为 `blocked`。`blocked` 必须停止交付并报告阻塞。
- 如果环境具备独立子代理或隔离评审能力，必须实际调用；未尝试已有能力，不得声称“没有独立 reviewer”。没有独立 reviewer 能力，或缺少实际调用/隔离证据时，状态必须是“Review Gate 未完成/阻塞”；不得把自审写成独立 Review，也不得报告任务已完成。可以保留候选草稿，但不得将其作为最终成品交付。
- 错别字、局部润色和用户明确限定的快速小改，仅在文章尚未触发 Review Gate 时豁免；一旦单次或累计修改影响判断、结构、事实或视觉层级，必须在下一次写入前升级到独立 Review，不得通过连续小改规避。
- 一旦同一文章触发 Review Gate，按 `gate_id` 和规范化目标路径或文章身份记录状态；后续所有会话、任务和修改都继承 Review Gate，不得通过拆成多个“小改”、换会话、换路径或改任务名称规避。首次 reviewer 调用为第一轮，最多只有一次复审；轮次必须绑定 `gate_id`，不得重置。

## 路由

| 任务 | 去向 |
| --- | --- |
| 判断框架、概念边界、项目认知、个人策略 | **td-logic-writer** |
| 个人系统、个人运行规则、个人决策文档 | **td-logic-writer** 的系统文档模式 |
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
- 个人系统/决策文档额外明确：核心损失、核心对象、对象之间的先后关系和容量边界。
- 骨架阶段为每节标注 **读者任务 → 主载体**；表格只用于真实横向比较，具体判定交给对应 writer。
- 标题、表、图和文字必须形成单一路径；页面割裂时先修视觉中心、分块和密度。
- 不把用户好句子改成无辨识度的 AI 书面语；不为完整感扩项。
- 中文线性文章默认使用 `一、二、三、四` 一级标题；加粗承担第二阅读路径；可执行代码仅用代码块。具体密度和例外交给对应 writer。
- 路由器不复述 writer 的细节规则；判断账本、证据位置和无损压缩由对应 writer 负责。

## 图与审查

正式技术文档的状态、时序和 ER 图由 **tech-doc-writer** 使用 Mermaid、DBML 等可编辑格式。需要自定义布局或文章配图时，调用 **knowledge-illustrator**。精确关系不用生成式位图。

个人文章的新写、重写、大改、高影响或带图任务，必须读取 [review-gate.md](references/review-gate.md)，先准备最小 Review 包并启动独立 reviewer；没有独立 reviewer 时必须阻塞。带图再读 [visual-checklist.md](references/visual-checklist.md)。正式技术文档只使用 **tech-doc-writer** 的 Review Gate。小改仍需自审。

## 复盘

最终认可成品是正向样本，用户删除或否定的内容是负向样本。只把跨项目规律写回公共 Skill；项目事实和一次性约定留在项目材料。
