# 🧠 LLM Behavior Playground

## 📌 Overview

This repository is a structured, experiment-driven exploration of how large language models (LLMs) actually generate text.

The goal is not to build applications, but to understand:

- How decoding strategies affect output
- Why responses vary across runs
- When models hallucinate
- Why constraints are probabilistic, not guarantees

Each notebook isolates **one specific mechanism** of language model behavior.

> Philosophy:  
> If you cannot explain why the model changed its output, you do not understand the model.

---

## 🎯 Objectives

This project aims to:

- Understand how LLMs generate tokens step by step
- Observe the effect of sampling parameters
- Measure determinism vs variability
- Study constraint-following behavior
- Build intuition about probabilistic text generation

---

## 📂 Repository Structure

```
llm-behavior-playground/
│
├── 01_sampling_behavior.ipynb
├── 02_...
├── 03_...
├── README.md
```

New notebooks will be added progressively as we explore deeper mechanisms.

---

# 📘 Notebook 01 — Sampling & Decoding Behavior

## 🔬 Question

How do decoding strategies influence output stability and variation?

## What Was Tested

- Greedy decoding (deterministic)
- Sampling with temperature
- Top-p (nucleus sampling)
- Multiple runs with different random seeds

Everything else remained constant:
- Same model
- Same prompt
- Same formatting constraints

---

## 📊 Observations

- Greedy decoding produces nearly identical outputs across runs.
- Sampling introduces variation even with the same prompt.
- Higher temperature increases diversity but may degrade format adherence.
- Constraints written in the prompt are not strict rules — they are probabilistic instructions.

---

## 🧠 Key Insight

Language models do not “follow rules.”

They predict the next token based on probability distributions.

Decoding strategy determines:

- Stability
- Creativity
- Constraint adherence
- Risk of hallucination

Sampling does not change the model —  
it changes how we traverse its probability space.

---

# 🔜 Upcoming Notebooks

The following experiments will progressively expand this repository:

---

## 📘 Notebook 02 — Temperature Scaling Deep Dive

- Visual intuition of probability flattening
- Low vs high temperature comparison
- Controlled diversity measurement
- When temperature increases hallucination risk

---

## 📘 Notebook 03 — Top-k vs Top-p Comparison

- Fixed candidate filtering (top-k)
- Probability mass filtering (top-p)
- Distribution tail effects
- Stability vs exploration tradeoff

---

## 📘 Notebook 04 — Determinism vs Random Seeds

- Why outputs differ across runs
- The role of random seeds
- When reproducibility breaks
- Production implications

---

## 📘 Notebook 05 — Constraint Following & Format Robustness

- Why models break formatting rules
- Prompt strength vs decoding strength
- Structured output enforcement
- Failure modes in real systems

---

## 📘 Notebook 06 — Hallucination Stress Test

- Incomplete prompts
- Ambiguous prompts
- High temperature behavior
- Confidence vs correctness

---

# 🧩 Design Principle of This Repository

Each notebook changes **only one variable**.

No hidden changes.
No pipeline complexity.
No multi-factor experiments.

Behavior is isolated.
Results are interpreted.
Conclusions are explicit.

---

# 🔬 Tools Used

- Hugging Face Transformers
- Instruction-tuned open-source models
- Controlled decoding parameters
- Google Colab (GPU)

---

# 🏁 Long-Term Goal

By the end of this repository, we aim to understand:

- How generation actually works
- Why models sometimes appear intelligent
- Why they sometimes fail unpredictably
- How decoding decisions affect system reliability

This repository complements:

- Retrieval-Augmented Generation (RAG) evaluation
- System-level LLM architecture understanding
- Production-oriented model reasoning

---

## 📌 Final Note

This is not a model showcase.

This is a controlled behavioral study of language models.

Understanding generation mechanics is the foundation of building reliable AI systems.
