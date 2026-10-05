# illuminati

An agent skill that picks a format a person can check, instead of a wall of prose.

The decision model follows [subhams07/Output-for-Best-Understanding](https://github.com/subhams07/Output-for-Best-Understanding), which is based on Andrej Karpathy's note from 2 Oct 2026. This repository is our own wording and checkers. It is not that project.

## Ladder

Each higher rung is usually easier to check than the one below. For anything that is not a few sentences, start at a diagram or a page.

| Rung | Format | Use when |
| --- | --- | --- |
| 1 | Controlled text, about 80% of the way to ASD-STE100 | A short answer, or the caption under a higher rung |
| 2 | Diagram (Mermaid, else SVG) | Structure, flow, architecture, sequence |
| 3 | One self-contained interactive HTML page | Explore, compare, or step through |
| 4 | Short explainer video | Dense idea, or the reader asked for a video |

Video is not the default. Say the render cost before you start one. If it fails, fall back to the HTML page and say so.

The ASD-STE100 notes here are a working subset, not the official specification. See [asd-ste100.org](https://www.asd-ste100.org/).

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

The scripts are optional checks. Call them by a path relative to this folder (`scripts/verify_ste`). They do not replace the ladder in `SKILL.md`.

## Install

Copy this folder into the skills directory your agent reads. Restart the session so it picks the skill up.
