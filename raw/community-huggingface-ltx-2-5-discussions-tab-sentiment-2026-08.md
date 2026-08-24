# Hugging Face Lightricks/LTX-2.5 Discussions Tab: 60+ Threads in Two Weeks (Aug 12-24, 2026)

**Source:** https://huggingface.co/Lightricks/LTX-2.5/discussions
**Date:** 2026-08-12 to 2026-08-24
**Retrieved:** 2026-08-24

## Content

### Engagement metrics (verified from page)

- The `Lightricks/LTX-2.5` model page carried **~1.3k-1.4k likes** and the LTX.io org **~4.64k-4.68k
  followers** at retrieval on 2026-08-24. Cached snapshots served during the same crawl session
  showed **918 likes / 44 community threads** and **1.11k likes / 52 threads**, indicating the
  page was still growing fast roughly two weeks post-launch.
- **59-61 community threads** open + **15 closed** as of 2026-08-24, from a model published
  2026-08-11.
- Repo is **gated** under the `ltx-2-community-license-agreement`; download requires accepting
  terms and an authenticated Read token with gated-repo scope.

### Positive threads

- **#4 "Thank You"** by `dns` — the single most-reacted thread, **25 reactions and 14 replies**.
- **#22 "Keep it up, LTX! Thank you!"** (5 replies), **#12 "Thanks for the model and thanks
  for..."** (2 fire reactions), **#23 "thank you!!"**, **#24** from `Sikaworld1990`: "1st o.a.
  thx LTX team for another topmodel! I have built a wf for the dev model."
- **#25 "LTX 2.5 on RTX 3060: Impressive Speed & Quality Out of the Box"** by `LabMike3D`:
  "Currently testing LTX 2.5 on my RTX 3060 12GB, and the speed and quality are absolutely
  mind-blowing. Running a basic, default ComfyUI workflow (960x544, T2V) gets me a **15-second
  video in just about 5 minutes**. That is freaking awesome performance for a 3060! No special
  CUI tweaks. No secret sauce."
- **#37 "LTX 2.5 Just Changed Local AI Video Forever!"** (LabMike3D), **#45 "Brilliant work
  LTX2.5! high-action boxing fight videos optimized"** (David-G2026).

### Negative threads

- **#38 "Atrocious model - object permanence/consistency is nonexistent"** by `kabachuha`
  (2026-08-23): "I'd *like* to like your model, the competition and stuff, but... the model is
  simply a disaster. Censorship/copyright aside, I don't know how you are going to sell it as a
  'world model' - there is simply NO object permanence. Objects appear, disappear, morph,
  transform, the image2video doesn't hold the consistency. I'm using a dev model with diffusion
  decoder for 'higher quality' and still all the bad things persist. **The current architecture
  / data approach is a dead end**, sorry." Posted with an attached failure video. No Lightricks
  reply at retrieval.
- **#30 "The character consistency in i2v is a disaster."** by `lol104` (2026-08-19). Follow-up
  detail: tested the same half-portrait photo of a European woman through 2.3 and 2.5 —
  "**LTX 2.3 rendered the woman correctly, but with LTX 2.5, she looked completely different.**"
  Adding `LTX-2.3-ID-LoRA-CelebVHQ-3K.safetensors` made it worse: "the woman suddenly had an
  Asian face." Reporter is on a Mac mini M4 Pro, 25GB RAM. Another user speculated a 2.5 face-ID
  LoRA would fix it; none was confirmed as planned.
- **#14 "still 2.5 character consistency not perfect"** (rafiislam) — same complaint, 4 replies.
- **#57 "Don't Use LTX 2.5 For Music Videos! Stick To LTX 2.3"** by `LabMike3D` (2026-08-23) —
  notable because the same user posted the enthusiastic #25 and #37. "Is newer always better?
  Not this time. If you are trying to create singing AI avatars, the older LTX 2.3 model
  delivers significantly better results than the new LTX 2.5... **LTX 2.5 clearly struggles with
  its text encoder (Gemma 4) implementation.** This causes major issues when trying to sync and
  process precise audio and lip movements for musical avatars... After extensive benchmark
  tests, I absolutely cannot recommend version 2.5 for singing avatars or music-focused
  workflows... It would be a huge shame to give up on LTX 2.5 completely, though. The new 2.5
  version is actually excellent and highly usable for many other use cases, just not for music
  video clips with external audio." (Diagnosis of Gemma 4 as the cause is the user's own
  hypothesis, not confirmed by Lightricks.)
- **#44 "custom audio lipsync for ltx 2.5 just doesnt work"** (4 replies) — corroborating
  external-audio complaint.
- **#58 "LTX 2.5 doesn't work on Apple Silicon"**, **#32** (Chinese): a user reports the new
  version feels like a "negative improvement" in their tests.
- **#36 "Prompt Enhancement Produces Unrelated Generations in LTX-2.5 ComfyUI Workflow"** —
  matches the Reddit-side advice to turn the enhancer off.

### Feature/format requests (open demand signals)

- **#18 "We need gguf and gguf workflow"**, **#11 "Will Support such as Workflow, GGUF, FP8,
  NVFP4, MLX, int4&int8, coming soon?"**, **#52 "W4A8 Diffusion Model Request"** (6 replies),
  **#13 "Request: fp16 (not just bf16) full-precision transformer file"** (4 upvotes — "not
  everyone has a new GPU with bf16 support"), **#7 "Request: ltx2.5_text_projection_bf16"**
  (4 upvotes), **#49 "OneTrainer support"**, **#46 "Feature Request: True Reference Image
  Conditioning for LTX 2.5"**, **#27 "Possibility of A2V on the fast, distilled 2.5?"**.
- **#20 "Please tell the settings for full model not just distilled"** — documentation gap; the
  shipped ComfyUI templates target the distilled int8 checkpoint.

### Vendor responsiveness (verified)

- **#16 "LTX-2.5 distilled NVFP4 fails in ComfyUI"** (opened 2026-08-15 by `YieumYoon`, RTX
  5090 / ComfyUI 0.32.0 / PyTorch 2.13.0+cu130): `RuntimeError: mat1 and mat2 shapes cannot be
  multiplied (3520x4096 and 2048x4096)`. Two users confirmed. Lightricks org member `art-alex`
  replied within a day — "Thank you for reporting about this issue. We are on it!" — and then
  **"We fixed the issue. NVFP4 checkpoint should be working both in ComfyUI and in the LTX-2
  inference pipeline."** Thread closed 2026-08-17. Turnaround: roughly 2 days. In the interim a
  community member pointed users at a third-party conversion,
  `BennyDaBall/LTX-2.5-22b-distilled-nvfp4-comfy`.
- **#15** (see the VRAM file) drew a detailed technical explanation from `art-alex` about the
  new diffusion VAE decoder and tiling tradeoffs, plus a confirmation that **no official
  int8_convrot VAE checkpoint exists yet**: "We are exploring all the options to optimize the
  VAE with minimal quality loss."

### Net read

Sentiment is genuinely split rather than uniformly positive. Speed and low-VRAM accessibility
draw near-universal praise; **identity/character consistency in image-to-video and external-audio
lip-sync are the two consistent, independently-reported regressions versus LTX-2.3**, to the
point where multiple users recommend staying on 2.3 for those specific workflows.
