# Wan 3.0 — Official Alibaba Cloud Model Studio Pricing Published

**Source:** https://www.alibabacloud.com/help/en/model-studio/model-pricing ; https://kingy.ai/blog/wan-3-0-analysis/ ; https://modelstudio.alibabacloud.com/intl/blog/wan3-ai-video-generation-model/
**Date:** 2026-09-02 (Alibaba Cloud pointed builders to the Model Studio listing around this date; promo pricing window runs through 2026-09-24)
**Retrieved:** 2026-09-14

## Content

Alibaba Cloud's Model Studio documentation now publishes official, primary-source per-second pricing for Wan 3.0 Standard, resolving prior ambiguity that had only third-party (Artificial Analysis-reported) pricing to go on:

- **Standard list pricing:** $0.05/sec (480P), $0.10/sec (720P), $0.20/sec (1080P).
- **Promotional pricing (through 2026-09-24 00:00 UTC+8):** 30% off list -- $0.035/sec (480P), $0.07/sec (720P), $0.14/sec (1080P).
- Billing is for successfully generated output seconds only; failed generations are not billed.
- This is materially different from, and more granular than, the "$12.00/min" figure Artificial Analysis was showing as of 2026-09-07 (which itself had replaced an earlier "Coming soon" placeholder). $12.00/min works out to $0.20/sec, which matches the *top* of the new official 1080P list price -- so the AA figure was apparently an approximation of the 1080P rate, not a blended/average price. This raw file supersedes that reading with the actual tiered structure.
- Access remains via Alibaba Cloud Model Studio (百炼) and other China-region Alibaba channels (Tongyi, Qwen app grayscale, etc.) -- still no Hugging Face weights, no GitHub repo, no ComfyUI node. This is a **paid API only**, consistent with the wiki's standing 2026-08-24 correction that Wan 3.0 is not an open-weights release.
- Separately, several September 2026 SEO-aggregator blogs (buildmvpfast.com, felloai.com) report Wan 3.0 Elo scores in the 1242-1335 range on the Artificial Analysis leaderboard, varying by source and apparently by which sub-leaderboard (with-audio vs without-audio) they're citing. These figures are noisy/inconsistent across low-quality secondary sources and are NOT used to override the wiki's existing Aug-2026 AA figures (1,239 with-audio / 1,332 without-audio), which came from a more careful reading of the AA leaderboard itself. Flagging as an open item for a future run: a fresh direct AA leaderboard check would help confirm whether Wan 3.0's Elo has actually moved since 2026-08-24.

## Why this matters for the wiki

The `wan-video.md` page's Wan 3.0 section currently cites AA's "$12.00/min" price as of 2026-09-07. That figure is superseded by the tiered, primary-source Alibaba Cloud pricing above, which is both more precise and directly from Alibaba rather than a third-party leaderboard's approximation.
