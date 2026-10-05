# ComfyUI Benchmark Templates Drop LTX-2.5 for HunyuanVideo Over Gating Friction

**Source:** https://github.com/Comfy-Org/workflow_templates/pull/1300
**Date:** 2026-09-30
**Retrieved:** 2026-10-05

## Content

PR #1300 in `Comfy-Org/workflow_templates` ("Replacing LTX 2.5 by Hunyuan Video because LTX 2.5 is gated"), opened and merged same-day by `alexisrolland` (reviewed/merged by `comfyui-wiki`) on **Sep 30, 2026**. The PR swaps the benchmark workflow file `benchmarks/video_ltx2_5_t2v.json` out in favor of `benchmarks/video_hunyuan_video_1.5_720p_t2v.json` inside Comfy-Org's shared benchmarks directory — the files ComfyUI uses to track/report generation performance across models.

The commit message gives the reason directly: **LTX-2.5 is a gated Hugging Face repository** (requires account + license acceptance + approval wait before weights download), which makes it unsuitable for automated/CI-style benchmarking pipelines that need to pull weights without a human in the loop. HunyuanVideo 1.5 (720p T2V) was substituted as the point of comparison instead.

This is a recurring friction point for LTX-2.5 specifically (unlike LTX-2.3 and earlier LTX-Video releases, which were ungated): several community tool maintainers have had to special-case LTX-2.5 to handle the HF gate (manual "request access" + approval latency), and this PR is a concrete instance of a maintainer choosing to route around the model entirely rather than carry that complexity in an automated benchmark harness.

## Context

This sits alongside previously logged LTX-2.5 community friction points (i2v identity-drift regressions, external-audio lip-sync issues, subtitle-like text artifacts per GitHub #319) as a distinct category of complaint: not quality, but **access friction** — gating makes LTX-2.5 harder to drop into automated pipelines than its predecessors or than ungated competitors like HunyuanVideo.
