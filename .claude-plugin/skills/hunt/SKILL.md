---
name: hunt
description: "Full pipeline: scout triage → fireside council debate → elder verdict → artisan execution → guardian review. The complete tribe workflow from task to delivered code."
argument-hint: "[--scale solo|party|tribe] task description"
---

# Hunt (/hunt) — Full Pipeline Orchestration

End-to-end orchestration from task input to code delivery. The main agent is a **pure dispatcher**: only passes data, never makes judgments.

## Core Principles

1. You are the dispatcher, not a participant. Do not analyze code, propose solutions, or write code yourself.
2. Each phase is handled by its corresponding agent — you only pass inputs and collect outputs.
3. All intermediate artifacts are saved to `.tmp/fireside/`.
4. This is a **task → code pipeline**.

## Workflow

### Step 1: Parse Arguments

Accept $ARGUMENTS.

**Extract `--scale` parameter (optional):**
- `--scale solo` / `--scale party` / `--scale tribe`
- If present, store as `USER_SCALE` and remove from arguments
- Remaining text is `TASK_DESC`

**If arguments are empty:** Extract task description from recent conversation context. If still unclear, ask the user.

```bash
mkdir -p .tmp/fireside
```

### Step 2: Scout — Reconnaissance

**REQUIRED AGENT CALL:**

```
Agent tool parameters:
  subagent_type: "fireside:zhencha"
  prompt: "Please perform reconnaissance on this task:

Task: {TASK_DESC}

Follow your workflow to scan the codebase and determine task scale (solo/party/tribe)."
  description: "🦅 Scout recon"
```

Wait for completion. Save output to `.tmp/fireside/zhencha-report.md`.

**Determine final scale:**
- If user specified `USER_SCALE`, use that
- Otherwise use scout's determination
- Store as `SCALE`

Report to user: `🦅 Scout recon complete: scale = {SCALE}`

### Step 3: Fireside Council (branch by scale)

**If SCALE = solo:**
Skip council, jump to Step 5. Report: `Solo task — skipping council, proceeding to execution.`

**If SCALE = party:**
Call Hunter + Gatherer in parallel (**1 message, 2 Agent calls**):

```
Agent call #1:
  subagent_type: "fireside:lieshou"
  prompt: "Please propose your Hunter strategy for this task:

Task: {TASK_DESC}

Scout report:
{ZHENCHA_REPORT}

Follow your workflow to research SOTA approaches and propose a bold implementation."
  description: "🐺 Hunter proposal"

Agent call #2:
  subagent_type: "fireside:caiji"
  prompt: "Please propose your Gatherer strategy for this task:

Task: {TASK_DESC}

Scout report:
{ZHENCHA_REPORT}

Follow your workflow to analyze existing code and propose a minimal-change approach."
  description: "🐝 Gatherer proposal"
```

Wait for both. Save to `.tmp/fireside/lieshou-proposal.md` and `.tmp/fireside/caiji-proposal.md`. Proceed to Step 4.

**If SCALE = tribe:**
First call Hunter + Gatherer in parallel (same as above), wait for completion. Then call Shaman:

```
Agent tool parameters:
  subagent_type: "fireside:wushi"
  prompt: "Please synthesize the Hunter and Gatherer proposals and add your Shaman perspective:

Task: {TASK_DESC}

Scout report:
{ZHENCHA_REPORT}

Hunter proposal:
{LIESHOU_PROPOSAL}

Gatherer proposal:
{CAIJI_PROPOSAL}

Follow your workflow to cross-validate both proposals and contribute cross-domain insights."
  description: "🦉 Shaman insight"
```

Wait for completion. Save to `.tmp/fireside/wushi-proposal.md`. Proceed to Step 4.

### Step 4: Elder Verdict

```
Agent tool parameters:
  subagent_type: "fireside:zhanglao"
  prompt: "Please review all council proposals and render your final verdict:

Task: {TASK_DESC}

Scout report:
{ZHENCHA_REPORT}

[Include reports based on SCALE]
Hunter proposal: {LIESHOU_PROPOSAL}
Gatherer proposal: {CAIJI_PROPOSAL}
[If SCALE = tribe] Shaman proposal: {WUSHI_PROPOSAL}

Render your final verdict. Critique the Hunter's recklessness and the Gatherer's excessive caution."
  description: "🦬 Elder verdict"
```

Wait for completion. Save to `.tmp/fireside/zhanglao-decision.md`.

### Step 5: Foreman Task Breakdown

```
Agent tool parameters:
  subagent_type: "fireside:gongtou"
  prompt: "Please decompose this plan into parallelizable subtasks:

{ZHANGLAO_DECISION or ZHENCHA_REPORT+TASK_DESC (for solo tasks)}

Analyze file dependencies and group into execution batches."
  description: "🐘 Foreman breakdown"
```

Wait for completion. Save to `.tmp/fireside/gongtou-tasks.md`. Extract subtask list and batch info.

### Step 6: Artisan Execution

Dispatch artisan agents in batches per the Foreman's plan. **Each batch dispatched in parallel in a single message:**

```
Agent call #N:
  subagent_type: "fireside:gongjiang"
  prompt: "Please execute this subtask:
{TASK_N_DESCRIPTION}
Related files: {TASK_N_FILES}
Read the relevant code and implement the changes."
  description: "🦫 Artisan task N"
```

Wait for batch completion. Save reports to `.tmp/fireside/gongjiang-{N}-result.md`. Continue to next batch.

### Step 7: Guardian Review

```
Agent tool parameters:
  subagent_type: "fireside:shouwei"
  prompt: "Please review all code changes from this hunt:

Elder verdict:
{ZHANGLAO_DECISION}

Artisan reports:
{ALL_GONGJIANG_REPORTS}

Perform code review and automated verification. Check completeness against the elder's verdict."
  description: "🐻 Guardian review"
```

Wait for completion. Save to `.tmp/fireside/shouwei-verdict.md`.

### Step 8: Handle Review Result

**Pass:** Report completion to user. Summarize changes and guardian notes.

**Reject (retries < 2):** Rebuild subtasks from rejection report, pass guardian feedback to new artisan agents, return to Step 6.

**Reject (retries >= 2):** Report failure, recommend manual intervention. All artifacts saved in `.tmp/fireside/`.

---

$ARGUMENTS
