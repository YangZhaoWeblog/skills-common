# skills-common

> Shared skills that are reusable across workflows. Keep them lean and general.

English | [中文](README.zh-CN.md)

This repository contains reusable skills that are not specific to one workflow.

Other languages: [中文](README.zh-CN.md)

* * *

## What belongs here

- shared skill logic useful across learning and development contexts
- reusable general-purpose behaviors that should stay available to multiple repos
- skill helpers that are still broad enough to remain common

## What stays out

- external one-off installs
- workflow-specific learning content
- workflow-specific engineering flows

## Install

Project scope:

```bash
npx skills add /Users/yangzhao/Code/skills-common -y
```

Global scope:

```bash
npx skills add /Users/yangzhao/Code/skills-common -g -y
```

Project scope is the default. `-g` switches to user-level installation.

* * *

## Layout

- `skills/shared/`

Sibling repos:

- [skills-develop](../skills-develop/README.md)
- [skills-learning](../skills-learning/README.md)
