# skills-common

<p align="center"><em>可复用的通用 skill。保持轻、保持宽，不要过早收窄。</em></p>

<p align="center">
  <img alt="License MIT" src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge">
  <img alt="Agent Skills Standard" src="https://img.shields.io/badge/Agent%20Skills-Standard-6DA544?style=for-the-badge">
  <img alt="skills.sh Compatible" src="https://img.shields.io/badge/skills.sh-Compatible-1E6FFF?style=for-the-badge">
  <img alt="Runtime" src="https://img.shields.io/badge/Runtime-Claude%20Code%20·%20Codex%20·%20Cursor-8A2BE2?style=for-the-badge">
</p>

<p align="center"><strong>这个仓库只放可复用的通用 skill。</strong></p>

中文 | [English](README.md)

* * *

## 安装

### 项目级

装到当前仓库。

```bash
npx skills@latest add YangZhaoWeblog/skills-common -y
```

### 全局级

装到你的用户空间。

```bash
npx skills@latest add YangZhaoWeblog/skills-common -g -y
```

`npx skills add` 默认是项目级，`-g` 会切换成用户级安装。

### 单个 skill

只安装仓库里的一个 skill：

```bash
npx skills@latest add YangZhaoWeblog/skills-common --skill td-logic-writer -y
```

只安装一个本地 skill 目录：

```bash
npx skills@latest add /Users/yangzhao/Code/skills-common/skills/shared/td-logic-writer -y
```

不安装，直接生成单个 skill 的使用 prompt：

```bash
npx skills@latest use YangZhaoWeblog/skills-common@td-logic-writer
```

把 `td-logic-writer` 或本地路径换成目标 skill；要全局安装这个单个 skill 时加 `-g`。

* * *

## Skill

| Skill | 作用 |
| --- | --- |
| [knowledge-illustrator](skills/shared/knowledge-illustrator/SKILL.md) | 把概念画成清晰的图。 |
| [td-logic-writer](skills/shared/td-logic-writer/SKILL.md) | 把混乱材料写成精炼的判断系统型文章。 |
| [td-logic-writing-flow](skills/shared/td-logic-writing-flow/SKILL.md) | 分流 Obsidian 写作任务，并执行骨架门与审查门。 |
| [tech-doc-writer](skills/shared/tech-doc-writer/SKILL.md) | 用结构化流程写技术文档。 |
| [td-external-agent](skills/shared/td-external-agent/SKILL.md) | 调用 Codex、Claude Code 或 CodeBuddy CLI 执行任务。 |

### 已废弃

| Skill | 状态 |
| --- | --- |
| [razor](skills/deprecated/razor/SKILL.md) | 已废弃，保留作参考。 |

## 目录

活跃技能位于 **skills/shared/**，已废弃技能位于 **skills/deprecated/**：**skills-common** 维护通用能力，[skills-develop](../skills-develop/README.zh-CN.md) 维护开发工作流，[skills-learning](../skills-learning/README.zh-CN.md) 维护学习工作流。
