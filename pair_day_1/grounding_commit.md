# grounding_commit.md

## Grounding Commit

I began updating my Week 11 evaluation documentation to better explain why my DPO-trained model did not outperform the base model.

Previously, I assumed that improved training (via preference optimization) would directly translate into higher evaluation scores. After the explainer and evening discussion, I now understand that this assumption is incorrect—performance depends on alignment between the training objective (preference ranking) and the evaluation metric (structured correctness).

At this stage, I have identified the specific gap in my documentation: it does not distinguish between **relative preference optimization** and **absolute benchmark performance**, which led to an overclaim in how I interpreted my results.

I am currently working on revising the evaluation section to:
- explicitly describe the mismatch between preference data and benchmark criteria
- clarify why DPO reshapes output probabilities rather than introducing new capabilities
- refine the explanation behind the observed performance gap

The update is not fully complete yet, but the mechanism-level understanding from this explainer is directly guiding the revision. This will result in a more defensible interpretation of my ablation results and clearer communication of when DPO is an appropriate training strategy.