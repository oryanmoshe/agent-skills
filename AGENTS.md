# Agent Skills

A collection of battle-tested skills for disciplined AI-assisted development.

## Project Structure

```
skills/                   # All skills live here
  tracking-tasks/         # Task tracking discipline
    SKILL.md
  ...                     # More skills to come
.claude-plugin/
  plugin.json             # Plugin manifest for Claude Code marketplace
```

## Skills

| Skill | Description |
|-------|-------------|
| `tracking-tasks` | Enforces disciplined task tracking across context boundaries |
| `exploring-in-parallel` | Parallelizes codebase exploration by launching multiple subagents simultaneously |
| `preserving-context` | Captures working state before compaction or task switches |

## Contributing

Each skill follows the [Agent Skills](https://agentskills.io) open standard:
- One folder per skill under `skills/`
- Each skill has a `SKILL.md` with YAML frontmatter (`name`, `description`)
- Names use gerund form (`tracking-tasks`, not `task-tracker`)
- No installation instructions in skills — the `description` field handles discovery
