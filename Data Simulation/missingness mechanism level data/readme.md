This folder contains simulated datasets generated for the VAE–IRT imputation experiments under controlled 2PL IRT conditions, with a fixed overall missingness level and varying missingness mechanisms.

The data were simulated with:

- **N = 3000** examinees  
- **I = 20** dichotomous items  
- **Overall missingness ≈ 60%**, generated under different missingness mechanisms:
  - **MCAR** (Missing Completely At Random)
  - **MAR** (Missing At Random; item-dependent)
  - **MNAR** (Missing Not At Random; ability-dependent)

Each scenario includes the following files:

- **X_obs** — the observed response matrix with missing values (NA); used as input for VAE and IRT imputation models.  
- **X_full** — the complete response matrix without missingness; used as ground truth for evaluating imputation accuracy.  
- **X_mask** — the missingness indicator matrix (`TRUE` = originally missing).

---

### Missingness Mechanisms

- **MCAR**: Missingness is independent of item responses and latent ability.  
- **MAR**: Missingness depends on observed item characteristics but not on latent ability.  
- **MNAR**: Missingness depends on the latent ability parameter (θ), with lower-ability examinees more likely to have missing responses.

The MNAR mechanism represents a non-ignorable missingness process that violates standard IRT assumptions.

---

### Usage for VAE and IRT Imputation

- Use **X_obs** as the model input.  
- Use **X_mask** to restrict the reconstruction loss to originally missing entries.  
- Evaluate imputation quality using:

```r
rmse <- sqrt(mean((X_imputed[X_mask] - X_full[X_mask])^2))
