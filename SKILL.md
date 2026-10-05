---
name: illuminati
description: >
  Use when someone must understand technical knowledge, not just read cleaner
  prose. Simplify language, remove ambiguity, keep one term for one concept,
  break a hard idea apart, add an example, draw a diagram when relationships
  matter, and check that nothing important was lost. STE100-style writing is
  one technique inside this skill, not the skill itself. Also when they type
  /illuminati.
---

# illuminati

STE100 optimizes technical English for comprehension. Illuminati optimizes technical knowledge for comprehension.

Simplified Technical English is one technique inside this skill. It is an inspiration, not a compliance target. Do not mangle an established technical name to satisfy an aviation writing rule.

```text
Illuminati
├── Simplify language
│      └── STE100-inspired rules
├── Remove ambiguity
├── Normalize terminology
├── Break complex concepts apart
├── Add examples
├── Draw diagrams when useful
└── Verify comprehensibility
```

## Rules

1. Use the simplest word that preserves the meaning.
2. One concept per sentence when possible.
3. One instruction per sentence.
4. Prefer active voice.
5. Use one term for one concept.
6. Never introduce a synonym merely for variety.
7. Explain an abbreviation before you rely on it.
8. Preserve established technical names. `distributed agent execution environment` stays that name if that is the name. Do not split it to satisfy a three-word noun limit.
9. Split a long causal chain into separate sentences.
10. Show an example for an abstract concept.
11. Use a diagram when relationships matter more than prose.
12. Never simplify away technically important information.

Rule 12 wins over every other rule. If a short sentence would drop a condition, a unit, a name, or a failure mode, keep the information and split the sentence.

## STE100-inspired writing

Use this only for the words, not as the goal. A working subset, not the official specification:

- Prefer a simple verb when it means the same thing. `start` instead of `commence`. `fill` instead of `replenish`.
- One approved meaning per word. Do not reuse a word for a second meaning.
- A procedural sentence is about 20 words. A descriptive sentence is about 25. A descriptive paragraph is about 6 sentences.
- One instruction per sentence. Active voice for a procedure.
- Do not drop `the`, `a`, or `this`.
- A warning is its own sentence, before the step it protects.
- A noun cluster of more than 3 words is a signal to check. If the cluster is an established technical name, keep it.

Example of the writing technique only:

> It is imperative that the operator ensures the hydraulic reservoir is replenished prior to commencing operation.

becomes:

> Make sure that the hydraulic reservoir is full before you start the operation.

That rewrite is not the skill. The skill is the list above. The writing rules are step 1.

Optional word check: `scripts/verify_ste <file>`. It flags long sentences and filler. It does not decide whether the knowledge is intact.

## When to leave prose

After the language is simple and the terms are stable:

- Add a concrete example when the concept is abstract.
- Draw a diagram when the reader must see a relationship, a flow, or a structure. In Grok Bot, use a fenced `mermaid` block. Attach an image only when Mermaid cannot say it.
- Attach a worked case (HTML, CSV, PDF, or a longer Markdown file) when one example must be followed in detail.
- Add a control the reader can change only when they must try a "what if".
- Make a short video only when the reader asks, or when a still picture cannot show change over time. Say the cost first. If it fails, say so and keep the still artifact.

Do not produce every form. Stop when the reader can check the claim without losing a technical fact.


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
