**Tab. 1. 26 controlled synthetic settings where ground-truth κ can be computed exactly.** We generate length-48 sequences from a process with hidden state s. Every 3rd position is a Bridge: the token is a deterministic function of s, emitted with prob p ∈ {0.75–0.95} (rest on 2 neighbors), and it updates s, so a single Bridge error derails all downstream Bridges (high κ). All other positions are Gardens: drawn uniformly from ~V/5 candidates without changing s, so errors stay local (low κ). κ is computed by exhaustive enumeration over state transitions. Teacher: 128-dim, 4-layer, 4-head Transformer (192-dim, 5-layer for V ≥ 300), trained 25 epochs (AdamW, lr 3e-4). Student: 2-head Transformer, pre-trained 10 epochs (lr 5e-4) on the same data, then distilled (lr 2e-4). We vary student dim d ∈ {32–72}, depth L ∈ {1, 2}, vocab V ∈ {100–1000}, peak p. Soft KD = forward KL(teacher ‖ student); Hard KD = CE on teacher-sampled hard labels; Hybrid = λ·soft + (1−λ)·hard, λ* from {0.1, 0.3, 0.5, 0.7, 0.9}, KD epochs swept over {1, 2, 3, 5}. Per-position EB = KL on student-generated sequences minus KL on training data. κ corr. = Pearson |r| between teacher confidence and ground-truth κ (0.83–0.99). **In all 26 settings: hard KD achieves lower EB at Bridges, soft KD achieves lower EB at Gardens, hybrid outperforms both.**

| # | Setting | κ corr. | Bridge EB (hard KD) | Bridge EB (soft KD) | Garden EB (hard KD) | Garden EB (soft KD) | Overall EB (hybrid) | λ* |
|---|---------|---------|-------------|-------------|-------------|-------------|--------|-----|
| 1 | d=36, L=1, V=200, seq=32, p=.90 | .992 | .0161 | .0179 | .0035 | .0021 | **.0085** | 0.3 |
| 2 | d=48, L=1, V=200, seq=32, p=.90 | .989 | .0139 | .0140 | .0041 | .0031 | **.0011** | 0.5 |
| 3 | d=52, L=1, V=200, seq=32, p=.90 | .993 | .0056 | .0071 | −.0015 | −.0021 | **.0000** | 0.7 |
| 4 | d=72, L=1, V=200, p=.75 | .956 | .0060 | .0068 | .0030 | .0025 | **.0007** | 0.5 |
| 5 | d=72, L=1, V=200, p=.85 | .947 | .0091 | .0096 | .0002 | .0001 | **−.0020** | 0.7 |
| 6 | d=64, L=1, V=100, p=.90 | .953 | .0093 | .0095 | −.0013 | −.0015 | **.0013** | 0.5 |
| 7 | d=52, L=1, V=100, p=.90 | .829 | .0219 | .0223 | .0011 | −.0001 | **.0079** | 0.9 |
| 8 | d=32, L=2, V=200, p=.85 | .887 | .0778 | .0781 | .0324 | .0281 | **.0302** | 0.5 |
| 9 | d=48, L=2, V=200, p=.85 | .989 | .0195 | .0220 | .0001 | −.0003 | **.0038** | 0.9 |
| 10 | d=48, L=2, V=200, p=.90 | .994 | .0098 | .0124 | −.0024 | −.0030 | **.0009** | 0.5 |
| 11 | d=72, L=1, V=200, p=.90 | .980 | .0042 | .0057 | −.0002 | −.0002 | **.0005** | 0.7 |
| 12 | d=52, L=1, V=200, p=.95 | .979 | .0212 | .0213 | .0074 | .0030 | **.0068** | 0.5 |
| 13 | d=36, L=2, V=300, p=.90 | .982 | .0324 | .0345 | .0342 | .0277 | **.0284** | 0.3 |
| 14 | d=48, L=2, V=300, p=.90 | .988 | .0096 | .0143 | .0077 | .0074 | **.0028** | 0.7 |
| 15 | d=64, L=2, V=300, p=.90 | .987 | .0061 | .0070 | −.0019 | −.0020 | **−.0017** | 0.1 |
| 16 | d=36, L=1, V=500, p=.90 | .974 | .0649 | .0671 | .0630 | .0480 | **.0348** | 0.7 |
| 17 | d=48, L=1, V=500, p=.90 | .986 | .0313 | .0321 | .0132 | .0105 | **.0109** | 0.9 |
| 18 | d=52, L=1, V=500, p=.90 | .980 | .0169 | .0202 | .0060 | .0054 | **.0050** | 0.9 |
| 19 | d=48, L=1, V=500, p=.95 | .987 | .0496 | .0561 | .0295 | .0290 | **.0183** | 0.1 |
| 20 | d=64, L=1, V=500, p=.95 | .969 | .0130 | .0139 | .0021 | .0009 | **−.0032** | 0.7 |
| 21 | d=64, L=2, V=500, p=.90 | .984 | .0060 | .0077 | .0014 | .0010 | **−.0026** | 0.7 |
| 22 | d=72, L=2, V=500, p=.90 | .986 | .0109 | .0117 | .0004 | −.0011 | **−.0004** | 0.7 |
| 23 | d=64, L=1, V=1000, p=.90 | .982 | .0287 | .0308 | .0154 | .0126 | **.0137** | 0.9 |
| 24 | d=48, L=1, V=1000, p=.95 | .975 | .0818 | .0838 | .0802 | .0738 | **.0462** | 0.5 |
| 25 | d=64, L=1, V=1000, p=.95 | .992 | .0439 | .0469 | .0448 | .0418 | **.0198** | 0.9 |
| 26 | d=72, L=1, V=1000, p=.95 | .962 | .0147 | .0192 | .0008 | .0006 | **−.0045** | 0.9 |

---

**Synthetic experiment visualizations (5 figures):** see [synthetic_figures/](synthetic_figures/)

---

**Tab. 2. New pair: Qwen2.5-32B → 3B (general reasoning).**

| Method | BBH | MMLU | ARC-C | ThmQA | Avg |
|--------|-----|------|-------|-------|-----|
| Hard KD | 34.35 | 67.18 | 79.45 | 23.05 | 51.01 |
| Soft KD | 43.97 | 65.56 | 78.07 | 22.85 | 52.61 |
| **Hybrid KD** | **45.73** | **66.82** | **80.02** | **23.98** | **54.14** |

---

**Tab. 3. New pair: Qwen2.5-Coder-7B → 1.5B (code).**

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Hard KD | 54.3 | 50.0 | 60.3 | 52.1 | 54.2 |
| Soft KD | 52.7 | 47.9 | 59.6 | 52.4 | 53.1 |
| **Hybrid KD** | **55.5** | **50.6** | **61.4** | **52.6** | **55.0** |

---

**Tab. 4. On-policy + hybrid KD: Qwen2.5-Coder-7B → 1.5B.** Combining on-policy with hybrid yields further gains over on-policy alone.

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Off-policy soft KD | 52.7 | 47.9 | 59.6 | 52.4 | 53.1 |
| Off-policy hybrid KD | 55.5 | 50.6 | 61.4 | 52.6 | 55.0 |
| On-policy soft KD | 56.4 | 51.5 | 61.4 | 53.2 | 55.6 |
| **On-policy + hybrid KD** | **56.8** | **52.9** | **61.1** | **52.9** | **55.9** |

---

**Tab. 5. On-policy + hybrid KD: Llama3.1-8B → 1B.**

| Method | BBH | MMLU | ARC-C | ThmQA | Avg |
|--------|-----|------|-------|-------|-----|
| Off-policy soft KD | 22.07 | 33.13 | 33.41 | 4.37 | 23.25 |
| Off-policy hybrid KD | 27.44 | 35.64 | 37.01 | 5.00 | 26.27 |
| On-policy soft KD | 26.84 | 36.15 | 39.73 | 6.95 | 27.42 |
| **On-policy + hybrid KD** | **26.86** | **36.39** | **40.22** | **6.90** | **27.59** |

---

**Tab. 6. On-policy + hybrid KD: DeepSeek-Coder-6.7B → 1.3B.**

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Off-policy soft KD | 38.4 | 33.5 | 63.5 | 51.6 | 46.8 |
| Off-policy hybrid KD | 41.5 | 36.6 | 63.2 | 50.5 | 48.0 |
| On-policy soft KD | 43.3 | 39.0 | 63.8 | 52.1 | 49.5 |
| **On-policy + hybrid KD** | **44.2** | **39.8** | **64.4** | **52.5** | **50.2** |

---

**Tab. 7. Regularization/temperature baselines: Qwen2.5-7B → 3B (general reasoning).** Entropy reg., T: high→low, and T: low→high all improve over pure soft KD. Random-label mixing performs worst because random tokens fail to reduce EB at Bridge positions.

| Method | BBH | MMLU | ARC-C | ThmQA | Avg |
|--------|-----|------|-------|-------|-----|
| Soft KD | 41.65 | 64.45 | 78.33 | 23.02 | 51.86 |
| +Entropy reg. | 46.58 | 67.04 | 80.49 | 23.80 | 54.48 |
| T: high→low | 45.22 | 66.10 | 80.12 | 23.77 | 53.80 |
| T: low→high | 46.41 | 66.51 | 80.56 | 23.30 | 54.20 |
| Random-label mixing | 40.10 | 61.24 | 74.23 | 20.27 | 48.96 |
| **Hybrid KD (ours)** | **46.54** | **69.05** | **81.23** | **23.82** | **55.16** |

---

**Tab. 8. Regularization/temperature baselines: Qwen2.5-Coder-7B → 1.5B (code).**

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Soft KD | 52.7 | 47.9 | 59.6 | 52.4 | 53.1 |
| +Entropy reg. | 53.0 | 48.2 | 63.5 | 55.3 | 55.0 |
| T: high→low | 53.0 | 47.6 | 60.3 | 52.6 | 53.4 |
| T: low→high | 54.0 | 48.7 | 60.9 | 51.9 | 53.9 |
| Random-label mixing | 51.8 | 48.2 | 60.6 | 53.2 | 53.5 |
| **Hybrid KD (ours)** | **55.5** | **50.6** | **61.4** | **52.6** | **55.0** |

---

**Tab. 9. Regularization/temperature baselines: Llama3.1-8B → 1B (general reasoning).**

| Method | BBH | MMLU | ARC-C | ThmQA | Avg |
|--------|-----|------|-------|-------|-----|
| Soft KD | 22.07 | 33.13 | 33.41 | 4.37 | 23.25 |
| +Entropy reg. | 24.52 | 35.73 | 34.88 | 5.96 | 25.27 |
| T: high→low | 26.02 | 35.08 | 34.74 | 5.78 | 25.41 |
| T: low→high | 25.68 | 35.38 | 34.78 | 4.97 | 25.20 |
| Random-label mixing | 19.17 | 30.10 | 30.23 | 2.13 | 20.41 |
| **Hybrid KD (ours)** | **27.44** | **35.64** | **37.01** | **5.00** | **26.27** |

---

**Tab. 10. Regularization/temperature baselines: DeepSeek-Coder-6.7B → 1.3B (code).**

| Method | HE | HE+ | MBPP | MBPP+ | Avg |
|--------|-----|------|------|-------|-----|
| Soft KD | 38.4 | 33.5 | 63.5 | 51.6 | 46.8 |
| +Entropy reg. | 41.5 | 36.6 | 61.6 | 50.0 | 47.4 |
| T: high→low | 40.1 | 35.4 | 62.7 | 49.9 | 47.0 |
| T: low→high | 39.7 | 34.7 | 62.9 | 50.3 | 46.9 |
| Random-label mixing | 35.4 | 32.3 | 57.4 | 47.6 | 43.2 |
| **Hybrid KD (ours)** | **41.5** | **36.6** | **63.2** | **50.5** | **48.0** |

---

**Tab. 11. AlpacaEval (GPT-5.2 judge, win rate against text-davinci-003).**

| Setting | Hard KD | Soft KD | Hybrid KD |
|---------|---------|---------|-----------|
| Qwen2.5-7B → 3B | 57.5 | 61.3 | **64.4** |
