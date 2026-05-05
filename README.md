# week-12-gap-research

# Week 12 — Knowledge Gap Research & Explainers

## Overview

This repository contains my Week 12 work focused on **closing real knowledge gaps in AI systems I previously built** (Weeks 10 & 11).

Instead of building new systems, this week focused on:
- identifying gaps in my understanding
- researching the underlying mechanisms
- writing public explainers
- grounding insights back into my existing portfolio

Each day followed a **paired research loop**:
1. Identify and sharpen a diagnostic question
2. Write an explainer for a peer’s question
3. Receive an explainer for my own gap
4. Update prior work based on new understanding

---

## Day 1 — Inference-Time Mechanics

📁 `pair_DAY_1/`

### My Question
Focused on understanding **why my DPO-trained model did not outperform the base model**, despite successful training.

Key gap:
> Misunderstanding the difference between **preference optimization (DPO)** and **evaluation metrics**.

---

### Explainer I Wrote
I wrote an explainer on:
- **Prefill vs Decode phases**
- **KV cache**
- **Why prompt length affects latency**
- **How prompt structure influences model behavior**

This addressed my partner’s gap about:
> what actually happens inside an LLM call and how prompt/output affect cost, latency, and behavior.

---

### Explainer I Received
My peer explained:
- what DPO optimizes at the gradient level
- why it reshapes **relative probabilities**, not absolute correctness
- why misalignment between training signal and evaluation leads to no improvement

---

### Key Insight

> Better training ≠ better evaluation performance

Specifically:
- DPO improves **preference alignment**
- Benchmarks measure **task correctness**
- If these are not aligned → no performance gain

---

### Grounding Into My Work

I began updating my Week 11 evaluation documentation to:
- correct my interpretation of ablation results
- explain why the fine-tuned model did not outperform the base model
- distinguish between **behavior shaping vs capability improvement**

---

## Repository Structure
