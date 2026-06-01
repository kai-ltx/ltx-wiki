# LTX-2.3: 17 New Model Variants Released (Audio VAE, MXFP8, Upscaler)

**Source:** https://ltxworkflow.com/changelog
**Date:** 2026-05-27
**Retrieved:** 2026-06-01

## Content

Lightricks and community contributors (notably Kijai) released 17 new model variant checkpoints for LTX-2.3 on or around May 27, 2026.

### New Official Lightricks Variants
- **Spatial Upscaler x2 v1.1** — updated upscaler model; improved quality over v1.0
- **Distilled LoRA rank-384 v1.0** — official high-rank distilled LoRA for LTX-2.3
- **Dynamic LoRA rank-105** — community variant by Kijai; dynamic-rank LoRA

### New Kijai Community Variants
- **LTX23 Audio VAE** — enables audio-conditioned video generation workflows in ComfyUI
- **LTX23 Video VAE BF16** and **Text Projection BF16** — component-level BF16 variants
- **Distilled 1.1 BF16** — BF16 precision version of the distilled v1.1 model
- **Distilled 1.1 MXFP8** — Microscaling FP8 (MX-format) transformer-only variant
- **Dev BF16**, **Dev FP8 Scaled**, **Dev MXFP8** — three precision variants of the full dev model
- **Distilled v1.0 BF16**, **Distilled v1.0 FP8 v1/v2/Scaled**, **Distilled v1.0 MXFP8** — six precision/version variants of the original distilled model

### Notes on MXFP8
MXFP8 (Microscaling FP8) is a newer quantization format offering better accuracy than standard FP8 at similar memory footprint. These are transformer-only variants — they require separate VAE and text encoder weights.

### Impact on ComfyUI Workflows
The Audio VAE by Kijai is particularly significant: it enables audio-conditioned generation in ComfyUI without the full LTX-2 audio inference stack, allowing community workflows to leverage LTX-2.3's audio capabilities in a modular way.
