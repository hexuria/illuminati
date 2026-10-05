# illuminati

A skill that picks a form a person can check, instead of a wall of prose.

The goal is understanding. After hard work, the reader should be able to say what a thing does, how the pieces connect, and what to verify. The skill chooses the lightest form that makes that check possible, then stops.

## What it produces

| Step | The reader can | Deliver |
| --- | --- | --- |
| Explain | Say what it does | Short controlled text, or a small Markdown table |
| Visualize | See how the pieces connect | A Mermaid diagram, or an image when Mermaid cannot say it |
| Demonstrate | Walk one real case | An attached page, CSV, PDF, or longer Markdown file |
| Simulate | Change an input and see the result | One interactive HTML file |
| Animate | Watch the change over time | A short video, only when a still page cannot show it |

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
3. Stay on Explain when a few sentences are enough. Move to Visualize, Demonstrate, or Simulate only when that check is still blind.
4. Animate only when the reader asks, or when a still page cannot show change over time. Say the cost first.
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
