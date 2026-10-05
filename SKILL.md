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

## Verify

Before you hand the result over, answer three questions:

1. Can the reader say what the thing does?
2. Is each technical name the same name the source uses?
3. Did a shorter sentence drop a condition, a unit, a failure mode, or a name?

If any answer is no, fix that. Do not add another format to hide it.

When the thing to understand is work you just did, name the few decisions that matter and the risk of each. Tie each claim to a file or a test the reader can open.

