# Community: Third-Party macOS App Ships Broken LTX-2.5 Support, Fixed Same Day (GitHub Issue #88)

**Source:** https://github.com/james-see/ltx-video-mac/issues/88
**Date:** 2026-09-20
**Retrieved:** 2026-09-28

## Content

`ltx-video-mac` (james-see/ltx-video-mac) is a community-built native macOS app for local AI video generation on Apple Silicon, supporting LTX-2, LTX-2.3, LTX-2.5, and MiniMax H3 via an `ltx2Mlx` MLX backend. Issue #88, opened September 20, 2026, reported that every LTX-2.5 generation request (`model_id: ltx25_distilled`) crashed unconditionally with a Python `SyntaxError: unterminated string literal`.

Key details:
- Reproduced identically across three different environment states (no local weights/no HF login; package installed but not logged in; full 66GB weights downloaded plus valid HF authentication) — proving the crash was unconditional and unrelated to auth, missing dependencies, or missing model files.
- Root cause (per maintainer follow-up): a `\n` inside a Swift multi-line string literal (`LTXBridge.swift:1170`) was interpreted literally, splitting an embedded Python string across two lines and breaking the dynamically generated Python script the app `exec`s to run generation.
- Fixed same day in PR #89 by properly escaping the newline (`\\n`) so the embedded Python source compiles correctly.
- App version affected: 2.3.84, tested on Apple Silicon with 48GB unified memory.

## Why this matters for the wiki
This is a third-party/community-integration bug, not a core Lightricks model or API defect, but it illustrates continued friction in the fast-growing ecosystem of unofficial LTX-2.5 wrappers and desktop apps as they race to add support for each new LTX release. It was resolved quickly (same-day PR), which is a positive signal for ecosystem responsiveness even where the initial rollout was broken.
