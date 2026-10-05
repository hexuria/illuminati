# Explainer video

Climb here only when the idea is a change over time, or when one screen cannot hold the mechanism. Do not make a video for a definition, a small map, or a comparison. Those already have cheaper rungs.

Stop if the prose, the diagram, or the page already lets the reader answer the question. A video the reader did not need is a worse explanation, because it is harder to check.

## Storyboard

Write markdown. It must pass `scripts/verify_ste` before you treat it as a script. Use the same synonym lock as the prose.

Required headings, spelled this way:

```markdown
# Hook

# Mechanism

# Check
```

- **Hook.** The question, and the part the reader cannot see from the outside.
- **Mechanism.** The beats in order. One beat is one change. Keep each sentence inside the prose limit.
- **Check.** A prediction the reader can now make: a close, a failure, or a boundary. If the reader cannot check the idea, the script is not done.

You may add more headings. You may not rename these three.

## Render is optional

ffmpeg, Manim, and local text-to-speech are optional tools. Do not require HeyGen, a hosted voice, or an API key.

`scripts/render_video FILE.md` does not build a video and does not call those tools.

- If Hook, Mechanism, or Check is missing, it exits non-zero.
- If ffmpeg is not installed, it exits 0 and prints `script-only, ffmpeg not installed`.
- If ffmpeg is installed, it still exits 0 without writing a media file. It only confirms the headings.

A later step may render pictures and call ffmpeg. That step is out of scope until the reader asks for a video and the tools are present. Do not invent frames.
