# Lab 11 — Qualitative Predictors and ANCOVA

**Applied Linear Models I**
**Pairs with:** Lecture 11 (Qualitative Predictors and ANCOVA)
**Files:** starter `R/lab_11/lab11.R` · solutions `R/lab_11/lab11_solutions.R`

## Objectives

- Encode and interpret dummy variables, including multi-level factors.
- Fit ANCOVA in both parallel-lines and separate-slopes forms.
- Test **equal slopes** and a **single common line** with partial $F$-tests.
- See that a factor-only regression is one-way ANOVA.

## Datasets

`mtcars` (transmission, cylinders), `iris` (species), `chickwts` (feed type).

## Exercises and self-check targets

1. **Dummy coding.** `mpg ~ factor(cyl)`; interpret relative to the 4-cylinder baseline. *Target: each coefficient is a group-mean difference from the baseline.*
2. **Parallel ANCOVA.** `mpg ~ hp + factor(am)`; interpret the transmission intercept shift. *Target: manual cars sit a fixed mpg above automatics at every horsepower.*
3. **Separate slopes.** `mpg ~ hp * factor(am)`; report both hp-slopes and test equality. *Target: the two slopes and a partial $F$ for the interaction.*
4. **Common line.** Test whether transmission matters at all. *Target: a joint $F$ against the `mpg ~ hp` model.*
5. **Multi-level joint test (iris).** Test `Species` as a whole. *Target: the joint $F$ is decisive ($p\approx6\times10^{-13}$); the individual $t$'s only compare to the baseline.*
6. **Factor-only = ANOVA.** `weight ~ feed` on `chickwts`. *Target: `summary(lm)` $F$ equals the `aov` $F$ exactly (15.37).*

## Deliverable

A reproducible script that, for the `mtcars` transmission analysis, (i) reports whether the parallel-lines or separate-slopes model is warranted (with the test that decides it), and (ii) if slopes differ, explains why there is then no single "manual vs automatic" mpg effect — it depends on horsepower. Include the two fitted lines in one figure.

## Data-sourcing note

ANCOVA is ubiquitous in program evaluation and applied micro: an outcome regressed on a continuous covariate and a treatment/group indicator, testing whether the treatment effect varies with the covariate. A public micro-dataset or `WDI` panel with a region/income-group factor extends this naturally. See `data/README.md`. Offline, `mtcars`, `iris`, and `chickwts` suffice.

## Connections forward

The decision between parallel and separate slopes is a **model-selection** question (Lecture 12), and the joint-$F$ logic underlies all nested-model comparison. ANCOVA's group-specific lines are exactly the interactions of Lecture 9 with a qualitative variable, and they figure in the **final capstone**, which requires a properly handled categorical predictor.
