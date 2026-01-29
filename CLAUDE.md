@AGENTS.md

## Claude Code Specific

- Commit messages must use conventional commits with gitmoji (e.g., `✨ feat: add new skill`)
- Skills use `TaskCreate`/`TaskUpdate`/`TaskList` as the reference tool interface
- Test every skill with a clean subagent before marking it complete
- **IMPORTANT:** When creating or editing skills in this repo, you MUST use the `writing-skills` skill. Read it first, follow it exactly.
