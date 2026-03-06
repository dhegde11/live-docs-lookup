# agent-skills

A collection of skills for AI coding assistants — Claude Code, Cursor, Codex, OpenCode, and others that support the skills plugin format.

## What are skills?

Skills are reusable instruction sets that extend what an AI coding assistant can do. Each skill lives in its own directory and contains a `SKILL.md` file with a name, a trigger description, and step-by-step instructions. When you install a skill, the assistant automatically invokes it when the trigger conditions are met.

## Skills in this repo

| Skill | What it does |
|-------|-------------|
| [live-docs-lookup](./live-docs-lookup/) | Fetches current AI SDK/API documentation before answering — prevents stale training data from producing wrong model IDs, deprecated parameters, or missed APIs |

## Installing a skill

### Claude Code (recommended)

Copy the skill directory into `~/.claude/skills/`:

```bash
cp -r live-docs-lookup ~/.claude/skills/
```

The skill is active immediately — no restart needed.

### Other tools

Check your tool's documentation for the skills or plugins directory. The `SKILL.md` format is shared across tools that support it.

## License

MIT — see [LICENSE](./LICENSE).
