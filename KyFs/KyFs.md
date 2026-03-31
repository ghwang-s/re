**Tab. 1. On-policy + hybrid KD: Qwen2.5-Coder-7B → 1.5B.** Off-policy hybrid already outperforms off-policy soft KD. Combining with on-policy yields further gains.

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Off-policy soft KD | 54.3 | 50.6 | 60.6 | 52.4 | 54.5 |
| Off-policy hybrid KD | 55.5 | 50.6 | 61.4 | 52.6 | 55.0 |
| On-policy soft KD | 56.4 | 51.5 | 61.4 | 53.2 | 55.6 |
| **On-policy + hybrid KD** | **56.8** | **52.9** | **61.1** | **52.9** | **55.9** |

---

**Tab. 2. On-policy + hybrid KD: Llama3.1-8B → 1B.**

| Method | BBH | MMLU | ARC-C | ThmQA | Avg |
|--------|-----|------|-------|-------|-----|
| Off-policy soft KD | 22.07 | 33.13 | 33.41 | 4.37 | 23.25 |
| Off-policy hybrid KD | 27.44 | 35.64 | 37.01 | 5.00 | 26.27 |
| On-policy soft KD | 26.84 | 36.15 | 39.73 | 6.95 | 27.42 |
| **On-policy + hybrid KD** | **26.86** | **36.39** | **40.22** | **6.90** | **27.59** |

---

**Tab. 3. On-policy + hybrid KD: DeepSeek-Coder-6.7B → 1.3B.**

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Off-policy soft KD | 38.4 | 33.5 | 63.5 | 51.6 | 46.8 |
| Off-policy hybrid KD | 41.5 | 36.6 | 63.2 | 50.5 | 48.0 |
| On-policy soft KD | 43.3 | 39.0 | 63.8 | 52.1 | 49.5 |
| **On-policy + hybrid KD** | **44.2** | **39.8** | **64.4** | **52.5** | **50.2** |

---

**Tab. 4. New pair: Qwen2.5-32B → 3B (general reasoning).** Added during rebuttal to test larger capacity gap (10×).

| Method | BBH | MMLU | ARC-C | ThmQA | Avg |
|--------|-----|------|-------|-------|-----|
| Hard KD | 34.35 | 67.18 | 79.45 | 23.05 | 51.01 |
| Soft KD | 43.97 | 65.56 | 78.07 | 22.85 | 52.61 |
| **Hybrid KD** | **45.73** | **66.82** | **80.02** | **23.98** | **54.14** |

---

**Tab. 5. New pair: Qwen2.5-Coder-7B → 1.5B (code).** Added during rebuttal to test code generation domain.

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Hard KD | 54.3 | 50.0 | 60.3 | 52.1 | 54.2 |
| Soft KD | 54.3 | 50.6 | 60.6 | 52.4 | 54.5 |
| **Hybrid KD** | **55.5** | **50.6** | **61.4** | **52.6** | **55.0** |

---

**Tab. 6. Training cost comparison (Qwen2.5-7B → 3B, 4×A100 80GB).** Hybrid adds negligible per-step cost over soft KD.

| Method | Extra computation | s/step |
|--------|------------------|--------|
| Soft KD | none | 14.06 |
| Hybrid KD | 1 log-sum-exp per token | 15.24 |
| On-policy KD | autoregressive student sampling | 147.83 |
