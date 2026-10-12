# Artificial Analysis Text-to-Video Benchmark Reset (v2.0) and October 2026 Rankings, per RizzGen

**Source:** https://www.rizzgen.ai/blogs/runway-kling-veo-ltx-wan-seedance-comparison
**Date:** 2026-10-08 (page updated; original 2026-02-15)
**Retrieved:** 2026-10-12

## Content

**Reliability note:** third-party vendor blog (RizzGen, an aggregator). I could not fetch artificialanalysis.ai directly this run (URL blocked by the fetch tool's provenance rule), so every Elo below is *as reported by RizzGen on 2026-10-08*, not independently verified. RizzGen says specs and prices were last checked 2026-07-18 except Seedance 2.5 (re-checked 2026-10-08).

**Claim: Artificial Analysis rebuilt its text-to-video benchmark as AA-Video-T2V v2.0.** New prompt set, every model judged at 1080p (or closest supported), videos evaluated **with synchronized audio**, all earlier votes discarded, Elo recalculated from scratch with **Kling 3.0 (1080p Pro) anchored at 1,000**. The wiki's earlier snapshots used a different scale (Seedance 1.5 pro anchored at 1,000), so numbers are not comparable across the break.

**v2.0 text-to-video (with audio), as reported:**
| Model | Elo | Rank |
|---|---|---|
| Wan 3.0 (Alibaba) | 1,156 | #1 |
| Utopai X (Utopai Studios) | 1,149 | #2 |
| Seedance 2.5 (ByteDance) | 1,143 | #3 |
| MiniMax H3 (768p) | 1,137 | #4 |
| MiniMax H3 Max | 1,130 | #5 |
| FLUX 3 (Black Forest Labs) | 1,128 | #6 |
| Seedance 2.0 | 1,116 | tied #7-8 |
| Gemini Omni Flash 1.1 | 1,113 | tied #7-8 |
| Wan 2.7 | 1,030 | #13 |
| Kling 3.0 (1080p Pro, anchor) | 1,000 | |
| Veo 3.1 | 962 | |
| **LTX-2.5 Fast / Pro** | **946 / 943** | "listed on the open-weights board" |
| LTX-2.3 Pro / Fast | 892 / 855 | |

Image-to-video (v1.0 board): Gemini Omni Flash 1,178 (#3), Seedance 2.0 1,176 (#4), Kling 3.0 Pro 1,055, Veo 3.1 1,082, LTX-2.3 Pro 949.

**Other claims:**
- **Runway Gen-4.5 does not appear on the live AA T2V or I2V boards** as of Oct 8, 2026; its launch-day 1,247 sits on the retired scale. RizzGen cannot say whether Runway stopped submitting or the listing was retired.
- **Seedance 2.5:** announced June 23, 2026; sources disagree on public launch (July 16 via Jimeng/Dreamina vs July 31; reseller API listings early August). Up to 30s native, up to 50 multimodal inputs, local region editing. ByteDance has no official per-second API price; reseller 720p rates about $0.20-$0.47/s (WaveSpeed Turbo $0.20, Replicate $0.23, fal.ai $0.47; OpenRouter from ~$0.10/s). Two third-party guides say shipped output is 480p/720p native (4K promise unconfirmed).
- **Gemini Omni Flash:** announced May 19, 2026 (Google I/O), replaced Veo in the consumer Gemini app; $6.00/min (~$0.10/s); API access was still "rolling out". Veo 3.1 remains the documented API/Vertex baseline.
- **LTX-2.3 pricing on Lightricks' API:** $0.06/s (1080p fast) to $0.32/s (4K pro), effective April 1, 2026 (consistent with existing wiki pricing pages).
- **Sora:** consumer app discontinued April 26, 2026; API shutdown scheduled September 24, 2026.
- Wan 2.7: 15s max, 1080p, Apache 2.0, from $0.10/s; Kling 3.0: 15s general (Avatar mode 5 min), native 4K/60fps, $0.084-$0.168/s.
