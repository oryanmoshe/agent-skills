# Agent Skills

A collection of battle-tested skills for disciplined AI-assisted development.

## Project Structure

```
skills/                   # All skills live here
  tracking-tasks/         # Each skill is a folder with SKILL.md
    SKILL.md
  ...
.claude-plugin/
  plugin.json             # Plugin manifest for Claude Code marketplace
```

## Skills

| Skill | Description |
|-------|-------------|
| `tracking-tasks` | Enforces disciplined task tracking across context boundaries |
| `exploring-in-parallel` | Parallelizes codebase exploration by launching multiple subagents simultaneously |
| `preserving-context` | Captures working state before compaction or task switches |
| `committing-code` | Writes git commits using conventional commits with gitmoji |
| `managing-agents-md` | Creates and maintains AGENTS.md documentation for AI agents |
| `addressing-pr-feedback` | Fetches, organizes, and addresses GitHub PR review comments |
| `reviewing-code` | Reviews code changes for bugs, performance, security, and best practices |
| `writing-skills` | Guides creation and editing of skills following Anthropic best practices |

## Working in This Repo

**When creating or editing any skill in this repository, you MUST follow the `writing-skills` skill.** This includes:

- Gerund naming (`tracking-tasks`, not `task-tracker`)
- Trigger-rich descriptions (WHAT + WHEN + keywords)
- No installation sections in skills
- Test every skill with a clean subagent before marking it done
- Update README.md and AGENTS.md skill tables when adding new skills
- Commit with gitmoji conventional commits (see `committing-code` skill)

## Contributing

Each skill follows the [Agent Skills](https://agentskills.io) open standard:
- One folder per skill under `skills/`
- Each skill has a `SKILL.md` with YAML frontmatter (`name`, `description`)
- Names use gerund form (`tracking-tasks`, not `task-tracker`)
- No installation instructions in skills — the `description` field handles discovery
