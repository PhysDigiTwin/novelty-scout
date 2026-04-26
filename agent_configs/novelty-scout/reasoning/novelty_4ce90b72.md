# Novelty Assessment: Delta-Crosscoder (4ce90b72)

## Paper
"Delta-Crosscoder: Robust Crosscoder Model Diffing in Narrow Fine-Tuning Regimes"

## Prior Work Scout
- Model: gemini-3-pro-preview
- Search confidence: High (0.95)
- Overlap assessment: Shares core crosscoder architecture, BatchTopK sparsity mechanism, and shared/unshared latent partitioning with existing work. The main divergence is the explicit delta-based loss term combined with contrastive paired data.
- Novelty risks: High. Given that BatchTopK and latent partitioning were already proposed to address crosscoder limitations, the novelty heavily depends on the delta-based loss and contrastive data formulation.

## Key Prior Work Cited by the Paper
1. **Lindsey et al. (2024)** - Core crosscoder architecture.
2. **Bussmann et al. (2024)** - BatchTopK sparsity mechanism to fix crosscoder optimization biases.
3. **Mishra-Sharma et al. (2024)** & **Jiralerspong & Bricken (2025)** - Shared and non-shared latent partitioning.
4. **Minder et al. (2025b)** - Activation Difference Lens (ADL) demonstrating that narrow fine-tuning leaves explicitly readable traces in activation differences.
5. **Wang et al. (2025a)** - Emergent misalignment captured via explicit activation differences.

## Paper's Novelty Claim
The paper claims novelty through the combination of Dual-K sparsity, shared feature masking, a delta-based auxiliary loss $L_\Delta$, and contrastive text pairs. It claims this combination enables crosscoders to isolate fine-tuning-specific features in narrow regimes where standard methods fail.

## Novelty Audit Conclusion
The paper's core architectural elements (Dual-K sparsity, shared feature masking) are directly adopted from prior work (Mishra-Sharma et al., Jiralerspong & Bricken). The BatchTopK mechanism is also borrowed (Bussmann et al.). The use of activation differences to track fine-tuning changes is established by Minder et al. and Wang et al. 

The genuine, albeit thin, novel contribution is the specific formulation of the delta-based auxiliary loss $L_\Delta$ combined with contrastive paired data to train a crosscoder. However, this is an incremental combination of known techniques rather than a fundamental breakthrough in model diffing. Furthermore, the delta-loss formulation appears to have an optimization bias toward high-amplitude directions, potentially missing distributed shifts, which limits the robustness claim. While empirically effective on the selected model organisms, the conceptual novelty is significantly overstated in the paper's framing.
