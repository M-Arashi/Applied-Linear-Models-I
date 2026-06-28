# Lab 8 — Standardized and No-Intercept Models

**Applied Linear Models I**
**Pairs with:** Lecture 8 (Standardized and No-Intercept Models)
**Files:** starter `R/lab_08/lab08.R` · solutions `R/lab_08/lab08_solutions.R`
**Note:** the **midterm** follows this session (covers Lectures 1–8).

## Objectives

- Compute and interpret standardized (beta) coefficients and rank predictor importance.
- Verify the scaling identity and the simple-regression "beta = correlation" fact.
- See that standardized coefficients depend on **sampled range** — a caution for importance claims.
- Fit and critique a **no-intercept** model.

## Datasets

`swiss` (importance ranking) and `cars` (a physically motivated through-origin model).

## Exercises and self-check targets

1. **Standardized importance.** Standardize `swiss` and rank predictors by $|\beta^*|$. *Target: a clean ranking on a common per-SD scale.*
2. **Scaling identity.** Verify $\beta_j^*=\beta_j\,(s_{x_j}/s_y)$ and that the standardized intercept is ≈ 0. *Target: machine-precision agreement.*
3. **Beta = correlation.** In simple regression `Fertility ~ Education`, the standardized slope equals $r$. *Target: both ≈ −0.664.*
4. **Range artifact.** Restrict the `Education` range and re-standardize. *Target: the standardized slope shrinks (−0.66 → −0.27) although the relationship is unchanged — beware comparing $\beta^*$ across samples with different ranges.*
5. **No-intercept.** Fit `dist ~ speed - 1` on `cars`; compare to the intercept model and inspect the residual sum. *Target: residuals do **not** sum to zero; the data actually give a significant (negative) intercept, illustrating that the linear form is imperfect (distance ∝ speed²) and that theory and data can disagree.*

## Deliverable

A reproducible script that (i) presents the standardized importance ranking for `swiss` with a one-sentence interpretation of the top predictor, and (ii) takes a clear position on the `cars` no-intercept model — does the physical argument (zero distance at zero speed) justify dropping the intercept, given that the data prefer one? Defend your answer.

## Data-sourcing note

Standardized coefficients are common in applied economics and social science for comparing the relative importance of predictors measured in different units (e.g. income in dollars vs years of education vs an index). A `WDI`-sourced cross-country model is a natural extension. See `data/README.md`. Offline, `swiss` and `cars` are self-contained.

## Connections forward

Standardization and centering reduce the collinearity that interaction and polynomial terms create — the subject of **Lectures 9–10**. The importance-ranking caution returns whenever coefficients are interpreted comparatively, including in **model selection** (Lecture 12). This session closes the midterm material; the second half opens with **Lecture 9** (polynomial and interaction models).
