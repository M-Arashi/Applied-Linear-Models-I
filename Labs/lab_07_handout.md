# Lab 7 — Leverage, Outliers, and Influence

**Applied Linear Models I**
**Pairs with:** Lecture 7 (Outliers, Leverage, Influence)
**Files:** starter `R/lab_07/lab07.R` · solutions `R/lab_07/lab07_solutions.R`

## Objectives

- Compute leverage, studentized deleted residuals, Cook's distance, and DFBETAS, and apply the standard cutoffs.
- See that leverage, outlyingness, and influence rank points **differently**.
- **Construct** points that isolate each component, proving influence requires both leverage and outlyingness.

## Datasets

`mtcars` (interpretable cases — students can name the influential cars) and constructed data for the isolation experiments.

## Exercises and self-check targets

1. **Leverage.** Fit `mpg ~ wt + hp`; flag high-leverage cars ($h>2p/n$) and confirm $\sum h_{ii}=p$. *Target: Maserati Bora and Lincoln Continental are high-leverage.*
2. **Outliers.** Studentized deleted residuals vs the Bonferroni cutoff. *Target: Toyota Corolla and Chrysler Imperial are the largest; none exceeds the (strict) Bonferroni bar.*
3. **Influence.** Cook's distance and DFBETAS for `wt`. *Target: Chrysler Imperial has the largest Cook's D (≈0.42) and the largest DFBETAS for `wt` (≈0.94).*
4. **Divergent rankings.** Build the top-3 table under each diagnostic. *Target: the leaders differ — Maserati Bora (leverage), Toyota Corolla (outlier), Chrysler Imperial (influence).*
5. **Isolate outlyingness.** Add a large $y$-outlier at the **center** of $x$. *Target: studentized residual ≈ 9 but Cook's D small — a big residual at average leverage barely moves the fit.*
6. **Isolate leverage.** Add a high-leverage point **on** the line. *Target: leverage ≈ 0.56 but tiny residual and small Cook's D — leverage alone is harmless.*

## Deliverable

A reproducible "influence report" for one model that (i) presents the divergent top-3 rankings and explains, for one specific point, why it is or is not influential, and (ii) demonstrates with the two constructed examples that influence is the *product* of leverage and outlyingness — and states the practical implication for how to treat flagged points.

## Data-sourcing note

Cross-country economic panels almost always contain a few influential outliers (resource economies, city-states, crisis years). A good extension reproduces the Libya-style analysis on `WDI` data and reasons about whether the influential country belongs in the model. See `data/README.md`. Offline, `mtcars` and the constructed data suffice.

## Connections forward

The decision of how to treat an influential point — investigate, down-weight, or respecify — leads directly to **robust regression** in **Lecture 15**. Influence diagnostics also guard **model selection** (Lecture 12) and **validation** (Lecture 13): a model whose performance hinges on one observation will not generalize.
