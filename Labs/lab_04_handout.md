# Lab 4 — Hypothesis Testing and Confidence Intervals

**Applied Linear Models I**
**Pairs with:** Lecture 4 (Inference I)
**Files:** starter `R/lab_04/lab04.R` · solutions `R/lab_04/lab04_solutions.R`

## Objectives

- Read and interpret individual $t$-tests in a multi-predictor model.
- Compute the overall $F$ and a **multi-restriction partial $F$** by hand and with `anova`.
- Test a **general linear hypothesis** (a linear combination of coefficients) directly.
- Distinguish confidence intervals for a mean from prediction intervals for a new case.

## Dataset

`state.x77` (US states; response `Murder` rate, predictors `Population`, `Illiteracy`, `Income`, `HS.Grad`). Column names are cleaned with `make.names`.

## Exercises and self-check targets

1. **Individual tests.** Fit the four-predictor model and identify which coefficients are individually significant. *Target: `Illiteracy` is strongly significant; `Income` and `HS.Grad` are not, conditional on the others.*
2. **Overall $F$ by hand.** *Target: matches `summary(fit)$fstatistic` exactly; the model is jointly significant.*
3. **Joint partial $F$.** Test `Income` and `HS.Grad` **together** beyond `Population + Illiteracy`. *Target: a 2-df partial $F$; note this differs from running two separate $t$-tests.*
4. **General linear hypothesis.** Test $\beta_{\text{Illiteracy}}+\beta_{\text{HS.Grad}}=0$ with the quadratic-form $F$. *Target: a single-restriction $F$ on $(1,n-p)$ df.*
5. **CI / test duality.** *Target: "CI excludes 0" matches "$p<0.05$" for every coefficient.*
6. **Confidence vs prediction.** Compute both intervals at a new state. *Target: identical center; the prediction interval is several times wider (here ≈ 5.7×) because it carries the irreducible error variance.*

## Deliverable

A reproducible script that (i) states, in words, the substantive conclusion of the joint partial $F$ in Ex3 (do income and education *together* explain murder rates beyond population and illiteracy?), and (ii) explains why the prediction interval in Ex6 is so much wider than the confidence interval, in terms of what each interval is about.

## Data-sourcing note

For a richer inference exercise, pull a cross-country panel from `WDI` and test a substantive joint hypothesis (e.g. that two governance indicators jointly predict an outcome). See `data/README.md`. Offline, `state.x77` is self-contained.

## Connections forward

The joint-test logic underlies **model selection** (Lecture 12), where comparing nested models is the basic move. The confidence-vs-prediction distinction is developed fully in **Lecture 5** (bootstrap and prediction). The general-linear-hypothesis machinery reappears whenever we test equality of slopes across groups — the **ANCOVA** tests of Lecture 11.
