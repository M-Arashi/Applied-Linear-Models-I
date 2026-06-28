# Lab 5 — Bootstrap Inference and Prediction Intervals

**Applied Linear Models I**
**Pairs with:** Lecture 5 (Bootstrap and Prediction)
**Files:** starter `R/lab_05/lab05.R` · solutions `R/lab_05/lab05_solutions.R`

## Objectives

- Compute pairs and residual **bootstrap** confidence intervals and compare to classical ones.
- Use the bootstrap where classical theory is awkward: **heteroskedasticity** and **nonlinear functions** of coefficients.
- Build and contrast confidence and prediction intervals, and see extrapolation inflate them.

## Dataset

`MASS::Boston` (506 census tracts; median home value `medv`, with predictors `lstat` (% lower-status population) and `rm` (rooms)). Boston is a classic **heteroskedastic** dataset, which makes the bootstrap genuinely useful here.

## Exercises and self-check targets

1. **Classical vs pairs bootstrap.** Fit `medv ~ lstat + rm`; compare `confint` to `boot_coef_ci(method="pairs")`. *Target: the intervals broadly agree on direction but the bootstrap is wider for the intercept and `rm`.*
2. **Three standard errors.** Compare classical, HC3 (`robust_se(...)[, "Robust SE"]`), and pairs-bootstrap SEs. *Target: HC3 and bootstrap SEs exceed classical (e.g. `lstat` ≈ 0.065 vs 0.044) — classical inference is over-optimistic under heteroskedasticity.*
3. **Nonlinear function.** Bootstrap a confidence interval for the ratio $\beta_{rm}/\beta_{lstat}$. *Target: a CI obtained directly from resampled refits, with no delta-method algebra.*
4. **Confidence vs prediction.** Compute both at several representative homes. *Target: prediction widths (~22) dwarf confidence widths (~1.5) — the irreducible error term.*
5. **Extrapolation.** Predict at the median `rm` and at an `rm` beyond the observed range. *Target: the out-of-range prediction interval is wider.*

## Deliverable

A reproducible script that (i) presents the three sets of standard errors side by side and states, in words, why the classical ones are too small for Boston, and (ii) reports the bootstrap CI for the coefficient *ratio* in Ex3, explaining why the bootstrap is the natural tool for a nonlinear function of the parameters.

## Data-sourcing note

For a heteroskedasticity-rich economic dataset, income or expenditure data (e.g. from `WDI` or a public household survey) typically show variance growing with the level — an ideal setting to compare classical, robust, and bootstrap inference. See `data/README.md`. Offline, `MASS::Boston` is self-contained.

## Connections forward

The robust-vs-classical SE comparison sets up **Lecture 6** (diagnosing heteroskedasticity) and **Lecture 14** (WLS/GLS as the efficiency-restoring response). Bootstrapping a function of coefficients reappears whenever a quantity of interest — an elasticity ratio, a turning point of a quadratic, a predicted probability in a GLM (Lecture 16) — lacks a clean closed-form standard error.
