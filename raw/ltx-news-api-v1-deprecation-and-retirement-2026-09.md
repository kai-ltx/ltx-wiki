# LTX API: V1 Video Generation Deprecation and Final Retirement Date

**Source:** https://docs.ltx.io/api-changelog
**Date:** 2026-09-07 (deprecation notice); 2026-09-24 (retirement date confirmed)
**Retrieved:** 2026-09-28

## Content

The LTX API Changelog posted two related entries bookending the research window:

### September 7, 2026 — V1 video generation deprecation
V1 video generation endpoints that have V2 replacements are being deprecated: `/v1/text-to-video`, `/v1/image-to-video`, `/v1/audio-to-video`, `/v1/retake`, and `/v1/extend`. Developers are told to move to the corresponding V2 endpoints to submit background jobs, poll for completion, and download the result. Authentication, generation request parameters, and pricing remain unchanged. The media upload endpoint `/v1/upload` is explicitly NOT part of the deprecation and remains as-is.

### September 24, 2026 — V1 video generation retirement date
The final retirement date was confirmed: after **October 26, 2026 at 11:59 PM UTC**, requests to `/v1/text-to-video`, `/v1/image-to-video`, `/v1/audio-to-video`, `/v1/retake`, and `/v1/extend` will no longer work. Developers must migrate to the corresponding V2 endpoints before then. The upload endpoint `/v1/upload` remains unaffected.

This mirrors the earlier LTX-2 model deprecation pattern (announced July 2, 2026, fully removed August 15, 2026) but this time targets the API's synchronous V1 endpoint generation, not a specific model. See the official migration guide at https://docs.ltx.io/migrate-v1-to-v2.

### Context: other adjacent changelog entries just outside the window
- Sept 2, 2026 (pre-window): `ltx-2-5-pro` gained 1440p/4K and 48fps support, billed at $0.25/s (1440p) and $0.39/s (4K).
- Sept 23, 2026: a separate Video Reframe change also shipped (see companion raw file `ltx-news-api-video-reframe-model-autoselect-2026-09.md`).
