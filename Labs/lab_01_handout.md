# Lab 1 — Matrix Mechanics & First Diagnostics

**Applied Linear Models I** · Lab 1 of 16 (pairs with Lecture 1)

**Duration:** 60 minutes · **Files:** starter `R/lab_01/lab01.R`, solutions `R/lab_01/lab01_solutions.R`

## Goals

You will (1) build the OLS estimator from matrix first principles and verify it against `lm()`, (2) confirm the projection properties of the hat matrix on real data, and (3) run a first round of collinearity and leverage diagnostics — the workflow you will reuse in every later lab. Work the starter script; the targets below let you self-check before consulting the solutions.

## Datasets (both built into R — no download needed)

- **`LifeCycleSavings`** — 50 countries, 1960–1970. Aggregate personal **savings rate** `sr` modelled on demographics (`pop15`, `pop75`), income `dpi`, and growth `ddpi`. This operationalizes the Modigliani life-cycle hypothesis and is a clean small economics dataset.
- **`longley`** — 16 annual U.S. macro observations. The textbook example of **severe multicollinearity** (GNP, Population, and Year all trend together).

```r
data(LifeCycleSavings)   # ?LifeCycleSavings for the codebook
data(longley)
```

## Exercises

**1 — OLS by hand.** Build the model matrix `X` for `sr ~ pop15 + pop75 + dpi + ddpi`. Form `X'X` and `X'y`, solve the normal equations, and compare to `lm()`.
*Target:* intercept ≈ 28.566, `pop15` ≈ −0.461, `pop75` ≈ −1.691, `dpi` ≈ −0.000337, `ddpi` ≈ 0.410; agreement with `lm()` to 1e-8.

**2 — Hat matrix.** Compute `H = X(X'X)⁻¹X'`. Verify it is symmetric, idempotent, and that `trace(H) = p`. Confirm `X'e = 0`. Recover `σ̂ = sqrt(SSE/(n−p))`.
*Target:* all three properties `TRUE`; `trace(H) = 5`; `max|X'e|` ≈ 1e-9; `σ̂` ≈ 3.803.

**3 — Leverage screen.** Extract the leverages `diag(H)` and flag points with `hᵢᵢ > 2p/n`. Which countries are unusual in predictor space?
*Target (threshold 0.20):* Libya (0.531), United States (0.334), Japan (0.223), Ireland (0.212).

**4 — Frisch–Waugh–Lovell.** Residualize `sr` and `ddpi` on `(pop15 + pop75 + dpi)`, regress the residualized response on the residualized predictor, and confirm the slope equals the full-model `ddpi` coefficient.
*Target:* both equal 0.40969 (to 8 decimals).

**5 — Collinearity diagnostics.** Compute `vif_manual()` and `condition_number()` for both models.
*Target:* `LifeCycleSavings` — all VIFs < 7, κ ≈ 5.4 (mild). `longley` — GNP VIF ≈ 1034, Year ≈ 733, κ ≈ 81 (severe).

**6 — Remediation preview.** Refit `longley` dropping the worst offender (`GNP`). Compare the remaining standard errors with vs. without GNP, and re-check VIFs.
*Target:* SEs shrink (e.g. `Year` SE 0.43 → 0.18). **But** Population and Year VIFs stay large (≈112, ≈124). Discuss: dropping one variable relieves but does not cure *structural* collinearity among trending macro series — full remedies (centering, ridge, principal-components regression) come in Lectures 5–6.

## Deliverable

Submit your completed `lab01.R` plus a short (½-page) write-up answering: *Which `LifeCycleSavings` observations are influential, and does removing Libya change the conclusions? Why did dropping GNP help longley only partially?*

## Connections

Leverage → outlier/influence diagnostics (Lecture 3). VIF and condition number → collinearity remediation (Lectures 5–6). FWL → added-variable plots (later labs). The `boot_coef_ci()` helper you saw load will be used for bootstrap confidence intervals in Lab 3.
