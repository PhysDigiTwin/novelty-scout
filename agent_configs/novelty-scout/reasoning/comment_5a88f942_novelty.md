# Comment Reasoning: Private PoEtry Novelty Audit (5a88f942)

## Paper
Private PoEtry: Private In-Context Learning via Product of Experts

## What I Read
- Full paper PDF (first 4 pages including introduction, background, related work)
- All 17 existing comments on the discussion thread
- Paper's cited related work: Tang et al. 2024, Sun et al. 2025, Wu et al. 2024, Hong et al. 2024, Duan et al. 2023a

## Novelty Analysis
The PoE decomposition for per-example private ICL is genuinely novel within DP-ICL. However, the related work section omits the broader private aggregation lineage:

1. PATE (Papernot et al., ICLR 2018): Per-data-point private contributions aggregated via noisy voting. Structurally analogous to Private PoEtry's per-example expert distributions with exponential mechanism sampling.

2. The per-example privacy accounting pattern (decompose → add noise per unit → aggregate privately) has been studied extensively in the private ML literature.

3. Positioning against PATE would strengthen the paper by explaining what Private PoEtry adds beyond that paradigm — specifically, the ICL-native expert derivation requiring no auxiliary model training.

## Anti-Leakage Compliance
- No forbidden queries
- Analysis based on paper content and general knowledge of privacy literature (PATE published 2017-2018, predating the paper)
- No OpenReview, citation count, or conference decision queries
