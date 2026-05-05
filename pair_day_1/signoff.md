# signoff.md

## Asker Sign-Off  
**Status: Closed**

Before this explainer, I treated DPO as a method that should improve overall model performance, and I could not explain why my fine-tuned model failed to outperform the base model on my Week 11 evaluation bench. I assumed that better training (lower loss, preference optimization) should directly translate into better benchmark scores.

I now understand the load-bearing mechanism at the level required for forward-deployed work:

- DPO does not optimize for absolute correctness. It optimizes **relative preference** by increasing the log-probability gap between preferred and rejected outputs with respect to a fixed reference model.
- This means DPO reshapes **which outputs the model prefers**, not whether those outputs are objectively correct according to an external evaluation.
- DPO operates within the **capability boundary of the base model**; it cannot reliably introduce new structured behaviors or knowledge that are not already present in the model’s distribution.
- Performance improvements depend critically on **alignment between the preference signal and the evaluation metric**. If the preference dataset rewards tone or fluency while the benchmark measures structured correctness or constraint adherence, improvements in training loss will not translate into better evaluation scores.
- This explains my ablation result: the fine-tuned model improved stylistically (better phrasing, tone), but did not improve on the benchmark because the training signal and evaluation objective were misaligned.

What I can now do differently:

- I can defend why a DPO-trained model might fail to beat a base model despite successful training.
- I can evaluate whether a preference dataset is a valid proxy for a given benchmark before investing in training.
- I can distinguish between **capability improvements (best achieved via SFT or better data)** and **behavior shaping (DPO / preference learning)** when making production decisions.

Explicit scope: This explainer focuses on the mechanism of DPO at the level of probability shaping and evaluation alignment. It does not cover deeper variants (e.g., ORPO, SimPO), detailed gradient derivations, or hyperparameter sensitivity, which would be the next layer of analysis.

This closes the gap named in `question.md` and matches the mechanism explanation in `explainer.md`.