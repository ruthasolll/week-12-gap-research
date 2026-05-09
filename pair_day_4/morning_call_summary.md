 
# Morning Call Summary — Day 4 (Evaluation & Statistics)



During the morning call, Yosef and I interrogated each other's draft questions to narrow them from broad evaluation concerns into specific gaps grounded in our previous systems.

For my question, we clarified that the central issue was not “what is bootstrap resampling” but whether the specific CI reported in `ablation_results.json` could be defended as evidence that the Delta A lift over a strong Delta B baseline was meaningful rather than benchmark noise. We sharpened the focus toward the distinction between what paired bootstrap actually estimates (sampling variance of the mean delta) versus what it cannot detect (systematic LLM judge bias and the spike-at-zero delta distribution produced when 36 of 60 tasks are unchanged). We also clarified that “Delta B” in my framing referred to baseline strength — the prompt-engineered same-backbone baseline — not a separately bootstrapped number, which changed what statistical claims could and could not be made about it.

For Yosef's question, I pushed him to sharpen his question from the general framing of “What does pass@k estimator capture that pass@1 didn't capture in scoring queries answers?” and instead focus on the specific information loss in `score_bench.py`'s current averaging approach — why collapsing five runs into five separate pass@1 numbers makes a query the agent solved once indistinguishable from one it never solved. We refined the scope to the unbiased pass@k estimator from the Codex paper and what it would reveal specifically about the Week 8–9 data-agent-challenge failures: which are high-variance misses the agent can solve under some conditions, and which are consistent capability gaps it never clears.

By the end of the call, both questions were narrowed into concrete, resolvable investigations tied directly to real Week 8–9 and Week 11 artifacts.

## Pair Questions



### Ruth's Question

> In my Week 11 Sales Evaluation Bench, I reported preference accuracy improvements and included paired-bootstrap confidence intervals in `ablation_results.json`, but I cannot defend what those intervals actually mean statistically. Specifically: how does paired bootstrap resampling estimate uncertainty in LLM evaluation benchmarks, what assumptions does it make about independence and sample distribution, and under what conditions can bootstrap confidence intervals become misleading or overconfident for small evaluation sets?

### Yosef's Question

> `score_bench.py` collapses five runs per query into five separate pass@1 numbers, making a query the agent solved once indistinguishable from one it never solved. What does pass@k estimator capture that the per-run average does not — and how would computing it over our five `score.json` files per query reveal which failures are high-variance misses vs. consistent capability gaps, changing what we should try next to improve the agent?

---

# Ruth's Sharpening Process

## Initial Question

The initial version of the question was too broad:

> “How do bootstrap confidence intervals work?”

During discussion, we realized the actual gap was not about textbook bootstrap definitions, but about:
- what the CI in the benchmark *actually estimates*
- what assumptions it silently makes
- and whether the benchmark conclusions are trustworthy at small sample sizes.

We identified several hidden concerns:
- n=60 tasks
- many zero-delta tasks
- judge-model bias
- confusion between significance and deployability

The discussion shifted the question from:
- generic statistics
to
- operational evaluation reliability in LLM benchmarks.

---

## What Changed

The sharpened question became:
- grounded in `ablation_results.json`
- tied to the actual `bootstrap_ci()` implementation
- and focused specifically on:
  - paired resampling
  - uncertainty estimation
  - and overconfidence failure modes.

---

# Yosef's Sharpening Process

## Initial Question

The initial version was:

> “What is the difference between pass@1 and pass@k?”

We realized this was too generic and disconnected from the actual Week 8–9 evaluation pipeline.

After inspecting `scripts/score_bench.py`, we noticed the benchmark:
- evaluates five runs independently
- then reports separate pass@1 values
- without preserving query-level retry behavior.

The key realization was:

> the current evaluation hides the difference between unstable capability and missing capability.

We identified two different failure types:

### High-variance failures
Some runs pass and some fail.

This suggests:
- the capability exists,
- but decoding variability or prompt sensitivity prevents consistency.

### Consistent capability gaps
All runs fail.

This suggests:
- the capability itself is absent.

Per-run averaging collapses both cases into similar-looking pass rates.

---

## What Changed

The sharpened question became:
- grounded in `score_bench.py`
- focused on query-level retry estimation
- and operationally tied to debugging agent reliability.

---

# Why These Gaps Matter

Both questions ultimately concern:
- evaluation reliability,
- interpreting stochastic model behavior,
- and avoiding misleading benchmark conclusions.

Ruth's question focuses on:
- uncertainty estimation and statistical validity.

Yosef's question focuses on:
- retry-aware capability estimation and stochastic failure diagnosis.

Together, both gaps directly affect:
- how FDEs defend benchmark claims,
- debug agent systems,
- and decide what improvements actually matter.