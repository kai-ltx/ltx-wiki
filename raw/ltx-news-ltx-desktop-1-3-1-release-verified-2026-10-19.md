# LTX Desktop 1.3.1 Release Notes (verified on GitHub)

**Source:** https://github.com/Lightricks/LTX-Desktop/releases/tag/v1.3.1
**Date:** 2026-10-19
**Retrieved:** 2026-11-02

## Content

Released 19 Oct 2026 by ltx-desktop-bot, commit 8ffed88 (GPG-verified signature). Marked "Latest". Pre-dates the research window but resolves the item marked unverified in the 2026-10-26 run.

New IC-LoRAs:
- AlphaGen: cut out a subject with no green screen and no prompt; outputs transparent cutout (WebM) plus matte (MP4), frame-aligned.
- Motion Track Control: draw up to three paths on a start frame to move objects or camera; pace control and live preview.
- Video Guide: Pose, Depth or Canny guide video; start frame optional.
- Ingredients: combine up to 10 reference images into one video (new Marketing section).
- IC-LoRA tools keep every frame; "Source" audio mode copies original audio.

1440p and 4K:
- T2V, I2V, A2V and prompt/start-frame LoRAs offer 1440p and 4K. 1440p up to 20 s; 4K up to 10 s; 4K has no 21:9.
- Long clips run in overlapping time windows.
- A 20 s 1080p clip now runs on 32 GB GPUs.

Assistant: plans and queues jobs from plain language on Desktop and phone; can generate, apply styles/effects, run Retake/Extend, find assets, extract frames. Backend choice: Gemini (API key) or a downloadable local model.

Prompt enhancement: Enhance reads the source video for IC-LoRAs, Extend and Retake; can write a prompt from video when empty; Gemini enhance can run during a generation.

Requirements: Windows GPUs with 9 GB+ VRAM and fp8 support can run local generation at smaller settings. macOS 14+ for the app; local generation needs macOS 26+.

Privacy: anonymous analytics now include OS version (and Linux distribution).

Bug fixes: Windows decode memory refusal no longer stops job; Mac long 1080p T2V fixed; Linux "Cannot allocate memory" on large models fixed; Retake/Extend on LTX 2.3 fixed when 2.5 is active; RTL window-button overlap fixed.

Repo state at fetch: 58 open issues, 14 open PRs.
