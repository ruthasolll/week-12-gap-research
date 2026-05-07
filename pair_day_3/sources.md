# Sources

## 1. Brown et al. (2020)
Language Models are Few-Shot Learners  
https://arxiv.org/abs/2005.14165

Key idea:
- Demonstrates in-context learning
- Shows prompting can induce task behavior without gradient updates

---

## 2. Ouyang et al. (2022)
Training language models to follow instructions with human feedback  
https://arxiv.org/abs/2203.02155

Key idea:
- Instruction tuning + RLHF improves alignment and controllability
- Does not fundamentally change base pretraining knowledge

---

## 3. Tool Used: Mental Model Decomposition (Inference-time conditioning analysis)

Used to separate:
- pretraining (representation learning)
- post-training (preference shaping)
- prompting (context-conditioned inference dynamics)

Function:
Helped formalize prompting as representation steering rather than capability creation.