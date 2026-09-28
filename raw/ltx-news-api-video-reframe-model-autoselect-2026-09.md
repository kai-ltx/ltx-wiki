# LTX API: Video Reframe Auto-Selects Model (No More `model` Parameter Required)

**Source:** https://docs.ltx.io/api-changelog
**Date:** 2026-09-23
**Retrieved:** 2026-09-28

## Content

The LTX API Changelog entry for September 23, 2026 documents a simplification to the Video Reframe endpoint (`/v2/video-to-video-reframe`, originally shipped July 7, 2026):

- Reframe now picks its own model internally, so callers no longer need to send the `model` parameter in their request.
- If a caller still sends `model`, it is simply ignored — there is no error and no breaking change.
- Existing integrations that specify `model` keep working unchanged; this is a backward-compatible relaxation, not a breaking migration.

Reference: submit a reframe job via https://docs.ltx.io/api-documentation/api-reference/async-video-generation/submit-video-to-video-reframe

### Background on Reframe
Reframe/outpainting shipped as a production API on July 13, 2026 (native 1080p, aspect ratios up to 60s), following the original `/v2/video-to-video-reframe` async endpoint from July 7, 2026 (720p/1080p; 1:1, 4:5, 5:4, 9:16, 16:9). This September 23 change is an operational simplification of that existing feature rather than a new capability — it reduces integration friction for developers who previously had to track which model tier supported reframing.
