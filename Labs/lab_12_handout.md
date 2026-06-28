# Lab 12 — Model Selection and Internal Validation

**Applied Linear Models I**
**Pairs with:** Lecture 12 (Model Selection and Internal Validation)
**Files:** starter `R/lab_12/lab12.R` · solutions `R/lab_12/lab12_solutions.R`

## Objectives

- Run an **all-subsets** search and rank models by adjusted $R^2$, AIC, BIC, and $C_p$.
- Compare stepwise selections under AIC and BIC penalties.
- Estimate prediction error with **$k$-fold cross-validation** and witness the in-sample **optimism gap**.

## Dataset

`swiss` (47 Swiss provinces, 1888; `Fertility` regressed on five socioeconomic predictors — small enough for exhaustive subset search).

## Exercises and self-check targets

1. **All subsets.** Enumerate the $2^5-1$ non-empty models; report the criterion-optimal model for each. *Target: the criteria largely agree on a four-predictor model (Education + Catholic + Infant.Mortality + Agriculture).*
2. **Stepwise.** Compare AIC- and BIC-stepwise. *Target: both select the same four-predictor model here.*
3. **Cross-validation.** 10-fold CV MSE across nested candidates. *Target: the four-predictor model wins (CV ≈ 57), beating the full five-predictor model (≈ 59).*
4. **Optimism gap.** Tabulate in-sample vs CV MSE. *Target: CV exceeds in-sample for every model; the full model has the lowest in-sample error but not the lowest CV error.*
5. **Mallows' $C_p$.** *Target: the four-predictor model has $C_p\approx k$ (5.03 vs 5), the standard "good model" signal.*

## Deliverable

A reproducible script that selects a model for `swiss` **Fertility** using *at least two* methods (a criterion plus cross-validation) and reports whether they agree. State explicitly why the full model is not the best choice despite its lowest in-sample error — the optimism/over-fitting argument — and name your chosen model with a one-line justification.

## Data-sourcing note

Model selection is most consequential when there are many candidate predictors — exactly the situation in applied work with `WDI` or survey microdata (dozens of potential controls). The all-subsets approach becomes infeasible past ~15 predictors, motivating stepwise, regularization (Lecture 10), and CV. See `data/README.md`. Offline, `swiss` keeps the search exhaustive and transparent.

## Connections forward

Cross-validation here is *internal* (one dataset). **Lecture 13** formalizes *external* validation and the PRESS statistic (leave-one-out CV via the leverage identity). The regularized models of **Lecture 10** are an alternative to discrete selection, and their tuning parameters are chosen by exactly this CV machinery. Selection discipline underlies both capstone projects.
