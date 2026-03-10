---
name: patrol
description: "Review only: run Guardian code review and automated tests on current working tree changes. Use after manual edits to check quality before committing."
argument-hint: "[optional focus areas or file paths]"
---

# Patrol (/patrol) — Guardian Review Only

Run code review + automated verification on current working tree changes.

## Workflow

### Step 1: Collect Changes

```bash
mkdir -p .tmp/fireside
git diff --name-only
git diff --stat
```

If no changes found, report: `No changes detected in working tree. Nothing to patrol.`

### Step 2: Call Guardian

```
Agent tool parameters:
  subagent_type: "fireside:shouwei"
  prompt: "Please review the current working tree changes.

[If user provided $ARGUMENTS]
Focus areas: {$ARGUMENTS}

Follow your workflow:
1. Run git diff to inspect all changes
2. Code review (quality, security, style, consistency)
3. Run test suite, linter, type checker
4. Render pass or reject verdict"
  description: "🐻 Guardian patrol"
```

Wait for completion. Save to `.tmp/fireside/shouwei-verdict.md`.

### Step 3: Report

Present the guardian's full review to the user.

---

$ARGUMENTS
