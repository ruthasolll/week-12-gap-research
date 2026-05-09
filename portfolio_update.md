# Portfolio Update — Week 12 Grounding Improvements

## Overview

During Week 12, I revisited my Week 10 and Week 11 AI systems and corrected several important conceptual and evaluation gaps through mechanism-level research and paired explainers.

The result was not a rebuild of the systems themselves, but a significant improvement in:
- technical defensibility,
- evaluation rigor,
- systems reasoning,
- and deployment interpretation.

This portfolio update summarizes how the five grounding commits collectively improved the quality of my work as an AI engineering candidate.

---

# Systems Improved

## Week 10 — Sales Agent / Conversion Engine

Improvements focused on:
- prompting behavior,
- tool-use architecture,
- inference-time reasoning,
- and structured generation.

## Week 11 — Sales Evaluation Benchmark

Improvements focused on:
- DPO interpretation,
- statistical evaluation,
- uncertainty estimation,
- and benchmark defensibility.

---

# Key Improvements Added

---

# 1. Corrected DPO Evaluation Interpretation

## Before

My original Week 11 framing implied:
- successful DPO training should directly improve benchmark performance.

This over-attributed downstream evaluation gains to preference optimization.

## After

I revised the evaluation documentation to distinguish:
- preference optimization,
- benchmark correctness,
- and deployment capability.

The updated interpretation now explains:
- DPO reshapes relative output probabilities,
- but does not inherently optimize structured correctness metrics.

## Why This Matters

This makes the benchmark interpretation:
- statistically defensible,
- mechanism-aware,
- and aligned with real post-training behavior.

---

# 2. Clarified Tool Use Architecture

## Before

My Week 10 documentation loosely described the system as:
> “an AI agent using tools.”

This implied model-driven execution that did not actually exist.

## After

I corrected the architecture description to explicitly state:
- the system is deterministic orchestration,
- tool execution is external,
- and valid tool use requires structured generation plus parsing.

I also documented:
- schema injection,
- constrained decoding,
- and parsing requirements.

## Why This Matters

This creates a more honest and technically accurate description of the system architecture.

It also demonstrates understanding of:
- inference-time structured generation,
- orchestration boundaries,
- and production agent reliability.

---

# 3. Refined Prompting & Inference Explanations

## Before

My earlier wording suggested:
- prompting “improves reasoning”
- or “creates smarter behavior.”

## After

I replaced this framing with:
- prompting as inference-time steering,
- latent behavior activation,
- and trajectory shaping in probability space.

I clarified the separation between:
- pretraining,
- instruction tuning,
- and prompting.

## Why This Matters

This reflects a much stronger understanding of:
- modern LLM behavior,
- representation-space conditioning,
- and inference-time computation.

---

# 4. Improved Statistical Evaluation Rigor

## Before

My benchmark report included paired-bootstrap confidence intervals without fully explaining:
- what uncertainty they measured,
- what assumptions they relied on,
- or their failure modes.

## After

I updated the evaluation documentation to distinguish:
- sampling uncertainty,
- statistical significance,
- judge-model bias,
- and operational usefulness.

I also added explicit warnings about:
- small sample size,
- spike-at-zero distributions,
- and bootstrap overconfidence.

## Why This Matters

This substantially improved:
- evaluation credibility,
- benchmark interpretation,
- and statistical maturity.

---

# 5. Better Systems-Level Understanding of Inference Cost

## Before

I treated latency and cost mostly as observable metrics.

## After

I now describe inference using:
- prefill,
- decode,
- and KV-cache dynamics.

I updated system notes to explain:
- why prompt length dominates TTFT,
- why repeated system prompts are expensive,
- and why retrieval trimming matters.

## Why This Matters

This strengthened the systems-engineering depth of the portfolio by connecting:
- architecture choices,
- latency behavior,
- and production optimization.

---

# Overall Portfolio Impact

Collectively, these grounding commits improved the portfolio in four major ways:

## 1. Stronger Mechanism-Level Understanding

The portfolio now explains:
- why systems behave the way they do,
not just:
- what they output.

---

## 2. More Defensible Evaluation Claims

Evaluation sections now:
- separate uncertainty from usefulness,
- avoid overstating significance,
- and communicate limitations explicitly.

---

## 3. More Accurate AI Systems Framing

The revised documentation avoids:
- anthropomorphic explanations,
- misleading “agent” claims,
- and vague reasoning terminology.

Instead, it uses:
- probability-based,
- inference-based,
- and architecture-grounded explanations.

---

## 4. Improved Professional AI Engineering Maturity

The updates demonstrate:
- critical self-correction,
- rigorous reasoning,
- and the ability to revise assumptions after deeper investigation.

This reflects stronger readiness for:
- forward-deployed engineering,
- AI systems evaluation,
- and client-facing technical work.

---

# Final Reflection

The biggest improvement from Week 12 was not adding new features.

It was improving:
- conceptual precision,
- evaluation honesty,
- and systems-level understanding.

The portfolio now better reflects:
- how modern LLM systems actually work,
- where their limitations exist,
- and how engineering decisions interact with model behavior.

This week transformed the projects from:
> “systems that function”

into:
> “systems I can now explain, defend, critique, and improve mechanistically.”