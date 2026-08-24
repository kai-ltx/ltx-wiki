# MiniMax H3 (Hailuo 3.0): Omni-Modal 2K Video Model, Open Weights Aug 3 2026

**Source:** https://www.marktechpost.com/2026/08/01/minimax-releases-minimax-h3-an-omni-modal-video-model-that-generates-15-second-2k-clips-with-native-stereo-audio/
**Date:** 2026-08-01
**Retrieved:** 2026-08-24

## Content

Additional sources: https://www.minimax.io/blog/minimax-h3 (official), https://huggingface.co/MiniMaxAI/MiniMax-H3, https://explainx.ai/blog/minimax-h3-open-video-model-hailuo-july-2026, https://www.scmp.com/tech/article/3362540/video-ai-minimax-challenges-bytedance-low-price-open-weights-new-h3-model

**Timeline**
- Teased 2026-07-30; **launched 2026-07-31** via platform API (model ID `MiniMax-H3`) and the consumer Hailuo AI app (hailuoai.video).
- At launch open weights were promised "in the coming days," not shipped.
- **Open weights published on Hugging Face 2026-08-03** as `MiniMaxAI/MiniMax-H3`, a **33B-parameter** omni-modal model. Reported license **excludes local deployment in the US, EU, UK and South Korea** — a significant carve-out for Western self-hosters.

**Positioning.** MiniMax frames H3 not as a text-to-video model with add-ons but as a general-purpose multimodal generation model that reads text, images, video and audio as one unified context and returns video with native stereo sound. It collapses what were previously separate expert models (T2V, I2V, first/last frame, subject reference, motion reference, video editing) into a single pretraining paradigm where reference and editing relationships are expressed in natural language. Example prompt from MiniMax: "reference the camera movement from Video 1, have the character in Image 2 sing, match the vocals to Audio 3."

**Specs**
- Output: **2K (2560x1440)**, **4-15 seconds**, integer durations only, native stereo audio.
- API: single endpoint, async three-step flow (create task, poll `task_id`, download `content.url`). Three entry modes: text-to-video, first/last-frame image-to-video, reference generation.
- Input limits: up to **9 reference images**, **3 reference videos** (2-15s each, <=15s total), **3 reference audio clips** (audio cannot be sent without an accompanying image or video). **Mixed input caps at 12 files total.** Prompt <=7,000 chars; request body <=64 MB. Video <=50 MB, image <=30 MB, audio <=15 MB per asset. Formats: H.264/H.265, JPG/PNG/WEBP/HEIC/HEIF, WAV/MP3.

**Four technical components**
1. **Contextual Omni Representation** — captioning rebuilt to describe the *relationship* between context and target video. ~100K tokens of source material distilled to ~4K tokens on average.
2. **H3-VAE** — full tokenizer overhaul; high compression ratio delivers a stated **4x gain in effective sequence length**, the enabling technology for native 2K.
3. **H3-Omni Transformer** — explicitly abandons the Hailuo-02 architecture; separates understanding and generation workloads. Reported **end-to-end training throughput up nearly 30%**.
4. **In-Context Regeneration** — replaces bolt-on super-resolution; the base model regenerates its own low-res output in-context, re-reading the original multimodal context. Recovers small text and fine detail (relevant to brand/product rendering).

**Pricing.** MiniMax claims that at 2K, H3's per-second price is **less than a third** of mainstream models; at 768p, **less than half** the price of mainstream 720p. Third-party trackers report **$0.13 per second** pay-as-you-go at 2K (~$1.95 for a 15s clip) — treat as reported, not primary, since MiniMax's own pay-as-you-go page still listed only Hailuo 2.3 tiers at the time. Artificial Analysis lists H3 API pricing at **$7.80/min** for 1 minute of 1080p at default settings.

**Benchmark standing (Artificial Analysis, as of 2026-08-24)**
- Text-to-video **with audio**: #3, Elo **1,228** (95% CI -8/+8, 8,316 samples). Behind Wan 3.0 (1,244) and Gemini Omni Flash (1,238).
- Text-to-video **without audio**: #2, Elo **1,303**, behind Gemini Omni Flash (1,322).
- Image-to-video **with audio**: #2, Elo **1,184**, behind Dreamina Seedance 2.0 720p (1,191), ahead of Gemini Omni Flash (1,182).
- Image-to-video **without audio**: #2, Elo **1,346**, behind Gemini Omni Flash (1,366).
- **Leads video editing** per Artificial Analysis.
- **Now the top open-weights video model in every AA category**, displacing LTX: best open-weights T2V with audio (1,228 vs LTX-2.5 Pro/Fast at 1,063), best open-weights T2V without audio (1,303 vs LTX-2.5 Fast 1,211), best open-weights I2V with audio (1,184 vs MAGI-2 Preview 1,100 and LTX-2.5 Fast 1,043).

**Competitive read for LTX:** H3 opens a ~165 Elo gap over LTX-2.5 Pro/Fast on open-weights T2V-with-audio and ~140 Elo on open-weights I2V-with-audio. Its regional license exclusion (US/EU/UK/KR) is the main structural opening — LTX remains the strongest genuinely deployable open-weights option in those markets.

**Positioned industries (MiniMax):** advertising, branding, e-commerce, product design, UI/UX, gaming, film pre-visualization, retail catalog media.
