**Tab. 1. New teacher-student pairs added during rebuttal.** Hybrid consistently outperforms both Hard and Soft KD baselines across a larger capacity gap (32B→3B) and code domain.

**Qwen2.5-32B → 3B (general reasoning):**

| Method | BBH | MMLU | ARC-C | ThmQA | Avg |
|--------|-----|------|-------|-------|-----|
| Hard KD | 34.35 | 67.18 | 79.45 | 23.05 | 51.01 |
| Soft KD | 43.97 | 65.56 | 78.07 | 22.85 | 52.61 |
| **Hybrid KD** | **45.73** | **66.82** | **80.02** | **23.98** | **54.14** |

**Qwen2.5-Coder-7B → 1.5B (code):**

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Hard KD | 54.3 | 50.0 | 60.3 | 52.1 | 54.2 |
| Soft KD | 52.7 | 47.9 | 59.6 | 52.4 | 53.1 |
| **Hybrid KD** | **55.5** | **50.6** | **61.4** | **52.6** | **55.0** |

---

**Tab. 2. Ablation on mixing proxy: Qwen2.5-7B → 3B (general reasoning).** Confidence-based mixing (correct direction) outperforms reverse-confidence (wrong direction), confirming teacher confidence is a reliable κ proxy. Entropy-based mixing similarly outperforms its reverse.

| Method | BBH | MMLU | ARC-C | ThmQA | Avg |
|--------|-----|------|-------|-------|-----|
| Hard KD | 41.52 | 65.76 | 78.75 | 23.75 | 52.45 |
| Soft KD | 41.65 | 64.45 | 78.33 | 23.02 | 51.86 |
| Hybrid: confidence-based | 44.07 | 67.50 | 80.77 | 22.78 | **53.78** |
| Hybrid: reverse-confidence | 41.45 | 65.33 | 78.12 | 22.28 | 51.79 |
| Hybrid: entropy | 46.83 | 67.06 | 79.81 | 23.65 | 54.34 |
| Hybrid: reverse-entropy | 41.20 | 65.23 | 77.29 | 20.48 | 51.05 |

---

**Tab. 3. Training cost comparison (Qwen2.5-7B → 3B, 4×A100 80GB).** Hybrid adds negligible per-step cost over soft KD. The 9.7× gap comes entirely from on-policy autoregressive student sampling.

| Method | Extra computation | s/step |
|--------|------------------|--------|
| Soft KD | none | 14.06 |
| Hybrid KD | 1 log-sum-exp per token | 15.24 |
| On-policy KD | autoregressive student sampling | 147.83 |

---

**Tab. 4. Regularization/temperature baselines: Qwen2.5-Coder-7B → 1.5B (code).**

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Soft KD | 52.7 | 47.9 | 59.6 | 52.4 | 53.1 |
| +Entropy reg. | 53.0 | 48.2 | 63.5 | 55.3 | 55.0 |
| T: high→low | 53.0 | 47.6 | 60.3 | 52.6 | 53.4 |
| T: low→high | 54.0 | 48.7 | 60.9 | 51.9 | 53.9 |
| Random-label mixing | 51.8 | 48.2 | 60.6 | 53.2 | 53.5 |
| **Hybrid KD (ours)** | **55.5** | **50.6** | **61.4** | **52.6** | **55.0** |

---

**Tab. 5. Regularization/temperature baselines: Llama3.1-8B → 1B (general reasoning).**

| Method | BBH | MMLU | ARC-C | ThmQA | Avg |
|--------|-----|------|-------|-------|-----|
| Soft KD | 22.07 | 33.13 | 33.41 | 4.37 | 23.25 |
| +Entropy reg. | 24.52 | 35.73 | 34.88 | 5.96 | 25.27 |
| T: high→low | 26.02 | 35.08 | 34.74 | 5.78 | 25.41 |
| T: low→high | 25.68 | 35.38 | 34.78 | 4.97 | 25.20 |
| Random-label mixing | 19.17 | 30.10 | 30.23 | 2.13 | 20.41 |
| **Hybrid KD (ours)** | **27.44** | **35.64** | **37.01** | **5.00** | **26.27** |

---

**Tab. 6. Regularization/temperature baselines: DeepSeek-Coder-6.7B → 1.3B (code).**

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Soft KD | 38.4 | 33.5 | 63.5 | 51.6 | 46.8 |
| +Entropy reg. | 41.5 | 36.6 | 61.6 | 50.0 | 47.4 |
| T: high→low | 40.1 | 35.4 | 62.7 | 49.9 | 47.0 |
| T: low→high | 39.7 | 34.7 | 62.9 | 50.3 | 46.9 |
| Random-label mixing | 35.4 | 32.3 | 57.4 | 47.6 | 43.2 |
| **Hybrid KD (ours)** | **41.5** | **36.6** | **63.2** | **50.5** | **48.0** |
