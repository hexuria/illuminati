# illuminati

A skill that picks a form a person can check, instead of a wall of prose.

The goal is understanding. After hard work, the reader should be able to say what a thing does, how the pieces connect, and what to verify. The skill chooses the lightest form that makes that check possible, then stops.

## What it produces

| Form | Use when |
| --- | --- |
| Controlled text | The answer fits in a few sentences, or you need a caption under a richer form |
| Diagram | The reader must see structure, flow, architecture, or a sequence |
| Interactive page, table, or document | The reader must explore, compare, step through, or keep the result |
| Short explainer video | The idea changes over time, or the reader asked for a video |

Controlled text stays about 80% of the way to ASD-STE100: short sentences, one word for one thing, the actor named, a warning in its own sentence. That is a working subset in `references/ste100.md`. It is not the official specification.

In Grok Bot, put the result on a surface the chat can show:

- Markdown in the message, including a table when the comparison is small
- A Mermaid diagram in a fenced block
- An image on the same message, when the picture is not Mermaid
- An attached HTML file, CSV, PDF, longer Markdown file, or video, when the artifact is bigger than the bubble

Do not assume a separate viewer. The file has to stand on its own. A question widget and a cloud-agent card are controls, not explanations.

## How to run it

1. Read `SKILL.md`.
2. Name the one thing the reader must be able to say.
3. For anything past a few sentences, start with a diagram or a page. Stay on text only when the whole answer is short.
4. Use a video only when the reader asks, or when a still page cannot show change over time. Say the cost first.
5. Optional checks live in `scripts/`. Call them by a path relative to this folder.

## Layout

```text
illuminati/
├── SKILL.md
├── references/
│   ├── ste100.md
│   ├── diagram.md
│   ├── interactive-html.md
│   └── explainer-video.md
└── scripts/
    ├── verify_ste
    ├── render_diagram
    ├── verify_html
    └── render_video
```

Copy this folder into the skills directory your agent reads, then start a new session.
