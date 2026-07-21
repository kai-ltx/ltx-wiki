# HunyuanVideo — Lower VRAM Floor via Community + ComfyUI Optimization (July 2026 update)

**Source:** https://willitrunai.com/blog/hunyuanvideo-1-5-vram-requirements ; https://blog.comfy.org/p/running-hunyuan-with-8gb-vram-and
**Date:** 2026-07-20 (guide updated)
**Retrieved:** 2026-07-21

## Content

A widely-cited GPU/VRAM guide for AI video models was updated on 2026-07-20, noting the practical HunyuanVideo hardware stack has shifted meaningfully since June 2026 benchmarks, mostly toward lower VRAM floors:

- **Tencent's official floor**: ~14GB with CPU offloading enabled for the original 13B HunyuanVideo; disabling offloading is faster but needs significantly more memory.
- **ComfyUI's native (non-optimized) recommendation**: 24GB consumer cards, because the pipeline also loads the Qwen 2.5-VL text encoder, the byT5 glyph encoder, the VAE, and a separate super-resolution model in addition to the diffusion transformer itself.
- **HunyuanVideo 1.5** (Tencent's slimmed 8.3B-parameter model, released Nov 2025): runs in roughly ~14GB with offloading; with FP8 quantization + tiling, practical VRAM drops to ~8GB.
- **Community workflows** (temporal-tiled VAE decode/encode nodes, introduced via ComfyUI v0.3.10) have brought the original 13B model down to ~8GB VRAM at reduced resolution — previously this required ~32GB.
- Net effect: HunyuanVideo, once considered VRAM-hungry compared to LTX and Wan, is now competitive on consumer 12-16GB GPUs via FP8 + tiling + offloading stacks.

Relevant for the wiki's comfyui-ltx-model-comparison and hardware-requirements pages, since this narrows the historical VRAM gap between LTX-2.3 (already efficient on consumer GPUs) and HunyuanVideo.
