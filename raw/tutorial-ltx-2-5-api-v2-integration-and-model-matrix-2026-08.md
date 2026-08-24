# LTX-2.5 Hosted API Integration: api.ltx.io v2 Endpoints, Model IDs, Pricing and the 2.3 Capability Gap

**Source:** https://docs.ltx.io/api-documentation/api-reference/async-video-generation/submit-text-to-video
**Source:** https://aireiter.com/blog/ltx-2-5-api-pricing-guide
**Date:** 2026-08-13 (AIReiter guide); docs page current as of retrieval
**Retrieved:** 2026-08-24

## Content

### Async text-to-video request (canonical example)

`POST https://api.ltx.io/v2/text-to-video`

```bash
curl -X POST https://api.ltx.io/v2/text-to-video \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "A majestic eagle soaring through clouds at sunset",
    "model": "ltx-2-5-pro",
    "duration": 8,
    "resolution": "1920x1080"
  }'
```

Responds immediately with the job `id` and `created_at` (ISO 8601). Poll `GET /v2/text-to-video/{id}` until status is `completed`, then download from `result.video_url`.

**Request fields:** `prompt` (string, required, ≤5000 chars), `model` (enum, required), `duration` (integer **or null**, required — pass `null` to let `ltx-2-5-fast` / `ltx-2-5-pro` choose length from the prompt via Automatic Duration), `resolution` (string, required), `fps` (optional, default `24`), `generate_audio` (boolean, optional, default `true`), `camera_motion` (enum, optional).

**Error codes:** 400, 401, 402 (Payment Required), 422, 429, 500, 503.

### Full async endpoint surface under /v2

`submit-text-to-video`, `submit-image-to-video`, `submit-audio-to-video`, `submit-retake`, `submit-extend`, `submit-video-to-video-hdr` (Upscale video to HDR), `submit-video-to-video-reframe`, `get-job-status`, plus `create-upload`. Sync equivalents live under `/v1/`.

### Model IDs and per-second pricing (docs.ltx.io/pricing)

**`ltx-2-5-fast`:** 720p $0.09/s ($0.90 per 10 s) · 1080p $0.13/s ($1.30) · 1440p $0.19/s ($1.90) · 4K $0.30/s ($3.00)
**`ltx-2-5-pro`:** 720p $0.12/s ($1.20) · 1080p $0.17/s ($1.70)

Versus the previous generation at shared resolutions:

| Resolution | ltx-2-3-fast | ltx-2-5-fast | ltx-2-3-pro | ltx-2-5-pro |
| --- | --- | --- | --- | --- |
| 720p | $0.03 | $0.09 | $0.04 | $0.12 |
| 1080p | $0.06 | $0.13 | $0.08 | $0.17 |
| 1440p | $0.12 | $0.19 | $0.16 | — |
| 4K | $0.24 | $0.30 | $0.32 | — |

**LTX-2.3 is cheaper than LTX-2.5 at every resolution and tier.** At 720p, 2.3 Fast is one-third the price of 2.5 Fast.

### The endpoint capability matrix — the bigger integration story

| Endpoint | ltx-2-5-fast | ltx-2-5-pro | ltx-2-3-fast | ltx-2-3-pro |
| --- | --- | --- | --- | --- |
| Text-to-video | yes | yes | yes | yes |
| Image-to-video | yes | yes | yes | yes |
| Audio-to-video | yes | no | no | yes |
| Retake | no | no | no | yes |
| Extend | no | no | no | yes |
| Reframe | no | no | no | yes |

Despite the name, **`ltx-2-5-pro` is the more restricted variant**: caps at 1080p, drops audio-to-video, and has no editing operations. **Retake, Extend and Reframe remain exclusive to `ltx-2-3-pro`** — if your pipeline edits rather than generates, LTX-2.5 offers no upgrade path. Extend on 2.3 Pro is capped at **505 billed frames**. Audio-to-video on 2.5 Fast is **async-only** through `v2/audio-to-video`.

### Spec table

| Spec | LTX-2.5 Fast | LTX-2.5 Pro |
| --- | --- | --- |
| Max resolution | 4K (3840×2160) | 1080p (1920×1080) |
| Frame rate | 24, 48 fps | 24 fps |
| Max single generation | ~20 s (24/25 fps) | ~10 s |
| Audio-to-video | yes | no |

### Latency data points

- Managed API: 10-second image-to-video clip in **23.7 seconds** at 1080p output (LTX launch materials).
- ComfyUI on **2× NVIDIA GB200**: 10-second 720p clip in **6.8 seconds**. Different resolutions, so not directly comparable.

### Competitive per-second cost at 720p (from LTX launch materials)

Veo 3.1 Lite $0.05 · **LTX-2.5 Fast $0.09** · Veo 3.1 Fast $0.10 · Gemini Omni Flash $0.10 · LTX-2.5 Pro $0.12 · FLUX 3 Video $0.17 · Veo 3.1 $0.40. LTX-2.5 Fast sits second-cheapest overall and is the **only open-weights model in its price bracket**.

### Getting started

Developer Console at https://console.ltx.io — log in, add credits, create an API key. Docs root exposes an agent-readable index: append `/llms.txt` to any URL for a page-level index, or `.md` for the markdown version of any page.
