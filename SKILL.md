---
name: illuminati
description: >
  Explains a hard idea by climbing a short ladder: controlled prose first,
  then a diagram, then one interactive HTML page, then a video script only
  if the idea is temporal or too dense for one view. Use when the user asks
  to understand, explain, walk through, compare, or oversee complex work,
  when they type /illuminati, or after an agent finishes complex work and
  the reader still needs to see how the pieces connect.
---

# illuminati

Use this skill when a reader must understand a mechanism, a flow, or the result of complex work. The name is the invocation. Do not wait for the reader to name a format.

This is a comprehension and rendering skill for agents. It is not a general writing style. Write the explanation, then prove it with the scripts in `scripts/`. Rules in this file are the short form. The full working rules are in `references/`.

This file is not the ASD-STE100 specification. Do not claim compliance with that specification.

## Routing

Climb in this order. After each artifact, ask one question: can the reader answer the original question with what you have now? If yes, stop. Do not add a diagram, a page, or a video to show effort.

1. **Name the question.** Write one sentence: "The reader must be able to say what X does." If you cannot name it, you are not ready to explain it.
2. **Controlled text.** Always write this first. Follow `references/ste100.md`. Save markdown or text. Run `scripts/verify_ste`. Fix hard failures before you climb.
3. **Diagram.** Climb only if the idea is spatial, architectural, or a flow the reader must see. Follow `references/diagram.md`. Run `scripts/render_diagram` on the `.mmd` file.
4. **Interactive HTML.** Climb only if the reader must explore, compare, or change an assumption ("what if"). Follow `references/interactive-html.md`. Run `scripts/verify_html`. One file. One question.
5. **Explainer video script.** Climb only if the idea is a sequence in time, or if it is too dense to hold in one view. Follow `references/explainer-video.md`. The script must already pass `scripts/verify_ste`. Run `scripts/render_video`. Do not render a video unless the reader asked for a video and the tools exist. A storyboard is a complete result.

Cheap levels are better. Text is cheaper than a diagram. A diagram is cheaper than a page. A page is cheaper than a video.

## What you write at the desk

Keep these rules in view. The checker does not replace them.

- One idea in each sentence. Put the actor first.
- Keep a descriptive sentence at or under 25 words. One action in an instruction.
- Use one word for one thing. Do not switch synonyms.
- Define a new term once, in one sentence, then keep that term.
- Do not use a metaphor as a stand-in for the mechanism.
- Put a warning in its own paragraph. Do not hide it inside a step.
- Banned filler, and the checker fails on these words: various, etc., appropriate, simply, just.

## After complex work

When you finish a design, a change, or a trace, run this skill on the result before you hand it over. Explain the mechanism the reader must check. Do not explain the chronology of your attempts.

## Harness

| Check | Script | Pass means |
| --- | --- | --- |
| Prose | `scripts/verify_ste` | No sentence over 25 words. No banned filler. Passive voice is a warning only. |
| Diagram | `scripts/render_diagram` | The `.mmd` file starts with a mermaid keyword. An SVG is written only if `mmdc` is installed. |
| Page | `scripts/verify_html` | One self-contained HTML file. Title present. No external URL. Tags balance. |
| Video script | `scripts/render_video` | Headings `Hook`, `Mechanism`, and `Check` exist. No video file is required. |

Read the matching file in `references/` before you write that artifact.
