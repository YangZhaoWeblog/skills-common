# skills-common

<p align="center"><em>Shared skills that are reusable across workflows. Keep them lean and general.</em></p>

<p align="center">
  <img alt="License MIT" src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge">
  <img alt="Agent Skills Standard" src="https://img.shields.io/badge/Agent%20Skills-Standard-6DA544?style=for-the-badge">
  <img alt="skills.sh Compatible" src="https://img.shields.io/badge/skills.sh-Compatible-1E6FFF?style=for-the-badge">
  <img alt="Runtime" src="https://img.shields.io/badge/Runtime-Claude%20Code%20·%20Codex%20·%20Cursor-8A2BE2?style=for-the-badge">
</p>

<p align="center"><strong>This repository contains reusable skills that are not specific to one workflow.</strong></p>

English | [中文](README.zh-CN.md)

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

### Project scope

Install into the current repo.

```bash
npx skills@latest add YangZhaoWeblog/skills-common -y
```

### Global scope

Install into your user space.

```bash
npx skills@latest add YangZhaoWeblog/skills-common -g -y
```

Project scope is the default. `-g` switches to user-level installation.

* * *

## Skills

| Skill | What it does |
| --- | --- |
| `knowledge-illustrator` | Turn concepts into clean diagrams and visual aids. |
| `razor` | Keep responses dense, terse, and actionable. |
| `tech-doc-writer` | Draft technical docs with a structured pipeline. |

## Layout

- `skills/shared/`

Sibling repos:

- [skills-develop](../skills-develop/README.md)
- [skills-learning](../skills-learning/README.md)
