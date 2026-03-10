---
name: craft
description: "Execute only: foreman task breakdown → artisan execution → guardian review. Use when you already have a plan from /council or your own specification."
argument-hint: "[plan description] or empty to use last council verdict"
---

# Craft (/craft) — Execution Only

Skip deliberation. Start directly from foreman task breakdown: Foreman → Artisans → Guardian.

## Workflow

### Step 1: Determine Plan

Accept $ARGUMENTS.

**If arguments provided:** Use $ARGUMENTS as the execution plan `PLAN`.

**If arguments empty:** Check `.tmp/fireside/zhanglao-decision.md`:
- Exists: Read its content as `PLAN`
- Missing: Ask user to run `/council` first or provide a plan directly

```bash
mkdir -p .tmp/fireside
```

### Step 2: Foreman Task Breakdown

```
Agent tool parameters:
  subagent_type: "fireside:gongtou"
  prompt: "Please decompose this plan into parallelizable subtasks:

{PLAN}

Analyze file dependencies and group into execution batches."
  description: "🐘 Foreman breakdown"
```

Wait for completion. Save to `.tmp/fireside/gongtou-tasks.md`.

### Step 3: Artisan Execution

Dispatch artisans in batches per the Foreman's plan. **Each batch dispatched in parallel in a single message:**

```
Agent call #N:
  subagent_type: "fireside:gongjiang"
  prompt: "Please execute this subtask:
{TASK_N_DESCRIPTION}
Related files: {TASK_N_FILES}"
  description: "🦫 Artisan task N"
```

Wait for batch completion. Save reports to `.tmp/fireside/gongjiang-{N}-result.md`. Continue to next batch.

### Step 4: Guardian Review

```
Agent tool parameters:
  subagent_type: "fireside:shouwei"
  prompt: "Please review all code changes:

Plan: {PLAN}
Artisan reports: {ALL_GONGJIANG_REPORTS}

Perform code review and automated verification."
  description: "🐻 Guardian review"
```

Wait for completion. Save to `.tmp/fireside/shouwei-verdict.md`.

### Step 5: Handle Result

**Pass:** Report completion with change summary.
**Reject (retries < 2):** Re-dispatch artisans with guardian feedback, return to Step 3.
**Reject (retries >= 2):** Report failure, recommend manual intervention.

---

$ARGUMENTS
