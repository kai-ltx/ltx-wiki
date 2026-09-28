# Community: Recurring Text/Subtitle Artifacts Reported in LTX-2.5 (GitHub Issue #319)

**Source:** https://github.com/Lightricks/LTX-2/issues/319
**Date:** 2026-09-23
**Retrieved:** 2026-09-28

## Content

GitHub user "The Code Learner" opened issue #319 on the official Lightricks/LTX-2 repository on September 23, 2026, titled "LTX-2.5 still produces unwanted text artifacts — is subtitle-heavy training data the cause?"

Key points from the report:
- LTX-2.5 frequently produces unwanted on-screen text/caption-like artifacts even when no text, captions, subtitles, titles, or overlays are requested in the prompt.
- The reporter frames this as "generation-breaking" — artifacts can ruin otherwise high-quality generations.
- The reporter hypothesizes the root cause is subtitle-heavy or caption-burned video in the training data, and asks whether Lightricks filters or masks such contamination during dataset preparation.
- The issue explicitly contrasts this with LTX-2.5's otherwise "major progress," framing the artifact issue as surprising given the model's overall quality level.
- As of retrieval, no official Lightricks response was recorded in the thread.

## Why this matters for the wiki
This is a distinct, named failure mode from the previously logged (2026-08-24 ingest) LTX-2.5 regressions — i2v identity consistency (HF #30, #14, #38) and external-audio lip-sync (#57, #44) — and from the diffusion-VAE-decoder gray-tile/crash family (GitHub #277, #288). Text/caption artifacts had not previously been logged as a distinct, actively-discussed community complaint. It adds to a growing pattern of community-reported quality regressions specific to LTX-2.5 relative to LTX-2.3, even as raw speed and local-VRAM feedback remains positive.
