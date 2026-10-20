# agent-skills

[Agent Skills](https://agentskills.io) for Claude Code, Codex, omp, and other agents that read `SKILL.md`. Published as a plugin marketplace.

| Plugin | What it does |
|---|---|
| `explain` | Explains a topic, code, diff, or design at one of four levels: L1 ASD-STE100 writing, L2 Mermaid diagram, L3 interactive HTML page, L4 narrated Manim video. |

## Install

Claude Code:

```
/plugin marketplace add zhengzheng-jason/agent-skills
/plugin install explain@zhengzheng-skills
```

Codex:

```bash
codex plugin marketplace add zhengzheng-jason/agent-skills
codex plugin add explain@zhengzheng-skills
```

Codex loads it as the plugin skill `explain:explain`. Pick it with `/skills` or `$`, or let Codex choose it from the description.

omp:

```
/marketplace add zhengzheng-jason/agent-skills
/marketplace install explain@zhengzheng-skills
```

Any other agent (Cursor, Gemini CLI, Copilot, OpenCode, and more) via the [`skills`](https://github.com/vercel-labs/skills) CLI:

```bash
npx skills add zhengzheng-jason/agent-skills --skill explain        # current project
npx skills add zhengzheng-jason/agent-skills --skill explain -g     # all projects
```

Manual: copy or symlink `plugins/explain/skills/explain` into your agent's skills folder:

| Agent | User skills folder |
|---|---|
| Claude Code | `~/.claude/skills/` |
| Codex, and other agents using the shared folder | `~/.agents/skills/` |

## Requirements

- L4 video: Manim and ffmpeg. The skill checks for them and prints install commands when they are missing.
- L2 uses the `archify` skill for standalone diagram files when it is installed; otherwise it is not needed.
