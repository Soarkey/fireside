<h1 align="center">🔥 Fireside</h1>

<p align="center">
  <strong>Primitive Society Multi-Agent Orchestration for Claude Code</strong><br/>
  原始社会多智能体编排框架
</p>

<p align="center">
  <img src="https://img.shields.io/badge/agents-8_specialized-red" alt="Agents">
  <img src="https://img.shields.io/badge/skills-5_workflows-yellow" alt="Skills">
  <img src="https://img.shields.io/badge/dependencies-zero-brightgreen" alt="Zero deps">
  <img src="https://img.shields.io/badge/Claude_Code-plugin-blue" alt="Claude Code Plugin">
  <img src="https://img.shields.io/badge/license-MIT-lightgrey" alt="MIT">
</p>

<p align="center">
  <em>"Around the fire, the tribe finds its wisdom."</em><br/>
  <em>"围坐火塘，部落得其智慧。"</em>
</p>

---

A zero-dependency Claude Code plugin that orchestrates AI agents through a **primitive tribal council** — scouts reconnoiter, hunters and gatherers debate by the fire, shamans divine cross-domain insights, and elders render decisive verdicts.

零依赖 Claude Code 插件，以**原始部落议事制**编排多个 AI 智能体——斥候侦察、猎手与采集者围火辩论、巫师提供跨域灵感、长老做出最终裁决。

## Table of Contents

- [Design Philosophy](#design-philosophy)
- [Architecture](#architecture)
- [Quick Start](#quick-start)
- [Commands](#commands)
- [Agents](#agents)
- [Scale Classification](#scale-classification)
- [Pipeline Flows](#pipeline-flows)
- [Intermediate Artifacts](#intermediate-artifacts)
- [Project Structure](#project-structure)

---

## Design Philosophy

### Why a Tribe?

Most multi-agent frameworks model corporate hierarchies or political systems. Fireside draws from a deeper source: **the survival logic of primitive tribes**.

> 大多数多智能体框架模仿企业层级或政治制度。Fireside 从更深处汲取灵感：**原始部落的生存逻辑**。

In a tribe, there are no meetings for the sake of meetings. Every debate around the fire serves one purpose — **the tribe must survive**. A hunter's bold raid and a gatherer's cautious foraging aren't competing ideologies; they are genuinely different survival strategies born from different ways of reading the world.

> 部落中没有为了开会而开的会。火塘边的每一次辩论只服务于一个目的——**部落必须存活**。猎手的大胆突袭和采集者的谨慎觅食不是对立的意识形态，而是源于不同世界观的真实生存策略。

This distinction matters. When you pit a "conservative approach" against an "aggressive approach" in a typical framework, you get shades of the same thinking. When you pit a **hunter against a gatherer**, you get fundamentally different ways of solving the problem — and that's where the best solutions emerge.

> 这种区别至关重要。在典型框架中对立"保守方案"与"激进方案"，得到的是同一思路的不同程度。而当**猎手对阵采集者**，你得到的是根本不同的解题方式——最好的方案往往从这里诞生。

### Four Principles

**1. Survival Over Procedure** / 生存优先于流程

Agents don't follow procedures for compliance — they act on survival instinct. The Scout doesn't fill out a form; it returns to camp with intelligence. The Elder doesn't tally votes; it makes a judgment call. This keeps the system fast and decisive.

**2. Genuine Opposition** / 真实对立

The Hunter and Gatherer are not "Option A" and "Option B". They embody fundamentally different risk appetites and worldviews. The Hunter seeks the best possible outcome; the Gatherer protects against the worst. The Elder sees both, and chooses.

**3. Verdicts, Not Votes** / 裁决而非投票

No consensus-seeking. No weighted scoring. The Elder listens to every voice around the fire, then speaks once. One decision. This eliminates analysis paralysis and produces clear, actionable plans.

**4. Narrative Output** / 叙事风格

Scout reports read like a returning scout briefing the tribe. Elder verdicts sound like fireside pronouncements. Guardian patrols feel like sentry watch logs. The tribal voice isn't decoration — it makes agent roles intuitive and outputs memorable.

---

## Architecture

```
                    ┌─────────────┐
                    │  🦅 Scout   │  Reconnaissance
                    │  (zhencha)  │  Scale → Solo / Party / Tribe
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        ┌──────────┐ ┌──────────┐ ┌──────────┐
        │ 🐺 Hunter│ │🐝Gatherer│ │ 🦉 Shaman│  Fireside Council
        │(lieshou) │ │ (caiji)  │ │ (wushi)  │  围火议事
        │  Bold    │ │ Cautious │ │ Creative │
        └────┬─────┘ └────┬─────┘ └────┬─────┘
             │             │             │
             └─────────────┼─────────────┘
                           ▼
                    ┌─────────────┐
                    │  🦬 Elder   │  Final Verdict
                    │ (zhanglao)  │
                    └──────┬──────┘
                           ▼
                    ┌─────────────┐
                    │  🐘 Foreman │  Task Breakdown
                    │  (gongtou)  │
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        ┌──────────┐ ┌──────────┐ ┌──────────┐
        │🦫Artisan │ │🦫Artisan │ │🦫Artisan │  Parallel Execution
        │(gongjiang)│ │(gongjiang)│ │(gongjiang)│
        └────┬─────┘ └────┬─────┘ └────┬─────┘
             │             │             │
             └─────────────┼─────────────┘
                           ▼
                    ┌─────────────┐
                    │ 🐻 Guardian │  Quality Patrol
                    │  (shouwei)  │  ✅ Pass / ❌ Reject
                    └─────────────┘
```

---

## Quick Start

```bash
git clone https://github.com/Soarkey/fireside.git
```

Place the `fireside/` directory in your workspace. No build step, no dependencies — ready to use.

将 `fireside/` 目录放入你的工作区，即装即用。

---

## Commands

| Command | Description | Use When |
|---------|-------------|----------|
| `/hunt <task>` | Full pipeline: scout → council → execute → review | End-to-end tasks / 完整任务 |
| `/council <task>` | Deliberation only, no code changes | Evaluate approaches first / 先看方案 |
| `/craft <plan>` | Execution only, skip deliberation | Plan already exists / 已有方案 |
| `/patrol [files]` | Review current changes | After manual edits / 手动修改后 |
| `/sos <task>` | Survival mode — skip all deliberation | Production incidents / 线上事故 |

### Examples

```bash
# Full pipeline
/hunt Refactor the authentication module to support OAuth2

# Deliberation only — see proposals before committing
/council --scale tribe How should we redesign the caching layer?

# Execute an existing plan
/craft Add rate limiting middleware using the approach from last council

# Review after manual edits
/patrol src/auth/ src/middleware/

# Production fire — all hands on deck
/sos Users are getting 500 errors on the payment endpoint
```

---

## Agents

### Council / 议事团

| Totem | Agent | Role | Creed |
|:-----:|-------|------|-------|
| 🦅 | **Scout** · zhencha / 斥候 | Reconnaissance & triage | *千里之行，始于足下* |
| 🐺 | **Hunter** · lieshou / 猎手 | Bold, high-reward proposals | *不入虎穴，焉得虎子* |
| 🐝 | **Gatherer** · caiji / 采集者 | Minimal-change, safe proposals | *细水长流，稳中求胜* |
| 🦉 | **Shaman** · wushi / 巫师 | Cross-domain creative solutions | *天地万物，皆可为师* |
| 🦬 | **Elder** · zhanglao / 长老 | Final verdict | *听百家之言，行一家之策* |

### Workers / 执行团

| Totem | Agent | Role |
|:-----:|-------|------|
| 🐘 | **Foreman** · gongtou / 工头 | Task decomposition & scheduling |
| 🦫 | **Artisan** · gongjiang / 工匠 | Precise code execution |
| 🐻 | **Guardian** · shouwei / 守卫 | Code review & automated verification |

---

## Scale Classification

The Scout classifies each task to determine deliberation depth:

斥候自动评估任务规模，决定议事深度：

| Scale | Criteria | Council Composition |
|-------|----------|-------------------|
| 🟢 **Solo** | <3 files, single concern | Skip deliberation → direct execution |
| 🟡 **Party** | 3–8 files, cross-module | Hunter + Gatherer (two perspectives) |
| 🔴 **Tribe** | >8 files or architectural | Hunter + Gatherer + Shaman (three perspectives) |

Override: `/hunt --scale tribe <task>`

---

## Pipeline Flows

### `/hunt` — Full Pipeline

```
Scout → [Hunter ∥ Gatherer (∥ Shaman)] → Elder → Foreman → Artisans (batched ∥) → Guardian
                                                                                      │
                                                                              ✅ Pass → Done
                                                                              ❌ Reject → Retry (max 2) → Escalate
```

### `/council` — Deliberation Only

```
Scout → [Hunter ∥ Gatherer (∥ Shaman)] → Elder → Report
                                                    └→ User decides: /craft to execute
```

### `/sos` — Survival Mode

```
Foreman (direct) → ALL Artisans (full ∥) → Guardian (automated checks only)
```

---

## Intermediate Artifacts

All outputs are persisted to `.tmp/fireside/{timestamp}/`:

| File | Content |
|------|---------|
| `zhencha-report.md` | Scout reconnaissance report / 侦察报告 |
| `lieshou-proposal.md` | Hunter's bold proposal / 猎手提案 |
| `caiji-proposal.md` | Gatherer's conservative proposal / 采集者提案 |
| `wushi-proposal.md` | Shaman's creative proposal *(Tribe only)* / 巫师提案 |
| `zhanglao-decision.md` | Elder's final verdict / 长老裁决 |
| `gongtou-tasks.md` | Foreman's task breakdown / 任务清单 |
| `gongjiang-{N}-result.md` | Artisan execution reports / 工匠报告 |
| `shouwei-verdict.md` | Guardian review verdict / 守卫报告 |

---

## Project Structure

```
fireside/
├── README.md
├── CLAUDE.md                           # Development guide
├── LICENSE                             # MIT
├── .gitignore
└── .claude-plugin/
    ├── marketplace.json                # Plugin manifest
    ├── agents/                         # 8 Agents
    │   ├── zhencha.md                  # 🦅 Scout
    │   ├── lieshou.md                  # 🐺 Hunter
    │   ├── caiji.md                    # 🐝 Gatherer
    │   ├── wushi.md                    # 🦉 Shaman
    │   ├── zhanglao.md                # 🦬 Elder
    │   ├── gongtou.md                  # 🐘 Foreman
    │   ├── gongjiang.md               # 🦫 Artisan
    │   └── shouwei.md                  # 🐻 Guardian
    ├── skills/                         # 5 Commands
    │   ├── hunt/SKILL.md              # /hunt
    │   ├── council/SKILL.md           # /council
    │   ├── craft/SKILL.md             # /craft
    │   ├── patrol/SKILL.md            # /patrol
    │   └── sos/SKILL.md              # /sos
    └── hooks/
        └── hooks.json                  # Reserved
```

---

## License

[MIT](LICENSE)

---

<p align="center">
  <strong>🔥 Around the fire, the tribe finds its wisdom. 🔥</strong><br/>
  围坐火塘，部落得其智慧。
</p>
