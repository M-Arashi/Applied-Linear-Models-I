# Lab 9 — Polynomial and Interaction Models

**Applied Linear Models I**
**Pairs with:** Lecture 9 (Polynomial and Interaction Models)
**Files:** starter `R/lab_09/lab09.R` · solutions `R/lab_09/lab09_solutions.R`

## Objectives

- Select a polynomial degree with nested $F$-tests and adjusted $R^2$.
- Confirm raw and orthogonal polynomials give the same fit but different collinearity.
- Specify and **interpret** quantitative×quantitative and quantitative×qualitative interactions.
- Use **centering** to control interaction collinearity, and respect **marginality**.

## Datasets

`trees` (polynomial), `mtcars` (interaction + centering + marginality), `iris` (qualitative interaction / ANCOVA preview).

## Exercises and self-check targets

1. **Degree selection (trees).** Nested $F$-tests for degree 1→2→3 of `Volume ~ Girth`. *Target: the quadratic is a clear win (volume ∝ girth²); the cubic adds little.*
2. **Raw vs orthogonal.** *Target: identical fitted values; raw `Girth` and `Girth²` are highly correlated.*
3. **Interaction (mtcars).** `mpg ~ hp * wt`; report $\partial(\text{mpg})/\partial(\text{hp})$ at light/medium/heavy cars. *Target: the horsepower penalty on mpg varies with weight.*
4. **Centering.** Compare interaction VIFs centered vs uncentered. *Target: VIFs collapse from the 10–43 range to ~1–2; the fit is unchanged.*
5. **Qualitative interaction (iris).** Test `Petal.Length * Species` against the parallel-slopes model. *Target: the interaction is **not** significant ($p\approx0.19$) — a common slope with species intercepts suffices; the same machinery becomes full ANCOVA in Lecture 11.*
6. **Marginality.** Drop the `wt` main effect from the interaction model. *Target: adjusted $R^2$ falls (0.872 → 0.693) — keep lower-order terms.*

## Deliverable

A reproducible script that (i) reports and interprets the changing slope in the Ex3 interaction (does horsepower matter more for light or heavy cars?), and (ii) shows the VIF collapse from centering, explaining why centering is the right first move whenever interactions or polynomials are present.

## Data-sourcing note

Interactions are central to applied economics — returns to education differing by experience, policy effects differing by group. A `WDI` panel or a public micro-dataset offers rich interaction questions. See `data/README.md`. Offline, `mtcars`, `trees`, and `iris` are self-contained.

## Connections forward

The collinearity that interactions and polynomials create — only partly cured by centering — is the explicit subject of **Lecture 10** (detection and ridge/PCR remedies). The qualitative interaction previewed here is developed into full **ANCOVA** in **Lecture 11**. Degree/term selection connects to **Lecture 12** (model selection and cross-validation).
