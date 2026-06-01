---
title: Wiki Log
type: overview
created: 2026-04-13
updated: 2026-04-13
---

# Wiki Log

Chronological record of wiki operations. Append-only — never edit past entries.

Format: `## [YYYY-MM-DD] verb | Subject`

---

## [2026-04-13] create | Wiki initialized

Scaffolding created: directory structure, CLAUDE.md schema, index.md, log.md.

## [2026-04-13] ingest | Bulk research — 236 raw sources across 11 research agents

Research conducted via 11 parallel agents covering: LTX Video models, Lightricks products, GitHub repos, API/developer docs, ComfyUI workflows, Python/Diffusers, research papers, community projects, social media/Reddit, competitors (model + product), LTX-2 deep dive. Total: 236 markdown source files saved to raw/.

## [2026-04-13] ingest | Bulk wiki build — 206 wiki pages across 20 ingest agents

20 parallel ingest agents processed all 236 raw sources into 206 structured wiki pages. Each agent owned a thematic domain:

1. **LTX Video Overview** (8 pages) — overview hub, versions, capabilities, changelog, variants, HuggingFace, evolution
2. **Early Versions 0.9.0–0.9.6** (10 pages) — per-version pages, distillation, CFG, FP8, dev vs distilled
3. **LTX Video 0.9.7–0.9.8** (7 pages) — 13B model, IC-LoRA, spatial upscaler, multiscale rendering, variants
4. **LTX-2 Core** (13 pages) — overview, architecture, versions, 2.3, capabilities, variants, benchmarks, reception, API, NVIDIA
5. **LTX-2 Integration** (9 pages) — ComfyUI, Diffusers, guides (T2V, I2V, IC-LoRA, training), system requirements
6. **Architecture** (10 pages) — VAE, denoising decoder, DiT, RoPE, compression, loss functions, conditioning, rectified flow
7. **Research Papers** (9 pages) — 6 Lightricks papers, citations, research overview
8. **Official API** (10 pages) — REST API, endpoints, models, pricing, prompting, formats, errors, HF model cards
9. **Inference Providers** (9 pages) — fal.ai, Replicate, Segmind, WaveSpeed, HuggingFace, Modal, RunPod, RunComfy
10. **Python Pipelines** (13 pages) — installation, all pipeline classes, scheduler API, VAE API, memory optimization, native API
11. **Python Advanced** (17 pages) — conditioning, schedulers, batch, callbacks, speed/memory optimization, LoRA, integration, SDKs
12. **ComfyUI** (12 pages) — official nodes, node reference, community nodes, workflows, tutorials, performance, LoRA, Manager
13. **Training** (7 pages) — methodology, LoRA training, datasets, hyperparameters, trainers, third-party services, community
14. **Community Projects** (10 pages) — GGUF, Jetson Thor, PromptGen, Turbo Space, LipSync, camera LoRAs, benchmarks
15. **Adoption & Feedback** (7 pages) — metrics, HF Spaces, Civitai, Discord, feedback, feature requests, showcases
16. **Social Media** (14 pages) — Reddit, YouTube, X/Twitter, blogs, HN, sentiment, desktop/studio reception
17. **Model Competitors** (11 pages) — Wan, HunyuanVideo, CogVideo, Mochi, Open-Sora, AnimateDiff, SVD, landscape
18. **Product Competitors** (9 pages) — Runway, Pika, Kling, Sora, Luma, Veo, desktop tools, MCP integrations
19. **Products & Company** (10 pages) — Lightricks, ecosystem, Studio, Desktop, MCP, licensing, NVIDIA, API, Builders
20. **Tutorials & Use Cases** (10 pages) — prompting, hardware, installation, Apple Silicon, upscalers, use cases, audio-video

## [2026-04-13] create | index.md consolidated

Built comprehensive index.md with 206 pages organized into 16 categories: Overviews, Company & Products, LTX-Video Versions, LTX-2, Architecture, Papers, API, Providers, Python, ComfyUI, Training, Community, Adoption, Social Media, Competitors (model + product), Guides.

## [2026-04-13] lint | Wiki health check

Full lint with 5 parallel agents. Found: 83 broken wikilinks (10 unique targets), 7 contradictions, 6 stale claims, 127 non-standard types, 179 missing References sections, 7 pages missing from index, 26 missing cross-references, 28 data gaps.

Fixed critical issues:
- 83 broken wikilinks resolved (8 naming mismatches: [[lightricks]]→[[lightricks-company]], [[comfyui-integration]]→[[comfyui-ltx-integration-overview]], [[dit-architecture]]→[[diffusion-transformer]], etc.)
- 7 missing GitHub pages added to index.md (new "GitHub & Code" section)
- API pricing contradiction in ltx-2-api-and-pricing.md (resolution tiers were shifted)
- Replicate LTX-2 availability corrected in replicate.md and inference-providers-overview.md
- Speed claim fixed in wan-video.md ("5-10x" → "18x faster than Wan 2.2")
- LTX-2.3 parameter count clarified ("~20B" → "22B (20.9B excluding text encoder)")
- LoRA support version corrected in ltx-video-overview.md ("v0.9.7+" → "v0.9.5+")

## [2026-05-19] ingest | Weekly update
Sources added: 23 files (LTX news: 6, Community: 5, Competitors: 7, Tutorials/Integrations: 5). Pages created: [[ltx-studio-canvas]], [[ltx-studio-flows]], [[ltx-api-async-hdr]], [[hunyuan-world]], [[ltx-studio-apr-may-2026-updates]]. Pages updated: [[ltx-desktop]], [[ltx-video-api]], [[ltx-studio]], [[ltx-video-098]], [[apple-silicon-setup]], [[replicate]], [[fal-ai]], [[runpod]], [[modal]], [[comfyui-ltx-workflows]], [[competitor-kling]], [[competitor-luma]], [[competitor-runway]], [[competitor-sora]], [[wan-video]], [[hunyuan-video]], [[ltx-2-community-reception]], [[ltx-studio-platform-reviews]], [[lora-community-ecosystem]].

## [2026-05-25] ingest | Weekly update
Sources added: 9 files (Area1/LTX news: 2, Area2/Community: 1, Area3/Competitors: 4, Area4/Tutorials: 2). Pages created: none. Pages updated: [[ic-lora]], [[camera-control-loras]], [[lora-community-ecosystem]], [[competitor-kling]], [[wan-video]].
Key findings: (1) Community IC-LoRA Cameraman V1 by Cseti released May 22 — camera motion transfer for LTX-2.3; (2) LTX Studio Video-to-Video and Flows already documented from prior week; (3) Sora app shutdown confirmed Apr 26; (4) Runway Gen-4 (May 3) with native audio; Kling 3.5 browser-based platform (May 2026); (5) Wan 2.7 pricing confirmed $6/min; LTX-2.3 Diffusers support still "coming soon".

## [2026-05-25] lint | Weekly health check
Broken links: 80 (all pre-existing; 0 introduced this week). Index drift: 0. Format issues: 0 (all 5 updated pages have clean frontmatter with correct updated: 2026-05-25).
Pre-existing broken link breakdown: ~50 trailing-backslash artifacts (CRLF encoding in source files), 5× [[related-work-and-comparisons]] (file not created), 6× [[comfyui-integration]] → should be [[comfyui-ltx-integration-overview]] (noted in Apr 13 lint, not yet fully resolved), 4 GitHub section-anchor links in github-community-forks.md, 1× [[character-consistency]] in competitor-pika.md. No new pages added to or removed from index — index drift remains at 0.

## [2026-06-01] ingest | Weekly update
Sources added: 3 files (Area1/LTX news: 2, Area2/Community: 0, Area3/Competitors: 1, Area4/Tutorials: 0). Pages created: none. Pages updated: [[ic-lora]], [[ltx-2-model-variants]], [[competitor-runway]].
Key findings: (1) Official Lightricks IC-LoRA HDR (16-bit HDR + SDR→HDR via LogC3) and IC-LoRA LipDub (JustDubIt-based joint audio-visual lip-dubbing) added to LTX-2.3 adapter family; (2) 17 new LTX-2.3 model variants released May 27 including MXFP8 transformer-only variants (Kijai), standalone Audio VAE, Spatial Upscaler x2 v1.1, and official Distilled LoRA rank-384 v1.0; (3) LTX 2.3 Dev NVFP4 (21.7 GB) official checkpoint for Blackwell/RTX 50xx released; (4) Runway Gen-4.5 confirmed holding #1 position on Artificial Analysis Text-to-Video benchmark (1,247 Elo) as of June 2026; (5) LTX Studio release notes show no new entries since May 11 — Video to Video and Flows remain the most recent Studio features; (6) Wan 2.7 open weights still pending (cloud since April 3).

## [2026-06-01] lint | Weekly health check
Broken links: 0 (in updated pages). Pre-existing broken links in log.md: 6 (all documented in prior lint entries — [[lightricks]], 2× [[comfyui-integration]], [[dit-architecture]], [[related-work-and-comparisons]], [[character-consistency]]). Index drift: 0 (no new pages created this week). Format issues: 0 (all 3 updated pages have valid frontmatter with correct updated: 2026-06-01).
