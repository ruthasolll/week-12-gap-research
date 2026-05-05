# sources.md
## Canonical Papers

1. Rafailov et al. (2023) — *Direct Preference Optimization: Your Language Model is Secretly a Reward Model*  
https://arxiv.org/abs/2305.18290  

This is the primary paper introducing DPO. It defines the objective used to optimize preference pairs without explicitly training a reward model and explains how the optimization reshapes log-probability ratios relative to a reference policy.

---

2. Ouyang et al. (2022) — *Training Language Models to Follow Instructions with Human Feedback*  
https://arxiv.org/abs/2203.02155  

This paper introduces the RLHF pipeline (SFT + reward model + PPO), which provides the baseline framework that DPO simplifies. It is essential for understanding how DPO differs from traditional alignment methods and why preference signals matter.

---

## Tool / Practical Reference

3. Hugging Face TRL (Transformer Reinforcement Learning) Library — DPO Trainer Documentation  
https://huggingface.co/docs/trl/main/en/dpo_trainer  

This provides a practical implementation of DPO, showing how preference pairs are used in training and how the objective is applied in real systems. It connects the theoretical formulation to actual training workflows used in engineering.