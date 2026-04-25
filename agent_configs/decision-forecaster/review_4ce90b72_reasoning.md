# Reasoning: Delta-Crosscoder: Robust Crosscoder Model Diffing in Narrow Fine-Tuning Regimes

## Summary of Analysis
The paper addresses a significant challenge in mechanistic interpretability: identifying sparse, localized representation shifts in LLMs that have undergone narrow fine-tuning. Traditional crosscoders often fail here because shared features dominate the joint reconstruction objective, causing fine-tuning-specific features to be suppressed or ignored.

### Key Strengths
1. **Mechanistic Innovation:** The combination of **dual-K sparsity** (explicitly allocating capacity for shared vs. task-specific latents) and the **delta-based loss** is a well-motivated response to the "structural failure" of joint reconstruction in narrow regimes.
2. **Task-Agnostic Recovery:** The use of contrastive pairs from a general corpus (creating information asymmetry through dual-timestep scheduling) allows the model to recover fine-tuning shifts without requiring access to the original fine-tuning data. This is a major practical advantage for safety auditing.
3. **Empirical Rigor:** The evaluation across 10 distinct "model organisms" (including emergent misalignment and synthetic false facts) across multiple model families (Gemma, LLaMA, Qwen) provides strong evidence of robustness.
4. **Reliability Check:** The "null test" on identical models (Section 7.1) demonstrating that the method does not fabricate differences where none exist is a critical sanity check that is often missing in interpretability research.

### Points for Discussion
- **Hyperparameter Sensitivity:** The delta loss weight ($\Delta\lambda$) and the ratio of shared vs. non-shared latents are key hyperparameters. While Appendix A mentions a choice of 0.005, more analysis on the sensitivity of the recovered features to these values would be valuable.
- **Comparison to Interactive Methods:** While matching the performance of Activation Difference Lens (ADL) is impressive given that Delta-Crosscoder is static, there's a trade-off between the depth of discovery in interactive methods vs. the efficiency of the crosscoder approach.

## Conclusion
Delta-Crosscoder represents a solid step forward for model diffing, particularly for safety-relevant fine-tuning where behavioral changes are "localized and asymmetric." My forecast leans toward a **strong accept** given the technical novelty and thorough validation.
