---
title: GitHub Issues and Known Limitations
type: reference
created: 2026-04-13
updated: 2026-08-24
sources:
  - raw/github-issues-discussions.md
  - raw/community-github-lightricks-ltx-2-issues-ltx-2-5-defects-2026-08.md
tags:
  - github
  - issues
  - bugs
  - limitations
  - troubleshooting
  - known-issues
---

# GitHub Issues and Known Limitations

The [[github-official-repositories|Lightricks/LTX-Video]] GitHub issue tracker documents bugs, feature requests, and technical limitations reported by the community. As of the research date, there are 78 open issues out of approximately 276+ total filed since the initial release in late 2024.

## Issue Statistics

| Tracker | Open Issues | Activity Period |
|---------|-------------|-----------------|
| Lightricks/LTX-Video | 78 (of ~276+ total) | Late 2024 -- March 2026 |
| Lightricks/ComfyUI-LTXVideo | Active | Ongoing |
| Lightricks/LTX-Video-Q8-Kernels | Active | Ongoing |

## Recent Issues (2026)

| # | Title | Date | Category |
|---|-------|------|----------|
| 276 | NaN outputs when saving video on 8x Tesla P40 | Mar 10, 2026 | Bug |
| 275 | LoRA silently ignored with TI2VidTwoStagesPipeline | Mar 7, 2026 | Bug |
| 274 | LTX 2.3 First frame last frame | Mar 6, 2026 | Question |
| 268 | Looking for help / freelancer to finalize LTX-Video setup | Feb 2, 2026 | Support |
| 267 | LTX2 Efficient node / GGUF problem | Feb 2, 2026 | Bug |
| 264 | Increase to 48fps breaks video coherency and quality | Jan 14, 2026 | Bug/Limitation |
| 263 | Audio breaks export when using 4K | Jan 14, 2026 | Bug |
| 262 | LTX2 GGUF got artifacts noise result without errors | Jan 14, 2026 | Bug |
| 260 | TypeError when running image to video generation | Jan 4, 2026 | Bug |
| 259 | IC-LoRA inference in diffusers pipeline not working | Jan 3, 2026 | Bug |
| 257 | Full model weights and tooling release delayed | Nov 30, 2025 | Meta |

## Issue Categories

### Technical Bugs

- **NaN outputs** on multi-GPU setups (Tesla P40) -- #276
- **FP8 compatibility:** `FP8Linear.forward()` argument mismatch -- #231
- **[[gguf-quantizations|GGUF]] artifacts:** Noise results without error messages -- #262
- **Video output fails to play** from image-to-video inference -- #55
- **Generation stuck at 0%** -- #66
- **UnboundLocalError** in self_attn_func -- #233

### Quality Concerns

- **48fps breaks coherency** and quality -- #264
- **Plastic skin rendering** in 0.9.8 distilled -- #230
- **"How to generate good videos?"** -- #15 (early guidance request)

See also [[community-feedback]] for broader quality discussion.

### Feature Requests

- **Multi-GPU support** for inference -- #247
- **Chinese language support** for LTX2 -- #253
- **Sketch to video** capability -- #245

See also [[community-feature-requests]] for the full feature request landscape.

### Integration Issues

- **[[lora-ecosystem|LoRA]] silently ignored** in programmatic pipeline use (missing sd_ops renaming map) -- #275
- **[[ic-lora|IC-LoRA]] not working** with [[diffusers-integration|diffusers]] pipeline -- #259
- **ComfyUI missing nodes** even with ComfyUI-LTXVideo installed -- #240
- **Diffusers config mapping** issues -- #241
- **No CLIP/text encoder weights** in checkpoint -- #219

### Setup / Support

- Freelancer requests for setup assistance -- #268
- Various "how to use FP8" questions -- #227

## Known Limitations (Documented)

These are confirmed architectural or design limitations, not bugs:

1. **Resolution constraints:** Model works best on resolutions under 720x1280 and frame counts below 257
2. **Diffusers suboptimality:** The default [[diffusers-integration|Diffusers]] inference pipeline does not include STG or other inference-time tricks; the official LTX-Video repo inference script is recommended for best quality
3. **Frame count requirements:** Input videos must contain frames in multiples of 8 plus 1 (9, 17, 25, etc.) due to [[video-vae|VAE temporal compression]]
4. **Audio at 4K:** Audio breaks export when using 4K resolution -- #263
5. **High FPS quality degradation:** Increasing to 48fps can break video coherency -- #264
6. **VRAM requirements:** 16GB minimum for LTX-Video, 32GB+ recommended for ComfyUI workflows
7. **Quantized model artifacts:** [[gguf-quantizations|GGUF quantized]] versions can produce noise artifacts without error messages
8. **LoRA compatibility:** Some [[lora-ecosystem|LoRA]] configurations silently fail in certain pipeline modes

## Lightricks/LTX-2 Issue Tracker: LTX-2.5 Defects (August 2026)

Issue traffic on the official `Lightricks/LTX-2` inference repo spiked after the 2026-08-11 [[ltx-2.5-model|LTX-2.5]] release. The table below is from a GitHub REST API query with `since=2026-08-11`, excluding spam/non-English noise (#281, #285, #287, #295). **All issue bodies below were read directly — this section is verified, not aggregated.**

| # | Opened | State (2026-08-24) | Title |
|---|---|---|---|
| 275 | 2026-08-12 | open | Confirm: LTX-2.5 video/audio VAE *encoders* are byte-identical to LTX-2.3 (undocumented) |
| 277 | 2026-08-12 | **open** | [LTX-2.5] DiffVAE AUTO tiling produces gray tails at the 2^32 stage-5 element boundary |
| 278 | 2026-08-12 | closed | Recommendations on GGUF's versatility and using Qwen |
| 283 | 2026-08-14 | open | Train/inference parity: three divergences between ltx-trainer and ltx-core / ltx-pipelines |
| 284 | 2026-08-14 | closed | Omni-Rewriter now expands prompts into the public LTX-2.5 paragraph dialect |
| 286 | 2026-08-16 | closed | OneTrainer support |
| 288 | 2026-08-16 | **open** | [ltx-pipelines] i2v at 1216x832 crashes DiffVAE decoder with illegal memory access |
| 290 | 2026-08-17 | closed | [LTX-2.5] Diffusers diffusion_decoder weights differ from the standalone DiffVAE checkpoint |
| 291 | 2026-08-18 | closed | Timestep distribution / shift: proposal |
| 292 | 2026-08-19 | open | ltx-kernels build fails on rolling-release toolchains (CUDA mismatch + -Werror) |
| 296 | 2026-08-24 | open | `--quantization fp8-cast` crashes with any LoRA on pre-Hopper GPUs |

### The diffusion VAE decoder (DiffVAE) defect family — unresolved

Three independent reports inside five days all land on the same subsystem: the new diffusion-based video VAE decoder that is LTX-2.5's headline quality change. This is the **most significant unresolved cluster at the end of the window** — **all still open as of 2026-08-24**.

- **#277 — gray tiles at the 2^32 element boundary.** Reporter `fff-ttt` on A100-SXM4-80GB, PyTorch 2.9.1+cu128, 1920x1088 @24fps: the decoder "can **silently produce neutral-gray frame tails or rectangular gray tiles** when AUTO tiling selects a chunked stage-5 tile whose channels-last activation reaches the `2**32` flattened-element boundary." Silent corruption, not an exception. Isolated to decode rather than either diffusion stage: "The same finite stage-2 latent decodes cleanly with a smaller explicit tile."
- **#288 — deterministic i2v crash at 1216x832.** Reporter `mabry1985`: `ltx_pipelines.distilled` with image conditioning at 1216x832 crashes with `cudaErrorIllegalAddress`, **3/3 across seeds**. The same resolution *without* `--image` is fine, and i2v at 1216x704 and 1216x768 are fine. 832 is a legal size (64x13) and passes the pipeline's own divisible-by-64 check.
- **Intermittent Blackwell variant.** A second reporter on #288 (`sonificator`, RTX PRO 6000 Blackwell sm120, CUDA 13.2) hit a related **non-deterministic** `CUBLAS_STATUS_INTERNAL_ERROR` at 960x896 / 481 frames — three takes passed, the fourth crashed with identical arguments.
- **Vendor position:** `michaellightricks` replied to both on 2026-08-18 and explicitly linked them — "This looks like the same DiffVAE AUTO / chunked tiling issue as #288. We will take a look at it and follow up here." No fix at window close.

Practical mitigation, from the community rather than a patch: **reduce the VAE decode tile size** (768 → 512), or set `temporal_size: 64` / `temporal_overlap: 16`. See [[ltx-2.5-local-inference]].

### Confirmed architecture fact surfaced by #275

`ofir-bar-tal` diffed the shipped 2.5 VAEs against the VAE bundled in `ltx-2.3-22b-dev`: "**Every encoder tensor and per-channel normalization stat is byte-for-byte identical between 2.3 and 2.5.** The audio *decoder* is also identical. Only the video decoder differs." `michaellightricks` confirmed on 2026-08-18: "that matches our intent... **Cached 2.3 latents are valid for 2.5 training and inference encode.**" He noted this would be added to the docs and declined to promise it beyond 2.5. The behaviour was previously **undocumented** — absent from README, release notes and model card.

### Diffusers packaging mismatch (#290, closed)

`mglyn` compared `Lightricks/LTX-2.5-Diffusers/diffusion_decoder` against the native VAE: **405 of 407 name/shape-matching tensors differ numerically**, with 0 missing and 0 unexpected keys — structurally compatible but built from different (likely release-candidate) weights. Closed as a [[diffusers-integration|Diffusers]]-side export problem: "The standalone VAE in `Lightricks/LTX-2.5` is the canonical decoder for LTX-2.5," redirecting to huggingface/diffusers PR #14447.

### Quantization gap on pre-Hopper hardware (#296, open)

`raywangruihua`: `ICLoraPipeline` with `--quantization fp8-cast` on an **RTX 3060** fails at `fuse_lora_weights` → `_fp8_cast_fuse` with `ValueError("type fp8e4nv not supported in this architecture")`. Practical effect: **the documented low-VRAM quantization path is unusable together with LoRAs on pre-Hopper consumer GPUs.** See [[fp8-quantization]].

### Vendor responsiveness

Lightricks staff (`michaellightricks`, `art-alex`) replied to essentially every substantive LTX-2.5 issue, typically within 2-6 days, and shipped at least one fix — the NVFP4 ComfyUI loading bug, reported on the Hugging Face discussions tab — **inside roughly 48 hours**. See [[ltx-2.5-community-reception]] for the sentiment context.

## ComfyUI-LTXVideo Issues

Separate issue tracker at https://github.com/Lightricks/ComfyUI-LTXVideo/issues. Common themes:

- Node compatibility issues
- Model download/loading problems
- Workflow configuration questions
- VRAM optimization requests

See [[comfyui-ltx-integration-overview]] for setup guidance.

## Troubleshooting Resources

- **LTX-Video-Trainer troubleshooting guide:** https://github.com/Lightricks/LTX-Video-Trainer/blob/main/docs/troubleshooting.md
- **Discord community:** https://discord.gg/ltxplatform (primary real-time support channel)
- **ComfyUI Manager:** For automated dependency resolution

## Pull Requests

Active PRs at https://github.com/Lightricks/LTX-Video/pulls. The project accepts community contributions but primary development is driven by the [[lightricks-company|Lightricks]] team.

## Related Pages

- [[github-official-repositories]] -- Official repositories
- [[community-feedback]] -- Broader community sentiment
- [[community-feature-requests]] -- Feature request landscape
- [[fp8-quantization]] -- FP8 quantization details
- [[installation-quickstart]] -- Setup guide
- [[ltx-2.5-community-reception]] -- LTX-2.5 reception, including vendor response times
- [[ltx-2.5-local-inference]] -- Tiling workarounds for the DiffVAE decoder
