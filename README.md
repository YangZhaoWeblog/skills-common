# skills-common

English | [中文](README.zh-CN.md)

This repository contains reusable skills that are not specific to one workflow.

## Rules

- Keep shared skill logic here when it is useful across learning and development contexts.
- Do not place external one-off installs here.
- If a shared skill becomes workflow-specific, move it into `skills-develop` or `skills-learning`.

## Layout

- `skills/shared/`

Sibling repos:

- [skills-develop](../skills-develop/README.md)
- [skills-learning](../skills-learning/README.md)

## Install

Use project scope for repo-local installs:

```bash
npx skills add /Users/yangzhao/Code/skills-common -y
```

Use global scope when you want the shared skills available across all projects:

```bash
npx skills add /Users/yangzhao/Code/skills-common -g -y
```

Project scope is the default. `-g` switches to user-level installation.
