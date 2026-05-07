 
# Morning Call Summary — Week 11 Pair Session

Today’s call focused on sharpening the core confusion behind my Week 10 Conversion Engine observation: why structured prompting changes model behavior so significantly without any change in model weights.

At the start, my framing was vague — I described it as “prompting improving reasoning and formatting,” but I couldn’t clearly separate pretraining, post-training, and inference-time behavior.

My pair helped refine the key distinction:

- Pretraining builds a broad latent capability space through next-token prediction on large-scale text.
- Post-training (instruction tuning / RLHF) reshapes how those capabilities are expressed and aligned with instructions.
- Prompting does not add capabilities; it conditions and steers which latent behaviors become active at inference time.

The most important shift in my understanding was moving from “prompting activates skills” to a more precise model:

> Prompting reconfigures the probability landscape over already-learned representations rather than creating new capabilities.

We also clarified that:
- in-context learning is a temporary computation-based adaptation, not parameter learning
- structured prompts work by biasing decoding trajectories toward specific behavioral regimes (formatting, reasoning style, tool-use patterns)

By the end of the session, my question was sharpened into a clearer causal decomposition of where “ability” actually resides in modern LLM systems versus where “behavior” is selected.

This directly led to refining my Week 10 observation into a more precise claim about inference-time steering rather than emergent new learning.