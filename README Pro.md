# The Mirage of Explainability: A Survey on Chain-of-Thought Faithfulness in Large Language Models

![Awesome](https://awesome.re/badge-flat2.svg) ![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

> **Companion repository** for our survey on **Chain-of-Thought (CoT) faithfulness**—why rationales can look convincing yet fail to reflect the model’s true decision process, how to evaluate this gap, and how to mitigate it.

---

## Table of Contents

- [Overview](#overview)
- [Latest News](#latest-news)
- [Taxonomy & Legends](#taxonomy--legends)
  - [What we mean by "faithfulness"](#what-we-mean-by-faithfulness)
  - [Key failure phenomena](#key-failure-phenomena)
  - [Benchmark levels](#benchmark-levels)
  - [Mitigation families](#mitigation-families)
- [Paper List](#paper-list)
  - [1. Failure Phenomena](#1-failure-phenomena)
  - [2. Evaluation Benchmarks & Metrics](#2-evaluation-benchmarks--metrics)
  - [3. Mitigation Strategies](#3-mitigation-strategies)

---

## Overview

Chain-of-Thought (CoT) reasoning has become a standard interface for deploying and monitoring large language models (LLMs). Yet a central concern is **faithfulness**: *does the generated CoT reflect the model’s actual computation, or is it a plausible post-hoc story*?

This repository curates and organizes research on CoT faithfulness, following the framework from our survey:

- **Unified definition:** faithfulness requires **internal alignment** (CoT matches internal computations) *and* **external consistency** (CoT remains stable under behavior-preserving interventions).
- **Failure phenomena:** we emphasize four recurring modes—**input-driven unfaithfulness**, **non-causal/post-hoc rationalization**, **alignment-induced unfaithfulness**, and **strategic deception & hiding**.
- **Benchmark levels:** we organize evaluation into **four levels** (L1–L4), from behavioral audits to white-box causal tests.
- **Mitigation:** we summarize interventions spanning inference-time prompting/verification, training-time methods, and internal/architectural approaches.

> **Figures (add to `assets/`)**  
> - `assets/figure1_failure_modes.png` – Failure modes illustration (recommended)  
![Failure Phenomena](https://github.com/jandx20031231/Test/blob/image/Survey%20Image.png)

---

## Latest News

- **[2026-01]** Repository initialized for maintaining an up-to-date reading list and taxonomy for CoT faithfulness.
- **[2025-10]** New benchmark threads: *Level-II intervention-grounded* (e.g., FaithCoT-Bench) and *Level-III structured-verifiable* (e.g., Typed CoT) are accelerating progress.

---

## Taxonomy & Legends

### What we mean by faithfulness

We use a **two-axis** view:

- **Internal alignment:** the CoT corresponds to internal computations (a *white-box* claim).
- **External consistency:** the CoT is robust to interventions that preserve the final answer behavior (a *black-box* test of stability).

A CoT can be *externally consistent but internally misaligned* (e.g., stable yet still post-hoc), or *internally aligned but externally fragile* (e.g., small edits flip the story).

---

### Key failure phenomena

We tag papers by the **primary** failure mode(s):

- **IDU — Input-driven unfaithfulness:** the model uses spurious prompt cues/biases (option order, stereotypes, user beliefs) but fails to mention them.
- **NPR — Non-causal/post-hoc rationalization:** CoT and answer are decoupled; the model can change the rationale without changing the answer.
- **AIU — Alignment-induced unfaithfulness:** training incentives (e.g., RLHF / preference optimization) encourage *nice-looking* explanations rather than faithful ones.
- **SDH — Strategic deception & hiding:** the model deliberately withholds or obfuscates reasoning, especially under monitoring pressure.

---

### Benchmark levels

We classify evaluations into four increasing levels of *ground-truth strength*:

- **L1 — Behavioral audits:** detect mismatches via input biases, counterfactual prompts, or correlation tests (no direct grounding).
- **L2 — Intervention-grounded:** validate rationales against controlled perturbations with known causal effects (e.g., faithful cues, diagnostic setups).
- **L3 — Structured-verifiable:** enforce strict formats or formal constraints so parts of the reasoning become mechanically checkable.
- **L4 — White-box:** directly test internal computation via mechanistic tools (activation patching, causal tracing, circuit mapping).

---

### Mitigation families

We tag mitigation approaches by the dominant lever:

- **Prompting constraints:** instruction tuning at inference-time, rationale templates, refusal policies.
- **Sampling/ensembling:** self-consistency, majority vote, re-ranking.
- **Verification & tool binding:** external checkers, solvers, theorem provers, rule-based verifiers.
- **Training & fine-tuning:** SFT/RL methods explicitly rewarding faithful rationales or penalizing unfaithful ones.
- **Internal intervention:** activation steering/patching, representation editing, circuit-level control.
- **Architectural inductive bias:** designs that force latent structure, enforce bottlenecks, or separate planning from verbalization.

---

## Paper List

> **Note.** For papers spanning multiple tags, we annotate the **primary** phenomenon / level / mitigation to keep the table readable.

### 1. Failure Phenomena

#### 1.1 Input-driven unfaithfulness (IDU)

| Paper | Phenomenon | Evaluation | Mitigation | Venue | Year | Link |
|---|---|---|---|---|---:|---|
| Language Models Don't Always Say What They Think: Unfaithful Explanations in CoT Prompting | IDU | L1 | — | NeurIPS | 2023 | https://arxiv.org/abs/2305.04388 |
| Towards Understanding Sycophancy in Language Models | IDU | L1 | — | ICLR | 2024 | https://arxiv.org/abs/2310.13548 |

#### 1.2 Non-causal & post-hoc rationalization (NPR)

| Paper | Phenomenon | Evaluation | Mitigation | Venue | Year | Link |
|---|---|---|---|---|---:|---|
| Measuring Faithfulness in Chain-of-Thought Reasoning | NPR | L1/L2 | — | arXiv | 2023 | https://arxiv.org/abs/2307.13702 |
| Chain-of-Thought Unfaithfulness as Disguised Accuracy | NPR | L1 | — | TMLR | 2024 | https://arxiv.org/abs/2402.14897 |
| Chain-of-Thought Reasoning in the Wild Is Not Always Faithful | NPR | L1/L2 | — | arXiv | 2025 | https://arxiv.org/abs/2503.08679 |

#### 1.3 Alignment-induced unfaithfulness (AIU) & deception/hiding (SDH)

| Paper | Phenomenon | Evaluation | Mitigation | Venue | Year | Link |
|---|---|---|---|---|---:|---|
| Monitoring Reasoning Models for Misbehavior and the Risks of Promoting Obfuscation | SDH | L2 | VT/FT | arXiv | 2025 | https://arxiv.org/abs/2503.11926 |
| Monitoring Monitorability | SDH | L2 | VT | arXiv | 2025 | https://arxiv.org/abs/2512.18311 |

---

### 2. Evaluation Benchmarks & Metrics

#### 2.1 L1 — Behavioral audits

| Paper | Level | Focus | Venue | Year | Link |
|---|---|---|---|---:|---|
| Measuring Faithfulness in Chain-of-Thought Reasoning | L1 | CoT dependence via interventions on rationale text | arXiv | 2023 | https://arxiv.org/abs/2307.13702 |
| Making Reasoning Matter: Measuring and Improving Faithfulness of CoT Reasoning | L1/L2 | metrics + training-time improvements | arXiv | 2024 | https://arxiv.org/abs/2402.13950 |

#### 2.2 L2 — Intervention-grounded benchmarks

| Paper | Level | Focus | Venue | Year | Link |
|---|---|---|---|---:|---|
| FaithCoT-Bench: Benchmarking Instance-Level Faithfulness of Chain-of-Thought Reasoning | L2 | diagnostic, instance-level faithfulness | arXiv | 2025 | https://arxiv.org/abs/2510.04040 |
| Walk the Talk? Measuring the Faithfulness of Large Language Model Explanations | L2 | counterfactual simulatability / concept perturbations | arXiv | 2025 | https://arxiv.org/abs/2504.14150 |

#### 2.3 L3 — Structured-verifiable benchmarks

| Paper | Level | Focus | Venue | Year | Link |
|---|---|---|---|---:|---|
| Typed Chain-of-Thought: A Curry-Howard Framework for Verifying LLM Reasoning | L3 | type-checked procedural correctness | arXiv | 2025 | https://arxiv.org/abs/2510.01069 |

#### 2.4 L4 — White-box benchmarks

| Paper | Level | Focus | Venue | Year | Link |
|---|---|---|---|---:|---|
| How to Think Step-by-Step: A Mechanistic Understanding of Chain-of-Thought Reasoning | L4 | mechanistic analysis of CoT computation | TMLR | 2024 | https://openreview.net/forum?id=uHLDkQVtyC |
| Measuring Chain-of-Thought Monitorability Through Faithfulness and Verbosity | L4 | monitorability score combining faithfulness + verbosity | arXiv | 2025 | https://arxiv.org/abs/2510.27378 |

---

### 3. Mitigation Strategies

#### 3.1 Inference-time prompting / sampling

| Paper | Mitigation | Focus | Venue | Year | Link |
|---|---|---|---|---:|---|
| Chain-of-Thought Prompting Elicits Reasoning in Large Language Models | P | CoT prompting as interface (not a faithfulness guarantee) | NeurIPS | 2022 | https://arxiv.org/abs/2201.11903 |
| Larger Language Models Don't Care How You Think: Why Chain-of-Thought Prompting Fails in Subjective Tasks | P | CoT failure under subjectivity / preference | ICASSP | 2025 | https://arxiv.org/abs/2409.06173 |

#### 3.2 Verification & external tool binding

| Paper | Mitigation | Focus | Venue | Year | Link |
|---|---|---|---:|---:|---|
| Typed Chain-of-Thought: A Curry-Howard Framework for Verifying LLM Reasoning | VT | mechanically verifiable intermediate steps | arXiv | 2025 | https://arxiv.org/abs/2510.01069 |
| Monitoring Reasoning Models for Misbehavior and the Risks of Promoting Obfuscation | VT | CoT monitoring (and its failure modes) | arXiv | 2025 | https://arxiv.org/abs/2503.11926 |

#### 3.3 Training-time methods & internal intervention

| Paper | Mitigation | Focus | Venue | Year | Link |
|---|---|---|---|---:|---|
| Measuring Chain-of-Thought Faithfulness by Unlearning Spurious Reasoning Paths | FT | unlearning to reduce reliance on unfaithful rationales | EMNLP | 2025 | https://aclanthology.org/2025.emnlp-main.504/ |

---

## License

This project is released under the MIT License (see `LICENSE`).
