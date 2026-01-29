<p align="center">
  <h1 align="center">agent-skills</h1>
  <p align="center">
    Battle-tested skills for disciplined AI-assisted development.
    <br />
    <em>Because your AI agent should have good habits, not just good vibes.</em>
  </p>
  <p align="center">
    <a href="https://agentskills.io"><img src="https://img.shields.io/badge/Agent_Skills-compatible-blue" alt="Agent Skills Compatible" /></a>
    <a href="https://code.claude.com"><img src="https://img.shields.io/badge/Claude_Code-ready-blueviolet" alt="Claude Code Ready" /></a>
    <a href="https://github.com/oryanmoshe/agent-skills/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-green" alt="MIT License" /></a>
    <a href="https://github.com/oryanmoshe/agent-skills/pulls"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen" alt="PRs Welcome" /></a>
  </p>
</p>

---

## The Problem

AI coding agents are powerful but undisciplined. They forget what they were doing after context compaction. They write "updated stuff" commit messages. They start five things at once and finish none. They skip code review because "it's just a small change."

These skills fix that.

## Skills

| Skill | What it does |
|-------|-------------|
| [`tracking-tasks`](skills/tracking-tasks/SKILL.md) | Never lose work to compaction — enforces task tracking across context boundaries |
| [`exploring-in-parallel`](skills/exploring-in-parallel/SKILL.md) | Stop searching sequentially — launch multiple subagents simultaneously |
| [`preserving-context`](skills/preserving-context/SKILL.md) | Capture working state before compaction so you can resume seamlessly |
| [`committing-code`](skills/committing-code/SKILL.md) | Conventional commits with gitmoji — no more "updated stuff" |
| [`managing-agents-md`](skills/managing-agents-md/SKILL.md) | Create and maintain AGENTS.md so any AI agent can navigate your codebase |
| [`addressing-pr-feedback`](skills/addressing-pr-feedback/SKILL.md) | Fetch, organize, and address GitHub PR review comments systematically |
| [`reviewing-code`](skills/reviewing-code/SKILL.md) | Catch N+1 queries, security issues, and missing tests before they ship |
| [`writing-skills`](skills/writing-skills/SKILL.md) | Meta-skill — how to write skills that actually trigger and work |

## Quick Start

### Claude Code (recommended)

```
/plugin add github:oryanmoshe/agent-skills
```

Done. All 8 skills are now available in every project.

### Claude Code — Manual

```bash
git clone https://github.com/oryanmoshe/agent-skills.git
cp -r agent-skills/skills/* ~/.claude/skills/
```

### Cursor

```bash
git clone https://github.com/oryanmoshe/agent-skills.git
cp -r agent-skills/skills/* .cursor/skills/
```

### GitHub Copilot

```bash
cp -r agent-skills/skills/* .github/skills/
```

### Other Tools

These skills follow the [Agent Skills open standard](https://agentskills.io). Any compatible tool can use them — just copy the skill folders to your tool's skills directory.

## How Skills Work

Each skill is a `SKILL.md` file with YAML frontmatter. The AI reads the `description` field and decides when to activate it automatically — no hooks, no configuration, no ceremony.

```yaml
---
name: tracking-tasks
description: Enforces disciplined task tracking. Use when starting any coding task...
---

# Tracking Tasks

## Overview
Every action must be tracked...
```

Drop it in the skills directory. It just works.

For the full spec, see [Extend Claude with skills](https://code.claude.com/docs/en/skills).

## Contributing

Want to add a skill? See [AGENTS.md](AGENTS.md) for conventions:

- **Gerund naming** — `tracking-tasks`, not `task-tracker`
- **Test with a subagent** before merging — if it doesn't trigger, it doesn't ship
- **Update README + AGENTS.md** with every new skill
- **Conventional commits with gitmoji** — see the [`committing-code`](skills/committing-code/SKILL.md) skill

## License

MIT
