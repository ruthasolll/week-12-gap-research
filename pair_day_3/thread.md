 
1/
I noticed something strange in my Week 10 Conversion Engine: changing only prompt structure dramatically improved reasoning, formatting, and agent behavior — without changing model weights.

So where did those “new abilities” come from?

2/
Modern LLMs don’t learn in a single place.

Pretraining builds a huge latent space from next-token prediction:
syntax, reasoning patterns, code, dialogue structures, etc.

But none of these are “skills” in a direct sense — they’re compressed statistical structures.

3/
Post-training (instruction tuning + RLHF) doesn’t add intelligence either.

It reshapes behavior:
- what the model prefers
- how it follows instructions
- how strictly it formats outputs

Think of it as alignment, not capability creation.

4/
Prompting is where things get interesting.

At inference time, the model doesn’t “retrieve answers.”
It computes next-token probabilities conditioned on context.

So prompts don’t add knowledge — they steer which internal representations dominate.

5/
That’s why structured prompts feel powerful.

They reshape the model’s internal trajectory:
- formatting becomes more stable
- reasoning becomes more explicit
- tool-like behavior becomes more likely

But nothing new is being learned.

6/
Key insight:

Pretraining builds capability space.
Post-training shapes preference.
Prompting selects behavior.

What looks like “new skill acquisition” is usually just better steering of an already learned representation space.