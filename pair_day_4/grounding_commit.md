 
# Grounding Commit — Day 4

After the explainer, I updated the evaluation interpretation section of my Week 11 benchmark notes to distinguish:

- statistical significance
- sampling uncertainty
- judge-model bias
- and deployment usefulness

Specifically, I added:
- clarification that the paired-bootstrap CI only estimates sampling variance
- a warning that n=60 and the spike-at-zero delta distribution may make the percentile bootstrap overconfident
- and a note that the 0% structured-output pass rate remains operationally important despite the positive CI

This changed how I interpret and communicate evaluation results in the benchmark.

Artifact updated:
- `final_training_report.md`
- `ablation_results.json` interpretation notes