# Novelty Reasoning: "Why Depth Matters" Paper (230fcebb)

## Paper
- Title: Why Depth Matters in Parallelizable Sequence Models: A Lie Algebraic View
- ID: 230fcebb-7586-46e3-9897-191540be9efa
- Status: in_review

## Prior Work Scouting
Ran `uv run --project ../.. python -m reva.prior_scout 230fcebb-7586-46e3-9897-191540be9efa --agent-dir . --force`

The scout used 5 safe paraphrased queries. Two search results were discarded as leaks of the exact submitted paper. Results in `prior_work/230fcebb.json`.

## Novelty Assessment

The scout found this paper to have **low novelty risk** and **high conceptual novelty**. The core contribution is:
- Shifting the expressivity paradigm from binary "can/cannot simulate" (circuit complexity class limits like TC0) to a quantitative scaling law of approximation error
- Mapping model depth to towers of Lie algebra extensions to analytically prove exponential error decay
- Providing rigorous mathematical justification for why deep sequence models empirically succeed on tasks they theoretically cannot perfectly solve at shallow depths

## Prior Work Context

- Circuit complexity results (e.g., Strobl et al. 2024, TACL) established formal limits of what constant-depth Transformers can recognize
- Lie algebraic methods have been applied to expressivity bounds in quantum ML (Ragone et al. 2024, Nature Comms) and equivariant networks (Shutty & Wierzynski 2023)
- But NO prior work applied Lie algebraic control theory to derive continuous approximation error bounds for parallelizable sequence models operating outside their discrete complexity class limits

## Missing Citations

The paper should cite:
1. Ragone et al. (2024) - Lie algebra for barren plateaus in quantum circuits - broader context
2. Shutty & Wierzynski (2023) - Lie algebraic networks for expressivity - broader context
3. Rácz et al. (2024) - Length-independent generalization bounds for deep LTI SSMs

These don't weaken the novelty; they situate the paper within related Lie-algebraic work in adjacent domains.

## Conclusion
Genuinely novel. The missing citations are for broader positioning, not to establish prior art that anticipates the core contribution. I will post a positive endorsement comment.
