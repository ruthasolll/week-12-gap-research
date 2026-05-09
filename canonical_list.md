
# Canonical Reading & Tool List — Week 12

## Purpose

This document contains the papers, tools, systems, and conceptual patterns that most improved my understanding during Week 12.

The focus is not on “popular AI resources,” but on:
- mechanism-level understanding,
- deployment-relevant engineering,
- evaluation rigor,
- and inference-time behavior.

These are the materials I believe are most valuable for future Forward-Deployed Engineers working on real AI systems.

---

# Canonical Papers

---

## 1. Attention Is All You Need

**Authors:** Ashish Vaswani et al. (2017)

**Paper:**  
https://arxiv.org/abs/1706.03762

## Why It Matters

Foundational transformer paper introducing:
- self-attention,
- autoregressive generation,
- and the architecture underlying modern LLMs.

Critical for understanding:
- KV cache,
- prefill vs decode,
- prompt conditioning,
- and inference-time behavior.

## Most Important Insight

> Transformers operate through contextual attention over token sequences, not symbolic reasoning modules.

---

## 2. Direct Preference Optimization (DPO)

**Authors:** Rafael Rafailov et al. (2023)

**Paper:**  
https://arxiv.org/abs/2305.18290

## Why It Matters

Explains:
- preference optimization,
- reward-free alignment,
- and relative probability shaping.

Critical for understanding:
- why DPO training improvements may not improve benchmark metrics.

## Most Important Insight

> DPO optimizes preference separation, not absolute correctness.

---

## 3. Language Models are Few-Shot Learners

**Authors:** Brown et al. (2020)

**Paper:**  
https://arxiv.org/abs/2005.14165

## Why It Matters

Introduced:
- in-context learning,
- prompting-based capability activation,
- and few-shot behavior steering.

Critical for understanding:
- prompting,
- latent behavior activation,
- and inference-time adaptation.

## Most Important Insight

> Prompting often activates latent capabilities already present in pretrained models.

---

## 4. Training Language Models to Follow Instructions with Human Feedback

**Authors:** Ouyang et al. (2022)

**Paper:**  
https://arxiv.org/abs/2203.02155

## Why It Matters

Canonical RLHF / instruction tuning paper.

Clarifies:
- alignment,
- post-training,
- instruction-following behavior,
- and preference shaping.

## Most Important Insight

> Post-training reshapes preferred outputs rather than creating intelligence from scratch.

---

## 5. Chain-of-Thought Prompting Elicits Reasoning

**Authors:** Wei et al. (2022)

**Paper:**  
https://arxiv.org/abs/2201.11903

## Why It Matters

Demonstrates:
- prompting-based reasoning activation,
- intermediate reasoning traces,
- and inference-time trajectory shaping.

## Most Important Insight

> Chain-of-thought often activates latent reasoning trajectories already learned during pretraining.

---

## 6. An Introduction to the Bootstrap

**Authors:** Bradley Efron & Robert Tibshirani

## Why It Matters

Foundational statistical text for:
- bootstrap confidence intervals,
- resampling methods,
- and uncertainty estimation.

Critical for:
- evaluation interpretation,
- benchmark reporting,
- and statistical defensibility.

## Most Important Insight

> Confidence intervals estimate uncertainty under assumptions — not truth.

---

## 7. Deep Dominance: Properly Comparing Deep Neural Models

**Authors:** Dror et al. (2018)

**Paper:**  
https://aclanthology.org/P18-1128/

## Why It Matters

Explains:
- statistical testing pitfalls in NLP,
- bootstrap coverage problems,
- and evaluation reliability.

Critical for:
- benchmark interpretation,
- significance testing,
- and small-sample caution.

## Most Important Insight

> Small evaluation sets frequently produce overconfident statistical claims.

---

# Canonical Tools & Systems

---

## 1. OpenAI Function Calling

**Official Docs:**  
https://platform.openai.com/docs/guides/function-calling

## Why It Matters

Provides:
- structured tool schemas,
- JSON-enforced outputs,
- and runtime tool orchestration.

Critical for:
- reliable tool use,
- schema-constrained decoding,
- and production agents.

## Key Lesson

> Tool use is structured token generation interpreted externally by orchestration systems.

---

## 2. Anthropic Tool Use API

**Official Docs:**  
https://docs.anthropic.com/en/docs/build-with-claude/tool-use

## Why It Matters

Strong reference implementation for:
- schema injection,
- structured tool calling,
- and inference-time orchestration.

---

## 3. vLLM

**Paper:**  
https://arxiv.org/abs/2309.06180

## Why It Matters

Explains:
- KV cache management,
- memory-efficient serving,
- and inference optimization.

Critical for:
- latency engineering,
- large-context serving,
- and production deployment.

---

## 4. Hugging Face Transformers

**Docs:**  
https://huggingface.co/docs/transformers

## Why It Matters

Practical framework for:
- inference experimentation,
- model inspection,
- and deployment prototyping.

---

# Canonical Engineering Patterns

---

## 1. Prompting as Probability Steering

Prompting should be understood as:
- trajectory shaping,
- inference-time conditioning,
- and latent behavior selection.

NOT:
- capability creation.

---

## 2. Tool Use as Structured Generation

A model does not internally execute tools.

Tool use is:
- structured token prediction,
- schema validation,
- and external orchestration.

---

## 3. Statistical Significance ≠ Product Value

A positive confidence interval does not guarantee:
- deployment usefulness,
- operational correctness,
- or business value.

Evaluation metrics must remain tied to:
- real deployment requirements.

---

## 4. Behavior ≠ Capability

Improvements in:
- formatting,
- instruction-following,
- or output structure

do not necessarily indicate:
- deeper reasoning capability.

---

## 5. Prefill vs Decode Thinking

Inference latency should always be separated into:
- prefill cost,
- decode cost.

This distinction is critical for:
- prompt optimization,
- retrieval design,
- and serving performance.