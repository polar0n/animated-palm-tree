# IRT Imputation Results (Missing-only RMSE & BCE)

This document summarizes the performance of **IRT-based imputation** across different missingness mechanisms and experimental conditions.  
All results are reported as **missing-only metrics**, computed **only on missing cells** for examinees with at least one observed response.

---

## 0. Summary Comparison Table (sorted by BCE on missing cells)

Lower is better.

| Rank_BCE | Scenario         | Group           | MissingRate | RMSE_missing | BCE_missing | Excluded_all_missing | Description                                          |
| -------: | :--------------- | :-------------- | ----------: | -----------: | ----------: | -------------------: | :--------------------------------------------------- |
|        1 | MCAR40           | MCAR rate       |         0.4 |       0.4231 |      0.5321 |                    0 | MCAR, 40% missing                                    |
|        2 | Booklet50_MCAR20 | Extended        |         0.6 |       0.4288 |      0.5447 |                    0 | Planned missingness (booklet) + MCAR20               |
|        3 | NR_simple        | Extended        |         0.6 |       0.4304 |      0.5485 |                    0 | Not-reached (position-based), no speed heterogeneity |
|        4 | MCAR60_mech      | Mechanism @~60% |         0.6 |       0.4307 |      0.5486 |                    0 | MCAR, ~60% missing                                   |
|        5 | MAR60            | Mechanism @~60% |         0.6 |       0.4324 |       0.553 |                    0 | MAR (item-dependent), ~60% missing                   |
|        6 | DIFMCAR60        | Extended        |         0.6 |       0.4354 |       0.557 |                    0 | Uniform DIF on 4 items (Δb=0.6) + MCAR               |
|        7 | GroupMAR60       | Extended        |         0.6 |       0.4371 |      0.5604 |                    0 | Group-specific MAR (MAR-item)                        |
|        8 | NR_speed         | Extended        |         0.6 |       0.4384 |      0.5659 |                   31 | Not-reached + speed heterogeneity                    |
|        9 | MCAR70           | MCAR rate       |         0.7 |       0.4403 |      0.5689 |                    6 | MCAR, 70% missing                                    |
|       10 | DIFMNARth60      | Extended        |         0.6 |       0.4426 |      0.5707 |                   51 | DIF + MNAR-θ                                         |
|       11 | MCAR50           | MCAR rate       |         0.5 |       0.4452 |      0.5792 |                    0 | MCAR, 50% missing                                    |
|       12 | MCAR60           | MCAR rate       |         0.6 |       0.4455 |      0.5797 |                    0 | MCAR, 60% missing                                    |
|       13 | MNAR60           | Mechanism @~60% |         0.6 |       0.4529 |      0.6041 |                   41 | MNAR-θ (ability-dependent), ~60% missing             |
|       14 | MNAR_Y1          | Extended        |         0.6 |       0.4848 |      0.6784 |                    0 | Response-dependent MNAR (γ=1.0)                      |
|       15 | MNAR_Y2          | Extended        |         0.6 |       0.5887 |      1.0065 |                    0 | Response-dependent MNAR (γ=2.0)                      |

---

## 1. Varying Missingness Proportion (MCAR)

| Scenario | MissingRate | RMSE_missing | BCE_missing | Excluded_all_missing | Description       |
| :------- | ----------: | -----------: | ----------: | -------------------: | :---------------- |
| MCAR40   |         0.4 |       0.4231 |      0.5321 |                    0 | MCAR, 40% missing |
| MCAR50   |         0.5 |       0.4452 |      0.5792 |                    0 | MCAR, 50% missing |
| MCAR60   |         0.6 |       0.4455 |      0.5797 |                    0 | MCAR, 60% missing |
| MCAR70   |         0.7 |       0.4403 |      0.5689 |                    6 | MCAR, 70% missing |

**Note.**  
For MCAR70, **6 persons** with 100% missing responses were excluded from evaluation.

---

## 2. Varying Missingness Mechanism (Fixed Missingness ≈ 60%)

| Scenario    | MissingRate | RMSE_missing | BCE_missing | Excluded_all_missing | Description                              |
| :---------- | ----------: | -----------: | ----------: | -------------------: | :--------------------------------------- |
| MCAR60_mech |         0.6 |       0.4307 |      0.5486 |                    0 | MCAR, ~60% missing                       |
| MAR60       |         0.6 |       0.4324 |       0.553 |                    0 | MAR (item-dependent), ~60% missing       |
| MNAR60      |         0.6 |       0.4529 |      0.6041 |                   41 | MNAR-θ (ability-dependent), ~60% missing |

**Note.**  
For MNAR60, **41 persons** with 100% missing responses were excluded from evaluation.

---

## 3. Extended Missingness Scenarios (Fixed Missingness ≈ 60%)

| Scenario         | MissingRate | RMSE_missing | BCE_missing | Excluded_all_missing | Description                                          |
| :--------------- | ----------: | -----------: | ----------: | -------------------: | :--------------------------------------------------- |
| MNAR_Y1          |         0.6 |       0.4848 |      0.6784 |                    0 | Response-dependent MNAR (γ=1.0)                      |
| MNAR_Y2          |         0.6 |       0.5887 |      1.0065 |                    0 | Response-dependent MNAR (γ=2.0)                      |
| NR_simple        |         0.6 |       0.4304 |      0.5485 |                    0 | Not-reached (position-based), no speed heterogeneity |
| NR_speed         |         0.6 |       0.4384 |      0.5659 |                   31 | Not-reached + speed heterogeneity                    |
| Booklet50_MCAR20 |         0.6 |       0.4288 |      0.5447 |                    0 | Planned missingness (booklet) + MCAR20               |
| DIFMCAR60        |         0.6 |       0.4354 |       0.557 |                    0 | Uniform DIF on 4 items (Δb=0.6) + MCAR               |
| DIFMNARth60      |         0.6 |       0.4426 |      0.5707 |                   51 | DIF + MNAR-θ                                         |
| GroupMAR60       |         0.6 |       0.4371 |      0.5604 |                    0 | Group-specific MAR (MAR-item)                        |

**Notes.**

- For **NR_speed**, **31 persons** with 100% missing responses were excluded from evaluation.  
- For **DIFMNARth60**, **51 persons** with 100% missing responses were excluded from evaluation.

---

## 4. Overall Conclusions (short)

- **Ignorable missingness** (MCAR/MAR) stays relatively stable (BCE ~ 0.53–0.58, RMSE ~ 0.42–0.45).
- **MNAR-θ** degrades moderately.
- **MNAR-Y** is hardest:  
  - γ=1.0 → BCE 0.6784  
  - γ=2.0 → BCE 1.0065 (worst)

---

## Methodological Note

- **RMSE (missing-only)** is computed on missing cells only, comparing imputed probabilities to the true binary responses.
- **BCE (missing-only)** is computed as the average Bernoulli negative log-likelihood on missing cells.
- Evaluation excludes examinees with **100% missing responses**, since no IRT ability estimate can be obtained for them.
