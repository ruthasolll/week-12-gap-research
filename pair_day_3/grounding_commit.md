 
# Grounding (Portfolio Update)

I updated my Week 10 Conversion Engine documentation to refine how I describe inference-time behavior in LLMs.

Previously, my framing loosely suggested that prompting “improves reasoning and agent behavior” in a way that could be interpreted as new capability emergence.

I corrected this to a more precise causal model:

- Prompting does not introduce new capabilities into the model
- It conditions and steers inference-time computation over pretrained representations
- Observable improvements in formatting, reasoning style, and agent behavior come from trajectory shaping in probability space, not new learning or parameter updates

This update strengthens the separation between the three core layers:

- **Pretraining:** builds the underlying representation space of language and reasoning patterns
- **Post-training (instruction tuning / RLHF):** shapes alignment, instruction-following behavior, and response preferences
- **Prompting (inference-time):** selects and reconfigures which latent behaviors are activated during generation

The key clarification added is that prompting should be understood as *runtime steering of computation paths*, not as capability creation.

This resolves ambiguity in earlier Week 10 language where “improved reasoning” could be misread as the model acquiring new skills during inference.

---

## Confirmation

Both partners reviewed the revised explanation and confirmed alignment on the updated framing of inference-time behavior.