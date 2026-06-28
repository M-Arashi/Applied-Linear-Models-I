# Lab 10 — Multicollinearity: Detection and Remedies

**Applied Linear Models I**
**Pairs with:** Lecture 10 (Multicollinearity)
**Files:** starter `R/lab_10/lab10.R` · solutions `R/lab_10/lab10_solutions.R`

## Objectives

- Diagnose multicollinearity with VIFs and the condition number.
- Witness coefficient **instability** firsthand.
- Apply **ridge regression** (GCV-tuned) and **principal-components regression**.
- Confirm the **bias–variance trade-off** improves out-of-sample prediction.

## Datasets

`longley` (the textbook severe-collinearity dataset — six macroeconomic series that all trend with time) and simulated collinear data for the prediction experiment.

## Exercises and self-check targets

1. **Detection.** VIFs and condition number for the full `longley` model. *Target: GNP's VIF > 1000, condition number ≈ 81; GNP/Year/Population are the worst.*
2. **Instability.** Compare the `Population` coefficient with and without `GNP`. *Target: a large shift — collinear predictors borrow each other's variance.*
3. **Ridge.** GCV-tuned `lm.ridge`; compare to OLS. *Target: ridge coefficients are pulled in from the wild OLS values.*
4. **PCR.** Cumulative $R^2$ by number of components. *Target: 3 components reach $R^2\approx0.98$; the first 2 PCs hold ~96% of predictor variance.*
5. **Bias–variance.** Simulate two correlated predictors; compare OLS vs ridge test MSE. *Target: ridge has lower test MSE.*

## Deliverable

A reproducible script that (i) presents the collinearity diagnosis for `longley` and names the offending predictors with a one-line economic explanation (they all grow with time), and (ii) reports a ridge or PCR remedy and states honestly what it does and does not accomplish — stabilized estimation, but not the recovery of separable individual effects.

## Data-sourcing note

Macroeconomic time series (GDP, population, employment) are collinear almost by construction, making `WDI` single-country time series a natural source for collinearity exercises — with the caveat that time series also need the autocorrelation tools of Lecture 14. See `data/README.md`. Offline, `longley` is the canonical example.

## Connections forward

The bias-for-variance trade is the same idea as **shrinkage/Stein estimation** in **Lecture 15**. The decision of how many components or how much shrinkage to use is a **model-selection** problem (Lecture 12), properly resolved by **validation** (Lecture 13). Centering as a partial collinearity remedy was introduced in Lecture 9.
