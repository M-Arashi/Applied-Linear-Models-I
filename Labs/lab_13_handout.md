# Lab 13 — External Validation and PRESS

**Applied Linear Models I**
**Pairs with:** Lecture 13 (External Validation and PRESS)
**Files:** starter `R/lab_13/lab13.R` · solutions `R/lab_13/lab13_solutions.R`

## Objectives

- Compute PRESS via the leverage shortcut and verify it against brute-force LOO.
- Use **predicted $R^2$** and a **held-out test set** to estimate true predictive performance.
- Appreciate the **variability** of a single train/test split.
- Select a model by out-of-sample criteria, not $R^2$.

## Dataset

`MASS::Boston` (506 tracts — large enough for a genuine train/test split and repeated-split experiments).

## Exercises and self-check targets

1. **PRESS shortcut.** On a 60-row subset, confirm `press(fit)` equals a brute-force LOO loop. *Target: exact agreement (≈ 472.24).*
2. **Predicted $R^2$.** Tabulate $R^2$ vs predicted $R^2$ for three nested models. *Target: predicted $R^2$ is just below $R^2$ throughout; both rise with sensible predictors.*
3. **Train/test split.** 70/30 split; report training vs validation $R^2$ and test RMSE. *Target: a train–test gap of ≈ 0.09; RMSE ≈ 5.7 ($1000s).*
4. **Split variability.** 50 random splits. *Target: validation $R^2$ varies widely (sd ≈ 0.05, range ≈ 0.52–0.80) — a single split is a noisy estimate.*
5. **Select by PRESS.** Compare candidate models by PRESS. *Target: the five-predictor model has the lowest PRESS here.*

## Deliverable

A reproducible script that (i) reports PRESS and predicted $R^2$ for a chosen Boston model and interprets the gap from $R^2$, and (ii) demonstrates, via repeated splits, why a single held-out estimate should be reported with caution — and recommends PRESS or $k$-fold CV as the more stable alternative for this sample size.

## Data-sourcing note

External validation is most meaningful across genuinely different conditions — a model fit on one time period or country tested on another. `WDI` panels make this possible: fit on one set of years/countries, validate on a disjoint set, and see whether the relationship **transports**. See `data/README.md`. Offline, random splits of `Boston` illustrate the mechanics.

## Connections forward

PRESS and held-out validation operationalize the over-fitting warnings of **Lecture 12** and the influence diagnostics of **Lecture 7** (high-leverage points dominate PRESS). They are the standard for honestly comparing the models built throughout the course, including the regularized fits of **Lecture 10** and the final **capstone**, whose external-validation component this session directly supports.
