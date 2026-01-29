---
name: writing-skills
description: Guides creation and editing of SKILL.md files following Anthropic best practices and this repo's conventions. Use when creating a new skill, editing an existing skill, porting a skill from another source, or reviewing skill quality. Triggers on "create skill", "new skill", "write skill", "edit skill", "improve skill", or any work that adds or modifies files under skills/.
---

# Writing Skills

## Overview

**A skill is a SKILL.md file that teaches an AI agent a specific technique, workflow, or discipline.** This skill defines how to write them well — with proper naming, trigger-rich descriptions, tested content, and no bloat.

## Skill Structure

```
skills/
  skill-name/
    SKILL.md              # Required — the skill itself
    supporting-file.md    # Optional — only for heavy reference (100+ lines)
```

Every skill is a single folder under `skills/` containing a `SKILL.md` with YAML frontmatter.

## SKILL.md Format

```yaml
---
name: skill-name-in-gerund-form
description: [WHAT it does] + [WHEN to use it]. Be specific about triggers.
---

# Skill Title

## Overview
Core principle in 1-2 sentences.

## [Core content — rules, patterns, workflow]

## Red Flags — STOP
Table of rationalizations and correct actions.

## Anti-Patterns
Common mistakes to avoid.
```

## Naming Rules

**Use gerund form** (verb + -ing) per Anthropic guidelines:

| Good | Bad |
|------|-----|
| `tracking-tasks` | `task-tracker` |
| `reviewing-code` | `code-reviewer` |
| `exploring-in-parallel` | `parallel-exploration` |
| `preserving-context` | `context-preservation` |
| `committing-code` | `commit-helper` |

**Hard constraints:**
- Lowercase letters, numbers, and hyphens only
- Maximum 64 characters
- Cannot contain `anthropic` or `claude`
- Folder name must match the `name` field

## Writing the Description

The `description` field is the **only thing Claude sees before deciding to load your skill**. It must include:

1. **WHAT** the skill does (third person): "Reviews code changes for bugs..."
2. **WHEN** to use it: "Use when reviewing PRs, before committing..."
3. **Trigger keywords** users would naturally say: "commit", "review", "fix comments"

```yaml
# GOOD — specific triggers, clear purpose
description: Reviews code changes for bugs, performance issues, and security problems. Use when reviewing PRs, before committing, or when user asks to review or check code.

# BAD — vague, no triggers
description: Helps with code quality.

# BAD — describes workflow (Claude will shortcut the body)
description: Fetches PR, groups comments, presents summary, lets user select fixes.
```

**Critical:** Never summarize the skill's workflow in the description. Claude may follow the description shortcut instead of reading the full skill body.

## What NOT to Include

- **No installation section** — skills auto-discover via the description field
- **No "When to Use" body section** — this belongs in the description (body loads AFTER triggering)
- **No README or changelog** — keep it to SKILL.md and optional reference files
- **No hook setup** — hooks are a separate system, not part of skills

## Checklist Before Done

1. **Name** is gerund form, hyphens only, matches folder name
2. **Description** includes WHAT + WHEN + trigger keywords, under 1024 chars
3. **Content** is self-contained, concise, actionable
4. **No installation section**, no "When to Use" body section
5. **Tested with a clean subagent** — does the agent understand and follow the skill correctly?
6. **README.md updated** — add skill to the skills table with link and one-line description
7. **AGENTS.md updated** — add skill to the skills table
8. **Committed** with gitmoji conventional commit (see `committing-code` skill)

Steps 6-8 happen with every skill change, not just creation. Treat docs as part of the deliverable, not an afterthought.

## Testing with a Subagent

Before marking a skill as done, launch a test subagent:

```
Task tool with subagent_type="general-purpose":
  "Read [skill path] and evaluate:
  1. Description quality (WHAT + WHEN + triggers, third person, <1024 chars)
  2. Naming (gerund form)
  3. No installation section
  4. Completeness — any gaps?
  5. Token efficiency — any redundancy?"
```

Use `model=haiku` for fast, cheap testing. Fix issues found, then commit.

## Token Budget

Skills should be concise — every token counts when loaded into context:

- Aim for **under 300 lines** for most skills
- Use tables over prose for reference data
- Cut redundancy between Red Flags and Anti-Patterns sections
- Reference other skills by name instead of repeating their content
