---
title: LTX-2.5 Local Inference
type: technical
created: 2026-08-24
updated: 2026-08-24
sources:
  - raw/tutorial-ltx-2-5-local-vram-quantization-guide-2026-08.md
  - raw/tutorial-ltx-2-5-python-ltx-pipelines-and-diffusers-2026-08.md
  - raw/tutorial-comfyui-ltx-2-5-nodes-workflows-2026-08.md
tags:
  - ltx-2-5
  - vram
  - quantization
  - fp8
  - nvfp4
  - gguf
  - local-inference
---

# LTX-2.5 Local Inference

VRAM baselines, quantization formats and out-of-memory triage for running [[ltx-2.5-model|LTX-2.5]] locally on the official `ltx-pipelines` PyTorch path. For the ComfyUI int8 path see [[ltx-2.5-comfyui-integration]].

## Official baseline (standard Python path)

docs.ltx.io system requirements for `ltx-pipelines` with LTX-2.5:

| Requirement | Value |
| --- | --- |
| GPU | NVIDIA, **at least 32 GB VRAM** |
| System RAM | 32 GB |
| Storage | ~100 GB free |
| CUDA | **12.7+** |
| Python | 3.12+ |
| PyTorch | ~= 2.7 |

> **CUDA version discrepancy — unresolved.** The docs.ltx.io system-requirements page and the LTX-2.5 model card state **CUDA 12.7+**. The LTX quantization blog separately states **CUDA 13.2+** as a hard prerequisite for its quantization walkthrough. Both figures are recorded here; treat 12.7 as the model-card/system-requirements number and 13.2 as what the quantization path was documented against.

Do **not** combine requirements from LTX-2.3, [[ltx-desktop]], community GGUF builds and LTX-2.5 Python pipelines as if they were one setup. The community ComfyUI **int8** figure (16 GB minimum) describes a different pipeline than the 32 GB **bf16** PyTorch path. See [[hardware-requirements]].

## FP8 — the only quantization natively supported in the codebase

FP8 cuts VRAM by **approximately 40%** with minimal quality loss. Two policies:

| Policy | FP8 Cast | FP8 Scaled MM |
| --- | --- | --- |
| CLI flag | `--quantization fp8-cast` | `--quantization fp8-scaled-mm` |
| Dependencies | None (built in) | TensorRT-LLM, `uv sync --frozen --extra fp8-trtllm` |
| GPU requirement | Any FP8-capable GPU (Ada Lovelace, Hopper, Blackwell) | Hopper (H100, H200) |
| Memory savings | Weight storage only, ~40% | Weight storage + compute, ~40% |
| Speed benefit | Moderate | Higher (native FP8 math) |
| Checkpoint | Use with **bf16** checkpoints (downcast on the fly) | Use with **fp8** checkpoints |

Both require `PYTORCH_CUDA_ALLOC_CONF=expandable_segments:True`:

```bash
PYTORCH_CUDA_ALLOC_CONF=expandable_segments:True python -m ltx_pipelines.ti2vid_two_stages \
  --quantization fp8-cast --checkpoint-path /path/to/checkpoint.safetensors
```

Programmatic form:

```python
from ltx_core.quantization.policy import QuantizationPolicy

pipeline = DistilledPipeline.from_config(
    "path/to/config.yaml",
    quantization=QuantizationPolicy.fp8_cast(),
)
```

Swap in `QuantizationPolicy.fp8_scaled_mm()` for the Hopper backend. Background on the format: [[fp8-quantization]].

## MXFP8 and NVFP4 (Blackwell-only)

| Format | Bits | Scaling | GPU requirement |
| --- | --- | --- | --- |
| FP8 (E4M3) | 8 | Per-tensor or per-channel | Ada Lovelace, Hopper, Blackwell |
| MXFP8 | 8 | Block-level (32 elements) | Blackwell |
| NVFP4 | 4 | Block-level microscaling | Blackwell |

- **MXFP8** — 8-bit with **block-level scaling over groups of 32 elements** (Open Compute Project Microscaling Formats Spec). Preserves more dynamic range than per-tensor FP8; matters most in cross-attention layers where video and audio weight distributions differ. Hardware: **B100, B200, GB200**.
- **NVFP4** — 4 bits, block-level microscaling. **A 22B model needs ~22 GB in FP8 and ~11 GB in NVFP4.** Only 16 discrete values per weight, so temporal consistency and fine texture can show artifacts. LTX-2.5 ships `ltx-2.5-22b-distilled-transformer-nvfp4.safetensors`, usable via `--quantization nvfp4-prequant` (Blackwell + `ltx-kernels`) — though **the ComfyUI loader for it was reported broken in the first 24 hours after launch**.

E4M3 (4 exponent, 3 mantissa bits) is the inference-relevant FP8 variant; E5M2 targets gradients.

## Recommended stack for a 32 GB card

The documented minimum working configuration is **fp8-cast + the distilled checkpoint**. Supporting levers, in order of impact:

1. **Distilled checkpoint** — 8 steps versus 20–50 for the full model; cuts both time and peak memory. "On a 32 GB card this is the difference between working and not."
2. **Tiled VAE decode** — splits decoding into tiles, lowering peak memory at slightly slower decode. This is the fix when OOM hits at the **decode** stage rather than during sampling; quantization alone does not address it. In Diffusers this is `pipe.vae.enable_tiling()` (see [[ltxv-memory-optimization]]).
3. **Offload text encoding to the API** — the Gemma 4 text encoder and prompt enhancer both occupy VRAM; running them through the LTX API ([[ltx-api]]) frees meaningful headroom.
4. `--offload cpu` for CPU offloading of the transformer.

## Frame and dimension constraints when tuning down

- Frame counts must satisfy `(F-1) % 8 == 0` — valid values include **57, 65, 97, 121**.
- Dimensions divisible by **64 for two-stage pipelines**, **32 for one-stage**.

Reducing frames or resolution below these grids silently fails or errors rather than rounding.

## Community GGUF

`Abiray/LTX-2.5-Distilled-GGUF` publishes quantized GGUF builds of the LTX-2.5 distilled transformer for memory-constrained local runs. **No GGUF existed at launch** — these were day-two community builds.

Reported community consensus:

| Quant | Verdict |
| --- | --- |
| Q8 | Virtually identical to full precision |
| Q4 | **Sweet spot** — minimal quality loss |
| Q3 | Noticeable degradation |

See [[gguf-quantizations]] for the broader GGUF landscape.

## OOM triage order

First identify **where** memory fails: loading the transformer, the text encoder, the VAE, the upscaler — or during decode. Decode-stage OOM is a tiling problem, not a quantization problem.

Then reduce one variable at a time:

1. Resolution
2. Frames
3. Batch size
4. Precision
5. Concurrent models
6. Decoding strategy

Close other GPU applications before retesting. If the gap between your hardware and the baseline is large, offloading plus aggressive quantization produces a **slow experimental setup, not a production machine**.

## See Also

- [[ltx-2.5-model]] · [[ltx-2.5-technical]]
- [[ltx-2.5-comfyui-integration]] — the int8 ComfyUI path
- [[ltx2-diffusers-pipeline]] — Diffusers and `ltx-pipelines` usage
- [[fp8-quantization]] · [[gguf-quantizations]] · [[ltxv-memory-optimization]]
- [[hardware-requirements]] · [[ltx2-system-requirements]]
