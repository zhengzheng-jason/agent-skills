---
name: explain
description: Explain a topic, code, diff, design, or prior AI output at one of four levels from Karpathy's "understanding AI output" ladder - ASD-STE100 writing, diagram, interactive HTML page, or narrated 3b1b-style explainer video. Use when the user asks to explain, clarify, visualize, or teach something, asks for "STE"/"simplified technical English", a diagram, an HTML explainer, or an explainer video, or names a level (L1-L4).
---

# Explain

Four output levels. Each level is easier to absorb than the one before it, and costs more to make.

| Level | Format | Artifact |
|---|---|---|
| L1 | Writing in ASD-STE100 style | Chat text |
| L2 | Diagram | Mermaid block in chat |
| L3 | Web page | One self-contained `.html` file, opened in the browser |
| L4 | Explainer video | Narrated `.mp4` rendered with Manim |

All text inside every level (captions, labels, page copy, narration) follows the L1 writing rules.

## Pick the level

1. The user names a level or format → use it.
2. Otherwise → L1. Add an L2 diagram when the topic has structure that prose hides:
   - flow or sequence (request path, pipeline, algorithm steps)
   - state and transitions
   - components and their links (architecture, data flow, dependencies)
   - hierarchy or a comparison across more than 3 options

   Skip the diagram for definitions, single ideas, rationale, or short answers.
3. Do not escalate to L3/L4 unasked. When the topic would gain much from interaction or motion (a parameter to vary, a process that unfolds in time), end with one line that offers it.

Before explaining code, a diff, or a system, read the source. Explain what it does, not what it probably does.

## L1 - Writing

Default mode is **soft** ("80% of the way to ASD-STE100"). Use **strict** when the user asks for strict STE, full STE, or ASD-STE100 without softening. Rules for both modes: [STE.md](STE.md).

Shape:
- First sentence: the answer or the main point.
- Then the support, one topic per paragraph.
- Use a numbered list for steps and a vertical list for parts.
- Keep code identifiers, commands, and product names exact.

## L2 - Diagram

1. Pick the Mermaid type from the structure: `flowchart` (flow, components), `sequenceDiagram` (calls over time), `stateDiagram-v2` (states), `classDiagram`/`erDiagram` (types, data).
2. Keep at most about 12 nodes. Split larger subjects into several diagrams, one per question.
3. Label each edge with the action or data that moves along it.
4. Write one or two STE sentences below each diagram: what to look at first.
5. Use an ASCII diagram only when Mermaid cannot show the shape (memory layout, bit fields, tables of boxes).
6. Polished architecture, sequence, data-flow, or lifecycle diagram as a standalone file → use the `archify` skill when it is installed.

## L3 - Web page

1. Write one file: `${TMPDIR:-/tmp}/explain/<slug>/index.html`. Use inline CSS and JS. Use a CDN script only for a heavy library the page cannot work without (D3, KaTeX, Three.js), and pin its version.
2. Build the page around interaction that teaches:
   - controls (sliders, toggles, inputs) that change a live model
   - step-through (prev/next) for processes
   - hover or click to reveal detail on diagram parts
3. Structure: title, one-paragraph summary, interactive core, short sections below it. Support light and dark (`prefers-color-scheme`). Use readable type (16px or larger, line length 60-80 characters).
4. Check the page: open it in a browser tab, take a screenshot and look at it, use every control once, and read the console. Fix every error and every visual defect before you hand it over.
5. Run `open <path>` and give the user the path.

## L4 - Explainer video

Follow [VIDEO.md](VIDEO.md). It starts with a check for the required tools. When a tool is missing, give the install commands and stop. Do not make a lower-quality substitute without telling the user.

## Output

- L1/L2: the explanation in chat.
- L3/L4: the file path, a 2-3 sentence summary of what the artifact shows, and what you checked.
- These artifacts are disposable. Do not add them to the repository unless the user asks.
