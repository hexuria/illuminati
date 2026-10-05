---
name: illuminati
description: >
  Use when someone wants to understand, review, or oversee something complex
  (code, a system, a paper, a plan, a concept, or an agent's own work).
  Pick the most digestible format instead of a wall of prose: controlled
  text, then a diagram, then one interactive HTML page, then an explainer
  video. Also when they type /illuminati.
---

# illuminati

Source idea: Andrej Karpathy, "We'll be spending a lot more time trying to understand the outputs of language models" (2 Oct 2026). The rung choices follow the public skill in [subhams07/Output-for-Best-Understanding](https://github.com/subhams07/Output-for-Best-Understanding). This file is our wording of that decision model. It is not that repository.

Premise: code is cheap, so a custom diagram, page, or short video is worth making when it helps a person check the work. Do not default to long prose.

## Trigger

Use this when the reader says "explain", "help me understand", "walk me through", "what did you just change", "summarize this", or "make this easier to follow". Also use it when a plain-text answer would be long, dense, or split into parts.

## The ladder

Each higher rung is usually easier to check than the one below it.

| Rung | Format | Use when | Cost |
| --- | --- | --- | --- |
| 1 | Controlled text, about 80% of the way to ASD-STE100 | The answer fits in a few sentences, or you need a short summary under a higher rung | Lowest |
| 2 | Diagram | Structure, flow, architecture, state, sequence, before and after | Low |
| 3 | One interactive HTML page | Parts to explore, compare, step through, or animate | Medium |
| 4 | Explainer video | A dense concept the reader must internalize, or they asked for a video | Highest |

### How to choose

- For anything that is not trivial, start at rung 2 or rung 3. Stay on rung 1 only when the whole answer fits in a few sentences.
- Use rung 4 only when the reader asks for a video, or the topic is dense and they have time to watch. Say the cost first (render time, and an API key only if narration needs one).
- If you are unsure, deliver the short rung-1 summary and offer one higher rung. Do not ask a list of questions.
- Ask one question of yourself: will a person read this, or check this? If they will check it, use a diagram or a page.
- Do not climb only to look thorough. A three-sentence answer stays three sentences.

## Rung 1: controlled text

ASD-STE100 is a controlled language for technical procedures. These rules are a working subset, not the official specification. Default to about 80% of the way: follow the rules, but keep a needed technical term, or a slightly longer sentence, rather than awkward phrasing. Use the strict form only if the reader asks.

- A step is about 20 words or fewer. A descriptive sentence is about 25 words or fewer.
- A paragraph is about 6 sentences. One topic per paragraph.
- One instruction per sentence. Use the imperative for a step.
- Active voice. Name who or what does the action.
- Simple present, past, or future. Do not drop "the" or "a" to save words.
- One word, one meaning. Do not swap synonyms.
- Plain words. No idioms.
- A warning is its own short sentence, before the step it protects.
- Use a list for a sequence or for parallel items.
- Do not stack nouns. Use a preposition.

Optional check, from this skill folder: `scripts/verify_ste <file>`. It fails a sentence over 25 words and the filler words various, etc., appropriate, simply, and just. Passive voice is a warning only. Fix a hard failure before you climb. The checker is not the official dictionary.

Full notes: `references/ste100.md`.

## Rung 2: diagram

Prefer a diagram over paragraphs for architecture, data flow, dependencies, sequences, state, ownership, timelines, and before/after.

Lightest tool that works:

1. Mermaid in a fenced block (flowchart, sequenceDiagram, stateDiagram, classDiagram, erDiagram).
2. Inline SVG in the HTML page when the layout must be custom.
3. A PNG or SVG file when the reader must paste it into slides or a doc.

Label every box and every edge. Keep about 12 nodes. Split a larger picture into several diagrams. After the diagram, write 1 to 3 sentences that say what to look at. Do not retell the diagram.

Optional check: `scripts/render_diagram <file.mmd>`. It accepts a file that starts with a mermaid keyword. It writes an SVG only if `mmdc` is installed.

Notes: `references/diagram.md`.

## Rung 3: HTML page

For complex output, ask "can this be a page?"

- One self-contained `.html` file. Inline CSS and JS. No build step. No required network. A CDN script is allowed only if it adds real value and the page still shows the core content without it.
- A clear title and a two-sentence summary at the top.
- Collapsible sections, tabs, or a table of contents when the page is long.
- Controls that teach: a slider, a step button, a filter, a side-by-side compare, a clickable node. Motion only when it shows cause and effect.
- Real content. No placeholder text.
- System font, strong contrast, line width about 70 characters, usable in dark and light, usable on a narrow window.
- Save it under a relative path such as `./explainers/<topic>.html`. Open it (`open` on macOS, `xdg-open` on Linux). If you can load it, look at it and fix layout bugs before you hand it over.
- It is disposable. Do not commit it unless the reader asks.

Optional check: `scripts/verify_html <file>`. It requires a title, balanced tags, and no external `http` or `https` URL in `src` or `href`.

Notes: `references/interactive-html.md`.

## Rung 4: explainer video

Use this when the reader asks, or when a still page cannot show a change over time. It may fail. Say so if it does.

1. Write a scene script first: hook, intuition, build-up, example, recap. Narration follows the rung-1 rules. If the render will take long, show the script before you render.
2. Animation: Manim Community Edition if `python -c "import manim"` works. Otherwise say what is missing. Do not pretend a video exists.
3. Narration: if `ELEVENLABS_API_KEY` is already in the environment, you may use it. Never ask the reader to paste a key into chat. Never print the key. If it is not set, use a local speech tool that is already installed, and say the quality trade-off.
4. Assemble with ffmpeg. Match each scene length to its audio clip. Add captions if that is cheap.
5. Render a low-quality draft first. Render the final file only after the draft pacing is right.
6. Deliver the `.mp4` path, the duration, and two sentences on what it covers. Keep it about 2 to 5 minutes unless asked for longer.

If render or speech fails and you cannot fix it, say that and fall back to rung 3.

`scripts/render_video` only checks that a storyboard has the headings Hook, Mechanism, and Check. It does not make a video.

Notes: `references/explainer-video.md`.

## Oversight

When the thing to understand is work you just did (a large diff, a refactor, a research result):

- Lead with a diagram or a page of what changed and why. Do not lead with a changelog.
- Name the 3 to 5 decisions that matter, and the risks, in short bullets.
- Tie each claim to a file, a line, or a test result the reader can open.
- If you already answered in prose and the topic was large, offer one diagram or one page. Do not offer a menu.

## Pitfalls

- Do not pick a higher rung only because it looks more finished.
- Do not use this controlled style for persuasion or fiction. It is for explanation and procedures.
- Do not ship a diagram or a page whose claims you did not check. A clear wrong picture is worse than plain text.
- Do not hand over an HTML file you did not open or render.
- Do not write a secret into a generated file.
