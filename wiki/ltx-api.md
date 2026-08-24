---
title: LTX API
type: product
created: 2026-04-13
updated: 2026-08-24
sources:
  - https://docs.ltx.video/welcome
  - https://ltx.io/
  - https://docs.ltx.video/open-source-model/integration-tools/pytorch-api
  - raw/tutorial-ltx-2-5-api-v2-integration-and-model-matrix-2026-08.md
tags:
  - ltx-api
  - developer-tools
  - ai-video
  - lightricks
  - ltx-2-5
---

# LTX API

The LTX API is [[lightricks-company]]'s developer API for programmatic video generation, part of the [[ltx-ecosystem]]. It provides HTTP endpoints for generating videos from text, images, and audio.

- **Documentation:** https://docs.ltx.io (formerly docs.ltx.video)
- **Developer Console:** https://console.ltx.io
- **Developer Portal:** https://ltx.dev

## Two API Surfaces

With the LTX-2.5 launch on 2026-08-11 the API gained a **new domain and a new async surface**:

| Surface | Base URL | Style |
|---|---|---|
| **v2 (async)** | `https://api.ltx.io/v2/...` | Submit returns a job `id`; poll `GET /v2/<endpoint>/{id}` until `completed`, then fetch `result.video_url`. Required for LTX-2.5. |
| v1 (sync) | `https://api.ltx.video/v1/...` | Single HTTP call returns binary MP4. |

Full schemas in [[ltx-video-api-endpoints]].

## Key Characteristics

- Cloud-hosted HTTP API
- Per-second billing model
- Multiple resolution tiers up to 4K
- Supports **LTX-2.5** (`ltx-2-5-fast`, `ltx-2-5-pro`) and LTX-2.3; LTX-2 model IDs were removed on 2026-08-15
- Async job submission on `/v2`; sync single-call responses still available on `/v1`
- **Automatic Duration** -- pass `duration: null` on `/v2` and LTX-2.5 picks the clip length from the prompt
- Audio generation support

## Endpoints

Under `/v2` (async): `submit-text-to-video`, `submit-image-to-video`, `submit-audio-to-video`, `submit-retake`, `submit-extend`, `submit-video-to-video-hdr`, `submit-video-to-video-reframe`, `get-job-status`, `create-upload`.

- **Text-to-Video** - Generate video from text prompts
- **Image-to-Video** - Create video from static images
- **Audio-to-Video** - Generate visuals synchronized to audio
- **Retake / Extend / Reframe** - Editing operations, **exclusive to `ltx-2-3-pro`** (LTX-2.5 supports none of them)

## Agent-Readable Docs

The docs root exposes a machine index: append `/llms.txt` to any URL for a page-level index, or `.md` for the markdown version of any page.

## Usage in LTX Desktop

[[ltx-desktop]] uses the LTX API in two ways:

- **Text encoding:** Free (included with API key)
- **Video generation:** Paid (used when running in API mode on unsupported hardware like macOS)
- **Prompt enhancement:** Included with API key

## Integration with AI Agents

The LTX API can be called from any environment including Claude Code via standard HTTP requests. See [[ltx-mcp-integration]] for details on agent integration patterns.

## Third-Party API Hosting

Several platforms also host LTX models as API services. See [[ltx-integration-projects]] for details on fal.ai, Replicate, Modal, and other hosting options.

## Related Pages

- [[ltx-video-api-endpoints]] -- request/response schemas for v1 and v2
- [[ltx-video-api-models]] -- model IDs and the capability matrix
- [[ltx-video-api-pricing]] -- per-second pricing including LTX-2.5
- [[ltx-2.5-model]]

## Developer Program

Developers actively building with the LTX API can apply to the [[ltx-builders-program]] for early access to features and direct communication with the model team.
