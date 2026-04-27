# Novelty Assessment: Quantized Evolution Strategies (d211dfcb)

## Paper Summary
Introduces QES — an optimization paradigm for fine-tuning quantized LLMs without backpropagation. Combines accumulated error feedback (inspired by Delta-Sigma modulation) with stateless seed replay to achieve high-precision learning dynamics at inference-level memory cost.

## Prior Work Scout Results

The grounded prior-work scout (Gemini) surfaced:
- **Salimans et al. (2017)**: Established seed replay as an ES technique for bypassing perturbation storage
- **MeZO (Malladi et al., 2024)**: ZO optimization for LLMs in continuous parameter space
- **QuZO (Zhou et al., 2025)**: Direct ZO baseline for quantized LLMs
- **QLoRA (Dettmers et al., 2023)**: Standard PEFT baseline for quantized models
- **QEFT (ACL 2024)**: Mixed-precision PEFT for quantized fine-tuning
- **QFT (2024)**: Full-parameter quantized tuning with integer-stored gradients
- **PEQA (NeurIPS 2023), QA-LoRA (ICLR 2024)**: Alternative QAT methods not discussed

Novelty risks: Low — the Delta-Sigma + ES bridge is genuinely novel. 

## Key Novelty Findings

### 1. Seed Replay Overclaim
The paper lists "Stateless Seed Replay" as its second primary contribution. However, seed replay is an established technique in ES literature (Salimans et al., 2017). The paper itself acknowledges this foundation in Section 3.2. The novelty is in the *specific application*: using seed replay to reconstruct the *accumulated error feedback buffer* rather than just perturbation vectors. The paper should frame seed replay as an enabling technique, not a standalone contribution.

### 2. Missing Prior Work Positioning
The related work section (2.1) discusses QLoRA and LLM-QAT but omits PEQA (NeurIPS 2023), QA-LoRA (ICLR 2024), and QEFT (ACL 2024) — all of which address quantized fine-tuning through different paradigms (parameter-efficient, mixed-precision). For an ICML submission claiming to "democratize fine-tuning," these are relevant comparison points.

### 3. Delta-Sigma + ZO Bridge Is Genuinely Novel
The mathematical formulation connecting Delta-Sigma modulation to ZO discrete optimization (Section 5, temporal equivalence proof) is elegant and original. The prior work scout confirms no prior work bridges these concepts in the quantized LLM fine-tuning context.

### 4. "Democratization" Claim Overreaches
The paper claims QES "democratizes fine tuning" and "opens up the possibility for scaling up LLMs entirely in the quantized space." These claims are supported by a single task (Countdown arithmetic reasoning) on two model sizes (1.5B, 3B). No evidence on standard NLG, instruction-following, or code generation tasks.

## Verdict Implication
The core technical contribution (accumulated error feedback for ZO discrete optimization) is genuinely novel and well-executed theoretically. However, the paper overclaims on two fronts: (1) treating seed replay as a standalone innovation, and (2) claiming broad democratization from narrow empirical evidence. These overclaims pull the accept ceiling down.

**Novelty-informed score range: 4.5–5.5** (weak accept at best, contingent on empirical expansion and repositioning of seed replay claim).
