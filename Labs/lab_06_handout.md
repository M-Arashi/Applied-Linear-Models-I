# Lab 6 — A Full Residual-Diagnostic Workflow

**Applied Linear Models I**
**Pairs with:** Lecture 6 (Assumptions and Diagnostics)
**Files:** starter `R/lab_06/lab06.R` · solutions `R/lab_06/lab06_solutions.R`

## Objectives

- Run the complete diagnostic battery — linearity, homoskedasticity, normality — on real models.
- Implement a **Breusch–Pagan** test and a **curvature** test from scratch.
- Choose and apply a remedy (transformation; robust SEs) and **re-diagnose** to confirm it helped.

## Datasets

`trees` (timber volume — curvature and variance that logs fix) and `mtcars` (the diagnostic battery, plus curvature in `wt`).

## Exercises and self-check targets

1. **Naive model + diagnostics.** Fit `Volume ~ Girth + Height`; report adjusted $R^2$, the curvature-test $p$, and Breusch–Pagan. *Target: detectable curvature ($p\approx0.0006$) and mild heteroskedasticity.*
2. **Log–log remedy.** Refit on the log scale and re-diagnose. *Target: curvature $p$ rises sharply and adjusted $R^2$ improves — the multiplicative model is better specified.*
3. **Normality.** QQ correlation for both models. *Target: residuals are close to normal; the log model is at least as good.*
4. **mtcars battery.** Fit `mpg ~ wt + hp + disp`; run curvature, Breusch–Pagan, and classical-vs-HC3 SEs. *Target: some curvature and mild heteroskedasticity; HC3 SEs slightly exceed classical.*
5. **Curvature in `wt`.** Compare `mpg ~ wt` to `mpg ~ wt + wt²`. *Target: significant curvature ($p\approx0.003$); the quadratic lifts adjusted $R^2$ from 0.745 to 0.807.*

## Deliverable

A reproducible "diagnostic report" for **one** model: state each assumption, show the plot or test that interrogates it, declare a verdict (pass/fail), and — for any failure — apply a remedy and re-run the relevant diagnostic to demonstrate improvement. The emphasis is on *reading and acting on* diagnostics, not producing them mechanically.

## Data-sourcing note

Real economic data routinely violate the constant-variance and linearity assumptions (income, expenditure, firm size). A good extension diagnoses a `WDI`-sourced model and applies a Box–Cox or log transform. See `data/README.md`. Offline, `trees` and `mtcars` give clear, fixable violations.

## Connections forward

The curvature you remedy here is the explicit subject of **Lecture 9** (polynomial and interaction models). The heteroskedasticity remedies (robust SEs now, WLS/GLS for efficiency) are developed in **Lecture 14**. Diagnostics that flag *individual* problem points — rather than whole-model violations — are the focus of the next session, **Lecture 7** (outliers, leverage, and influence).
