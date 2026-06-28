# Lab 3 — OLS Mechanics, Standard Errors, and Omitted-Variable Bias

**Applied Linear Models I**
**Pairs with:** Lecture 3 (OLS and Gauss–Markov)
**Files:** starter `R/lab_03/lab03.R` · solutions `R/lab_03/lab03_solutions.R`

## Objectives

- Compute OLS coefficients and standard errors **from the matrix formulas** and reconcile with `lm`.
- See **omitted-variable bias** concretely and predict its direction and size from the bias formula.
- Build confidence intervals by hand.
- Confirm the **efficiency** half of Gauss–Markov by simulation.

## Datasets

`mtcars` (fuel economy: `mpg`, `wt`, `hp`) and, for extension, `swiss`.

## Exercises and self-check targets

1. **OLS by hand.** Form $\mathbf{X}=[\mathbf{1}\ \text{wt}\ \text{hp}]$ and compute $\hat{\boldsymbol\beta}=(\mathbf{X}^\top\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{y}$; compare to `lm(mpg ~ wt + hp)`. *Target: agreement to $\sim10^{-9}$.*
2. **Standard errors by hand.** $\hat\sigma^2=\text{SSE}/(n-p)$, $\widehat{\operatorname{Var}}(\hat{\boldsymbol\beta})=\hat\sigma^2(\mathbf{X}^\top\mathbf{X})^{-1}$. *Target: SEs match `lm` to $\sim10^{-8}$; residual SE ≈ 2.59 on 29 df.*
3. **Omitted-variable bias.** Compare the `wt` coefficient with and without `hp`, then reproduce the shift via $\text{bias}=\hat\beta_{hp}\times(\text{slope of hp on wt})$. *Target: the `wt` coefficient moves from −3.88 (full) to −5.34 (short), exactly the predicted bias of −1.47.*
4. **Confidence intervals.** $\hat\beta_j\pm t_{n-p,.975}\,\widehat{\text{SE}}$; check against `confint`. *Target: exact match.*
5. **Efficiency.** Simulate homoskedastic data and compare the OLS slope's Monte Carlo variance to a mismatched-weight (arbitrary WLS) estimator. *Target: both unbiased; OLS variance smaller — Gauss–Markov.*

## Deliverable

A reproducible script that (i) reports the hand-computed vs `lm` coefficients and SEs for one model, and (ii) demonstrates and *explains* the omitted-variable bias in words, naming which direction the bias goes and why (sign of the omitted variable's effect × its correlation with the included regressor).

## Data-sourcing note

Omitted-variable bias is the central threat to interpreting observational regressions. A good extension uses World Bank data (`WDI`) to regress, say, life expectancy on GDP per capita with and without an education or health-spending control, and to reason about the resulting shift. See `data/README.md`. Offline, `mtcars` and `swiss` suffice.

## Connections forward

The standard-error machinery feeds directly into **Lecture 4** (testing and CIs). Omitted-variable bias motivates the diagnostics of **Lectures 6–7** and the model-selection caution of **Lecture 12**. The efficiency comparison previews **Lecture 14**, where matching weights to the *true* variance structure (WLS/GLS) restores efficiency under heteroskedasticity.
