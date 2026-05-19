# LTX API New Async and HDR Endpoints (April–May 2026)

**Source:** https://docs.ltx.video/api-changelog
**Date:** 2026-05-03
**Retrieved:** 2026-05-19

## Content

Two significant batches of new endpoints were added to the LTX REST API between late April and early May 2026.

### April 23, 2026 — HDR Conversion Endpoint

**New endpoint:** `POST /v2/video-to-video-hdr`

Converts SDR (Standard Dynamic Range) video to HDR (High Dynamic Range). Returns per-frame EXR images suitable for professional color grading and HDR rendering pipelines.

Use case: post-production workflows requiring HDR masters from AI-generated SDR footage.

### May 3, 2026 — Async Endpoints for All Major Operations

The Async API was expanded with non-blocking versions of all major generation endpoints:

| Endpoint | Description |
|---|---|
| `POST /v2/text-to-video` | Submit text-to-video job |
| `POST /v2/image-to-video` | Submit image-to-video job |
| `POST /v2/audio-to-video` | Submit audio-to-video job |
| `POST /v2/retake` | Re-generate specific sections of a video |
| `POST /v2/extend` | Add duration to an existing video |

**Async pattern:**
1. Submit job → receive `job_id`
2. Poll `GET /v2/jobs/{job_id}` for status (`pending`, `processing`, `complete`, `failed`)
3. On `complete`, download from `result.video_url`

This matches the pattern used by other async AI APIs (e.g., fal queue, Replicate predictions) and enables long-running generations without HTTP timeout issues.

### Additional LTX-2.3 API Endpoints (from WaveSpeed survey)

Source: https://wavespeed.ai/blog/posts/ltx-2-3-api-endpoints-guide/

LTX-2.3 exposes 7 documented endpoints across providers:
1. Text-to-video
2. Image-to-video
3. Audio-to-video
4. Video retake
5. Video extend
6. Portrait/9:16 generation
7. HDR upscale/conversion

Authentication uses Bearer tokens. Base URL: `https://api.ltx.video/v2`.

### References

- https://docs.ltx.video/api-changelog
- https://wavespeed.ai/blog/posts/ltx-2-3-api-endpoints-guide/
- https://apidog.com/blog/ltx-2-api/
