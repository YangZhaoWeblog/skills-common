# skills-common

中文 | [English](README.md)

这个仓库只放可复用的通用 skill。

## 规则

- 当一个 skill 在学习和开发两个场景里都能复用时，放这里。
- 不要把外部一次性安装的 skill 放进来。
- 如果某个通用 skill 变成了具体工作流的一部分，把它迁到 `skills-develop` 或 `skills-learning`。

## 目录

- `skills/shared/`

兄弟仓库：

- [skills-develop](../skills-develop/README.zh-CN.md)
- [skills-learning](../skills-learning/README.zh-CN.md)

## 安装

项目级安装，适合只在当前仓库生效：

```bash
npx skills add /Users/yangzhao/Code/skills-common -y
```

全局安装，适合所有项目都可用：

```bash
npx skills add /Users/yangzhao/Code/skills-common -g -y
```

`npx skills add` 默认是项目级，`-g` 会切换成用户级安装。
