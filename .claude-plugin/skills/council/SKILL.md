---
name: council
description: "Deliberation only: scout triage → hunter-gatherer debate → elder verdict. Produces an implementation plan without touching code. Run /craft to execute later."
argument-hint: "task description"
---

# Council (/council) — Deliberation Only

Run scout reconnaissance → fireside council debate → elder verdict. Produces an implementation plan but **does not execute code changes**.

## Core Principles

1. You are the dispatcher, not a participant.
2. This command **does not execute code changes** — it only produces a plan.
3. All intermediate artifacts are saved to `.tmp/fireside/`.

## Workflow

### Step 1: Parse Arguments

Accept $ARGUMENTS as `TASK_DESC`. If empty, extract from conversation context.

```bash
mkdir -p .tmp/fireside
```

### Step 2: Scout — Reconnaissance

```
Agent tool parameters:
  subagent_type: "fireside:zhencha"
  prompt: "Please perform reconnaissance on this task:

Task: {TASK_DESC}

Scan the codebase and determine task scale (solo/party/tribe)."
  description: "🦅 Scout recon"
```

Wait for completion. Save to `.tmp/fireside/zhencha-report.md`. Extract `SCALE`.

### Step 3: Fireside Council

**Regardless of scale, /council always runs the full council** (even for solo tasks — the user explicitly requested deliberation).

Call Hunter + Gatherer in parallel (1 message, 2 Agent calls):

```
Agent call #1:
  subagent_type: "fireside:lieshou"
  prompt: "Please propose your Hunter strategy for this task:

Task: {TASK_DESC}
Scout report: {ZHENCHA_REPORT}"
  description: "🐺 Hunter proposal"

Agent call #2:
  subagent_type: "fireside:caiji"
  prompt: "Please propose your Gatherer strategy for this task:

Task: {TASK_DESC}
Scout report: {ZHENCHA_REPORT}"
  description: "🐝 Gatherer proposal"
```

Wait for both. Save reports.

**If SCALE = tribe:** Additionally call Shaman (passing both Hunter and Gatherer reports).

### Step 4: Elder Verdict

```
Agent tool parameters:
  subagent_type: "fireside:zhanglao"
  prompt: "Please review all council proposals and render your final verdict:

Task: {TASK_DESC}
Scout report: {ZHENCHA_REPORT}
Hunter proposal: {LIESHOU_PROPOSAL}
Gatherer proposal: {CAIJI_PROPOSAL}
[If available] Shaman proposal: {WUSHI_PROPOSAL}"
  description: "🦬 Elder verdict"
```

Wait for completion. Save to `.tmp/fireside/zhanglao-decision.md`.

### Step 5: Report

Present the elder's full verdict to the user.

```
Council complete. Verdict saved to .tmp/fireside/zhanglao-decision.md
To execute this plan, run: /craft
```

---

$ARGUMENTS
