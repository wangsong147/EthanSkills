# EthanSkills

个人开发工作流的 Skill 沉淀库。把开发里反复用到、已经验证过的做法，按阶段写成 [Cursor Agent Skill](https://cursor.com/docs/context/skills)，让之后每次做到同一阶段时都按同一套方法协作。

Skill 记录的是本人真实在用的步骤、检查项和产出，随实践更新。

## 阶段

| 阶段 | 目录 | 这一阶段要拿到的结果 |
| --- | --- | --- |
| 需求澄清 | `skills/01-requirements/` | 需求被收成可实现、可验收的说明：范围、验收标准、待确认项 |
| 技术实现 | `skills/02-implementation/` | 按已澄清的需求落地改动，并留下可追溯的实现说明 |
| Code Review | `skills/03-code-review/` | 按个人审查标准看变更，给出可执行的审查结论 |
| 测试 | `skills/04-testing/` | 按测试层级验证改动。三个子目录分开存放，互不混用 |
| Bug 修复 | `skills/05-bugfix/` | 定位缺陷、做最小修复，并留下回归验证的做法 |
| 维护复盘 | `skills/06-maintenance/` | 复盘近期 Bug、返工、回滚和重复修改，把可预防的共性问题沉淀成规则、自动化或 Skill |

测试阶段再分三层：

| 层级 | 目录 | 验什么 |
| --- | --- | --- |
| 冒烟 | `skills/04-testing/smoke/` | 主路径能否跑通，构建、启动、核心操作是否可用 |
| 功能 | `skills/04-testing/functional/` | 需求里的验收点是否满足，正常、边界和失败路径是否覆盖 |
| SIT | `skills/04-testing/sit/` | 在联调环境里和上下游、数据、配置一起验证 |

功能开发按这个顺序推进：需求澄清 → 技术实现 → Code Review → 测试（冒烟 → 功能 → SIT）。前一阶段的产出是后一阶段的输入。

Bug 修复单独放在 `skills/05-bugfix/`，记录定位、最小修复和回归验证，不插进上面这条顺序。维护复盘单独放在 `skills/06-maintenance/`，回头看一段时间内反复付出的成本，同样不插进这条顺序。

## 一条 Skill 长什么样

每条 Skill 独占一个目录，入口文件固定为 `SKILL.md`：

```text
skills/<阶段>/<skill-name>/
├── SKILL.md          # 必需。给 Agent 的操作说明
├── reference.md      # 可选。检查表、模板、判定标准
├── examples.md       # 可选。真实案例
└── scripts/          # 可选。可重复执行的脚本
```

`SKILL.md` 开头使用 YAML frontmatter：

```markdown
---
name: skill-name
description: 用第三人称写清两件事——这条 Skill 做什么，以及出现哪些说法或场景时应该使用它。
---
```

- `name`：小写字母、数字、连字符，最多 64 字符，与目录名一致。
- `description`：写清「做什么」和「什么时候用」。Agent 靠这段决定要不要加载这条 Skill。

正文用中文，写成可以照着做的步骤：输入是什么、先读什么、按什么顺序做、产出放在哪里、做到什么程度算完成。

## 在日常项目里怎么用

1. 先判断当前停在哪个阶段。
2. 打开本仓库对应目录下的 `SKILL.md`，让 Agent 按其中的步骤执行。
3. 做完后，把这次新确认的做法补回同一条 Skill，而不是只留在当次对话里。

本仓库是 Skill 的存放处。希望 Cursor 在其他项目里自动发现时，把对应的 `skill-name` 目录符号链接到 `~/.cursor/skills/`，链接指回这里，避免出现两份副本。

## 当前 Skill

新增、改名或删除后，在下表补一行，一行对应一个真实存在的 `SKILL.md`。

| 阶段 | 名称 | 路径 | 做什么 |
| --- | --- | --- | --- |
| Bug 修复 | root-cause | `skills/05-bugfix/root-cause/SKILL.md` | 从第一性原理出发，找到最本质原因 |
| 维护复盘 | retrospective | `skills/06-maintenance/retrospective/SKILL.md` | 复盘近期 Bug、返工、回滚和重复修改，把可预防的共性问题沉淀下来 |

## 维护约定

- 一条实践只放在它所属的那一个阶段目录里。测试类 Skill 放进 `smoke`、`functional`、`sit` 之一。
- 同一阶段已有 Skill 能覆盖时，直接更新那一条。
- 提交说明使用中文。
