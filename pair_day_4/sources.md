

# Sources — Day 4

## Canonical Sources

1. Efron, Bradley & Tibshirani, Robert (1993)
   *An Introduction to the Bootstrap*
   Chapman & Hall/CRC

   Why it mattered:
   - Canonical reference for bootstrap resampling
   - Explains percentile bootstrap confidence intervals
   - Covers assumptions and undercoverage behavior

---

2. Dror, Rotem et al. (2018)
   *Deep Dominance: How to Properly Compare Deep Neural Models*
   ACL 2018
   https://aclanthology.org/P18-1128/

   Why it mattered:
   - Shows statistical testing pitfalls in NLP evaluation
   - Demonstrates bootstrap reliability issues for small evaluation sets
   - Motivated the discussion around n=60 limitations and permutation testing

---

## Tool / Artifact Used

3. Week 11 Evaluation Artifact:
   `ablations/run_ablation_analysis.py`

   Specifically:
   - `bootstrap_ci()`
   - `paired_sign_flip_p_value()`

   Why it mattered:
   - Allowed direct inspection of the exact bootstrap implementation used in the benchmark
   - Made the explainer grounded in the real evaluation pipeline rather than generic theory