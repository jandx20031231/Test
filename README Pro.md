# The Mirage of Explainability: A Survey on Chain-of-Thought Faithfulness in Large Language Models

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re) ![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

> Chain-of-Thought (CoT) reasoning is widely used as a practical “window” into model reasoning. However, CoT traces can be *unfaithful*—they may look plausible while failing to reflect the model’s actual decision process.  
> This repository accompanies our survey and provides (i) a unified definition of CoT faithfulness, (ii) a taxonomy of unfaithfulness phenomena and their underlying causes, (iii) an evaluation landscape (metrics + benchmarks), and (iv) mitigation strategies and future directions.

## Table of Contents

- [Overview](#overview)
- [Latest News](#latest-news)
- [Taxonomy & Legends](#taxonomy--legends)
  - [Interpretable Objects](#interpretable-objects)
  - [Localizing Methods](#localizing-methods)
  - [Steering Methods](#steering-methods)
- [Paper List](#paper-list)
  - [1. Improve Alignment](#1-improve-alignment)
    - [Safety and Reliability](#safety-and-reliability)
    - [Fairness and Bias](#fairness-and-bias)
    - [Persona and Role](#persona-and-role)
  - [2. Improve Capability](#2-improve-capability)
    - [Logic and Reasoning](#logic-and-reasoning)
    - [Domain-specific and Multilingualism](#domain-specific-and-multilingualism)
    - [Knowledge Management](#knowledge-management)
  - [3. Improve Efficiency](#3-improve-efficiency)
    - [Efficient Training](#efficient-training)
    - [Efficient Inference](#efficient-inference)
- [Contributing](#contributing)
- [Citation](#citation)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## Overview

This survey focuses on **CoT faithfulness**: when and why a model’s *verbalized reasoning trace* aligns with the *computation that actually drives its answer*, and what we can do about mismatches. Concretely, we:

1. **Define faithfulness** by integrating *internal alignment* (causal dependence of the answer on the trace) and *external consistency* (agreement with the intended reasoning standard).
2. Systematize **unfaithfulness phenomena** and summarize **root causes**.
3. Organize **evaluation** into **four benchmark levels** (from behavior-only to white-box), and discuss what each level can/cannot certify.
4. Review **mitigation strategies** and highlight open **future directions**.

![Overview Figure](assets/overview.png)

## Latest News

- **2026-01-08**: Initial repository release (paper coverage primarily up to **Jan 2026**).

## Taxonomy & Legends

### Interpretable Objects

- 📝 **CoT Trace**: the full natural-language reasoning trace.
- 🧩 **CoT Step / Claim**: step-level statements, pivots, or intermediate assertions.
- 🔍 **Verifier Artifacts**: programs, proofs, constraints, tool outputs used to check steps.
- 🧠 **Latent Computation**: internal activations / features / circuits / weights that drive decisions.

![Interpretable Objects](assets/interpretable_objects.png)

### Localizing Methods

- 📏 **Behavior-only (Black-box)**: compare answers vs. traces via I/O probes and controlled prompts.
- 🔁 **Counterfactual Resampling**: perturb prompts/traces/steps and test answer dependence.
- ✅ **External Verifiability**: require checkable intermediate steps (symbolic solvers, proof checkers, tools).
- 🧪 **Human Annotation**: judge plausibility/consistency/decision
