# Lab 2 — Functional Form: Linear, Transformed, and Nonlinear Models

**Applied Linear Models I**
**Pairs with:** Lecture 2 (Linear vs Nonlinear Models)
**Files:** starter `R/lab_02/lab02.R` · solutions `R/lab_02/lab02_solutions.R`

## Objectives

- Decide when a relationship needs a nonlinear term, a transformation, or a genuinely nonlinear model.
- Use residual plots to **detect misspecified functional form** rather than trusting $R^2$.
- Interpret log–log exponents as elasticities / geometric scaling.
- Fit and compare exponential and logistic growth with `nls`.

## Datasets (all built-in — no internet needed)

| Dataset | Response | Use |
|---|---|---|
| `cars` | stopping distance | linear vs quadratic (physics: distance ∝ speed²) |
| `trees` | timber volume | log–log scaling (geometry: V ∝ girth²·height) |
| `uspop` | US population 1790–1970 | exponential vs logistic growth |

## Exercises and self-check targets

1. **Linear vs quadratic (cars).** Fit `dist ~ speed` and `dist ~ poly(speed, 2)`; compare $R^2$ and AIC and run the partial $F$-test. *Target: the quadratic AIC is lower; the quadratic term is at least marginally supported, and it is theoretically motivated by kinetic energy.*
2. **Functional-form diagnostics.** Examine residuals-vs-fitted for the linear fit; test for leftover curvature. *Target: detectable curvature confirms the linear mean function is incomplete.*
3. **Log–log volume (trees).** Fit `log(Volume) ~ log(Girth) + log(Height)` and test whether the girth exponent equals 2. *Target: girth exponent ≈ 1.98, height exponent ≈ 1.12 — matching cylinder geometry; the test of "exponent = 2" is not rejected.*
4. **Additive vs multiplicative (trees).** Compare the additive model to the log–log model on the **original scale** via back-transformed SSE. *Target: the multiplicative model has lower original-scale SSE (~181 vs ~422) and stabilizes the variance.*
5. **Exponential growth (uspop).** Fit linearized OLS and direct `nls`; convert to %/decade. *Target: growth of ~1.6–2.2% per decade, with a note that pure exponential overpredicts late-century population.*
6. **Challenge — logistic growth (uspop).** Fit `nls(pop ~ SSlogis(...))`; compare SSE to the exponential fit and report the carrying capacity. *Target: logistic SSE (~277) far below exponential SSE (~1087); estimated asymptote ≈ 316 million.*

## Deliverable

A short reproducible script (or R Markdown) that, for **one** of the three relationships, argues from residual diagnostics and a model comparison which functional form is appropriate, and interprets the chosen model's parameters substantively (an elasticity, a growth rate, or a carrying capacity). One figure required.

## Data-sourcing note

To extend beyond built-ins: real growth/elasticity questions are abundant in World Bank data (`WDI`) — e.g. GDP per capita over time (exponential-ish), or a log–log demand relationship between quantity and price. See `data/README.md` for `WDI::WDI()` usage. For offline work, `uspop`, `trees`, and `cars` are sufficient.

## Connections forward

The curvature diagnostics here return in **Lecture 6** (assumption checking) and **Lecture 9** (polynomial and interaction models). The variance-stabilizing role of the log transform previews **Lecture 14** (weighted/generalized least squares), and the multiplicative-error discussion sets up the link-function idea in **Lecture 16** (GLMs).
