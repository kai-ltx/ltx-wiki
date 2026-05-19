---
title: LTX API Async Endpoints and HDR Conversion
type: technical
created: 2026-05-19
updated: 2026-05-19
sources:
  - raw/tutorial-ltx-api-async-hdr-endpoints-may-2026.md
  - raw/ltx-news-ltx-studio-api-async-hdr-may-2026.md
tags:
  - api
  - async
  - hdr
  - ltx-api
  - rest-api
  - lightricks
---

# LTX API Async Endpoints and HDR Conversion

Two significant endpoint additions were made to the [[ltx-video-api|LTX REST API]] between late April and early May 2026: an HDR conversion endpoint and a full suite of asynchronous generation endpoints under the `/v2/` prefix.

- **API docs:** https://docs.ltx.video/api-changelog
- **Base URL:** `https://api.ltx.video/v2`

## HDR Conversion Endpoint (April 23, 2026)

**Endpoint:** `POST /v2/video-to-video-hdr`

Converts an SDR (Standard Dynamic Range) video to HDR (High Dynamic Range), returning per-frame EXR images suitable for professional color grading and HDR rendering pipelines.

**Use case:** Post-production workflows requiring HDR masters from AI-generated SDR footage. Also available as a one-click UI tool in [[ltx-studio]].

**Output:** Per-frame `.exr` files (OpenEXR format, industry standard for HDR).

## Async Endpoints (May 3, 2026)

All major generation operations are now available as non-blocking async endpoints under `/v2/`. This decouples request submission from result polling, enabling scalable integration into production pipelines without HTTP timeout issues.

### Available Async Endpoints

| Endpoint | Description |
|----------|-------------|
| `POST /v2/text-to-video` | Submit text-to-video job |
| `POST /v2/image-to-video` | Submit image-to-video job |
| `POST /v2/audio-to-video` | Submit audio-to-video job |
| `POST /v2/retake` | Re-generate specific sections of a video |
| `POST /v2/extend` | Add duration to an existing video |

### Async Pattern

```
1. Submit job
   POST /v2/text-to-video
   → Response: { "job_id": "abc123" }

2. Poll for status
   GET /v2/jobs/abc123
   → Response: { "status": "processing" }  (or "pending" / "complete" / "failed")

3. Download result
   GET /v2/jobs/abc123  (when status == "complete")
   → Response: { "status": "complete", "result": { "video_url": "https://..." } }
```

This pattern matches other async AI APIs (fal queue, Replicate predictions) and is the standard approach for production integrations.

### Authentication

All endpoints require Bearer token:
```
Authorization: Bearer YOUR_API_KEY
```

API keys generated at https://console.ltx.video/

## Full LTX-2.3 Endpoint Inventory

LTX-2.3 exposes 7 documented endpoints across providers (per WaveSpeed survey):

1. Text-to-video
2. Image-to-video
3. Audio-to-video
4. Video retake
5. Video extend
6. Portrait / 9:16 generation
7. HDR upscale / conversion

## Integration with LTX Studio

Both the HDR conversion and async generation patterns are reflected in [[ltx-studio]] platform features:

- The platform UI's SDR-to-HDR tool calls the `/v2/video-to-video-hdr` endpoint
- [[ltx-studio-flows|Flows]] automation leverages async endpoint patterns for batch pipeline execution

## References

- [[ltx-video-api]] — Full LTX REST API overview
- [[ltx-video-api-endpoints]] — All endpoints with parameters
- [[ltx-studio]] — Platform UI for HDR conversion and Flows
- [[ltx-studio-flows]] — Workflow automation using async patterns
- [[fal-ai]] — Third-party provider with comparable async queue (`fal_client.submit`)
- [[replicate]] — Third-party provider with webhook-based async
