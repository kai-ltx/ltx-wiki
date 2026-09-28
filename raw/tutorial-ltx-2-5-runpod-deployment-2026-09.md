# Tutorial: Deploying LTX-2.5 on Runpod (ComfyUI Day-Zero Setup + GPU Sizing)

**Source:** https://www.runpod.io/blog/ltx-2-5-the-open-weights-world-model-built-for-speed-and-how-to-run-it-on-runpod
**Date:** 2026-09-13 (updated)
**Retrieved:** 2026-09-28

## Content

RunPod published (updated Sept 13, 2026) a deployment/sizing guide for running LTX-2.5 on their cloud GPU platform, framed around LTX-2.5's ComfyUI day-zero support (three official templates: Text-to-Video, Image-to-Video, First/Last-Frame-to-Video).

### GPU sizing table (RunPod-specific)
| Tier | VRAM | Example GPUs | Capability |
|---|---|---|---|
| Entry | 16-24GB | RTX 4090, A5000 | Quantized/int8 only, lower res, offloading required — workable for testing |
| Comfortable | 32-48GB | RTX 5090, L40S | int8 ComfyUI checkpoints run well; bf16 distilled viable at 48GB with offloading |
| Recommended | 80-96GB | RTX PRO 6000, H100, A100 80GB | Full bf16 distilled pipeline, spatial upscaler, higher res, longer multishot |
| Maximal | 141GB+ | H200, B200 | 4K HDR, full dev two-stage pipelines, batch generation, fine-tuning |

- Storage floor: ~66 GiB for the distilled bf16 component pack (transformer + Gemma 4 text encoder + video/audio VAEs + spatial upscaler); RunPod recommends a 100GB+ network volume.
- Setup steps: deploy pod with official ComfyUI template → request/accept gated HF license for `Lightricks/LTX-2.5` → update ComfyUI via Manager → authenticate with HF CLI (Read token; fine-grained tokens need "read access to gated repos" scope) → download either Comfy-optimized int8 checkpoints (ComfyUI-only, won't load in ltx-pipelines/PyTorch path) or the full bf16 pack for 80GB+ cards.
- Caveat: the bundled LTX-specific Gemma 4 encoder is required — Google's stock Gemma 4 is not a substitute since the pipeline validates encoder version against training.

### Reiterated LTX-2.5 headline numbers (vendor-reported, dated to the Aug 11 launch but repeated in this Sept update)
- 6.8s to generate a 10s/24fps clip self-hosted on 2x NVIDIA GB200; 23.7s end-to-end via the LTX API at 1080p.
- Vendor comparison of competitor API end-to-end times for the same task: Gemini Omni Flash 52s, Grok 1.5 63s, Veo 3.1 70s (8s clip), MiniMax H3 180s, Seedance 2.5 317s, Kling 3.0 Pro 398s — roughly 7.6x faster than the nearest closed alternative per LTX's own vendor-run benchmark.
- Blind human-preference win rate: LTX-2.5 67%, Seedance 2.5 65%, Gemini Omni Flash 55%, MiniMax H3 50%, Seedance 2.0 44%, Wan 2.6 42% (LTX flags these as preliminary).
- LTX family has surpassed 33 million cumulative downloads, per RunPod's citation of LTX's own claim.
- NVIDIA optimization pass: up to 20% faster / 40% memory savings on RTX 6000 PRO vs. prior releases; minimum VRAM floor of 16GB for quantized variants.

## Why this matters for the wiki
This is a substantive third-party deployment guide (not a Lightricks-authored piece) that operationalizes the GPU tiering question raised generically in [[hardware-requirements]] and [[ltx-2.5-local-inference]] specifically for cloud rental via RunPod, with exact CLI-level guidance. It's useful to cross-reference against [[runpod]] (existing inference-provider page).
