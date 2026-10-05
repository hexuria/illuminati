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

The goal is one check the reader can do. Pick Explain, Visualize, Demonstrate, Simulate, or Animate. Do not do all five.

Premise: code is cheap, so a custom diagram, page, or short video is worth making when it helps a person check the work. Do not default to long prose.

## Trigger

Use this when the reader says "explain", "help me understand", "walk me through", "what did you just change", "summarize this", or "make this easier to follow". Also use it when a plain-text answer would be long, dense, or split into parts.

## The ladder

```text
illuminati
├── Explain
├── Visualize
├── Demonstrate
├── Simulate
└── Animate
```

Each step is a different kind of check. Do not do all five. Pick the first one that lets the reader verify the claim, then add one step only if that check is still blind.

| Step | The reader can | Deliver |
| --- | --- | --- |
| Explain | Say what it does, in a few sentences | Controlled text in the message. A small Markdown table if the comparison is short. |
| Visualize | See how the pieces connect | A Mermaid diagram in the chat. An image only when Mermaid cannot say it. |
| Demonstrate | Walk one real case | A page, a CSV, a PDF, or a longer Markdown file with one worked example. Attach it. |
| Simulate | Change an input and see the result | One interactive HTML file: a slider, a step button, or a side-by-side compare. |
| Animate | Watch the change over time | A short video, only if a still page cannot show it, or the reader asked. Say the cost first. |

### How to choose

- A few sentences stay at Explain. Do not add a picture to look thorough.
- If the reader must check structure, start at Visualize.
- If they must follow one case, use Demonstrate.
- If they must try a "what if", use Simulate. A static page is Demonstrate, not Simulate.
- Animate last. If render fails, say so and fall back to Simulate.
- If you are unsure, deliver Explain and offer the one next step. Do not ask a list of questions.


## Grok Bot surfaces

When you run inside Grok Bot, deliver on a surface this chat can actually show. Do not invent a viewer.

In the message:

- Markdown, including lists and tables. This is Explain, and the caption under any later step.
- A Mermaid diagram, in a fenced `mermaid` block. This is Visualize. It renders in the chat.
- Math, with `\( ... \)` inline and `$$ ... $$` on its own line.
- An image, attached on the same message. Use this when a diagram is not Mermaid (a chart, a screenshot, an SVG or PNG).
- A video, as its own attachment. This is Animate, and only after a real render.
- A voice memo, only when the reader asked to hear the answer.

As a file attached to the message, when the artifact is bigger than a chat bubble:

- HTML, when the reader must click, compare, or step through.
- CSV or TSV, when the reader must sort, filter, or open rows in a spreadsheet. A small comparison stays a Markdown table.
- PDF, when the reader must keep a fixed document.
- A Markdown file, when the controlled text is too long for the bubble.
- SVG or PNG, when the picture must leave the chat.

Do not claim a separate HTML viewer, PDF viewer, or document viewer. Attach the file. If the app previews it, that is extra. The file must still stand on its own.

A question widget, a secret prompt, and a cloud-agent card are controls. They are not steps on this ladder. Do not use them to explain.

Pick one primary artifact. You may add a short Markdown caption. Do not dump every format.

## Explain

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

## Visualize

Prefer a diagram over paragraphs for architecture, data flow, dependencies, sequences, state, ownership, timelines, and before/after.

Lightest tool that works:

1. Mermaid in a fenced `mermaid` block in the chat (flowchart, sequenceDiagram, stateDiagram, classDiagram, erDiagram). In Grok Bot this is the diagram. Do not also attach the same diagram as an image.
2. Inline SVG in the HTML page when the layout must be custom.
3. A PNG or SVG file when the reader must paste it into slides or a doc.

Label every box and every edge. Keep about 12 nodes. Split a larger picture into several diagrams. After the diagram, write 1 to 3 sentences that say what to look at. Do not retell the diagram.

Optional check: `scripts/render_diagram <file.mmd>`. It accepts a file that starts with a mermaid keyword. It writes an SVG only if `mmdc` is installed.

Notes: `references/diagram.md`.

## Demonstrate and Simulate

Demonstrate is one worked case the reader can follow. Simulate is the same case with a control that changes an input. If there is no control, stop at Demonstrate.

- One self-contained `.html` file. Inline CSS and JS. No build step. No required network. A CDN script is allowed only if it adds real value and the page still shows the core content without it.
- A clear title and a two-sentence summary at the top.
- Collapsible sections, tabs, or a table of contents when the page is long.
- Controls that teach: a slider, a step button, a filter, a side-by-side compare, a clickable node. Motion only when it shows cause and effect.
- Real content. No placeholder text.
- System font, strong contrast, line width about 70 characters, usable in dark and light, usable on a narrow window.
- Save it under a relative path such as `./explainers/<topic>.html`. In Grok Bot, attach that file in the chat. Elsewhere, open it (`open` on macOS, `xdg-open` on Linux). If you can load it, look at it and fix layout bugs before you hand it over.
- It is disposable. Do not commit it unless the reader asks.

Optional check: `scripts/verify_html <file>`. It requires a title, balanced tags, and no external `http` or `https` URL in `src` or `href`.

Notes: `references/interactive-html.md`.

## Animate

Use this when the reader asks, or when a still page cannot show a change over time. It may fail. Say so if it does.

1. Write a scene script first: hook, intuition, build-up, example, recap. Narration follows the Explain rules. If the render will take long, show the script before you render.
2. Animation: Manim Community Edition if `python -c "import manim"` works. Otherwise say what is missing. Do not pretend a video exists.
3. Narration: if `ELEVENLABS_API_KEY` is already in the environment, you may use it. Never ask the reader to paste a key into chat. Never print the key. If it is not set, use a local speech tool that is already installed, and say the quality trade-off.
4. Assemble with ffmpeg. Match each scene length to its audio clip. Add captions if that is cheap.
5. Render a low-quality draft first. Render the final file only after the draft pacing is right.
6. Deliver the `.mp4` path, the duration, and two sentences on what it covers. Keep it about 2 to 5 minutes unless asked for longer.

If render or speech fails and you cannot fix it, say that and fall back to Simulate.

`scripts/render_video` only checks that a storyboard has the headings Hook, Mechanism, and Check. It does not make a video.

Notes: `references/explainer-video.md`.

## Oversight

When the thing to understand is work you just did (a large diff, a refactor, a research result):

- Lead with a diagram or a page of what changed and why. Do not lead with a changelog.
- Name the 3 to 5 decisions that matter, and the risks, in short bullets.
- Tie each claim to a file, a line, or a test result the reader can open.
- If you already answered in prose and the topic was large, offer one diagram or one page. Do not offer a menu.

## Pitfalls

- Do not pick a later step only because it looks more finished.
- Do not use this controlled style for persuasion or fiction. It is for explanation and procedures.
- Do not ship a diagram or a page whose claims you did not check. A clear wrong picture is worse than plain text.
- Do not hand over an HTML file you did not open or render.
- Do not write a secret into a generated file.
