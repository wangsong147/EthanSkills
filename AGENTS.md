# EthanSkills — Agent 协作约束

本仓库只沉淀个人开发工作流 Skill。这里没有业务代码，也没有某个具体项目的需求文档。

在本仓库里的默认动作是：把用户描述的做法写成或更新到对应阶段的 `SKILL.md`，并让 `README.md` 的「当前 Skill」表和目录保持一致。

## 先判断阶段，再动手

用户提到开发过程中的一种做法时，先归入下面一个阶段，再打开该目录里已经存在的 `SKILL.md`。

| 用户在说 | 阶段 | 目录 |
| --- | --- | --- |
| 需求不清、范围、验收标准、待确认问题 | 需求澄清 | `skills/01-requirements/` |
| 怎么实现、怎么改代码、分支与提交过程中的个人习惯 | 技术实现 | `skills/02-implementation/` |
| 怎么审变更、审什么、审查结论怎么写 | Code Review | `skills/03-code-review/` |
| 冒烟、主路径能不能跑起来 | 测试 · 冒烟 | `skills/04-testing/smoke/` |
| 功能是否满足验收点 | 测试 · 功能 | `skills/04-testing/functional/` |
| 联调、上下游、SIT 环境 | 测试 · SIT | `skills/04-testing/sit/` |
| 缺陷、线上问题、定位、最小修复、回归 | Bug 修复 | `skills/05-bugfix/` |
| 复盘、返工、回滚、重复修改、反复支付同样成本 | 维护复盘 | `skills/06-maintenance/` |

归错阶段就改正目录。同一份内容只保留在一个阶段里。

阶段之间的交接物要写进 Skill：

- 需求澄清的产出（范围、验收标准、待确认项）是技术实现的输入。
- 技术实现的产出（改动与实现说明）是 Code Review 的输入。
- Code Review 通过后的改动，按冒烟 → 功能 → SIT 的顺序进入测试。每层 Skill 只写本层要验的事。
- Bug 修复的做法放在 `skills/05-bugfix/`。它记录定位、最小修复和回归验证，不并进 01–04 的功能开发顺序。
- 维护复盘的做法放在 `skills/06-maintenance/`。它复盘一段时间内的 Bug、返工、回滚和重复修改，把可预防的共性问题沉淀成规则、自动化或 Skill，不并进 01–04 的功能开发顺序。

## 写 Skill 时遵守的事实来源

Skill 正文只记录用户明确说过、或本仓库里已经写下来的做法。

用户还没给出的步骤、检查项、工具和阈值，在 Skill 里标成「待补充」，向用户确认后再写死。用通用最佳实践填满一份 Skill，会把本人流程冲掉。

同一阶段已经有 Skill 能覆盖这次内容时，更新那一条。新建 Skill 前先读完该阶段目录下现有的 `SKILL.md`。

## Skill 文件要求

路径：

```text
skills/<阶段>/<skill-name>/SKILL.md
```

测试类 Skill 放在 `smoke/`、`functional/`、`sit/` 之下。`skills/04-testing/` 根目录不放 `SKILL.md`。

`SKILL.md` 必须带 frontmatter：

```markdown
---
name: skill-name
description: 第三人称。写清这条 Skill 做什么，以及哪些说法或场景下应该使用它。
---
```

- `name` 与目录名相同：小写字母、数字、连字符，最多 64 字符。
- `description` 同时包含「做什么」和「什么时候用」，最多 1024 字符。这段会进入 Agent 的技能发现，含糊的描述会导致该用时调不起来。
- 正文使用中文。
- 步骤要能执行：输入、阅读顺序、动作、产出、完成标准。
- 检查表、长模板、真实案例分别放进同目录的 `reference.md`、`examples.md`，在 `SKILL.md` 里用相对路径指向它们。`SKILL.md` 保持为操作入口。

## 改完 Skill 后同步 README

新增、改名或删除任一 `SKILL.md` 时，同时更新 `README.md` 的「当前 Skill」表：

- 每一行对应一个仓库里真实存在的 `SKILL.md`。
- 表中的路径、名称、阶段与目录一致。
- 计划中、尚未落盘的 Skill 不写入这张表。

改名或删除前，在全仓库搜索旧的 `name` 和旧路径，把 `README.md`、`AGENTS.md` 以及其他 Skill 里的引用一起改掉。

## Git

- Commit message 使用中文，说明这次沉淀或修正了哪条工作流。
- 用户没有明确要求时，不创建提交，也不推送远端。
