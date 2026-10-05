# Interactive HTML

Climb to a page only when the reader must explore, compare, or change an assumption. A page that only restates the prose is waste.

## One file, one question

- Write one HTML file. Put CSS in a `<style>` block. Put script in a `<script>` block.
- Do not load a network resource. No CDN, no remote font, no remote image, no analytics.
- Put the question in `<title>` and in the first heading. The page answers that question and no second question.
- Show the answer without script. Use the script to toggle, filter, or compare. A reader with script off must still see the answer.
- Use `<button>` or a native input for controls. Do not use a click-only `<div>`.
- Show a visible focus style. Do not use color as the only signal.
- Keep the words locked to the prose. Do not introduce a new synonym on the page.

`#` anchors and `data:` URIs are the only URL forms you may use. A relative file path is still a second file. Do not use one.

## What verify_html checks

`scripts/verify_html FILE.html` exits 0 only when all of these hold:

- The path is one file.
- The file is not empty and is under 2 MB.
- A `<title>` exists and is not blank.
- No `src`, `href`, `action`, or CSS `url()` points at `http:`, `https:`, or a protocol-relative `//` URL.
- No `src` or `href` points at another file. Only empty values, `#` anchors, and `data:` URIs pass.
- Start tags and end tags balance after comments and after the insides of `<script>` and `<style>` are ignored. Void tags (`meta`, `link`, `img`, `br`, `hr`, `input`, and the other HTML void tags) may omit an end tag.

The script does not judge whether the page teaches the idea. You still have to match the page to the question.
