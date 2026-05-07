 
# Evening Call Summary — Feedback Review

In the evening review, we revisited the sharpened question and evaluated whether the explanation properly distinguishes between capability formation and behavior activation.

The main feedback was that the explanation was directionally correct but needed tighter precision in three areas:

1. Avoid overstating “activation” as a binary switch — prompting also *reconfigures representations*, not just selects them.
2. Clarify that pretraining does not directly encode “skills,” but rather distributions over text where skill-like patterns emerge.
3. Emphasize that post-training modifies interpretability and instruction sensitivity, not just surface behavior.

We refined the central mental model into a cleaner decomposition:

- Pretraining → builds representation space of linguistic and reasoning patterns
- Post-training → aligns and reshapes instruction-following behavior
- Prompting → conditions and steers inference-time computation paths

We also clarified that in-context learning is not true learning in the weight-update sense, but temporary task structure construction inside the forward pass.

Final conclusion of the review:
My original confusion (“why does prompting feel like learning?”) is resolved by reframing prompting as runtime representation steering rather than capability creation.

The explanation now cleanly separates:
capability formation vs behavior selection vs inference-time computation.