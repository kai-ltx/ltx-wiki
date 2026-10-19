# LTX Diffusers and LoRA Third-Party Mirrors: Supply-Chain Flags

**Source:** https://huggingface.co/Lightricks/LTX-2.5-Diffusers ; https://huggingface.co/Lightricks/LTX-2.3/blob/main/LICENSE ; https://huggingface.co/Resgard/LTX-Video/tree/main ; https://huggingface.co/Hussi/LTX-2/discussions ; https://huggingface.co/liltyn/LTX-2.3/discussions ; https://huggingface.co/Muapi/ltx2.3/discussions
**Date:** Model cards current as of retrieval (2026-10); mirror pages undated
**Retrieved:** 2026-10-19

## Content

Search results for LTX Diffusers usage surfaced several non-Lightricks Hugging Face repos alongside official cards. Security-relevant observations (review, not advisory findings):

- **Official card:** Lightricks/LTX-2.5-Diffusers loads via DiffusionPipeline in bfloat16 on CUDA. Access is gated (contact-info share required). Commercial use allowed under the LTX-2.x Community License. Transferring fine-tunes may require a paid license.
- **Unofficial mirrors:** Resgard/LTX-Video, Hussi/LTX-2, liltyn/LTX-2.3 are third-party copies, not Lightricks repos. Risk: CWE-494 (download of code without integrity check). Mitigation: load only from the Lightricks org, pin a commit with revision=, verify hashes.
- **Third-party LoRA:** Muapi example calls pipe.load_lora_weights("Muapi/ltx2.3") on a pipeline from another repo. Risk: CWE-502 if the weights are pickle-based. Mitigation: accept .safetensors only, review provenance.
- **Unpinned checkout:** Muapi page clones the LTX-2 repo and runs uv sync with no version pin. Mitigation: tagged release or commit, uv sync --frozen.
- **Remote image input:** Example fetches an image by URL. If exposed to user-supplied URLs in a service, risk is SSRF (CWE-918). Mitigation: host allowlist, block private and link-local ranges.

Not verified against a formal advisory. CWE classes are the analysis, not search-sourced findings.
