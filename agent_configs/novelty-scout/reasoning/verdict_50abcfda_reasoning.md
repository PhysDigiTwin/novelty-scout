# Verdict Reasoning: LoRDS (50abcfda) — Weak Accept (5.0)

## Paper Summary

"Breaking the Blocks: Continuous Low-Rank Decomposed Scaling for Unified LLM Quantization and Adaptation" proposes LoRDS: decompose block-wise quantization scaling matrices into low-rank factors (S=BA via SVD) to unify PTQ, QAT, and PEFT under a single linear framework. Claims include: strictly superior expressive power vs. block-wise scaling, unified lifecycle, high-rank multiplicative PEFT with zero inference overhead, and up to 27% accuracy improvement at 3-bit.

## Prior Work Overlap Assessment

The prior-work scout identified four prior works that preempt individual components:

1. **LRQ** (Lee et al., NAACL 2025): Low-rank weight-scaling for PTQ — the most conceptually similar work. LoRDS differentiates via linear SVD initialization vs. exponential mapping, and unified lifecycle vs. PTQ-only. The paper honestly acknowledges this.

2. **QA-LoRA** (Xu et al., ICLR 2024): Already achieves zero-inference-overhead quantized PEFT by integrating LoRA into quantized zero-points. Challenges the uniqueness of the zero-overhead claim.

3. **LoQA / HQ-LoRA**: Fine-tune quantization parameters directly for adaptation — multiplicative adaptation paradigm already explored.

4. **HiRA** (Huang et al., ICLR 2025): Pioneered high-rank adaptation via Hadamard transform — the high-rank PEFT benefit claim is preempted.

5. **LQER / SERQ**: Use SVD on quantization error for reconstruction — low-rank decomposition for quantization explored from another angle.

## Genuine Novelty

1. **Unified lifecycle under a single linear formulation (S=BA)**: No prior work unifies PTQ, QAT, and PEFT under the same low-rank scaling representation. This is elegant and practically valuable.

2. **SVD-based initialization from block-wise statistics**: The linear formulation enables direct initialization that exactly recovers block-wise scaling, then refines. LRQ's exponential mapping precludes this.

3. **Multiplicative PEFT with full-rank weight updates**: Empirically validated (Fig 3) that multiplicative scaling naturally unfolds updates across a full-rank space, unlike additive LoRA.

## Critical Limitations

1. **Missing multiplicative PEFT baselines**: The PEFT experiments (Table 5) compare against only QLoRA and LoftQ — both additive methods. The paper claims multiplicative PEFT, zero-overhead, and high-rank updates as advantages, but does not experimentally compare against QA-LoRA, HiRA, or LoQA. The 4.19% gain over LoftQ cannot be attributed to any specific claimed mechanism.

2. **Incremental individual components**: Each component (low-rank scaling, zero-overhead PEFT, multiplicative adaptation, high-rank updates) was explored in prior work. The contribution is synthesis, not discovery.

3. **No head-to-head against LRQ in PTQ experiments**: While the paper discusses LRQ in Related Work, the PTQ experiments (Table 1) do not include an LRQ baseline. The comparison would strengthen the claim that linear formulation matters.

## Score Justification

**5.0 — Weak Accept**

The paper is well-engineered with strong empirical results and clean methodology. The unification concept (S=BA serving PTQ, QAT, and PEFT) is genuinely elegant and practically useful. The SVD initialization provides a real algorithmic advantage over LRQ's scratch reconstruction.

However: (a) each individual component is preempted by prior work (LRQ, QA-LoRA, LoQA/HQ-LoRA, HiRA), (b) the missing multiplicative PEFT baselines prevent a full assessment of the PEFT contribution, and (c) the novelty is synthesis/unification, not a new principle or discovery.

Acceptance is warranted with the expectation that: (1) multiplicative PEFT baselines (QA-LoRA, HiRA) are added to Table 5, and (2) novelty claims are properly scoped to unification rather than individual components. Without these additions, the paper falls to weak reject (4.5).
