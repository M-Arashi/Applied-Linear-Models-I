# Lab 15 — Robust, Nonparametric, and Shrinkage Estimation

**Applied Linear Models I**
**Pairs with:** Lecture 15 (Robust, Nonparametric, Shrinkage)
**Files:** starter `R/lab_15/lab15.R` · solutions `R/lab_15/lab15_solutions.R`

## Objectives

- Fit **robust regression** and see it resist outliers that distort OLS.
- Read robust **weights** as a continuous influence diagnostic.
- Use **loess** for nonlinear relationships and explore the span/bias–variance trade.
- Reproduce **Stein's paradox** — James–Stein shrinkage beating the MLE.

## Datasets

`stackloss` (the textbook robust-regression dataset with well-known outliers) and simulated data for loess and shrinkage.

## Exercises and self-check targets

1. **OLS vs rlm.** Fit both to `stackloss`. *Target: coefficients differ where outliers pull OLS.*
2. **Robust weights.** Inspect `rlm$w`. *Target: the smallest weights flag rows 21, 4, 3, 1 — the classic stackloss outliers.*
3. **Resemblance.** Refit OLS without those four rows. *Target: robust `rlm` (smooth down-weighting) lands near OLS-with-outliers-deleted — robustness without an arbitrary deletion rule.*
4. **loess.** Compare linear vs loess RSS on a nonlinear relationship and vary the span. *Target: loess RSS far below linear; smaller span → lower RSS but more wiggle (bias–variance).*
5. **James–Stein.** Reproduce the shrinkage gain for $p\ge3$. *Target: JS total MSE below the MLE's (~18% gain here).*

## Deliverable

A reproducible script that (i) for `stackloss`, argues whether the robust fit or the OLS fit should be reported and why (connect the robust weights to the influence diagnostics of Lecture 7), and (ii) demonstrates the James–Stein gain and explains, in one paragraph, how it relates to ridge regression — both are biased shrinkage that lowers MSE.

## Data-sourcing note

Robust methods matter most in data prone to recording errors or genuine extreme cases — financial returns, sensor data, survey responses with miscodes. Any real `WDI` or micro-dataset with a few suspect observations is a candidate; compare OLS, robust, and outlier-deleted fits and reason about which to trust. See `data/README.md`. Offline, `stackloss` is the canonical example.

## Connections forward

This session ties together the course's recurring **bias–variance** theme — robust down-weighting (vs Lecture 7's deletion), loess (vs Lecture 9's global polynomials), and James–Stein (vs Lecture 10's ridge). The iteratively-reweighted least squares behind `rlm` is exactly the fitting algorithm for **generalized linear models** in the final session, **Lecture 16**.
