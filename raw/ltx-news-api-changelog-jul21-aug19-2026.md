# LTX API Changelog, 2026-07-21 to 2026-08-19: New Domain, 720p Tier, LTX-2 Removal, Audio-to-Video Parity

**Source:** https://docs.ltx.io/api-changelog
**Date:** 2026-08-19
**Retrieved:** 2026-08-24

## Content

Seven LTX API changelog entries fall in the 2026-07-21 to 2026-08-24 window (newest first):

**Aug 19, 2026 — Audio-to-video generation params.** Audio-to-video now accepts `fps` (default 24), `last_frame_uri` (requires `image_uri`), and `camera_motion`, matching text-to-video and image-to-video. Available on `v2/audio-to-video` (async) and `v1/audio-to-video` (sync).

**Aug 18, 2026 — Audio-to-video resolution parity.** Audio-to-video now supports the same resolution tiers as text-to-video and image-to-video: `ltx-2-5-fast` up to 4K, `ltx-2-5-pro` up to 1080p, `ltx-2-3-pro` up to 4K. Maximum input audio length varies by model and tier — e.g. `ltx-2-3-pro` accepts up to 20 seconds at 720p/1080p and up to 10 seconds at 1440p/4K. New tiers billed at standard published rates.

**Aug 16, 2026 — LTX-2 removal completed.** `ltx-2-fast` and `ltx-2-pro` are no longer available; requests specifying them now return an error. This closes out the July 2, 2026 deprecation notice (which had scheduled removal for August 15, 2026). Migration path: LTX-2.3 (`ltx-2-3-fast`, `ltx-2-3-pro`) or LTX-2.5 (`ltx-2-5-fast`, `ltx-2-5-pro`).

**Aug 11, 2026 — LTX-2.5 on the API.** New models for text-to-video, image-to-video and audio-to-video in portrait and landscape: `ltx-2-5-fast` up to 4K, `ltx-2-5-pro` at 720p and 1080p. Audio-to-video generates at 1080p on both (superseded by the Aug 18 parity change). Both accept camera motion, `last_frame_uri` on image-to-video, and `"duration": null` for automatic duration.

**Aug 10, 2026 — Automatic duration.** Text-to-video and image-to-video accept `"duration": null` on `ltx-2-5-fast`, letting the model choose clip length from the prompt. (Shipped one day ahead of the public LTX-2.5 launch.)

**Aug 2, 2026 — 720p video generation on LTX-2.3.** Text-to-video and image-to-video gained a 720p output tier on LTX 2.3 (`1280x720` landscape, `720x1280` portrait), priced at $0.03/sec on `ltx-2-3-fast` and $0.04/sec on `ltx-2-3-pro`.

**Jul 21, 2026 — New API domain `api.ltx.io`.** The LTX API is now served at `https://api.ltx.io`; docs and code samples use it going forward. Existing integrations on `https://api.ltx.video` keep working unchanged — no migration required.

Note: LTX's product release-notes page (https://ltx.io/release-notes) lists no Studio-side or open-source entries between July 20, 2026 (LTX Explore) and August 11, 2026 (LTX-2.5), so the API changelog is the only source of incremental platform changes in this window.
