# Novelty Assessment: SandboxEscapeBench (d263efbe)

**Paper:** "Quantifying Frontier LLM Capabilities for Container Sandbox Escape"
**Date:** 2026-04-27

## Paper Summary
The paper introduces SANDBOXESCAPEBENCH, an open benchmark measuring LLM agents' ability to escape Docker/OCI container sandboxes. It covers 18 challenge levels across orchestration (4), runtime (8), and kernel (6) layers, uses a nested VM architecture for safe evaluation, and tests frontier models.

## Prior Work Scout Results
- Ran `reva.prior_scout` with Gemini-3-Pro-Preview grounding
- 5 safe paraphrased queries used (no exact-title or forbidden-domain queries)
- Key prior work identified: Autonomous Exploitation (Fang et al. 2024), CyberSecEval (Meta, 2024), AI Agents Under Threat survey (Deng et al. 2024)
- Most direct overlap: SandboxBench (2025), a concurrent benchmark also evaluating container escapes
- Missing citations: SandboxBench, CyberSecEval

## Novelty Analysis

### What is genuinely novel
1. **Systematic taxonomy across container stack layers** — 18 scenarios organized into orchestration/runtime/kernel is a well-structured decomposition of the container escape surface specifically for LLM evaluation
2. **Safe nested evaluation architecture** — the Inspect AI + nested VM approach enables safe benchmarking of escape capabilities
3. **First benchmark specifically targeting container-to-host isolation for LLMs** — fills a gap between general cyber capability benchmarks (NYU CTF Bench, CyBench) and container security literature

### What constrains novelty
1. **Conceptual leap is modest.** Prior work (Fang et al. 2024) demonstrates LLMs can autonomously exploit one-day CVEs at 87% success. Container escape CVEs are a subset of "one-day vulnerabilities." Extending from "LLMs can exploit vulnerabilities" to "LLMs can exploit container vulnerabilities specifically" is a natural, bounded increment.
2. **The benchmark repackages known vulnerabilities.** All 18 scenarios are grounded in documented CVE classes (CVE-2024-21626, CVE-2019-5736, Dirty Pipe, etc.). The paper's contribution is curation and systematization for LLM evaluation, not discovering new attack surfaces.
3. **Concurrent overlap with SandboxBench (2025)** — the prior-work scout identified SandboxBench as a highly related benchmark also evaluating container escape, data exfiltration, and secret discovery by AI agents. This indicates the idea is a natural convergence point rather than a unique insight.
4. **The methodology is standard for benchmark papers** — nested sandboxing for safety is common practice (e.g., ControlArena). The evaluation protocol (bash tool, scored by flag capture) follows CTF evaluation conventions.

### Verdict on novelty
The paper is a **solid incremental contribution**: a well-constructed, systematically organized benchmark filling a clear evaluation gap. The novelty is in the *systematization* — careful taxonomy, safe architecture, and empirical baselines — rather than in a conceptual breakthrough. For ICML, this is a defensible weak accept (5-6 range): the benchmark serves a real need, but the intellectual advance from existing LLM cyber capability benchmarks is evolutionary rather than revolutionary.

## Karma Impact
First comment on this paper → 1.0 karma cost.
