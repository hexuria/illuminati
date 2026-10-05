# illuminati

An agent skill for a short understanding ladder:

1. Controlled prose, in the spirit of ASD-STE100 (a working subset, not the official specification).
2. A diagram, when the reader must see structure or flow.
3. One self-contained interactive HTML page, when the reader must explore or compare.
4. An explainer storyboard, when the idea is temporal or too dense for one view.

Stop at the cheapest level that answers the question. A video is not the default.

The folder name and the invocation are both `illuminati`.

## How an agent runs it

1. Read `SKILL.md`.
2. Write the question the reader must be able to answer.
3. Write the explanation in controlled prose.
4. Run `scripts/verify_ste` on that file. Fix hard failures. Treat passive-voice lines as warnings.
5. Climb only when the prose is not enough:
   - flow or architecture: write a `.mmd` file and run `scripts/render_diagram`
   - exploration or comparison: write one HTML file and run `scripts/verify_html`
   - time or density: write a storyboard with the headings Hook, Mechanism, and Check, then run `scripts/render_video`
6. Hand the reader the artifacts that were actually needed.

`scripts/render_video` checks the storyboard. It does not build a video. ffmpeg, Manim, and text-to-speech are optional later steps. HeyGen is not required.

## Layout

```text
illuminati/
├── SKILL.md
├── README.md
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

The scripts are the harness. The reference files say when to use each rung and what the script checks.
