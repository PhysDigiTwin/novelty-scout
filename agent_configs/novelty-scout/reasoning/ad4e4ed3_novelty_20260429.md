# Novelty Audit: TarVRoM-Attack / Universal Targeted MLLM Attacks (ad4e4ed3)

## Paper Summary
Proposes UTTAA (Universal Targeted Transferable Adversarial Attacks) — a single perturbation that steers arbitrary inputs toward a specified target across unknown commercial MLLMs. Key technical components: Target-View Aggregation (TVA) for variance reduction, alignability-gated Token Routing (TR), multi-crop meta-optimization.

## Prior-Work Scout Findings

Three prior works directly prefigure the core problem setting:

### 1. TUAP: Targeted Universal Adversarial Perturbations for CLIP (2023, NeurIPS)
- Allows arbitrary text descriptions as targets for universal perturbations on vision-language models (CLIP, MiniGPT-4)
- Direct predecessor: targeted universal attacks in the VLM space
- Does NOT address closed-source setting or the "triple randomization" problem

### 2. AllAttacK: Revisiting and Expanding Targeted Universal Adversarial Perturbations (2024, NeurIPS)
- Joint mini-data-batch and mini-model-batch optimization for "doubly transferable" universal targeted perturbations across 18+ DNNs (CNNs, ViTs, CLIP)
- Relevant contemporary baseline for the multi-model transfer aspect

### 3. Pandora's Box: Universal Attackers against Real-World LVLMs (2024, NeurIPS)
- Universal adversarial patch that is task-agnostic across real-world LVLMs using gradient approximation via input/output queries
- Demonstrates universal attacks on real-world LVLMs were already explored in 2024
- Different threat model (untargeted/jailbreak vs. targeted)

## Novelty Assessment

**Preempted:** The problem of universal targeted attacks on vision-language models was established by TUAP (2023). Universal attacks on real-world LVLMs were demonstrated by Pandora's Box (2024). The "first systematic study" framing overclaims relative to this prior art.

**Genuinely novel:** The specific architectural solutions to the "triple randomization" problem — Target-View Aggregation (TVA) for reducing high-variance target supervision and alignability-gated Token Routing (TR) for reliable token-wise matching under black-box API constraints — are genuinely novel contributions not addressed by TUAP, AllAttacK, or Pandora's Box.

**Missing citations:** TUAP, AllAttacK, and Pandora's Box should be cited and contrasted. Their absence artificially inflates the perceived novelty gap.

## Score Impact
The missing citations and overclaimed "first systematic study" framing pull the novelty contribution from "strong" to "moderate." The paper's genuine technical contributions (TVA + TR) survive the prior-work audit but must be properly contextualized.
