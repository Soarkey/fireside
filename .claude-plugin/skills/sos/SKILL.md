---
name: sos
description: "Survival mode: skip all deliberation, maximum parallelism, automated-only verification. For production incidents and urgent fixes where speed is critical."
argument-hint: "urgent task description"
---

# SOS (/sos) — Survival Mode

Skip scout, council, and elder verdict. Execute immediately. Trade deliberation quality for maximum speed.

## Core Principles

1. **Skip all deliberation**: No scout, no hunter/gatherer, no elder
2. **Direct breakdown**: Foreman works directly from user description
3. **Full parallel**: All subtasks dispatched in one batch
4. **Fast verification**: Guardian runs automated checks only, skips deep code review

## Workflow

### Step 1: Parse Arguments

Accept $ARGUMENTS as `TASK_DESC`. If empty, ask user to provide.

```bash
mkdir -p .tmp/fireside
```

Report to user: `⚠️ Survival mode activated. Skipping deliberation, executing immediately.`

### Step 2: Foreman Direct Breakdown

```
Agent tool parameters:
  subagent_type: "fireside:gongtou"
  prompt: "[SURVIVAL MODE] Please decompose this task into parallelizable subtasks:

Task: {TASK_DESC}

Note: Survival mode — no elder verdict available. Break down directly from the task description and codebase state. Maximize parallelism in a single batch."
  description: "🐘 Emergency breakdown"
```

Wait for completion. Save to `.tmp/fireside/gongtou-tasks.md`.

### Step 3: All Artisans — Full Parallel

Dispatch **all subtasks in a single message** (no batching):

```
Agent call #N:
  subagent_type: "fireside:gongjiang"
  prompt: "[SURVIVAL MODE] Please execute this subtask:
{TASK_N_DESCRIPTION}
Related files: {TASK_N_FILES}"
  description: "🦫 Emergency fix N"
```

Wait for all to complete. Save reports.

### Step 4: Guardian Fast Check

```
Agent tool parameters:
  subagent_type: "fireside:shouwei"
  prompt: "[SURVIVAL MODE — fast check]

Please perform quick verification on code changes. Automated checks only:
1. Run test suite
2. Run linter
3. Run type checker

**Skip deep code review.** Pass if all automated checks pass.

Artisan reports: {ALL_GONGJIANG_REPORTS}"
  description: "🐻 Emergency check"
```

Wait for completion. Save to `.tmp/fireside/shouwei-verdict.md`.

### Step 5: Report

**Pass:** Report completion. Remind: `Deep code review was skipped. Run /patrol for a full review.`
**Fail (retries < 1):** Re-dispatch artisans with feedback, return to Step 3.
**Fail (retries >= 1):** Report failure (survival mode allows only 1 retry).

---

$ARGUMENTS
