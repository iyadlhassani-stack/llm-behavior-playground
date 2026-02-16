# 🧠 LLM Behavior Playground

## 📌 Overview

This repository is a structured, experiment-driven exploration of how large language models (LLMs) actually generate text.

The goal is not to build applications, but to understand:

- How decoding strategies influence output
- Why responses vary across runs
- When structure breaks
- How randomness impacts reproducibility
- Why constraints are probabilistic rather than guaranteed

Each notebook isolates **one specific behavioral mechanism** of language models.

> Philosophy:  
> If you cannot explain why the model changed its output, you do not understand the model.

---

## 🎯 Objectives

This project aims to:

- Build intuition about probabilistic text generation
- Understand decoding strategies at a system level
- Observe constraint-following behavior empirically
- Study reproducibility and randomness
- Connect model internals to real-world reliability concerns

---

## 📂 Repository Structure

```
llm-behavior-playground/
│
├── 01_sampling_behavior.ipynb
├── 02_temperature_scaling_deep_dive.ipynb
├── 03_top_k_vs_top_p_comparison.ipynb
├── 04_determinism_vs_random_seeds.ipynb
├── 05_constraint_following_and_format_robustness.ipynb
└── README.md
```

All notebooks use controlled experiments:
- Same model
- Same prompt (when relevant)
- Only one variable changed at a time

---

# 📘 Notebook 01 — Sampling & Decoding Behavior

## 🔬 Question

How do decoding strategies influence output stability and variation?

## Experiments

- Greedy decoding (deterministic)
- Sampling with temperature
- Multiple runs with different seeds

## Key Observations

- Greedy decoding produces nearly identical outputs.
- Sampling introduces controlled variation.
- Temperature influences diversity and stability.
- The model does not "change its mind" — decoding changes traversal of probabilities.

## Core Insight

Decoding strategy determines how we explore the model's probability distribution.

The model itself does not change — only how we sample from it.

---

# 📘 Notebook 02 — Temperature Scaling Deep Dive

## 🔬 Question

What does temperature actually do to generation?

## Experiments

- Temperature = 0.3
- Temperature = 0.7
- Temperature = 1.0
- Temperature = 1.3

## Key Observations

- Low temperature → sharper distributions, more deterministic outputs.
- Medium temperature → controlled lexical variation.
- High temperature → increased diversity and structural drift.
- Very high temperature increases format violations.

## Core Insight

Temperature reshapes the probability distribution:

- Lower temperature sharpens it.
- Higher temperature flattens it.

Flattened distributions increase diversity but reduce stability.

---

# 📘 Notebook 03 — Top-k vs Top-p Comparison

## 🔬 Question

How do Top-k and Top-p sampling differ?

## Experiments

- Baseline (no constraint)
- Top-k = 10, 20, 50
- Top-p = 0.8, 0.9, 0.95

## Key Observations

- Top-k keeps a fixed number of candidate tokens.
- Smaller k strongly limits diversity.
- Top-p keeps tokens up to a probability mass threshold.
- Top-p adapts better when distributions are sharp or flat.

## Core Insight

Top-k controls diversity by limiting candidate count.  
Top-p controls diversity by limiting probability mass.

Both restrict randomness, but in structurally different ways.

---

# 📘 Notebook 04 — Determinism vs Random Seeds

## 🔬 Question

Why do outputs differ across runs?

## Experiments

- Greedy decoding
- Sampling with different seeds
- Sampling with fixed seed

## Key Observations

- Greedy decoding is deterministic.
- Sampling introduces randomness.
- Changing the seed changes the output.
- Fixing the seed restores reproducibility.

## Core Insight

Output variability is not mysterious.

It is a direct consequence of stochastic sampling.

Reproducibility requires:
- Fixed seed
- Fixed decoding parameters
- Stable environment

---

# 📘 Notebook 05 — Constraint Following & Format Robustness

## 🔬 Question

How reliably does the model follow strict output constraints?

## Experiments

- Rule-based prompt
- Template-based prompt
- Greedy vs Sampling
- Multiple seeds
- Bullet count validation

## Key Observations

- Models may violate strict constraints.
- Sampling increases violation probability.
- Template prompts improve structure adherence.
- Even with strict instructions, compliance is not guaranteed.

## Core Insight

Language models optimize probability, not rule compliance.

Prompt constraints influence output but do not enforce it.

In production systems, strict formatting often requires:
- Post-generation validation
- Structured parsing
- Retry or correction loops

---

# 🧠 Overarching Lessons From This Repository

Across all five notebooks, we observe:

1. Decoding shapes output behavior.
2. Temperature reshapes probability distributions.
3. Top-k and Top-p restrict exploration differently.
4. Seeds control reproducibility.
5. Constraints are probabilistic, not guaranteed.

LLMs are stochastic sequence predictors.

Understanding generation mechanics is essential for building reliable AI systems.

---

# 🔬 Tools Used

- Hugging Face Transformers
- Instruction-tuned open-source models
- Controlled decoding parameters
- Google Colab (GPU)

---

# 🏁 Final Note

This repository is not a model showcase.

It is a behavioral study of language models.

Understanding how LLMs generate text is the foundation for:

- Reliable system design
- Robust structured outputs
- Safe deployment
- Advanced RAG architectures

The goal is not to trust the model.

The goal is to understand it.
