**Tab. 1. Training cost comparison (Qwen2.5-7B → 3B, 4×A100 80GB).** Hybrid adds negligible per-step cost over soft KD. The 9.7× gap comes entirely from on-policy autoregressive student sampling.

| Method | Extra computation | s/step |
|--------|------------------|--------|
| Soft KD | none | 14.06 |
| Hybrid KD | 1 log-sum-exp per token | 15.24 |
| On-policy KD | autoregressive student sampling | 147.83 |

---

**Tab. 2. Regularization/temperature baselines: Qwen2.5-7B → 3B (general reasoning).** Entropy reg., T: high→low, and T: low→high all improve over pure soft KD. Random-label mixing performs worst because random tokens (unlike teacher-sampled tokens) fail to reduce EB at Bridge positions.

| Method | BBH | MMLU | ARC-C | ThmQA | Avg |
|--------|-----|------|-------|-------|-----|
| Soft KD | 41.65 | 64.45 | 78.33 | 23.02 | 51.86 |
| +Entropy reg. | 46.58 | 67.04 | 80.49 | 23.80 | 54.48 |
| T: high→low | 45.22 | 66.10 | 80.12 | 23.77 | 53.80 |
| T: low→high | 46.41 | 66.51 | 80.56 | 23.30 | 54.20 |
| Random-label mixing | 40.10 | 61.24 | 74.23 | 20.27 | 48.96 |
| **Hybrid KD (ours)** | **46.54** | **69.05** | **81.23** | **23.82** | **55.16** |

---

**Tab. 3. Regularization/temperature baselines: Qwen2.5-Math-7B → 1.5B (math).**

| Method | GSM8K | MATH | Gaokao23 | Avg |
|--------|-------|------|----------|-----|
| Soft KD | [TBD] | [TBD] | [TBD] | [TBD] |
| +Entropy reg. | [TBD] | [TBD] | [TBD] | [TBD] |
| T: high→low | [TBD] | [TBD] | [TBD] | [TBD] |
| T: low→high | [TBD] | [TBD] | [TBD] | [TBD] |
| Random-label mixing | [TBD] | [TBD] | [TBD] | [TBD] |
| **Hybrid KD (ours)** | **[TBD]** | **[TBD]** | **[TBD]** | **[TBD]** |

---

**Tab. 4. Regularization/temperature baselines: Qwen2.5-Coder-7B → 1.5B (code).**

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Soft KD | 54.3 | 50.6 | 60.6 | 52.4 | 54.5 |
| +Entropy reg. | 53.0 | 48.2 | 63.5 | 55.3 | 55.0 |
| T: high→low | 53.0 | 47.6 | 60.3 | 52.6 | 53.4 |
| T: low→high | 50.0 | 45.7 | 59.3 | 51.9 | 51.7 |
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
| T: low→high | 39.7 | 34.7 | 61.9 | 49.4 | 46.4 |
| Random-label mixing | 35.4 | 32.3 | 57.4 | 47.6 | 43.2 |
| **Hybrid KD (ours)** | **41.5** | **36.6** | **63.2** | **50.5** | **48.0** |
