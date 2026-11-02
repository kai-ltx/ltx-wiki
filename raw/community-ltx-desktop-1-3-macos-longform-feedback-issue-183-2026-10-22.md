# LTX Desktop 1.3 macOS Long-Form Workflow Feedback (GitHub Issue #183)

**Source:** https://github.com/Lightricks/LTX-Desktop/issues/183
**Date:** 2026-10-22
**Retrieved:** 2026-11-02

## Content

Single detailed user report (open, unassigned, no labels at fetch). Test setup: LTX Desktop 1.3 (1.3.1 not yet tested), macOS 26.7.1, M4 Max 128 GB, local LTX 2.5 Fast.

Positive: quick setup, no Comfy backend needed, combining generation/refinement/editing in one app "exactly right"; First/Last-Frame works well; short one-shot clips run great. User exceeds 1 minute by using their own audio track (a2v) instead of Extend.

Pain points for 1 to 5 minute projects:
- Gen Space shows "retiring soon" but is the only place to play, favourite and delete clips; Home/Explore are not replacements.
- No project management: no titles, comments, labels; no project file/bundle export or import; asset folder holds only media, metadata presumably in ~/Library/Application Support/LTXDesktop/. Exports are Final Cut XML (~3 KB, structure only) or rendered movie.
- Timeline: no snapping on drop (overlaps trim existing clips), audio lands on unpredictable tracks, waveform mismatch, no scrubbing, crossfades not findable/not working, tiny asset thumbnails.
- Generation: LTX 2.5 Fast local 720p duration only 5/6/8/10/20 s; Extend lengthens the clip rather than making a chainable follow-up, re-extending exhausts memory even at 128 GB and becomes very slow; Extend continues but cannot change an action; gap fill ignores start frame (confirms #179); split audio segments evaluated from file start in a2v (workaround: ffmpeg); no per-generation seed override.

Top requested: project management with labels/export, better timeline, 1 s duration steps, Extend as separate clip, correct audio segment timing.
