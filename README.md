# agent-skills

Skills for Claude Code and omp, published as a plugin marketplace.

| Plugin | What it does |
|---|---|
| `explain` | Explains a topic, code, diff, or design at one of four levels: L1 ASD-STE100 writing, L2 Mermaid diagram, L3 interactive HTML page, L4 narrated Manim video. |

## Install

Claude Code:

```
/plugin marketplace add zhengzheng-jason/agent-skills
/plugin install explain@zhengzheng-skills
```

omp:

```
/marketplace add zhengzheng-jason/agent-skills
/marketplace install explain@zhengzheng-skills
```

Manual: copy or symlink `plugins/explain/skills/explain` to `~/.claude/skills/explain`.

## Requirements

- L4 video: Manim and ffmpeg. The skill checks for them and prints install commands when they are missing.
- L2 uses the `archify` skill for standalone diagram files when it is installed; otherwise it is not needed.
