# Novelty Audit: DecompressionLM (74b119eb)

## Paper Summary
DecompressionLM proposes a stateless framework for zero-shot concept graph extraction using Van der Corput low-discrepancy sequences with arithmetic decoding. Key claims: deterministic, embarrassingly parallel concept extraction without pre-specified queries; AWQ-4bit expands concept coverage 30-170% while GPTQ-Int4 causes 71-86% collapse; concept coverage as a complementary evaluation dimension beyond perplexity.

## Prior-Work Scout Results

The prior-work scout identified three relevant works not cited by the paper:

### 1. "Through a Compressed Lens: Investigating The Impact of Quantization on Factual Knowledge Recall" (2024, arXiv)
- Uses LRE (Linear Relation Extraction) dataset to evaluate factual knowledge recall under quantization
- Finds quantization disrupts "knowledge neurons" causing forgetting of specific facts
- **Relevance**: Directly establishes that quantization degrades factual knowledge — the core phenomenon DecompressionLM measures via concept coverage. DecompressionLM provides a behavioral diagnostic for the same underlying phenomenon.

### 2. "From Signal Degradation to Computation Collapse: Uncovering the Two Failure Modes of LLM Quantization" (2024, arXiv)
- Uses Layer-wise Knowledge Probing with Logit Lens to investigate quantization failure modes
- Shows knowledge signals remain decodable at 4-bit but collapse at lower precisions
- **Relevance**: Shares the goal of diagnosing quantization failure modes but via internal (Logit Lens) rather than behavioral (sampling-based) methods. DecompressionLM's behavioral approach is complementary but the paper doesn't acknowledge this prior internal-probing work.

### 3. "Discovering Latent Knowledge in Language Models Without Supervision" (Burns et al., 2023, ICLR)
- CCS (Contrast-Consistent Search) is a landmark unsupervised method that finds truth directions in model latent space
- Extracts knowledge without labeled data or pre-specified per-concept queries
- **Relevance**: The paper claims to be the first framework for knowledge extraction "without pre-specified queries." CCS achieves a similar high-level goal (unsupervised knowledge discovery) via a fundamentally different approach (latent directions vs. output sampling). The paper should engage with CCS and clarify what "zero-shot" and "without pre-specified queries" means in relation to this established method.

## Novelty Assessment

The core methodological contribution — Van der Corput sequences with arithmetic decoding for stateless parallel sampling — is genuinely novel and well-motivated. The three identified decoding limitations (cross-sequence coupling, competitive decoding suppressing long-tail, sequential scalability) are real problems.

However, the paper's novelty framing overclaims in two ways:

1. **The quantization finding extends rather than discovers**: "Through a Compressed Lens" (2024) already established that quantization degrades factual knowledge recall and disrupts knowledge neurons. DecompressionLM's AWQ-4bit expansion finding is a valuable *refinement* of this picture (showing some quantization methods preserve/expand coverage) but doesn't establish a new phenomenon. The paper should cite and distinguish from this prior work.

2. **The "zero-shot" / "without pre-specified queries" framing needs qualification against CCS**: CCS (Burns et al., 2023) already demonstrated that knowledge can be extracted from LLMs without per-concept queries in an unsupervised setting. DecompressionLM's approach is methodologically distinct (output sampling vs. latent directions) but the paper's framing as the first to bypass pre-specified queries is misleading without engaging with CCS.

3. **The "From Signal Degradation to Computation Collapse" omission**: This 2024 work investigates the same quantization failure modes via internal Logit Lens probing. DecompressionLM's behavioral diagnostic complements this but the paper neither cites nor distinguishes from it.

## Verdict

The paper makes a genuine methodological contribution (VdC sampling for stateless parallel concept extraction) but the novelty framing inflates the contribution relative to prior work on quantization-knowledge probing and unsupervised knowledge elicitation. The missing citations — particularly CCS (ICLR 2023) and "Through a Compressed Lens" (2024) — are not minor omissions: they are directly relevant prior work that would change how a reader interprets the paper's novelty claims.
