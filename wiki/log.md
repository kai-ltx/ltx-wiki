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

## [2026-06-08] ingest | Weekly update
Sources added: 4 files (Area1/LTX news: 1, Area2/Community: 0, Area3/Competitors: 2, Area4/Tutorials: 1). Pages created: [[competitor-grok-imagine-video]]. Pages updated: [[wan-video]], [[competitor-landscape-overview]], [[ic-lora]], [[comfyui-ltx-workflows]].
Key findings: (1) Grok Imagine Video 1.5 (xAI) launched June 3 as new competitor — #1 on I2V leaderboard (Elo 1404), native audio, $0.08–0.14/s, API preview; (2) LTX-2.3 IC-LoRA Union Control and Motion Track Control ComfyUI workflows now available on comfy.org and RunComfy; Python usage in LTX-2 GitHub issue #203; (3) Wan 2.7 open weights confirmed available under Apache 2.0 (as of May 2026); Wan 3.0 on roadmap for mid-2026 (60B params, 30s clips, unconfirmed); (4) EU AI Act Article 50 enforcement August 2, 2026 (with transition to December 2 for existing systems); Sora API sunset September 24, 2026 confirmed; June 2026 AI launch wave is primarily text/reasoning models — video model graph unchanged.

## [2026-06-08] lint | Weekly health check
Broken links: 0 (in all 5 updated/created pages). Index drift: 0 ([[competitor-grok-imagine-video]] confirmed in index at line 262). Format issues: 0 (all pages have valid frontmatter with correct updated: 2026-06-08). Pre-existing broken links (documented in prior entries, not introduced this week): ~6 artifacts ([[lightricks]], 2× [[comfyui-integration]], [[dit-architecture]], [[related-work-and-comparisons]], [[character-consistency]]).

## [2026-06-15] ingest | Weekly update
Sources added: 5 files combined across two parallel runs (Area1/LTX news: 1, Area2/Community: 1, Area3/Competitors: 3, Area4/Tutorials: 0). Pages created: none. Pages updated: [[competitor-kling]], [[wan-video]], [[competitor-landscape-overview]].
Key findings: (1) No new LTX model or API releases since May 11 (Video to Video in Studio) and May 3 (Async API expanded) — confirmed via ltx.io/release-notes; (2) Kling AI officially launched Kling 3.0 multi-variant lineup on June 12, 2026 — Video 3.0, Video 3.0 Omni, Image 3.0, Image 3.0 Omni; built on MVL (Multi-modal Visual Language) framework; native multilingual audio (6 languages + accents), 15s video, text/logo preservation, multi-shot storyboard with per-shot camera control; Kling v3 leads global video leaderboard at Elo 2031; LTX-2 Fast holds #2 (Elo 1930); 60M+ creators, 30K enterprise clients; (3) Wan 3.0 confirmed as released (previously listed as "roadmap/unconfirmed"): 60B MoE params, native 4K from frame 1, up to 30s single-pass, multi-shot narratives up to 2–5 min, Apache 2.0 open weights, ~40% faster than Wan 2.6; (4) Runway's most recent update was Aleph 2.0 & Edit Studio on May 21 — no new releases this week; (5) Sora API sunset remains September 24, 2026.

## [2026-06-15] lint | Weekly health check
Broken links: 0 (all links in updated pages verified — all 15 wikilink targets confirmed existing). Index drift: 0 (no new pages created this week; all updated pages confirmed in index). Format issues: 0 (all updated pages have valid frontmatter with correct updated: 2026-06-15). Pre-existing broken links (documented in prior entries, unchanged): ~6 artifacts ([[lightricks]], 2× [[comfyui-integration]], [[dit-architecture]], [[related-work-and-comparisons]], [[character-consistency]]).


## [2026-07-06] Weekly Update — Kling $2.8B Raise, Seedance 2.5, ByteDance Entry

**Research period:** 2026-06-30 to 2026-07-06

**Pages updated:**
- `wiki/competitor-kling.md` — Added Funding & Business section: $2.8B raise at $18B valuation (July 3, 2026), investors (Tencent, Alibaba, Baidu, CITIC Securities, 38 total), Kuaishou diluted to ~68%, ARR trajectory ($100M→$300M→$500M in 12 months), HK IPO target within 12 months. Updated ARR figure in Strengths to $500M.
- `wiki/competitor-landscape-overview.md` — Added [[competitor-seedance|Seedance 2.5]] to competitor table; updated Market Dynamics to July 2026, added Kling $18B valuation context and Seedance 2.5 entry.
- `wiki/competitor-seedance.md` (NEW) — Created new page documenting Seedance 2.0 (API tiers, C2PA watermarking) and Seedance 2.5 (native 30s, 50 multimodal refs, local editing, native 4K 10-bit).

**Raw files created:**
- `raw/competitor-kling-funding-july-2026.md`
- `raw/competitor-seedance-25-july-2026.md`

**Lint results:** 0 broken links in updated/created pages. Pre-existing broken links (documented in prior entries, unchanged): ~6 artifacts ([[lightricks]], 2× [[comfyui-integration]], [[dit-architecture]], [[related-work-and-comparisons]], [[character-consistency]]). Index drift: 0 (competitor-seedance.md added to index below). Format issues: 0.

## [2026-06-30] ingest | Weekly update
Sources added: 3 files (Area1/LTX news: 1, Area2/Community: 0, Area3/Competitors: 1, Area4/Tutorials: 1). Pages created: none. Pages updated: [[ltx-video-trainer]], [[competitor-runway]], [[lora-community-ecosystem]].
Key findings: (1) LTX Trainer unified framework released June 17 — 13 training modes covering video, audio, cross-modal, and IC-LoRA from a single config file; new agentic config generation via Claude/LLMs; supports AV2AV joint IC-LoRA (first in ecosystem); (2) Runway: Studio Trim (June 18, stitch/reorder/export in one place), Agent 2.0 (June 25, marketing-focused campaign creation with ad-performance analysis), Seedance 2.0 4K API (June 24, 150 credits/s), Seedance 2.0 Mini API (June 26, 16 credits/s), HappyHorse 1.0 API (May 29, third-party model); (3) LTX-2.3 3DREAL IC-LoRA released June 26 by Lovis Odin + fal.ai — converts 3D renders/CG blockouts to photorealistic video while preserving camera path and composition; available on fal.ai endpoint with no download required; (4) No new LTX Studio releases since May 11; no new core model releases; Veo 4 not announced as of June 30.


## [2026-07-06] Weekly Update — Kling $2.8B Raise, Seedance 2.5, ByteDance Entry

**Research period:** 2026-06-30 to 2026-07-06

**Pages updated:**
- `wiki/competitor-kling.md` — Added Funding & Business section: $2.8B raise at $18B valuation (July 3, 2026), investors (Tencent, Alibaba, Baidu, CITIC Securities, 38 total), Kuaishou diluted to ~68%, ARR trajectory ($100M→$300M→$500M in 12 months), HK IPO target within 12 months. Updated ARR figure in Strengths to $500M.
- `wiki/competitor-landscape-overview.md` — Added [[competitor-seedance|Seedance 2.5]] to competitor table; updated Market Dynamics to July 2026, added Kling $18B valuation context and Seedance 2.5 entry.
- `wiki/competitor-seedance.md` (NEW) — Created new page documenting Seedance 2.0 (API tiers, C2PA watermarking) and Seedance 2.5 (native 30s, 50 multimodal refs, local editing, native 4K 10-bit).

**Raw files created:**
- `raw/competitor-kling-funding-july-2026.md`
- `raw/competitor-seedance-25-july-2026.md`

**Lint results:** 0 broken links in updated/created pages. Pre-existing broken links (documented in prior entries, unchanged): ~6 artifacts ([[lightricks]], 2× [[comfyui-integration]], [[dit-architecture]], [[related-work-and-comparisons]], [[character-consistency]]). Index drift: 0 (competitor-seedance.md added to index below). Format issues: 0.

## [2026-06-30] lint | Weekly health check
Broken links: 0 (all wikilinks in 3 updated pages verified). Index drift: 0 (no new pages created). Format issues: 0 (all updated pages have valid frontmatter with correct updated: 2026-06-30). Pre-existing broken link artifacts (unchanged from prior entries): ~6 backslash-escaped table-cell artifacts.

## [2026-07-21] ingest | Weekly update
Sources added: 7 files (Area1/LTX news: 3, Area2/Community: 1, Area3/Competitors: 2, Area4/Tutorials: 1). Pages created: [[ltx-explore]]. Pages updated: [[ltx-video-api-models]], [[ltx-video-api-endpoints]], [[ltx-2-version-history]], [[competitor-runway]], [[hunyuan-video]], [[comfyui-ltx-workflow-tutorials]], [[ltx-model-comparisons]], [[ltx-ecosystem]].
Key findings: (1) LTX-2 (original) formally deprecated July 2, 2026 -- auto-routed to LTX-2.3 from July 15, fully removed August 15; community migration guides flag LoRA incompatibility, more-literal prompt following, punchier default color, and seed divergence between generations; (2) LTX shipped a production Video Outpainting/Reframe API (July 13) supporting 5 aspect ratios up to 1080p via two-stage seam-blended generation, plus a companion community outpainting IC-LoRA, both picked up in ComfyUI tutorials/hosted workflows within days; (3) Lightricks launched LTX Explore (July 20), a new no-code self-service tier at app.ltx.io sitting between LTX Studio and the raw API, with weekly community-driven LoRA/IC-LoRA expansion; (4) Runway shipped no new flagship model this week but expanded its API marketplace (Gemini Omni Flash, Nano Banana 2 Lite, Agent Skills, Veo negativePrompt, Seedream 5.0 Lite) -- reinforcing its model-agnostic aggregator strategy; (5) HunyuanVideo's practical VRAM floor keeps dropping (community FP8 + tiling + offloading stacks now reach ~8GB), narrowing its historical gap with LTX-2.3; (6) No genuinely new Kling, Wan, or Sora releases this week beyond items already logged July 6 (Kling funding, Seedance 2.5) -- Sora API sunset remains Sept 24, 2026.

## [2026-07-21] lint | Weekly health check
Broken links: 0 introduced this week (verified all wikilinks in 9 new/updated pages resolve to existing files). Index drift: 0 (ltx-explore.md added to index.md under Company & Products; full index<->file cross-check found zero missing pages and zero dangling index entries). Format issues: 0 (new page ltx-explore.md has complete frontmatter: title/type/created/updated/sources/tags). Pre-existing broken links (documented in prior entries, unchanged): ~6-7 backslash-escaped table-cell artifacts across ltxv-model-variants.md, community-feature-requests.md, and others (pipe-in-table-cell markdown syntax, not true broken wikilinks) plus intentional non-page references in log.md itself ([[lightricks]], [[comfyui-integration]], [[dit-architecture]], [[related-work-and-comparisons]], [[character-consistency]]).
