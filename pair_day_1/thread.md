1/ I trained a model using DPO… but it didn’t beat the base model.

Here’s what actually happened 👇

2/ DPO does NOT directly optimize task accuracy.

It optimizes preference separation:
👉 increase probability of preferred responses
👉 decrease probability of rejected responses
(relative to a frozen reference model)

3/ Mechanism:
DPO updates parameters to widen the log-probability gap between preferred and rejected outputs.

But this only works if the preference signal matches the evaluation target.

4/ In my case:
- training preferences rewarded tone + fluency
- evaluation measured structured correctness + compliance

So the model improved “style” but not benchmark score.

5/ This creates a failure mode:
If your preference dataset ≠ evaluation objective → no measurable lift.

Even if training loss improves.

6/ Takeaway:
DPO only improves downstream metrics when preference labels are a *true proxy* for the evaluation function.

Otherwise, you are optimizing the wrong surface.

