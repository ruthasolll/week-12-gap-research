Week 12 — Knowledge Gap Research & Explainers
Overview

This repository contains my Week 12 work focused on closing real knowledge gaps in AI systems I previously built (Weeks 10 & 11).

Instead of building new systems, this week focused on:

identifying gaps in my understanding
researching the underlying mechanisms
writing public explainers
grounding insights back into my existing portfolio

Each day followed a paired research loop:

Identify and sharpen a diagnostic question
Write an explainer for a peer’s question
Receive an explainer for my own gap
Update prior work based on new understanding
Day 1 — Inference-Time Mechanics

📁 pair_DAY_1/

My Question

Focused on understanding why my DPO-trained model did not outperform the base model, despite successful training.

Key gap:
Misunderstanding the difference between preference optimization (DPO) and evaluation metrics.

Explainer I Wrote

I wrote an explainer on:

Prefill vs Decode phases
KV cache
Why prompt length affects latency
How prompt structure influences model behavior

This addressed my partner’s gap about:

what actually happens inside an LLM call and how prompt/output affect cost, latency, and behavior.

Explainer I Received

My peer explained:

what DPO optimizes at the gradient level
why it reshapes relative probabilities, not absolute correctness
why misalignment between training signal and evaluation leads to no improvement
Key Insight

Better training ≠ better evaluation performance

Specifically:

DPO improves preference alignment
Benchmarks measure task correctness
If these are not aligned → no performance gain
Grounding Into My Work

I began updating my Week 11 evaluation documentation to:

correct my interpretation of ablation results
explain why the fine-tuned model did not outperform the base model
distinguish between behavior shaping vs capability improvement
Day 2 — Post-Training Objective vs Behavioral Change

📁 pair_DAY_2/

My Question

Focused on understanding why instruction-tuned models feel “smarter” or more capable even when their underlying pretraining remains unchanged.

Key gap:
Confusion between:

improved instruction-following
actual improvement in reasoning capability
Explainer I Wrote

I wrote an explainer on:

attention patterns during multi-turn instruction following
how structured prompts reshape decoding trajectories
why format compliance improves without capability gain

This addressed my partner’s gap about:

why prompt formatting strongly affects reasoning consistency and output structure in LLM systems.

Explainer I Received

My peer explained:

post-training (SFT/RLHF) does not add new knowledge
it modifies preference distributions over outputs
instruction tuning makes prompts more “legible” to the model
Key Insight

Instruction tuning improves control, not raw intelligence

Specifically:

pretraining defines capability space
post-training improves navigation of that space
prompting selects trajectories inside it
Grounding Into My Work

I updated my Week 10 Conversion Engine notes to:

remove implied equivalence between “better formatting” and “better reasoning”
clarify that structured prompts improve decoding stability, not model intelligence
refine agent behavior design assumptions in my pipeline
Day 3 — Inference-Time Steering and Latent Behavior Activation

📁 pair_DAY_3/

My Question

Focused on understanding why structured prompts drastically change agent behavior even though no model weights are updated.

Key gap:
Misinterpreting prompting as “activation of skills” instead of runtime computation shaping.

Explainer I Wrote

I wrote an explainer on:

pretraining vs post-training vs prompting
latent representation space in transformers
how structured prompts bias probability distributions

This addressed my partner’s gap about:

how prompting can reliably produce structured outputs (JSON, reasoning steps, tool-like behavior) without explicit training for each format.

Explainer I Received

My peer explained:

prompting works by conditioning internal representations, not switching modules
behavior emerges from trajectory shifts in token probability space
in-context learning is temporary task construction inside the forward pass
Key Insight

Prompting is not activation — it is representation steering

Specifically:

no new capabilities are created at inference time
prompts reshape computation paths across layers
behavior emerges from constrained decoding trajectories
Grounding Into My Work

I updated my Week 10/11 Conversion Engine documentation to:

correct “prompting improves reasoning” framing
replace it with “prompting steers inference-time computation”
formalize capability vs behavior vs selection separation across system layers
Final Outcome of Week 12

Across all three days, the core shift was:

moving from a “prompting creates behavior” model
to a “prompting selects and reshapes existing representation trajectories” model

This clarified:

why training improvements don’t always reflect in benchmarks
why instruction tuning changes behavior without adding capability
why prompting can appear to “unlock intelligence”
Overall Impact
Strengthened conceptual grounding of Week 10 Conversion Engine
Corrected multiple over-attributions of capability gain
Established a consistent mental model of LLM behavior across training stages
Improved evaluation interpretation for future experiments
