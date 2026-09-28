# Tutorial: What Training Data You Need to Fine-Tune LTX-2.5 (Official LTX Blog Guide)

**Source:** https://ltx.io/blog/video-model-training-data
**Date:** 2026-09-07
**Retrieved:** 2026-09-28

## Content

Official LTX blog post by Tally Moran (LTX Content Manager), a practical guide to preparing training data for LoRA/full fine-tuning/IC-LoRA on LTX-2, LTX-2.3, and LTX-2.5 via the current unified LTX Trainer (13+ training modes: t2v, i2v, video/audio extension, inpainting/outpainting, audio-to-video, video-to-audio, IC-LoRA transformations).

Key technical facts:
- **Resolution/frame rules**: with the default LTX Video VAE, spatial dimensions must be multiples of 32, and frame counts must satisfy `frames % 8 == 1` (valid values: 1, 9, 17, 25, 33, 41, 49, 57, 65, 73, 81, 89, 97, 121...). The trainer derives actual compression factors from the loaded checkpoint, so this can differ for other VAEs. Sequence length formula: `(H/32) * (W/32) * ((F-1)/8 + 1)` — e.g. a 768x448x89 clip = 4,032 tokens.
- **Choosing an approach**: LoRA (lightweight adapters, frozen base model, single-GPU-capable) is the default for focused style/effect/subject training. Full fine-tuning updates all parameters and needs multiple high-end GPUs (documented FSDP setups: 4-8x H100 80GB). IC-LoRA needs paired reference+target data and is for transformations (depth/pose control, style transfer, deblurring, colorization).
- **Hardware**: standard config recommends 80GB VRAM; low-VRAM config brings LoRA training to 32GB consumer cards (e.g. RTX 5090) via INT8 quantization.
- **LTX-2.5 specifics**: must use the LTX-specific fine-tuned Gemma 4 12B encoder — Google's vanilla Gemma 4 will fail the checkpoint compatibility check. Older LTX-2/LTX-2.3 checkpoints use a matching Gemma 3 encoder instead. If migrating an existing dataset from LTX-2.3 to LTX-2.5, text features must be reprocessed with the new Gemma 4 encoder — Gemma 3 and Gemma 4 embeddings are not interchangeable (use a fresh `.precomputed` directory or `--overwrite`).
- **Captioning**: the trainer can auto-caption via `caption_videos.py` using either a local `qwen_omni` captioner or the `gemini_flash` API captioner; captions can describe both visual and audio content. Auto-captions can hallucinate and should be manually reviewed. A `--lora-trigger` word can be set, prepended to every caption, later used to activate the LoRA at inference.
- **Preprocessing workflow** (3 steps): (1) optional scene-splitting via `scripts/split_scenes.py --filter-shorter-than 5s`; (2) optional captioning into `dataset.json`; (3) `scripts/process_dataset.py` to compute/cache latents and text embeddings with `--resolution-buckets`. Metadata file can be CSV/JSON/JSONL with `caption`/`video` columns (`media_path` is a legacy alias). Mixed image+video datasets need multiple resolution buckets and training batch size of 1.
- **Common mistakes flagged**: invalid resolution buckets, mixing images/video without separate frame-count buckets, trusting raw auto-captions without review, and (for IC-LoRA) reference/target pairs that don't cover matching content.

## Why this matters for the wiki
This is the first officially published, LTX-2.5-specific training-data guide since the LTX Trainer's major June 17, 2026 unification. It fills a documentation gap for creators wanting to fine-tune LTX-2.5 specifically (as opposed to LTX-2.3), particularly the hard requirement to use the new Gemma 4 encoder and reprocess cached features when migrating datasets.
