# LTX-2.5 on fal.ai: Six Endpoints, Per-Second Pricing and Client SDK Example

**Source:** https://fal.ai/ltx-2.5
**Date:** 2026-08-11 (LTX-2.5 launch; page live in window)
**Retrieved:** 2026-08-24

## Content

fal.ai serves LTX-2.5 as **six separate endpoints**, billed per second, no subscription underneath. Every modality ships in a quality-optimized **Pro** variant and a speed-optimized **Fast** variant.

### Endpoint IDs

| Endpoint ID | Modality | Variant |
| --- | --- | --- |
| `lightricks/ltx-2.5/text-to-video/pro` | text-to-video | Pro |
| `lightricks/ltx-2.5/text-to-video/fast` | text-to-video | Fast |
| `lightricks/ltx-2.5/image-to-video/pro` | image-to-video | Pro |
| `lightricks/ltx-2.5/image-to-video/fast` | image-to-video | Fast |
| `lightricks/ltx-2.5/audio-to-video/pro` | audio-to-video | Pro |
| `lightricks/ltx-2.5/audio-to-video/fast` | audio-to-video | Fast |

Image-to-video also accepts an **end frame** so you can pin where a shot finishes.

### Pricing (per second, audio included at every resolution)

**Fast:** $0.09/s at 720p, $0.13/s at 1080p, $0.19/s at 1440p, **$0.30/s at 4K**.
**Pro image-to-video:** $0.12/s at 720p, $0.17/s at 1080p.
**Audio-to-video bills per second of *input audio*, not output:** $0.13/s on Fast and $0.17/s on Pro at 1080p.

### Capability split by variant

- **Pro** — 720p or 1080p, 24/25/50 fps, clips of 6, 8 or 10 seconds. Runs **Diffusion Fidelity Rendering** (Pro endpoints only).
- **Fast** — 720p, 1080p, 1440p or 2160p (4K), 24/25/48/50 fps, clips **up to 20 seconds**. Trades some DFR fidelity for speed, 4K and the lower per-second price.
- Both: synchronized audio by default, 16:9 and 9:16, `duration` defaults to `"auto"` (Auto Duration reads the described action and picks clip length before diffusion begins).

### JavaScript client example

```javascript
import { fal } from "@fal-ai/client";

const result = await fal.subscribe("lightricks/ltx-2.5/text-to-video/pro", {
  input: {
    prompt: "Cinematic drone shot over misty mountains at sunrise",
    resolution: "1080p",
    duration: "auto",
    generate_audio: true,
  },
  logs: true,
  onQueueUpdate: (update) => {
    if (update.status === "IN_PROGRESS") {
      update.logs.map((log) => log.message).forEach(console.log);
    }
  },
});

console.log(result.data);
console.log(result.requestId);
```

Python and JavaScript SDKs both available; API key from https://fal.ai/dashboard/keys; parameter reference at `/models/lightricks/ltx-2.5/text-to-video/pro/api`.

### Fine-tuning on fal

fal hosts **LTX trainers** as well as inference on the resulting fine-tunes, with **more than 80 LTX fine-tunes already on the platform**. LTX-2.5 also ships a **raw pretrained (non-SFT) checkpoint** alongside the production model, aimed at aggressive adaptation toward robotics, synthetic AV, industrial digital twins and private domain models.

### Professional color / EXR

fal's page confirms a **native EXR workflow** reading and writing cinema-grade EXR inside ACES and DaVinci Wide Gamut, with generative edits returning EXR and no lossy 8-bit round-trip.

### Licensing note surfaced on the endpoint page

LTX-2.x Community License, not OSI open source. Commercial use permitted, but entities with **annual revenue of at least $10 million must obtain a paid commercial license** from Lightricks first; the license restricts training competing models.
