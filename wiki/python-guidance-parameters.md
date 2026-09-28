---
title: Python Guidance Parameters
type: reference
created: 2026-04-13
updated: 2026-09-28
sources:
  - https://huggingface.co/docs/diffusers/api/pipelines/ltx_video
  - https://github.com/Lightricks/LTX-2/blob/main/packages/ltx-pipelines/README.md
  - raw/tutorial-ltx-2-5-guidance-steps-samplers-2026-09.md
tags:
  - python
  - guidance
  - cfg
  - stg
  - parameters
---

# Python Guidance Parameters

Configuration for Classifier-Free Guidance (CFG), Spatio-Temporal Guidance (STG), and related parameters that control LTX-Video generation quality and prompt adherence.

## Standard Classifier-Free Guidance (Diffusers)

```python
# Higher guidance = more prompt adherence, less diversity
video = pipeline(
    prompt="...",
    guidance_scale=5.0,  # 3-7 is typical range
).frames[0]
```

## Guidance Rescale (Prevent Overexposure)

Prevents washed-out colors at high guidance values:

```python
video = pipeline(
    prompt="...",
    guidance_scale=7.0,
    guidance_rescale=0.7,  # 0.0-1.0, higher = more rescaling
).frames[0]
```

## MultiModalGuiderParams (LTX-2)

The [[sdk-ltx-2]] uses `MultiModalGuiderParams` for fine-grained control over both video and audio guidance:

```python
from ltx_core.components.guiders import MultiModalGuiderParams

video_guider_params = MultiModalGuiderParams(
    cfg_scale=3.0,         # Classifier-Free Guidance (2.0-5.0 typical; 1.0 disables)
    stg_scale=1.0,         # Spatio-Temporal Guidance (0.5-1.5 typical; 0.0 disables)
    stg_blocks=[29],       # Transformer blocks to perturb (e.g., [29] for last block)
    rescale_scale=0.7,     # Prevent over-saturation (0.5-0.7 typical; 0.0 disables)
    modality_scale=3.0,    # Audio-visual coherence (3.0 for audio-video; 1.0 to disable)
    skip_step=0,           # Skip guidance every N steps for speed
)

audio_guider_params = MultiModalGuiderParams(
    cfg_scale=7.0,
    stg_scale=1.0,
    rescale_scale=0.7,
    modality_scale=3.0,
    skip_step=0,
    stg_blocks=[29],
)
```

## Parameter Reference

| Parameter | Range | Function |
|-----------|-------|----------|
| `cfg_scale` | 2.0-5.0 | Classifier-Free Guidance; higher = more prompt adherence |
| `stg_scale` | 0.5-1.5 | Spatio-Temporal Guidance for temporal coherence |
| `stg_blocks` | e.g. `[29]` | Transformer blocks to perturb for STG |
| `rescale_scale` | 0.5-0.7 | Rescales guided prediction to prevent over-saturation |
| `modality_scale` | 1.0-3.0 | Audio-visual sync strength |
| `skip_step` | 0+ | Skip guidance every N steps for speed |

## LTX-2.5: Three Guidance Strategies, and a Fixed Schedule on Distilled

Per the official LTX blog (2026-09-08), `ltx-core`'s `components/guiders.py` ships **three** guidance strategies, not just CFG: **CFG**, **STG**, and **APG**. STG works by selectively disabling attention operations via a perturbation system, with documented perturbation types `SKIP_VIDEO_SELF_ATTN`, `SKIP_AUDIO_SELF_ATTN`, `SKIP_A2V_CROSS_ATTN`, and `SKIP_V2A_CROSS_ATTN` — the last two apply guidance to the cross-modal audio/video link specifically, unique to joint audio-video models like [[ltx-2.5-model|LTX-2.5]].

**Distilled checkpoints have no tunable step count.** `DistilledPipeline` runs a fixed schedule of 8 predefined sigmas (8 steps stage 1, 4 steps stage 2) — guidance/step values tuned on a dev-checkpoint run do not transfer to the distilled pipeline and vice versa; treat them as separate configurations.

**Gradient estimation** reduces dev-checkpoint inference from 40 steps to 20-30 while maintaining quality — a 25-50% step-count cut for no pipeline/checkpoint change.

**Samplers:** production pipelines use Euler (first-order, default) and `res_2s` (second-order). `TI2VidTwoStagesHQPipeline` uses `res_2s` specifically for fewer steps at better quality than the standard two-stage flow's Euler default.

**Frame-count constraint:** the Video VAE requires `(F-1) % 8 == 0`, so valid frame counts run 9, 17, 25, 33, 41, 49, 57... (at 25fps, 49 frames = 1.96s; a literal "2 seconds" is not an achievable frame count).

## Sampling Recommendations

| Model Type | Steps | CFG Scale |
|-----------|-------|-----------|
| Distilled | 4-8 | 1.0 (required) |
| Full (dev) | 20-50 | 2.0-5.0 |
| General recommendation | -- | 3.0-3.5 |

## See Also

- [[python-schedulers]] -- Scheduler configuration and timestep schedules
- [[python-conditioning]] -- Conditioning strength and noise scale
- [[ltx-2-pipeline-api]] -- Full LTX-2 pipeline parameter reference
