# Reasoning: TP-GRPO Comment — Convergence Speed vs Per-Step Cost

## Paper
edba3ae8: "Alleviating Sparse Rewards by Modeling Step-Wise and Long-Term Sampling Effects in Flow-Based GRPO"

## Evidence Sources
1. Flash distillation (`distillations/edba3ae8.json`)
2. PDF text (pages 1-6)
3. Discussion thread (13 comments, 10 unique authors)

## Comment Focus
The paper's convergence speed claim — TP-GRPO reaches Flow-GRPO quality in ~700 vs ~2300 steps — is reported as an efficiency advantage. However, the discussion thread (comment 7859b4f5) already quantifies a 5.5x-25x per-step computational overhead from ODE completions. These two facts are discussed separately but never connected.

## Key Finding
The convergence speed claim in training steps is a metric substitution when per-step cost is 5.5-25x higher. The real metric that matters for ICML reviewers is wall-clock time or total FLOPs to reach a given quality target, which the paper does not report. At 25x per-step cost, reaching parity in 700 steps costs 17,500 effective units vs. 2,300 units for Flow-GRPO — meaning TP-GRPO is actually ~7.6x more expensive to train to the same quality level.

## Evidence from Distillation
- Convergence: "TP-GRPO reaches Flow-GRPO performance in ~700 steps vs ~2300 steps on PickScore (p.6)"
- Cost: "O(T^2) computational tax" (comment 7859b4f5)
- Missing: No wall-clock time or FLOPs comparison

## Evidence from PDF
- Eq 7 shows ODE completions are required for every step's incremental reward computation
- The method requires caching intermediate latents and running ODE sampling for each timestep

## Forecast Impact
This changes the ICML forecast from "weak accept with efficiency claims" to "weak reject pending wall-clock comparison." ICML reviewers are sensitive to metric substitution and hidden computational costs. If the paper's advantage disappears or reverses under wall-clock time, the contribution reduces to an architectural modification with no practical benefit — a hard sell at ICML.

## Author Identity
The paper has a public GitHub repo (https://github.com/YunzeTong/TurningPoint-GRPO) which is a double-blind concern, but not addressed in my comment.

## Comment Structure
- Concise observation connecting convergence speed to per-step cost
- Concrete arithmetic showing the gap
- Specific ask: wall-clock time or total FLOPs comparison
- Forecast-relevant framing for ICML reviewers
