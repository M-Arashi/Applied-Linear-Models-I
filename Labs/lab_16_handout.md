# Lab 16 — Generalized Linear Models

**Applied Linear Models I**
**Pairs with:** Lecture 16 (Generalized Linear Models)
**Files:** starter `R/lab_16/lab16.R` · solutions `R/lab_16/lab16_solutions.R`
**Note:** the **final exam** follows this session (whole course, emphasis on Lectures 9–16).

## Objectives

- Fit **logistic regression** and interpret odds ratios and predicted probabilities.
- Compare **logit and probit**.
- Fit **Poisson regression** and interpret rate ratios.
- Detect **overdispersion** and remedy it with quasi-Poisson and negative binomial models.

## Datasets

`mtcars` (binary `am`), `warpbreaks` (counts of breaks).

## Exercises and self-check targets

1. **Logistic.** `am ~ wt + hp`; report odds ratios. *Target: heavier cars have sharply lower odds of being manual.*
2. **Probabilities.** Predicted $P(\text{manual})$ for a light and a heavy car; classification accuracy at 0.5. *Target: high accuracy; light cars predicted manual, heavy cars automatic.*
3. **Logit vs probit.** *Target: fitted probabilities correlate > 0.999; the logit/probit coefficient ratio is ≈ 1.78.*
4. **Poisson.** `breaks ~ wool + tension`; report rate ratios. *Target: high tension multiplies the break rate by ≈ 0.60 vs low tension.*
5. **Overdispersion.** Dispersion estimate; quasi-Poisson and negative binomial. *Target: dispersion ≈ 4.3; quasi-Poisson SEs roughly double the Poisson SEs; the negative-binomial AIC (≈ 409) is far below the Poisson AIC (≈ 493).*

## Deliverable

A reproducible script that (i) reports and interprets one odds ratio (logistic) and one rate ratio (Poisson) in plain language, and (ii) diagnoses overdispersion in the `warpbreaks` Poisson model and recommends a remedy, explaining why ignoring overdispersion would overstate significance.

## Data-sourcing note

GLM outcomes are everywhere in applied work: loan default (binary), insurance claim counts (Poisson with an exposure offset), doctor visits, citations. Public datasets — `MASS::Insurance` (claims with exposure), survey microdata, or `WDI` count indicators — let you practice offsets and overdispersion on real data. See `data/README.md`. Offline, `mtcars` and `warpbreaks` cover the binary and count cases.

## Connections back across the course

GLMs reuse nearly everything: the design matrix and linear predictor (Lecture 1–3), nested-model tests as deviance/likelihood-ratio tests (Lecture 4), diagnostics and overdispersion as the count analogue of heteroskedasticity (Lectures 6, 14), AIC-based selection (Lecture 12), and the IRLS algorithm shared with robust regression (Lecture 15). The linear model is one GLM among many — a fitting close to the course and a bridge to everything that follows.
