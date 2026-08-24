---
title: LTX Video Memory Optimization
type: guide
created: 2026-04-13
updated: 2026-08-24
sources:
  - https://huggingface.co/docs/diffusers/main/optimization/memory
  - https://huggingface.co/docs/diffusers/api/pipelines/ltx_video
  - https://huggingface.co/Lightricks/LTX-Video
  - raw/tutorial-ltx-2-5-local-vram-quantization-guide-2026-08.md
tags:
  - memory
  - optimization
  - vram
  - fp8
  - offloading
  - performance
  - ltx-2-5
---

# LTX Video Memory Optimization

This page covers all techniques for reducing VRAM usage when running LTX Video pipelines. These techniques can be combined to run even the 2B model on ~10 GB VRAM.

## FP8 Layerwise Weight Casting

Stores the [[ltxv-transformer-architecture|transformer]] weights in FP8 format while computing in BF16, roughly halving the model's memory footprint:

```python
from diffusers import AutoModel

transformer = AutoModel.from_pretrained(
    "Lightricks/LTX-Video",
    subfolder="transformer",
    torch_dtype=torch.bfloat16
)
transformer.enable_layerwise_casting(
    storage_dtype=torch.float8_e4m3fn,
    compute_dtype=torch.bfloat16
)
```

## Group Offloading

Moves model components between GPU and CPU on demand, allowing much larger models to fit in limited VRAM:

```python
from diffusers.hooks import apply_group_offloading

onload_device = torch.device("cuda")
offload_device = torch.device("cpu")

# Transformer: leaf-level offloading with streaming
pipeline.transformer.enable_group_offload(
    onload_device=onload_device,
    offload_device=offload_device,
    offload_type="leaf_level",
    use_stream=True
)

# Text encoder: block-level offloading
apply_group_offloading(
    pipeline.text_encoder,
    onload_device=onload_device,
    offload_type="block_level",
    num_blocks_per_group=2
)

# VAE: leaf-level offloading
apply_group_offloading(
    pipeline.vae,
    onload_device=onload_device,
    offload_type="leaf_level"
)
```

**Note:** System RAM should be at least 2x model size when using CPU offloading with streams.

## CPU Offloading (Simple)

For a simpler approach with less fine-grained control:

```python
pipe.enable_model_cpu_offload()
# or for more aggressive offloading:
pipe.enable_sequential_cpu_offload()
```

## VAE Tiling

Splits the [[ltxv-video-vae|Video-VAE]] input into overlapping tiles for memory-efficient processing of large resolutions:

```python
pipeline.vae.enable_tiling()

# With custom tile parameters
pipeline.vae.enable_tiling(
    tile_sample_min_height=256,
    tile_sample_min_width=256,
    tile_sample_stride_height=192,
    tile_sample_stride_width=192
)
```

This is especially important for the [[two-stage-inference-pattern]] where upscaled latents may be very large.

## VAE Slicing

Processes VAE inputs in smaller batches:

```python
pipeline.vae.enable_slicing()
```

## torch.compile

Compiles the transformer for optimized execution. Has a warm-up cost on the first run but speeds up subsequent runs:

```python
pipeline.transformer.to(memory_format=torch.channels_last)
pipeline.transformer = torch.compile(
    pipeline.transformer, mode="max-autotune", fullgraph=True
)
```

## GGUF Quantized Models

Community-provided GGUF quantizations provide smaller model files:

```python
from diffusers import LTXPipeline, AutoModel, GGUFQuantizationConfig

transformer = AutoModel.from_single_file(
    "https://huggingface.co/city96/LTX-Video-gguf/blob/main/ltx-video-2b-v0.9-Q3_K_S.gguf",
    quantization_config=GGUFQuantizationConfig(compute_dtype=torch.bfloat16),
    torch_dtype=torch.bfloat16
)
```

## FP8 Quantized Model Variants

Pre-quantized FP8 model variants are available directly from Lightricks. See [[ltxv-model-variants]] for the full list. These require Ada Lovelace GPUs (RTX 40xx) or newer and CUDA Toolkit 12.8+.

## Combined Low-VRAM Setup (~10 GB)

The complete recipe for running on ~10 GB VRAM combines FP8 casting and group offloading:

```python
import torch
from diffusers import LTXPipeline, AutoModel
from diffusers.hooks import apply_group_offloading
from diffusers.utils import export_to_video

# 1. FP8 transformer
transformer = AutoModel.from_pretrained(
    "Lightricks/LTX-Video", subfolder="transformer", torch_dtype=torch.bfloat16
)
transformer.enable_layerwise_casting(
    storage_dtype=torch.float8_e4m3fn, compute_dtype=torch.bfloat16
)

# 2. Build pipeline
pipeline = LTXPipeline.from_pretrained(
    "Lightricks/LTX-Video", transformer=transformer, torch_dtype=torch.bfloat16
)

# 3. Group offloading for all components
onload_device = torch.device("cuda")
offload_device = torch.device("cpu")
pipeline.transformer.enable_group_offload(
    onload_device=onload_device, offload_device=offload_device,
    offload_type="leaf_level", use_stream=True
)
apply_group_offloading(
    pipeline.text_encoder, onload_device=onload_device,
    offload_type="block_level", num_blocks_per_group=2
)
apply_group_offloading(
    pipeline.vae, onload_device=onload_device, offload_type="leaf_level"
)

# 4. Generate
video = pipeline(
    prompt="...",
    negative_prompt="worst quality, inconsistent motion, blurry, jittery, distorted",
    width=768, height=512, num_frames=161,
    decode_timestep=0.03, decode_noise_scale=0.025,
    num_inference_steps=50,
).frames[0]
export_to_video(video, "output.mp4", fps=24)
```

## VRAM Budget Reference

| VRAM | Best Configuration |
|------|-------------------|
| 8 GB | 2B + FP8 + group offloading |
| 10 GB | 2B + FP8 + leaf-level offloading |
| 16 GB | 2B BF16 or 13B + FP8 + offloading |
| 24 GB | 13B + FP8 or 2B BF16 + torch.compile |
| 40+ GB | 13B BF16 + torch.compile |

## LTX-2.5 Memory Figures

The numbers above target the 2B/13B [[ltx-video-overview|LTX-Video]] family. LTX-2.5's 22B transformer is a different budget entirely -- full detail in [[ltx-2.5-local-inference]].

| Item | Figure |
|---|---|
| Official baseline (bf16 `ltx-pipelines`) | **32 GB VRAM**, 32 GB system RAM, ~100 GB storage |
| ComfyUI int8 pack (community/launch materials) | **16 GB VRAM** minimum, 24 GB comfortable |
| 22B transformer weights in FP8 | **~22 GB** |
| 22B transformer weights in NVFP4 | **~11 GB** |
| FP8 saving vs bf16 | **~40%** |

The 16 GB and 32 GB numbers describe **different pipelines** (ComfyUI int8 vs bf16 PyTorch) and must not be conflated.

### Minimum working config on a 32 GB card

`--quantization fp8-cast` plus the **distilled checkpoint** (8 steps vs 20-50). Supporting levers, in order:

1. Distilled checkpoint -- "on a 32 GB card this is the difference between working and not"
2. **Tiled VAE decode** -- the fix when OOM hits at the *decode* stage rather than during sampling; quantization alone does not address it
3. Offload text encoding to the LTX API -- the Gemma 4 encoder and prompt enhancer both hold VRAM
4. `--offload cpu` for the transformer

### OOM triage order

Identify *where* memory fails (transformer / text encoder / VAE / upscaler / decode), then reduce one variable at a time: **resolution -> frames -> batch size -> precision -> concurrent models -> decoding strategy**. Close other GPU applications before retesting. A large hardware gap closed by offloading plus aggressive quantization yields a slow experimental setup, not a production machine.

### Grid constraints when tuning down

- Frame counts must satisfy `(F-1) % 8 == 0` -- valid values include 57, 65, 97, 121
- Dimensions divisible by **64** for two-stage pipelines, **32** for one-stage

## Environment Variables

```bash
# Recommended for FP8 memory management
export PYTORCH_CUDA_ALLOC_CONF=expandable_segments:True
```

## See Also

- [[ltx-2.5-local-inference]] -- LTX-2.5 VRAM, quantization and OOM triage
- [[fp8-quantization]] -- FP8 cast vs scaled-mm, MXFP8, NVFP4
- [[ltxv-model-variants]] -- choosing the right model for your hardware
- [[python-installation-setup]] -- installation including optional dependencies
- [[ltxv-video-vae]] -- VAE tiling details
- [[two-stage-inference-pattern]] -- the recommended workflow
