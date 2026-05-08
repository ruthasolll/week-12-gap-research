# **Week 12 — Knowledge Gap Research & Explainers Overview**

This repository contains my Week 12 work focused on closing real knowledge gaps in AI systems I previously built during Weeks 10 and 11.

Instead of building new systems, this week focused on:

- identifying diagnostic gaps in my understanding
- researching underlying LLM mechanisms
- writing technical explainers
- grounding insights back into existing portfolio artifacts
- publicly documenting findings through LinkedIn explainers

Each day followed a paired research loop:

1. Identify and sharpen a diagnostic question
2. Write an explainer for a peer’s question
3. Receive an explainer for my own gap
4. Ground the insight back into prior project work

---

# **Day 1 — Preference Optimization vs Evaluation Metrics**

📁 `pair_DAY_1/`

## **My Question**

Focused on understanding why my DPO-trained model in Week 11 underperformed the original base model despite successful fine-tuning.

### Key gap:

I misunderstood what DPO actually optimizes.

I initially assumed:

> lower training loss → better benchmark performance

But DPO does not directly optimize task correctness.

It optimizes relative preference probabilities between chosen and rejected outputs.

---

## **Explainer I Wrote**

I wrote an explainer on:

- inference-time mechanics
- prefill vs decode phases
- KV cache behavior
- prompt-token latency effects
- how prompt structure affects runtime behavior

This addressed my partner’s gap about:

> what physically happens inside an LLM inference call and how prompt length changes latency, memory, and generation behavior.

---

## **Explainer I Received**

My peer explained:

- DPO reshapes relative output probabilities
- it widens preference margins rather than improving correctness
- preference datasets only help when aligned with evaluation metrics
- benchmark failure can happen even when training “succeeds”

---

## **Key Insight**

Better training loss ≠ better benchmark performance.

Specifically:

- DPO optimizes preference separation
- benchmarks measure task correctness
- if those objectives differ → performance may not improve

---

## **Grounding Into My Work**

I updated my Week 11 evaluation interpretation to:

- separate preference alignment from capability improvement
- correctly interpret negative Delta B results
- explain why training success did not transfer into evaluation success

---

## **Public Explainer**

LinkedIn Post:

[Day 1 LinkedIn Explainer](https://www.linkedin.com/posts/ruth-solomon-6676ab239_10academy-trp1-week12-share-7458621324387803136-fwG8?utm_medium=member_desktop&rcm=ACoAADtej-8B5I7GKDmFX4hLNF3i1fyZ5Qlk1FM&utm_source=chatgpt.com)

---

# **Day 2 — Tool Use, Schemas, and Structured Decoding**

📁 `pair_DAY_2/`

## **My Question**

Focused on understanding why my MCP-based tool system in the Week 10 Conversion Engine failed to reliably trigger tool calls.

The model frequently:

- generated normal text
- produced malformed JSON
- ignored tools entirely

### Key gap:

I misunderstood how tool calling actually works at inference time.

---

## **Explainer I Wrote**

I wrote an explainer on:

- inference-time token prediction
- structured decoding
- schema-constrained generation
- API-level tool registration
- probability shaping toward structured outputs

This addressed my partner’s gap about:

> why prompt formatting and schema structure strongly affect reliable tool usage in LLM systems.

---

## **Explainer I Received**

My peer explained:

- tool use is not a special internal reasoning capability
- models only predict token sequences
- tool schemas injected as plain text are not equivalent to registered API tools
- passing tools through `tools=[...]` changes the generation distribution because the schema becomes part of the provider’s structured tool interface

This was the major missing mechanism in my system.

---

## **Key Insight**

Tool use is not execution inside the model.

It is:

> probability shaping toward structured token sequences under constrained decoding.

The runtime system — not the model — parses and executes the tool call.

---

## **Grounding Into My Work**

I updated my Week 10 Conversion Engine assumptions to:

- separate orchestration from generation
- stop treating malformed JSON as “partial tool use”
- recognize that API-level schema registration matters more than natural-language tool descriptions
- redesign my tool schemas toward strict structured outputs

---

## **Public Explainer**

LinkedIn Post:

[Day 2 LinkedIn Explainer](https://www.linkedin.com/posts/ruth-solomon-6676ab239_10academy-trp1-week12-share-7458623093977071616-kYF3?utm_medium=member_desktop&rcm=ACoAADtej-8B5I7GKDmFX4hLNF3i1fyZ5Qlk1FM&utm_source=chatgpt.com)

---

# **Day 3 — Pretraining, Post-Training, and Prompt Steering**

📁 `pair_DAY_3/`

## **My Question**

Focused on understanding why changing only prompt structure dramatically improved behavior in my Week 10 Conversion Engine without changing any model weights.

### Key gap:

I confused prompting with “activating new abilities.”

---

## **Explainer I Wrote**

I wrote an explainer on:

- pretraining mechanics
- instruction tuning
- RLHF behavior shaping
- latent representation steering
- prompting as inference-time conditioning

This addressed my partner’s gap about:

> how prompting can produce reasoning, formatting, and tool-like behavior without new training.

---

## **Explainer I Received**

My peer explained:

- pretraining builds latent capability space
- post-training reshapes preference distributions
- prompting steers which internal trajectories dominate during inference
- no new capability is created at runtime

---

## **Key Insight**

Prompting does not create intelligence.

It steers computation trajectories through already-learned representations.

Specifically:

- pretraining builds capability space
- post-training shapes behavioral preference
- prompting selects trajectories inside that space

---

## **Grounding Into My Work**

I updated my Week 10/11 project framing to:

- stop describing prompting as “unlocking abilities”
- replace it with inference-time representation steering
- distinguish capability learning from behavioral control
- formalize the separation between:
  - capability
  - alignment
  - prompting
  - decoding behavior

---

## **Public Explainer**

LinkedIn Post:

[Day 3 LinkedIn Explainer](https://www.linkedin.com/posts/ruth-solomon-6676ab239_10academy-trp1-week12-share-7458623628818001921-bcYU?utm_medium=member_desktop&rcm=ACoAADtej-8B5I7GKDmFX4hLNF3i1fyZ5Qlk1FM&utm_source=chatgpt.com)

---

# **Day 4 — Bootstrap Confidence Intervals in LLM Evaluation**

📁 `pair_DAY_4/`

## **My Question**

Focused on understanding what paired-bootstrap confidence intervals actually mean in my Week 11 Sales Evaluation Bench.

### Key gap:

I reported confidence intervals and p-values but could not statistically defend what they represented.

---

## **Explainer I Received**

My peer explained:

- paired bootstrap resampling
- uncertainty estimation over task deltas
- why percentile bootstrap can become overconfident
- spike-at-zero failure modes
- assumptions behind exchangeability and independence
- why statistical significance ≠ deployment usefulness

---

## **Key Insight**

Bootstrap confidence intervals only estimate sampling uncertainty.

They do NOT measure:

- benchmark validity
- judge-model bias
- deployment usefulness
- product effectiveness

A statistically significant improvement can still fail the real deployment requirement.

---

## **Grounding Into My Work**

I updated my Week 11 evaluation interpretation to:

- properly explain paired bootstrap assumptions
- separate statistical significance from product usefulness
- identify overconfidence risks in small evaluation sets
- clarify limitations of judge-based evaluation pipelines

---

# **Overall Outcome of Week 12**

Across all four days, the major shift was moving from:

> “models gain new behaviors through prompting and fine-tuning”

to:

> “LLM behavior emerges from probability shaping across training, post-training, prompting, and decoding constraints.”

This clarified:

- why training improvements may not appear in benchmarks
- why prompting changes behavior without changing capability
- why tool use depends on structured decoding constraints
- why statistical significance does not guarantee deployment usefulness
- why inference-time behavior is fundamentally trajectory selection inside pretrained representation space

---

# **Overall Impact**

Week 12 significantly strengthened the conceptual grounding behind my previous projects.

### Key improvements:

- corrected multiple misunderstandings about DPO and evaluation
- formalized a clearer mental model of inference-time behavior
- improved understanding of tool calling and structured decoding
- strengthened statistical interpretation of benchmark results
- improved ability to defend evaluation claims technically
- grounded theoretical mechanisms back into Weeks 10 and 11 artifacts
