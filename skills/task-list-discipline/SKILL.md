---
name: task-list-discipline
description: Use when starting any task, planning work, discovering new items mid-task, or before context compaction. Applies to ALL work sessions regardless of task size or complexity.
---

# Task List Discipline

## Overview

**Every action must be tracked.** The task list is your memory across context boundaries. No mental notes. No exceptions. If it's not written down, it will be lost at the next compaction.

## Installation

Place this skill at `~/.claude/skills/task-list-discipline/SKILL.md` (personal) or install via plugin. To ensure it triggers reliably:

1. **Add to your CLAUDE.md** (project or global `~/.claude/CLAUDE.md`):
   ```markdown
   ## Task List Management
   **REQUIRED:** Use `task-list-discipline` skill for all work.
   Key rules: never delete tasks, track ALL work in TodoWrite, checkpoint before compaction.
   ```

2. **Optional startup hook** to force activation on every session:
   ```json
   {
     "hooks": {
       "SessionStart": [{
         "type": "command",
         "command": "echo 'REQUIRED: Use task-list-discipline skill - track ALL work in TodoWrite.'"
       }]
     }
   }
   ```
   Add this to `.claude/settings.json` (project) or `~/.claude/settings.json` (global).

3. **Verify it's working:** At the start of any session, Claude should create tasks via `TaskCreate` before doing any work.

## When to Use

Every work session that involves creating, modifying, or debugging code.

- Starting a new task from the user
- Discovering sub-tasks or issues mid-work
- Before context compaction (system warning)
- Switching between unrelated tasks
- Resuming work from a previous session

**Skip for:** Purely informational questions that require no code changes ("What files handle routing?", "Explain this function").

## Core Rules

### RULE 1: Track Before Acting

```
NEVER start work without a task created via TaskCreate.
"I'll just quickly..." → CREATE TASK FIRST
```

### RULE 2: Never Delete

```
NEVER delete tasks. EVER.

Done?        → Mark completed
Not needed?  → Mark completed + note why
Wrong?       → Mark completed + create corrected task
```

**Why:** Deleted tasks lose history. Completed tasks preserve context for future sessions.

### RULE 3: One In-Progress at a Time

```
Maximum ONE task as in_progress at any time.
Starting new work? Complete or pause current first.
```

This prevents confusion about what you're actually doing and makes status clear to the user.

### RULE 4: Deviation Protocol

When you discover something unexpected while working:

```
1. KEEP current task as in_progress
2. CREATE new task (pending) for the discovery
3. Note in description: "Discovered while working on #N"
4. DECIDE: handle now (switch in_progress) or defer
5. RETURN to original task when done
```

### RULE 5: Pre-Compaction Checkpoint

Before context compaction:

```
1. ALL discovered work captured as tasks
2. Current task status accurate
3. Blocked tasks have reason noted
4. NO mental notes — everything in TaskCreate/TaskUpdate
```

## Task Lifecycle

```
pending ──→ in_progress ──→ completed
```

**Blocked?** Keep as `pending` or `in_progress` and note the blocker in the task description. There is no separate "blocked" status — use descriptions to communicate why.

Use `TaskCreate` to create tasks, `TaskUpdate` to change status, `TaskList` to review.

## Resuming a Session

When continuing work from a previous session or after compaction:

1. Run `TaskList` to see all existing tasks
2. Review `in_progress` and `pending` tasks — are statuses still accurate?
3. Update any stale statuses via `TaskUpdate`
4. Resume the highest-priority `pending` task or continue the `in_progress` one

## Red Flags — STOP

| Thought | Action |
|---------|--------|
| "I'll just quickly fix this" | CREATE TASK FIRST |
| "This is too small to track" | CREATE TASK ANYWAY |
| "I'll remember to come back" | CREATE TASK NOW |
| "Let me clean up old tasks" | NEVER DELETE |
| "I have two things in progress" | PAUSE ONE |
| "I'll batch-add tasks later" | ADD EACH AS DISCOVERED |

## Anti-Patterns

**Mental task list:** If it's not in TaskCreate, it will be lost at compaction.

**Batching discoveries:** Add each task as discovered, not in batches later.

**Multiple in_progress:** Creates confusion about what you're actually doing.

**Vague descriptions:** "Fix bug" vs "Fix null pointer in UserService.getById at line 45"

**Deleting tasks:** Losing history. Mark completed with a note instead.

## Quick Start Template

When a session begins:

```
TaskCreate: "[Main task from user request]"  → in_progress
TaskCreate: "Verify changes work correctly"  → pending
```

When discovering issues mid-work:

```
TaskCreate: "Discovered: [issue] while working on #N"  → pending
```

Before compaction:

```
TaskUpdate: Ensure all statuses are accurate
TaskCreate: Any remaining mental notes as tasks
```
