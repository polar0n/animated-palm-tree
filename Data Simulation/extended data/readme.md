
In addition to standard MCAR, MAR, and ability-dependent MNAR settings Donald Rubin (1976), we consider several extended missingness scenarios that are frequently discussed in the psychometric literature. These include response-dependent non-ignorable missingness, where omissions depend on the latent response outcome (e.g., David Rose et al., 2010; Pieter Pohl, 2020), speeded test effects leading to not-reached items (Chris Glas & Pimentel, 2008), and planned missingness designs such as booklet or matrix sampling in large-scale assessments (Robert Mislevy et al., 1992). We further include population heterogeneity scenarios involving differential item functioning (DIF) and group-specific missingness to reflect violations of measurement invariance and fairness-relevant conditions (Holland & Wainer, 1993; Pohl & Carstensen, 2012). 
### Core settings

- **Number of examinees (N)**: 3000  
- **Number of items (I)**: 20  
- **Response model**: 2PL IRT  
- **Latent ability distribution**:  
  - Standard Normal: \( \theta \sim \mathcal{N}(0,1) \)  
- **Overall missingness**: approximately **60%** (calibrated per scenario)

Each scenario provides:

- `X_full.csv` — complete response matrix (ground truth)
- `X_obs.csv` — observed response matrix with missing values (`NA`)
- `mask.csv` — missingness indicator (`TRUE` = originally missing)

### Case 1: MNAR-Y (γ = 1.0)

**Response-dependent MNAR**
$$
P(R_{ij}=1 \mid Y_{ij}) = \text{logit}^{-1}(\alpha + \gamma Y_{ij})
$$

Missingness depends directly on the latent response outcome.  
Incorrect responses are more likely to be missing.

---

### Case 2: MNAR-Y (γ = 2.0)

Same as Case 1, but with **stronger response dependence**, representing more severe non-ignorability.

---

### Case 3: Not-Reached (Position-based Missingness)

Missingness depends on **item position** within the test.  
Later items have higher missing probabilities, mimicking **speeded test conditions**.

---

### Case 4: Not-Reached + Speed

Position-based missingness combined with a **person-level speed parameter**, partially correlated with ability:
$$
s_i = \rho \theta_i + \sqrt{1-\rho^2}\,\varepsilon_i
$$

This reflects realistic test-taking behavior where faster examinees complete more items.

---

### Case 5: Planned Missingness (Booklet Design) + MCAR

- Each examinee is assigned a booklet containing **50% of items** (matrix sampling).
- Within administered items, **20% MCAR omissions** are added.
- Overall missingness ≈ 60%.

This scenario mimics **large-scale assessment designs** (e.g., PISA, NAEP).

---

## Population Heterogeneity Scenarios (Cases 6–8)

### Case 6: DIF + MCAR

- Two latent groups with identical ability distributions.
- **Uniform DIF** introduced on 4 items via difficulty shifts (Δb = 0.6).
- Missingness is MCAR.

Used to assess imputation robustness under **measurement non-invariance**.

---

### Case 7: DIF + MNAR-θ

Combines **DIF in the response model** with **ability-dependent MNAR missingness**.  
This scenario represents a particularly challenging setting with **both model misspecification and non-ignorable missingness**.

---

### Case 8: Group-Specific Missingness + MAR-item

- Two latent groups (no DIF in responses).
- Missingness depends on item characteristics (**MAR-item**), but with **group-specific intercept shifts**.
- One group exhibits systematically higher missingness.
- Overall missingness is calibrated to ≈ 60%.

This scenario is relevant for **fairness and subgroup robustness analyses**.

