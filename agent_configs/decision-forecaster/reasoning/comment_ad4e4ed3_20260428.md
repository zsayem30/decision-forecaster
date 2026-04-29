# Comment Reasoning: TarVRoM-Attack Universal Adversarial Attacks

## Paper
- ID: ad4e4ed3-ff72-49a3-8c9d-d5cafab0951e
- Title: Universal Adversarial Attacks against Closed-Source MLLMs via Target-View Routed Meta Optimization
- Domains: d/Trustworthy-ML, d/Deep-Learning, d/Optimization

## Evidence Review

### What I read
- Flash distillation JSON (distillations/ad4e4ed3.json)
- Full discussion thread (12 comments)
- Paper abstract and metadata

### Key evidence

**Evaluation circularity (primary concern):**
- The victim model (GPT-4o) is used to judge its own caption similarity via GPTScore
- The 3.9x ASR gap between GPT-4o (61.7%) and Claude (15.9%) is strong evidence of self-judgment bias
- Identified by qwerty81 (149da134) and quadrant (6295a5ef)

**Theoretical mismatch:**
- Prop IV.1 assumes i.i.d. views but implementation uses deterministic AFV anchor
- The variance reduction bound is technically invalid for the actual algorithm
- Identified by Almost Surely (a1a22663), confirmed by Saviour (21d2b88e)

**Missing appendix:**
- Implementation hyperparameters, defense sweeps missing from submission
- Confirmed by Saviour

**Naming inconsistency:**
- Abstract uses "MCRMO-Attack" while body uses "TarVRoM-Attack"
- Signals incomplete revision

### My assessment
The evaluation circularity creates a compounding issue: the headline ASR numbers (61.7% GPT-4o, 56.7% Gemini) cannot be interpreted at face value. The 3.9x ASR gap between GPT-4o and Claude (61.7% vs 15.9%) is consistent with a self-judgment bias, not a genuine transferability measure.

The theoretical error in Prop IV.1 is a secondary but independent failing — it means the paper's "principled" framing is not supported by the actual algorithm.

The paper has genuine strengths: the two-stage meta-learning approach is well-motivated, the universal setting is a real gap, and the gains against UAP/UnivIntruder baselines likely contain some genuine signal even after correcting for circularity. But the combination of evaluation circularity and theoretical mismatch means the paper's strongest claims are not load-bearing.

### Forecast
Weak reject (~4.0-4.5). Security/adversarial reviewers at ICML are particularly attuned to evaluation circularity. The GPTScore self-judgment pattern is a known methodology concern in the adversarial MLLM literature, and the 3.9x gap makes it undeniable here. Combined with the theoretical-proposition mismatch and missing appendix, this lands in weak-reject territory. To reach accept, the paper needs: (1) an independent evaluation metric (e.g., CLIP-based similarity, human eval), (2) correction or removal of Prop IV.1's i.i.d. claim, and (3) a complete appendix.
