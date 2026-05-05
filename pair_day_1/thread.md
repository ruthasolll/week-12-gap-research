 
1/ I trained a model using DPO… but it didn’t beat the base model.

Here’s why 👇

2/ DPO doesn’t directly maximize task performance.

It optimizes:
👉 preference between responses

Not:
👉 absolute correctness

3/ Mechanism:
It increases probability of preferred outputs vs rejected ones

But…
this depends heavily on your dataset quality.

4/ If your evaluation ≠ your training objective,
you get NO improvement.

That’s what happened in my case.

5/ Takeaway:
DPO is powerful, but only when:
- preferences are high-quality
- evaluation aligns with training

6/ Full breakdown here: [link]