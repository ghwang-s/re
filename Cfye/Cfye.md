**Tab. 1. Synthetic experiment results across 3 domains.** Sequences synthesized in Code, Math, Dialogue (~120–180 token vocabulary, 512 train + 128 test each), with ground-truth Bridge/Garden annotations and κ computed via path sampling. **Hard KD achieves lower Bridge EB in all 3 domains; Soft KD achieves lower Garden EB in all 3 domains; Hybrid achieves lowest overall EB.**

**EB decomposition** (lower = less error accumulation):

| Domain | Hard Bridge EB | Soft Bridge EB | Hard Garden EB | Soft Garden EB |
|--------|---------------|----------------|----------------|----------------|
| Code | 0.003 | 0.009 | 0.533 | **0.108** |
| Math | 0.019 | 0.067 | 0.116 | **0.086** |
| Dialogue | 0.004 | 0.215 | 0.186 | **0.056** |

**κ-confidence correlation and overall EB:**

| Domain | κ-conf. r | Overall EB (Hard) | Overall EB (Soft) | Overall EB (Hybrid) |
|--------|-----------|-------------------|-------------------|---------------------|
| Code | **0.91** | 0.095 | 0.085 | **0.047** |
| Math | **0.70** | 0.068 | 0.081 | **0.049** |
| Dialogue | **0.80** | 0.032 | 0.070 | **0.001** |

**Synthetic experiment visualizations:** see [BfWQ/synthetic_figures/](../BfWQ/synthetic_figures/)

---

**Tab. 2. Training cost comparison (Qwen2.5-7B → 3B, 4×A100 80GB).** Hybrid adds negligible per-step cost over soft KD. The 9.7× gap comes entirely from on-policy autoregressive student sampling.

| Method | Extra computation | s/step |
|--------|------------------|--------|
| Soft KD | none | 14.06 |
| Hybrid KD | 1 log-sum-exp per token | 15.24 |
| On-policy KD | autoregressive student sampling | 147.83 |
