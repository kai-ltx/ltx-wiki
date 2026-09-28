# Tutorial: Classifier-Free Guidance, Denoising Steps and Samplers in LTX-2.5 (Official LTX Blog)

**Source:** https://ltx.io/blog/guidance-steps-samplers
**Date:** 2026-09-08
**Retrieved:** 2026-09-28

## Content

Official LTX Team blog post explaining the local Python pipeline parameters that control generation quality/behavior in LTX-2.5. Explicitly scoped to the open-source `ltx-pipelines`/`ltx-core` package — the hosted LTX API does not expose these parameters (callers just pick `ltx-2-5-fast` or `ltx-2-5-pro`).

Key facts:
- **Three guidance strategies**, not one: CFG (classifier-free guidance), STG (Spatio-Temporal Guidance), and APG, implemented in `ltx-core`'s `components/guiders.py`.
- **STG** works by selectively disabling attention operations via a perturbation system, with documented perturbation types `SKIP_VIDEO_SELF_ATTN`, `SKIP_AUDIO_SELF_ATTN`, `SKIP_A2V_CROSS_ATTN`, and `SKIP_V2A_CROSS_ATTN` — the latter two let guidance target the cross-modal audio/video link specifically, relevant only to joint audio-video models like LTX-2.5.
- **Distilled checkpoint has no tunable step count**: `DistilledPipeline` runs a fixed schedule of 8 predefined sigmas (8 steps stage 1, 4 steps stage 2). The two-stage pipelines that run the full ("dev") model in stage one require a separate distilled LoRA (`ltx-2.5-22b-distilled-lora-450-bf16.safetensors`) fused into that stage.
- **Gradient estimation** reduces inference from 40 steps to 20-30 while maintaining quality on dev-checkpoint runs (a 25-50% step-count cut for the same pipeline/checkpoint).
- **Samplers**: production pipelines use Euler (first-order) and `res_2s` (second-order). `TI2VidTwoStagesHQPipeline` uses `res_2s` specifically for "fewer steps, better quality" versus the standard two-stage flow's Euler default.
- **Frame-count constraint**: Video VAE requires `(F-1) % 8 == 0`, so valid frame counts are 9, 17, 25, 33, 41, 49, 57... (at 25fps, 49 frames = 1.96s — a literal 2-second request isn't achievable).
- **Hardware/setup**: pure PyTorch targeting NVIDIA GPUs with 80GB+ VRAM (distilled variants work on 32GB with quantization); CUDA 13+ recommended, tested against CUDA 12.7+; install via `uv sync --extra natten`; quick-start download is ~66 GiB including the required `gemma4-12b-with-proj-ltx-2.5-bf16.safetensors` text encoder. Memory-pressure flags: `--quantization fp8-cast` with `--offload cpu`/`--offload disk`; Hopper+ GPUs can use `--quantization fp8-scaled-mm`. Blackwell datacenter GPUs need FlashAttention 4 (pinned revision `flash-attn-4==4.0.0b9`); Hopper uses FlashAttention 3; other CUDA GPUs fall back to PyTorch SDPA.
- **Recommended starting configs by goal**: fast iteration → `DistilledPipeline`; guided two-stage → dev transformer + `TI2VidTwoStagesPipeline` + gradient estimation; quality-constrained/step-constrained → `TI2VidTwoStagesHQPipeline` (res_2s); production quality → `DFRPipeline` + Detailing IC-LoRA (`ltx-2.5-22b-ic-lora-pixel-spatial-upscaler-x2-1.0.safetensors`) — note DFR runs on the distilled transformer, not dev.

## Why this matters for the wiki
This is the first official, LTX-2.5-specific deep-dive on guidance/steps/samplers, correcting the common mistake of applying 2023-era image-model guidance intuition to a distilled audio-video pipeline with a fixed sigma schedule. It's a natural companion to the existing [[python-guidance-parameters]] and [[ltxv-schedulers]] pages.
