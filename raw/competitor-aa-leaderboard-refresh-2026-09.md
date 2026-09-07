# Artificial Analysis Video Leaderboard Refresh (September 2026)

**Source:** https://artificialanalysis.ai/video/leaderboard/text-to-video
**Date:** 2026-09 (leaderboard snapshot, continuously updated; page notes these were "added in the last month")
**Retrieved:** 2026-09-07

## Content

The Artificial Analysis Text-to-Video (With Audio) leaderboard shows several changes since the 2026-08-24 wiki snapshot:

**New entrants (added within the last month per the page's own banner):**
- **Minimax H3 Max (post-trained by fal)** — Fal-hosted, fal-post-trained variant of MiniMax H3. Debuts at **#3, Elo 1235** (-10/+10, 5,451 samples), released Aug 2026, $2.40/min. This is a *new, separate leaderboard entry* from the base "MiniMax H3" (Elo 1227, #4, $7.80/min, Jul 2026, Hugging Face open weights) — the fal post-training appears to meaningfully improve blind-vote preference while cutting API cost roughly 3x versus the vendor-hosted version.
- **Agnes-Video-2.5** (Sapiens AI) — new version, debuts at **#19, Elo 1080** (-9/+9, 5,860 samples), released Aug 2026, **$1.50/min** — notably the cheapest model in the top 20. Supersedes the previously-tracked Agnes-Video-V2.0 (Elo ~916-920, unranked in top 30 now), a large jump in both quality and leaderboard position for the Sapiens AI line.
- **Vidu Q3 Turbo** — Elo 1028 (#25-26 tie with Wan 2.6), Feb 2026, $3.90/min.

**Wan 3.0 pricing now published:** AA's leaderboard lists Wan 3.0 API pricing as **$12.00/min** — resolving the "Coming soon" placeholder noted in the wiki's 2026-08-24 correction entry. Wan 3.0 still carries **no Hugging Face open-weights badge** on AA, consistent with the wiki's standing read that Wan 3.0 is a closed public beta / paid API, not an open-weights release. Wan 3.0 remains **#1** on both the with-audio (Elo 1239) and without-audio (Elo 1332) text-to-video boards.

**LTX-2.5 position:** LTX-2.5 Fast and LTX-2.5 Pro are essentially unchanged in Elo (1062 and 1061 respectively, vs 1063/1063 on 2026-08-24) but have slipped in *rank* from #19-20 to **#22 and #24** purely because of the three new entrants above pushing into the mid-table — not because of any score regression. LTX-2.5 Fast is confirmed as the **#2 open-weights model** on the with-audio board (behind MiniMax H3, ahead of MAGI-2 Preview), and LTX-2.5 Fast/Pro are **#2/#3 open-weights** on the without-audio board behind MiniMax H3.

**Without-audio board leaders unchanged:** Wan 3.0 (1332), Gemini Omni Flash (1324), MiniMax H3 (1302), HappyHorse-1.0 (1282), Dreamina Seedance 2.0 720p (1267) — same top 5 as before, no reordering.

## Assessment

This is a minor/incremental update, not a new model release cycle. The one genuinely new fact worth recording is the Wan 3.0 pricing confirmation ($12/min) plus the emergence of "post-trained by fal" as a distinct, cheaper, higher-scoring leaderboard entry for MiniMax H3 — a pattern (third-party post-training beating the vendor's own hosted checkpoint on blind preference) worth watching for LTX post-training opportunities too.
