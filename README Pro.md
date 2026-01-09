# The Mirage of Explainability: A Survey on Chain-of-Thought Faithfulness in Large Language Models

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> A practical survey on **defining**, **evaluating**, and **improving** Chain-of-Thought (CoT) faithfulness in large language models.

## Table of Contents
* Overview
* Latest News
* Taxonomy & Legends
* Paper List
  * 1. Empirical Landscape of Unfaithfulness
    * 1.1 Key Phenomena
    * 1.2 Sources & Drivers
  * 2. Evaluating Faithfulness
    * 2.1 Level I: Behavioral (Black-box)
    * 2.2 Level II: Intermediate (Representation / Attribution)
    * 2.3 Level III: Mechanistic (Interventions)
    * 2.4 Level IV: Strong Supervision (Verifiable / Grounded)
  * 3. Mitigating Unfaithfulness
    * 3.1 Inference-time Mitigations
    * 3.2 Training-time Mitigations
  * 4. Future Directions

* * *

## Overview

![Overview Figure](assets/overview.png)

This repository accompanies our survey on **Chain-of-Thought (CoT) faithfulness**.

**Core definition (survey):** CoT faithfulness requires that a model’s verbalized reasoning is (i) **internally aligned** with its actual decision process and (ii) **externally consistent** with the resulting decision/output.

**What the survey provides in one framework:**
- A clear separation between *faithfulness* vs. *plausibility/consistency*.
- A structured view of **unfaithfulness phenomena** observed in practice.
- A unified lens to **evaluate** methods/benchmarks by their **grounding level** (from behavioral audits to mechanistic protocols).
- A practical map of **mitigation strategies** across prompting, decoding, supervision, and training.

> Note: For studies that touch multiple aspects (phenomena / evaluation / mitigation), we list the paper under the **primary** aspect it focuses on.

## Latest News
- [2026-01-09] Initialized the survey companion repo structure and aligned the README layout to the reference template.
- [2026-01-09] Added a first-pass taxonomy + curated paper list aligned with the survey sections.

## Taxonomy & Legends

### Key Terms
- **CoT**: Chain-of-Thought (explicit reasoning traces in natural language).
- **CoT Faithfulness**: *internal alignment* (trace reflects actual internal decision process) + *external consistency* (trace matches the produced answer/behavior).
- **Unfaithfulness**: the CoT trace is **not causally responsible** for the model’s decision, or is distorted/edited/misaligned relative to the true internal computation.

### Phenomena Tags (P)
- **P1 — Post-hoc Rationalization**: the model generates a plausible explanation after deciding (not the true cause).
- **P2 — Catering / Sycophancy**: the model adapts reasoning to user cues/preferences rather than truth/decision basis.
- **P3 — Performative Editing**: the model rewrites/beautifies CoT for presentation, masking true heuristics.
- **P4 — Restoration Errors**: reasoning text “restores” missing/incorrect steps to look coherent.
- **P5 — Unfaithful Shortcuts**: the model internally uses a shortcut but outputs a longer faithful-looking trace.

### Evaluation Grounding Levels (G)
- **G1 — Behavioral**: black-box tests (counterfactuals, perturbations, consistency tests) on outputs/CoT.
- **G2 — Intermediate**: representation/probe/attribution-based checks connecting CoT tokens to internal states.
- **G3 — Mechanistic**: causal interventions on components (e.g., patching/ablation) to test causal dependence.
- **G4 — Strong Supervision**: externally verifiable reasoning (tools/constraints/grounded steps) enabling strict auditing.

### Mitigation Tags (M)
- **M1 — Prompt / Format Control**: CoT elicitation constraints, structured reasoning, rationale policies.
- **M2 — Decoding-Time Controls**: constrained decoding, reranking, calibration to reduce performative CoT.
- **M3 — Supervised Signals**: process supervision, step-level labels, verifiable intermediate targets.
- **M4 — Training Interventions**: RL/RLAIF objectives, unlearning shortcut traces, causal regularizers.

* * *

## Paper List

> We group papers by the **primary** question they answer:  
> (1) *What unfaithfulness looks like?* → (2) *How to measure it?* → (3) *How to reduce it?*

### 1. Empirical Landscape of Unfaithfulness

#### 1.1 Key Phenomena

| Paper | Focus | Tags | Venue/Type | Year | Link |
|---|---|---|---|---:|---|
| Chain-of-Thought Prompting Elicits Reasoning in Large Language Models (Wei et al.) | CoT prompting as a capability / reason traces | P? | arXiv | 2022 | https://arxiv.org/abs/2201.11903 |
| Language Models Don’t Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting (Turpin et al.) | Unfaithful rationales; behavioral faithfulness tests | P1, P5, G1 | arXiv | 2023 | https://arxiv.org/abs/2305.04388 |
| Measuring Faithfulness in Chain-of-Thought Reasoning (Lanham et al.) | Behavioral measurement suite; stress-tests | P1, G1 | arXiv | 2023 | https://arxiv.org/abs/2307.13702 |
| Towards Understanding Sycophancy in Language Models (Sharma et al.) | RLHF-driven sycophancy; user-cue effects | P2 | ICLR | 2024 | https://arxiv.org/abs/2310.13548 |
| LLM Sycophancy Under User Rebuttal (OpenReview: VfyYOT9yIa) | Sycophancy trigger: rebuttal vs. evaluative setting | P2, G1 | OpenReview | 2025 | https://openreview.net/forum?id=VfyYOT9yIa |

#### 1.2 Sources & Drivers

| Paper | Focus | Tags | Venue/Type | Year | Link |
|---|---|---|---|---:|---|
| Sycophancy in Large Language Models (Malmqvist et al.) | Technical survey of sycophancy causes/impacts/mitigations | P2 | arXiv | 2024 | https://arxiv.org/abs/2411.15287 |
| CoT Faithfulness in the Wild: A Causal View of CoT Faithfulness (Arcuschin et al.) | Real-world faithfulness failures; causal framing | P1, P4, G1/G2 | arXiv | 2025 | https://arxiv.org/abs/2503.08679 |
| Bias and CoT Faithfulness (Balasubramanian et al.) | Bias–CoT interactions; faithfulness under bias | P1/P5, G1 | arXiv | 2025 | https://arxiv.org/abs/2505.23945 |

### 2. Evaluating Faithfulness

#### 2.1 Level I: Behavioral (Black-box)

| Paper | Focus | Tags | Venue/Type | Year | Link |
|---|---|---|---|---:|---|
| Language Models Don’t Always Say What They Think (Turpin et al.) | Counterfactual/feature-based tests for faithfulness | G1 | arXiv | 2023 | https://arxiv.org/abs/2305.04388 |
| Measuring Faithfulness in Chain-of-Thought Reasoning (Lanham et al.) | Behavioral metrics & protocols | G1 | arXiv | 2023 | https://arxiv.org/abs/2307.13702 |

#### 2.2 Level II: Intermediate (Representation / Attribution)

| Paper | Focus | Tags | Venue/Type | Year | Link |
|---|---|---|---|---:|---|
| (Survey framework) Intermediate checks linking CoT tokens ↔ internal evidence | Probing/attribution as “mid-grounding” diagnostics | G2 | Survey | — | (see paper PDF) |

#### 2.3 Level III: Mechanistic (Interventions)

| Paper | Focus | Tags | Venue/Type | Year | Link |
|---|---|---|---|---:|---|
| Faithfulness by Unlearning: Improving CoT Faithfulness by Unlearning Reasoning Steps (Tutek et al.) | Training intervention; faithfulness gains via unlearning | G3, M4 | EMNLP | 2025 | https://aclanthology.org/2025.emnlp-main.504/ |
| A Causal Analysis of Bias-Driven CoT Faithfulness (Arcuschin et al.) | Causal methods; intervention-oriented analysis | G3 | arXiv | 2025 | https://arxiv.org/abs/2503.08679 |

#### 2.4 Level IV: Strong Supervision (Verifiable / Grounded)

| Paper | Focus | Tags | Venue/Type | Year | Link |
|---|---|---|---|---:|---|
| Making Reasoning Matter: Measuring and Improving Faithfulness of Chain-of-Thought Reasoning (Paul et al.) | Verifiable/process-sensitive evaluation + improvements | G4, M3/M4 | arXiv | 2024 | https://arxiv.org/abs/2402.13950 |

### 3. Mitigating Unfaithfulness

#### 3.1 Inference-time Mitigations

| Paper | Focus | Tags | Venue/Type | Year | Link |
|---|---|---|---|---:|---|
| (Survey synthesis) Prompt/format constraints, decoding controls, and auditing protocols | Practical knobs without retraining | M1/M2 | Survey | — | (see paper PDF) |

#### 3.2 Training-time Mitigations

| Paper | Focus | Tags | Venue/Type | Year | Link |
|---|---|---|---|---:|---|
| Faithfulness by Unlearning (Tutek et al.) | Unlearning reasoning steps to reduce unfaithful traces | M4 | EMNLP | 2025 | https://aclanthology.org/2025.emnlp-main.504/ |
| Making Reasoning Matter (Paul et al.) | Objectives that make reasoning causally relevant | M3/M4 | arXiv | 2024 | https://arxiv.org/abs/2402.13950 |

### 4. Future Directions

| Direction | One-line Summary |
|---|---|
| Functional Faithfulness | Move beyond “verbatim trace matching” to task-oriented causal efficacy and decision auditability. |
| Mechanistic Evaluation at Scale | Bridge behavioral metrics with scalable mechanistic interventions for routine auditing. |
| Faithfulness–Safety Coupling | Treat CoT monitorability/faithfulness as a safety-relevant property (and measure it explicitly). |

## (Optional) Assets
Place figures here to match the template rendering:
- `assets/overview.png` — one-page conceptual overview figure
- `assets/taxonomy.png` — taxonomy diagram (phenomena → evaluation → mitigation)
