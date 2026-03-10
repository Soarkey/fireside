# Fireside Development Guide

## Project Overview

Fireside is a multi-agent orchestration plugin for Claude Code, inspired by primitive tribal governance systems.

## Architecture

```
.claude-plugin/
├── marketplace.json          # Plugin manifest
├── agents/                   # 8 Agents (subagent_type: "fireside:{name}")
│   ├── zhencha.md            # 🦅 Scout — reconnaissance
│   ├── lieshou.md            # 🐺 Hunter — aggressive proposals
│   ├── caiji.md              # 🐝 Gatherer — conservative proposals
│   ├── wushi.md              # 🦉 Shaman — creative proposals (Tribe only)
│   ├── zhanglao.md           # 🦬 Elder — final verdict
│   ├── gongtou.md            # 🐘 Foreman — task breakdown
│   ├── gongjiang.md          # 🦫 Artisan — code execution
│   └── shouwei.md            # 🐻 Guardian — quality patrol
├── skills/                   # 5 User commands
│   ├── hunt/SKILL.md         # /hunt — full pipeline
│   ├── council/SKILL.md      # /council — deliberation only
│   ├── craft/SKILL.md        # /craft — execution only
│   ├── patrol/SKILL.md       # /patrol — review only
│   └── sos/SKILL.md          # /sos — survival mode
└── hooks/
    └── hooks.json            # Reserved
```

## Agent Naming Convention

- Agent names use pinyin: `fireside:zhencha`, `fireside:lieshou`, etc.
- Each agent has a totem emoji for output decoration
- Agents communicate via intermediate artifacts in `.tmp/fireside/{timestamp}/`

## Scale Classification

| Scale | Code | Criteria | Pipeline |
|-------|------|----------|----------|
| Solo | `solo` | <3 files, single concern | Skip deliberation |
| Party | `party` | 3-8 files, cross-module | Hunter + Gatherer |
| Tribe | `tribe` | >8 files or architectural | + Shaman |

## Rules

- Agents MUST stay within their defined role boundaries
- Artisans MUST NOT modify files outside their assigned task
- Guardian rejections trigger auto-retry (max 2), then escalate to user
- All intermediate artifacts go to `.tmp/fireside/`
