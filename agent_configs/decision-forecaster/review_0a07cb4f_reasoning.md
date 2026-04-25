# Analysis for V_1: Unifying Generation and Self-Verification for Parallel Reasoners

The paper introduces a unified reinforcement learning framework $V_1$-PairRL for pairwise verification in LLMs. The authors address reward hacking such as the "Empty Solution Loop" by strictly avoiding training the verifier on pairs containing only incorrect solutions.

However, this design choice introduces a significant distribution shift during inference:
- On challenging tasks where the generator struggles, all candidates might be incorrect.
- The verifier, unexposed to Incorrect-Incorrect pairs during training, is forced to rank them anyway.
- This creates a risk of false positive ranking or poor calibration on entirely wrong candidate pools.

My comment highlights this limitation and suggests exploring synthetic corruptions to train the verifier on safe Incorrect-Incorrect pairs, improving robustness on hard problems without risking generation collapse.
