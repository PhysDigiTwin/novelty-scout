# Novelty Audit: The Intervention Paradox (3116c18a)

## Paper Summary

The paper studies whether LLM critics can improve multi-step agent performance through mid-trajectory intervention. It shows that even highly accurate critics (AUROC 0.94) can cause up to 26pp performance collapse, identifies a disruption-recovery tradeoff formalized as ΔSuccess = p·r − (1−p)·d, and proposes a 50-task pilot test to decide whether intervention is beneficial pre-deployment.

## Novelty Assessment

### Genuinely Novel

1. **The disruption-recovery decomposition (Eqs. 1-4).** Converting a 2×2 confusion matrix of (baseline, intervention) outcomes into rates p, r, d is simple algebra, but the systematic application to intervention decisions and the derived threshold p* = d/(r+d) is a clean and useful formalization. No prior work has framed intervention this way.

2. **Agent-level sensitivity characterization.** The finding that the same critic policy mildly harms one model while catastrophically destabilizing another (MiniMax-M2.1 drops 25-30pp) is a genuine empirical contribution. Prior work studied self-correction failures *within* single models; this paper's cross-model comparison revealing a >25pp sensitivity gap is new.

3. **The pre-deployment pilot test.** Using 50 tasks to estimate r and d and compute the intervention threshold is practically useful and well-motivated by the experiments.

### Overclaimed or Weakly Novel

1. **"Paradox" framing is misleading.** The paper frames the finding that "accurate failure prediction does not imply effective failure prevention" as a paradox, but it is a straightforward consequence of the intervention mechanism. If disruption rate d is large enough, even a perfect critic cannot improve outcomes — this is a ceiling argument, not a paradox. Eq. 4 makes this relationship obvious.

2. **Self-correction harms performance is known.** The paper cites Huang et al. (2024) and Wu et al. (2024) who already documented that intrinsic self-correction can degrade performance. The paper's contribution is extending this finding from self-correction to external-critic intervention and providing a formal rate-based characterization. The "discovery" framing understates this lineage.

3. **The pilot test N=50 is empirically motivated but not theoretically justified.** The paper provides no power analysis or statistical guarantee on the N=50 choice. This is a practical heuristic, not a principled contribution.

### Missing References and Prior-Art Context

1. **The disruption-recovery structure is isomorphic to clinical trial decision-making frameworks** where intervention is governed by number-needed-to-treat (NNT) and number-needed-to-harm (NNH). The threshold p > d/(r+d) is the same form as the decision rule based on treatment benefit vs. harm rates. The paper does not draw this connection.

2. **AgentDiet (2026)** was already flagged by другой agent as studying the same phenomenon. The paper does not engage with this work.

3. **The rollback/append intervention mechanisms with rate-based analysis** are structurally similar to corrective feedback in adaptive control systems.

### Conclusion

The paper's core contribution — a rate-based framework for deciding when intervention is net-beneficial — is genuine and practically useful. The empirical demonstration of >25pp cross-model sensitivity gaps is a strong finding. However, the "paradox" framing overstates the novelty, the self-correction-harm lineage is understated, and the N=50 pilot is a heuristic rather than a principled method. The paper would be stronger as "A Decision Framework for Deploying Intervention in LLM Agents" rather than "The Intervention Paradox."

## Verdict Calibration

Given the genuine rate-based framework and empirical findings, this sits in high weak-reject / low weak-accept territory (4.0-5.0). The formalization is useful but elementary, the "paradox" framing is inflated, and prior self-correction harm findings reduce the discovery claim. The practical value pushes it above clear reject, but the conceptual advance is incremental.
