# Developer Bug Reports on github.com/Lightricks/LTX-2 After the LTX-2.5 Release (Aug 12-24, 2026)

**Source:** https://github.com/Lightricks/LTX-2/issues (queried via GitHub REST API, `since=2026-08-11`)
**Date:** 2026-08-12 to 2026-08-24
**Retrieved:** 2026-08-24

## Content

Issue traffic on the official inference repo spiked after the 2026-08-11 LTX-2.5 release.
Substantive LTX-2.5 issues opened in the window (excluding spam/non-English noise such as #281,
#285, #287, #295):

| # | Opened | State | Title |
|---|---|---|---|
| 275 | 2026-08-12 | open | Confirm: LTX-2.5 video/audio VAE *encoders* are byte-identical to LTX-2.3 (undocumented) |
| 277 | 2026-08-12 | open | [LTX-2.5] DiffVAE AUTO tiling produces gray tails at the 2^32 stage-5 element boundary |
| 278 | 2026-08-12 | closed | Recommendations on GGUF's versatility and using Qwen |
| 283 | 2026-08-14 | open | Bug - Train/inference parity: three divergences between ltx-trainer and ltx-core / ltx-pipelines |
| 284 | 2026-08-14 | closed | Omni-Rewriter now expands prompts into the public LTX-2.5 paragraph dialect |
| 286 | 2026-08-16 | closed | OneTrainer support |
| 288 | 2026-08-16 | open | [ltx-pipelines] i2v at 1216x832 crashes DiffVAE decoder with illegal memory access |
| 290 | 2026-08-17 | closed | [LTX-2.5] Diffusers diffusion_decoder weights differ from the standalone DiffVAE checkpoint |
| 291 | 2026-08-18 | closed | Timestep distribution / shift: proposal |
| 292 | 2026-08-19 | open | ltx-kernels build fails on rolling-release toolchains (CUDA toolkit mismatch + -Werror) |
| 296 | 2026-08-24 | open | `--quantization fp8-cast` crashes with any LoRA on pre-Hopper GPUs |

### The dominant theme: the new diffusion VAE decoder (DiffVAE)

Three independent issues in five days all land on the same subsystem — the decoder that is
LTX-2.5's headline quality change.

- **#277** (`fff-ttt`, A100-SXM4-80GB, PyTorch 2.9.1+cu128, 1920x1088 @24fps): "LTX-2.5's
  diffusion-based video VAE decoder can **silently produce neutral-gray frame tails or
  rectangular gray tiles** when AUTO tiling selects a chunked stage-5 tile whose channels-last
  activation reaches the `2**32` flattened-element boundary." Isolated to decode, not to either
  diffusion stage: "The same finite stage-2 latent decodes cleanly with a smaller explicit tile."
- **#288** (`mabry1985`): `ltx_pipelines.distilled` with image conditioning at **1216x832
  deterministically crashes with `cudaErrorIllegalAddress`**, 3/3 across seeds. Same resolution
  *without* `--image` is fine; i2v at 1216x704 and 1216x768 are fine. "832 is a legal size
  (64x13) and passes the pipeline's own divisible-by-64 check." A second reporter
  (`sonificator`, RTX PRO 6000 Blackwell sm120, CUDA 13.2) hit a related **intermittent**
  `CUBLAS_STATUS_INTERNAL_ERROR` at 960x896/481 frames — 3 takes passed, the 4th crashed with
  identical args.
- Lightricks member `michaellightricks` replied to both on 2026-08-18, linking them: "This looks
  like the same DiffVAE AUTO / chunked tiling issue as #288. We will take a look at it and
  follow up here." **Both remained open as of 2026-08-24.**

### Confirmed architecture fact from a community investigation (#275)

`ofir-bar-tal` diffed the shipped 2.5 VAEs against the VAE bundled in `ltx-2.3-22b-dev`:
"**Every encoder tensor and per-channel normalization stat is byte-for-byte identical between
2.3 and 2.5.** The audio *decoder* is also identical. Only the video decoder differs." Lightricks
(`michaellightricks`, 2026-08-18) confirmed: "that matches our intent. LTX-2.5 keeps the 2.3
video and audio encoders (and audio decoder, and per-channel stats). Only the video decoder
changed (diffusion VAE). **Cached 2.3 latents are valid for 2.5 training and inference encode.**
We will add this to the docs/release notes. We are not making a compatibility promise beyond
2.5; a later generation could change the encoder." This was previously undocumented — the
reporter noted he "couldn't find it stated anywhere in the README, release notes, or model card."

### Diffusers packaging mismatch (#290)

`mglyn` compared `Lightricks/LTX-2.5-Diffusers/diffusion_decoder` against the native VAE and
found **405 of 407 name/shape-matching tensors differ numerically**, with 0 missing and 0
unexpected keys — i.e. structurally compatible but built from different (likely release-candidate)
weights. Lightricks closed it as a Diffusers-side export problem: "The standalone VAE in
`Lightricks/LTX-2.5` is the canonical decoder for LTX-2.5," and redirected to
huggingface/diffusers PR #14447.

### Quantization gaps on older hardware (#296, opened 2026-08-24)

`raywangruihua`: `ICLoraPipeline` with `--quantization fp8-cast` on an **RTX 3060** fails at
`fuse_lora_weights` -> `_fp8_cast_fuse` with
`ValueError("type fp8e4nv not supported in this architecture")`. Practical effect: the
documented low-VRAM quantization path is unusable with LoRAs on pre-Hopper consumer GPUs.

### Third-party ecosystem pickup

`deepbeepmeep/Wan2GP` (8.5k stars) issue **#2134, "LTX-2.5 has been released. We're looking
forward to it."**, opened 2026-08-11 — the day of release — by `dreammoto12-cell`, body just the
Hugging Face link. WanGP shipped LTX-2.5 support with 6GB-VRAM optimization within two days.
https://github.com/deepbeepmeep/Wan2GP/issues/2134

### Vendor responsiveness summary (verified)

Lightricks staff (`michaellightricks`, `art-alex`) replied to essentially every substantive
LTX-2.5 issue, typically within 2-6 days, and shipped at least one fix (the NVFP4 ComfyUI
loading bug) inside 48 hours. The open DiffVAE tiling family is the most significant unresolved
cluster at the end of the window.
