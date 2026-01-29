# agent-skills

Battle-tested skills for disciplined AI-assisted development. Built for [Claude Code](https://claude.com/claude-code), compatible with any tool supporting the [Agent Skills](https://agentskills.io) open standard.

## Skills

| Skill | What it does |
|-------|-------------|
| [`tracking-tasks`](skills/tracking-tasks/SKILL.md) | Enforces disciplined task tracking across context boundaries — never lose work to compaction |
| [`exploring-in-parallel`](skills/exploring-in-parallel/SKILL.md) | Parallelizes codebase exploration by launching multiple subagents simultaneously |
| [`preserving-context`](skills/preserving-context/SKILL.md) | Captures working state before compaction or task switches so work can resume seamlessly |
| [`committing-code`](skills/committing-code/SKILL.md) | Writes git commits using conventional commits format with gitmoji |
| [`managing-agents-md`](skills/managing-agents-md/SKILL.md) | Creates and maintains AGENTS.md documentation for AI coding agents |
| [`addressing-pr-feedback`](skills/addressing-pr-feedback/SKILL.md) | Fetches, organizes, and addresses GitHub PR review comments |
| [`reviewing-code`](skills/reviewing-code/SKILL.md) | Reviews code changes for bugs, performance, security, and best practices with priority-based rules |
| [`writing-skills`](skills/writing-skills/SKILL.md) | Guides creation and editing of skills following Anthropic best practices |

## Installation

### Claude Code — Plugin (recommended)

```
/plugin add github:oryanmoshe/agent-skills
```

All skills become available immediately across all projects.

### Claude Code — Manual

Copy individual skill folders into your skills directory:

```bash
# Clone the repo
git clone https://github.com/oryanmoshe/agent-skills.git

# Install all skills (personal — available in all projects)
cp -r agent-skills/skills/* ~/.claude/skills/

# Or install a single skill
cp -r agent-skills/skills/tracking-tasks ~/.claude/skills/

# Or install per-project
cp -r agent-skills/skills/tracking-tasks .claude/skills/
```

### Cursor

Copy skill folders into Cursor's skills directory:

```bash
# Clone and copy to Cursor's skill directory
git clone https://github.com/oryanmoshe/agent-skills.git
cp -r agent-skills/skills/* .cursor/skills/
```

### GitHub Copilot

```bash
cp -r agent-skills/skills/* .github/skills/
```

### Other Tools

These skills follow the [Agent Skills open standard](https://agentskills.io). Any tool that supports `SKILL.md` files can use them. Check your tool's documentation for the skills directory location.

## How Skills Work

Each skill is a `SKILL.md` file with YAML frontmatter. The AI reads the `description` field to decide when to activate it — no hooks or configuration needed. Just place the skill in your skills directory and it works.

```yaml
---
name: skill-name
description: What this does. Use when [specific triggers].
---

# Skill content here...
```

For details on the skill format, see [Extend Claude with skills](https://code.claude.com/docs/en/skills).

## Contributing

See [AGENTS.md](AGENTS.md) for repo conventions. Key rules:

- Skills use **gerund naming** (`tracking-tasks`, not `task-tracker`)
- Every skill must be **tested with a clean subagent** before merging
- **README.md and AGENTS.md** must be updated with each new skill
- Commits use **conventional commits with gitmoji** (see `committing-code` skill)

## License

MIT
