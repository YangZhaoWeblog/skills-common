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

## 放这里

- 在学习和开发两个场景里都能复用的 skill 逻辑
- 需要给多个仓库共用的通用行为
- 仍然足够宽泛、可以保持通用的 skill 辅助能力

## 不放这里

- 外部一次性安装品
- 只适用于学习场景的内容
- 只适用于工程工作流的内容

## 安装

### 项目级

装到当前仓库。

```bash
npx skills add /Users/yangzhao/Code/skills-common -y
```

### 全局级

装到你的用户空间。

```bash
npx skills add /Users/yangzhao/Code/skills-common -g -y
```

`npx skills add` 默认是项目级，`-g` 会切换成用户级安装。

* * *

## Skill

| Skill | 作用 |
| --- | --- |
| `knowledge-illustrator` | 把概念画成清晰的图。 |
| `razor` | 保持回答密度高、冗余低。 |
| `tech-doc-writer` | 用结构化流程写技术文档。 |

## 目录

- `skills/shared/`

兄弟仓库：

- [skills-develop](../skills-develop/README.zh-CN.md)
- [skills-learning](../skills-learning/README.zh-CN.md)
