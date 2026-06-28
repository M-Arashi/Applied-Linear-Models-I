# Lab 14 — Weighted and Generalized Least Squares

**Applied Linear Models I**
**Pairs with:** Lecture 14 (WLS and GLS)
**Files:** starter `R/lab_14/lab14.R` · solutions `R/lab_14/lab14_solutions.R`

## Objectives

- Detect heteroskedasticity and respond with **feasible GLS**.
- Compute the WLS estimator from the matrix formula and reconcile with `lm(weights=)`.
- Compare classical, robust (HC3), and WLS standard errors.
- Quantify the **efficiency gain** of correct weighting.

## Datasets

`cars` (stopping distance — variance grows with speed) and simulated data with a known variance function.

## Exercises and self-check targets

1. **Detect.** Breusch–Pagan on `dist ~ speed`. *Target: significant heteroskedasticity — variance rises with speed.*
2. **FGLS.** Model `log(resid²)` on speed, form weights, refit. *Target: FGLS coefficients shift modestly as noisy high-speed points are down-weighted.*
3. **Three SEs.** Classical vs HC3 vs FGLS. *Target: classical SEs are the smallest (over-optimistic); HC3 corrects inference; FGLS re-weights for efficiency.*
4. **WLS by hand.** With known weights $w_i=1/(0.5x_i)^2$, confirm $(\mathbf{X}^\top\mathbf{W}\mathbf{X})^{-1}\mathbf{X}^\top\mathbf{W}\mathbf{y}$ equals `lm(weights=)`. *Target: machine-precision match.*
5. **Efficiency.** Compare OLS vs WLS slope variance over many simulations. *Target: WLS variance is ~35% smaller — both unbiased.*

## Deliverable

A reproducible script that, for the `cars` data, (i) documents the heteroskedasticity and the FGLS response, and (ii) presents the three sets of standard errors with a one-paragraph recommendation: when would you prefer FGLS, and when OLS with robust standard errors? Tie the answer to whether you trust your variance model.

## Data-sourcing note

Heteroskedasticity is the rule in cross-sectional economic data (variance of spending, wages, or firm outcomes rising with scale) and aggregated data (group averages with different group sizes — a natural source of *known* weights $\propto n_g$). A grouped `WDI` indicator or survey aggregate gives a clean WLS exercise with defensible weights. See `data/README.md`. Offline, `cars` and the simulation suffice.

## Connections forward

WLS/GLS complete the response to the diagnostics of **Lecture 6**: detect non-constant variance there, fix it efficiently here (or use the robust SEs of Lecture 6 / bootstrap of Lecture 5 for inference without a variance model). The down-weighting idea generalizes to **robust regression** in **Lecture 15**, where weights respond to *outliers* rather than to known variances, and the iteratively-reweighted scheme reappears in **Lecture 16** (GLMs).
