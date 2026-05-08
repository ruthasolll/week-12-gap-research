 
In my Week 11 Sales Evaluation Bench, I reported preference accuracy improvements and included paired-bootstrap confidence intervals in `ablation_results.json`, but I cannot defend what those intervals actually mean statistically. Specifically: how does paired bootstrap resampling estimate uncertainty in LLM evaluation benchmarks, what assumptions does it make about independence and sample distribution, and under what conditions can bootstrap confidence intervals become misleading or overconfident for small evaluation sets?

Grounding:
Closing this gap would let me justify whether my reported “Delta B” improvements are statistically meaningful or just variance from a small benchmark slice, and improve how I report confidence in future model evaluations.