# agent-skills

Battle-tested skills for disciplined AI-assisted development. Built for [Claude Code](https://claude.com/claude-code), compatible with any tool supporting the [Agent Skills](https://agentskills.io) open standard.

## Skills

| Skill | What it does |
|-------|-------------|
| [`tracking-tasks`](skills/tracking-tasks/SKILL.md) | Enforces disciplined task tracking across context boundaries — never lose work to compaction |
| [`exploring-in-parallel`](skills/exploring-in-parallel/SKILL.md) | Parallelizes codebase exploration by launching multiple subagents simultaneously |
| [`preserving-context`](skills/preserving-context/SKILL.md) | Captures working state before compaction or task switches so work can resume seamlessly |

## Installation

### Via Claude Code Plugin (recommended)

```
/plugin add github:oryanmoshe/agent-skills
```

### Manual

Copy any skill folder into your skills directory:

```bash
# Personal (all projects)
cp -r skills/tracking-tasks ~/.claude/skills/

# Project-specific
cp -r skills/tracking-tasks .claude/skills/
```

## How Skills Work

Each skill is a `SKILL.md` file with YAML frontmatter. Claude reads the `description` field to decide when to activate it — no hooks or configuration needed. Just place the skill in your skills directory and it works.

For details on the skill format, see [Extend Claude with skills](https://code.claude.com/docs/en/skills).

## License

MIT
