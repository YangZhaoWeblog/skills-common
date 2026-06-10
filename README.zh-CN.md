# skills-common

> 可复用的通用 skill。保持轻、保持宽，不要过早收窄。

中文 | [English](README.md)

这个仓库只放可复用的通用 skill。

其他语言：[English](README.md)

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

项目级：

```bash
npx skills add /Users/yangzhao/Code/skills-common -y
```

全局级：

```bash
npx skills add /Users/yangzhao/Code/skills-common -g -y
```

`npx skills add` 默认是项目级，`-g` 会切换成用户级安装。

* * *

## 目录

- `skills/shared/`

兄弟仓库：

- [skills-develop](../skills-develop/README.zh-CN.md)
- [skills-learning](../skills-learning/README.zh-CN.md)
