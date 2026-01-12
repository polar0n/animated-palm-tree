# IRT Imputation Results (RMSE on Missing Cells)

This document summarizes the performance of **IRT-based imputation** across different missingness mechanisms and experimental conditions.  
All results are reported as **RMSE on missing cells**.

---

## 1. Varying Missingness Proportion (MCAR)

| Missingness Mechanism | Missing Rate | IRT RMSE |
| --------------------- | ------------ | -------- |
| MCAR                  | 40%          | 0.4231   |
| MCAR                  | 50%          | 0.4452   |
| MCAR                  | 60%          | 0.4455   |
| MCAR                  | 70%          | 0.4403   |

**Note.**  
For MCAR70, a small number of examinees exhibit 100% missing responses. RMSE values may depend on exclusion rules for such cases.

---

## 2. Varying Missingness Mechanism (Fixed Missingness ≈ 60%)

| Missingness Mechanism      | Missing Rate | IRT RMSE |
| -------------------------- | ------------ | -------- |
| MCAR                       | 60%          | 0.4307   |
| MAR (item-dependent)       | 60%          | 0.4324   |
| MNAR-θ (ability-dependent) | 60%          | 0.4529   |

---

## 3. Extended Missingness Scenarios (Fixed Missingness ≈ 60%)

### 3.1 Non-Ignorable Missingness Variants

| Scenario         | Description                    | IRT RMSE |
| ---------------- | ------------------------------ | -------- |
| MNAR-Y (γ = 1.0) | Response-dependent MNAR        | 0.4848   |
| MNAR-Y (γ = 2.0) | Strong response-dependent MNAR | 0.5887   |
| MNAR-θ           | Ability-dependent MNAR         | 0.4529   |

**Note.**  
MNAR-Y represents a stricter non-ignorable mechanism than MNAR-θ, as missingness depends directly on the latent response outcome rather than latent ability alone.

---

### 3.2 Structural and Design-Based Missingness

| Scenario                     | Description                           | IRT RMSE |
| ---------------------------- | ------------------------------------- | -------- |
| Not-reached (position-based) | Speeded test (no speed heterogeneity) | 0.4304   |
| Not-reached + speed          | Position-based + person-level speed   | 0.4384   |
| Booklet50 + MCAR20           | Planned missingness + random omission | 0.4288   |

**Note.**  
Speeded conditions may lead to examinees with fully missing response patterns; such individuals are excluded from RMSE evaluation.

---

### 3.3 Population Heterogeneity

| Scenario           | Description                                 | IRT RMSE |
| ------------------ | ------------------------------------------- | -------- |
| DIF + MCAR         | Uniform DIF on 4 items (Δb = 0.6)           | 0.4354   |
| DIF + MNAR-θ       | DIF combined with non-ignorable missingness | 0.4426   |
| Group-specific MAR | Group-dependent missingness (MAR-item)      | 0.4371   |

---

## 4. Overall Conclusions

### 4.1 Robustness under Ignorable Missingness

IRT imputation performance is stable under ignorable missingness mechanisms, including MCAR, MAR (item-dependent), and planned missingness designs.  
Across these settings, RMSE values remain consistently around **0.43–0.45**, even at high missingness rates.

### 4.2 Sensitivity to Non-Ignorable Missingness

Imputation accuracy deteriorates substantially under non-ignorable missingness:

- Ability-dependent MNAR (MNAR-θ) leads to moderate degradation.
- Response-dependent MNAR (MNAR-Y) leads to severe degradation, with RMSE increasing sharply as the strength of dependence increases.

### 4.3 Structural Missingness vs. Non-Ignorability

Structural missingness mechanisms (e.g., not-reached, booklet designs) do not substantially degrade RMSE relative to MCAR, although they may introduce selection effects via fully missing response patterns.

### 4.4 Heterogeneity and Fairness Considerations

Measurement heterogeneity (DIF) and group-specific missingness introduce additional complexity but do not dramatically affect RMSE on missing cells.  
However, RMSE alone may mask bias in latent ability recovery and subgroup comparisons.

---

## Methodological Note

RMSE is computed only on missing cells for examinees with at least one observed response.  
Scenarios with non-ignorable missingness may exclude a larger number of examinees with fully missing response patterns, which should be considered when interpreting results.
