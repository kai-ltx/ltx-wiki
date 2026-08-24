# LTX-2.5 Local Inference: VRAM Baselines, FP8/MXFP8/NVFP4 Quantization and OOM Triage

**Source:** https://nextvibeai.uk/resources/ltx-2-5-local-vram-setup
**Source:** https://ltx.io/blog/quantization-formats-explained
**Source:** https://huggingface.co/Abiray/LTX-2.5-Distilled-GGUF
**Date:** 2026-08-12 (Next Vibe AI guide, published and updated); LTX quantization blog byline reads 2026-06-10 but the body documents LTX-2.5 flags and was clearly refreshed post-launch
**Retrieved:** 2026-08-24

## Content

### Official baseline for the standard Python path

docs.ltx.io system requirements for the standard `ltx-pipelines` LTX-2.5 path:

- **NVIDIA GPU with at least 32 GB VRAM**
- **32 GB system RAM**
- **~100 GB free storage**
- **CUDA 12.7+** (the LTX quantization blog separately states CUDA 13.2+ as a hard prerequisite for its quantization walkthrough — figures conflict; treat 12.7 as the model-card/system-requirements number)
- **Python 3.12+**

Caution flagged by the Next Vibe AI guide: do **not** combine requirements from LTX-2.3, LTX Desktop, community GGUF builds and LTX-2.5 Python pipelines as if they were the same setup. Community ComfyUI int8 figures (16 GB minimum) describe a different pipeline than the 32 GB bf16 PyTorch path.

### FP8: the only quantization natively supported in the LTX-2.5 codebase

FP8 reduces VRAM by **approximately 40%** with minimal quality loss. Two policies:

| Policy | FP8 Cast | FP8 Scaled MM |
| --- | --- | --- |
| CLI flag | `--quantization fp8-cast` | `--quantization fp8-scaled-mm` |
| Dependencies | None (built in) | TensorRT-LLM, `uv sync --frozen --extra fp8-trtllm` |
| GPU requirement | Any GPU with FP8 support (Ada Lovelace, Hopper, Blackwell) | Hopper (H100, H200) |
| Memory savings | Weight storage only, ~40% | Weight storage + compute, ~40% |
| Speed benefit | Moderate | Higher (native FP8 math) |
| Checkpoint | Use with **bf16** checkpoints (downcast on the fly) | Use with **fp8** checkpoints |

Both require setting `PYTORCH_CUDA_ALLOC_CONF=expandable_segments:True`:

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

Swap in `QuantizationPolicy.fp8_scaled_mm()` for the Hopper backend.

### MXFP8 and NVFP4 (Blackwell-only, forward-looking)

- **MXFP8** — 8-bit with **block-level scaling over groups of 32 elements** (Open Compute Project Microscaling Formats Spec). Preserves more dynamic range than per-tensor FP8; matters most in cross-attention layers where video and audio weight distributions differ. Hardware support: **B100, B200, GB200**.
- **NVFP4** — 4 bits, block-level microscaling. **A 22B model needs ~22 GB in FP8 and ~11 GB in NVFP4.** Only 16 discrete values per weight, so temporal consistency and fine texture can show artifacts. LTX-2.5 ships `ltx-2.5-22b-distilled-transformer-nvfp4.safetensors` (usable via `--quantization nvfp4-prequant`, Blackwell + `ltx-kernels`), though the ComfyUI loader for it was reported broken in the first 24 hours after launch.

| Format | Bits | Scaling | GPU requirement |
| --- | --- | --- | --- |
| FP8 (E4M3) | 8 | Per-tensor or per-channel | Ada Lovelace, Hopper, Blackwell |
| MXFP8 | 8 | Block-level (32 elements) | Blackwell |
| NVFP4 | 4 | Block-level microscaling | Blackwell |

E4M3 (4 exponent, 3 mantissa bits) is the inference-relevant FP8 variant; E5M2 targets gradients.

### Recommended stack for a 32 GB card

The documented minimum working configuration is **fp8-cast + the distilled checkpoint**. Supporting levers:

1. **Distilled checkpoint** — 8 steps versus 20–50 for the full model; cuts both time and peak memory. "On a 32 GB card this is the difference between working and not."
2. **Tiled VAE decode** — splits decoding into tiles, lowering peak memory at slightly slower decode. This is the fix when OOM hits at the **decode** stage rather than during sampling; quantization alone does not address it.
3. **Offload text encoding to the API** — the Gemma 4 text encoder and prompt enhancer both occupy VRAM; running them through the LTX API frees meaningful headroom.
4. `--offload cpu` for CPU offloading of the transformer.

### Frame/dimension constraints when tuning down

- Frame counts must satisfy `(F-1) % 8 == 0` — valid values include **57, 65, 97, 121**.
- Dimensions divisible by **64 for two-stage pipelines**, **32 for one-stage**.

### Community GGUF

`Abiray/LTX-2.5-Distilled-GGUF` publishes quantized GGUF builds of the LTX-2.5 distilled transformer for memory-constrained local runs. Community consensus reported: **Q4 is the sweet spot** with minimal quality loss, **Q3 shows noticeable degradation**, **Q8 is virtually identical to full precision**. No GGUF existed at launch — these were day-two community builds.

### OOM triage order

Identify whether memory fails while loading the transformer, text encoder, VAE, or upscaler, or during decode. Then reduce one variable at a time: resolution → frames → batch size → precision → concurrent models → decoding strategy. Close other GPU applications before retesting. If the gap is large, offloading plus aggressive quantization produces a slow experimental setup, not a production machine.
