# Founder Reel MVP

## Product direction

Turn a founder's raw talking-head recording into a polished, vertical social video, guided by a reference Reel they like.

The product is not a general-purpose motion-graphics editor. The primary workflow is:

1. Upload a reference video (or a legally accessible file the user has permission to use).
2. Upload raw founder footage.
3. Analyze the reference's editing pattern: pacing, shot changes, caption treatment, framing, overlays, and audio style.
4. Transcribe the founder footage and identify pauses, sentence boundaries, and useful cut points.
5. Generate an editable edit plan and preview.
6. Render a 9:16 video with captions, cuts, reframing, optional B-roll, music/audio mixing, and brand styling.
7. Let the founder request targeted revisions and export a post-ready file.

Use the reference as inspiration for editing language; do not copy its footage, logos, or other protected creative elements into the output without permission.

## MVP principles

- **Reference-guided, not reference-copied:** match broad pacing and treatment while preserving the founder's own content and identity.
- **Editable, not flattened-only:** retain a project/edit plan so the user can change captions, cuts, crop, B-roll, and styling after generation.
- **Preview before render:** show a draft edit plan and a quick preview before expensive final rendering.
- **Targeted revisions:** a request like "make captions smaller" should modify caption styling only, not regenerate the entire edit.
- **Affordable by design:** use deterministic video/audio processing for cuts, captions, resizing, and mixing; use models only where interpretation or selection adds value.
- **Safe uploads:** validate file types and duration, isolate processing, and never expose provider keys in client code.

## First MVP scope

### Required
- Upload reference video and raw founder video.
- Transcription with timestamps.
- Reference analysis for aspect ratio, cut timing, caption position/style cues, and average shot duration.
- Automatic 9:16 reframing with a manual crop override.
- Word- or phrase-timed captions with a small set of polished styles.
- Silence/pause trimming with a reviewable cut list.
- Simple branded end card and logo option.
- Preview, undo/revert, and MP4 export.
- A revision panel with safe, structured operations such as:
  - change caption style/size/position
  - tighten or loosen pacing
  - change crop/reframing
  - add/remove an approved B-roll segment
  - adjust music volume
- Persist an editable edit plan alongside rendered output.

### Defer until the core workflow works
- Automatic publishing to social networks.
- Full social account management and analytics.
- Complex generative video creation.
- Multi-user workspaces and agency workflows.
- Large stock-media marketplace.
- Fully autonomous edits without a review step.

## Suggested architecture

Keep OpenFilm's rendering and project foundation where it fits, but validate this before committing the product to it.

- **Media ingest:** probe and validate uploaded assets; generate low-resolution proxies and thumbnails.
- **Speech pipeline:** ASR with word timestamps; detect silence and candidate cut points.
- **Reference analyzer:** extract shot boundaries, timing, framing, caption/overlay positions, and broad style features.
- **Edit planner:** produce a validated, versioned JSON edit plan; never allow an LLM to rewrite the entire project for a small change.
- **Timeline/render adapter:** translate the edit plan into OpenFilm's project format and render with the existing engine where possible.
- **Revision engine:** apply scoped operations, record inverses, and support undo/redo.
- **Export:** render vertical MP4, with audio normalization and safe margins for platform UI overlays.

## First technical spike

Before changing core editor architecture, prove one end-to-end sample:

1. Take one reference Reel and one 30–90 second founder recording.
2. Transcribe the founder recording with timestamps.
3. Produce a basic edit plan: trim pauses, add timed captions, apply 9:16 crop, and match approximate cut rhythm.
4. Render a draft MP4.
5. Apply a targeted change (e.g. "move captions higher") without rebuilding unrelated edit decisions.
6. Confirm the result is reproducible and can be reverted.

## Success criteria for the spike

- Output is understandable and visually coherent without manual timeline editing.
- Captions align with speech and remain inside safe areas.
- The founder's message and identity are preserved.
- A targeted revision changes only its intended properties.
- Re-running the same edit plan yields the same output, within renderer limitations.
- Processing time and model cost are measured, not guessed.

## Licensing and branding

This repository is a fork of OpenFilm. Preserve the upstream MIT license and notices. Before distributing a branded product, use a distinct product name, logo, app identity, and update feed; review upstream trademark guidance. Audit all dependencies and media assets for their own licenses.
