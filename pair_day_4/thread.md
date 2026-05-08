 
# Day 4 Thread — Bootstrap Confidence Intervals in LLM Evaluation

1/ I used paired-bootstrap confidence intervals in my Week 11 Sales Evaluation Bench…

…but realized I could not actually defend what the interval meant statistically.

2/ Bootstrap CI ≠ “95% chance the model is better.”

It means:

“If we repeatedly resampled tasks from this benchmark distribution, the estimated score gap would fall inside this range most of the time.”

3/ My implementation bootstrapped *paired task deltas*:

(fine-tuned score − baseline score)

NOT the two models independently.

That matters because it removes between-task difficulty variance.

4/ Big issue:

36/60 tasks had exactly zero improvement.

That creates a “spike-at-zero” distribution where percentile bootstrap can become overconfident and underestimate uncertainty.

5/ Another important insight:

Bootstrap only measures sampling uncertainty.

It does NOT detect:
- judge-model bias
- benchmark bias
- prompt leakage
- or deployment usefulness

6/ Statistical significance is not the same as product usefulness.

A model can show:
✓ positive CI
✓ low p-value

…and still fail the real deployment requirement.

That was the biggest thing I learned from this evaluation gap.