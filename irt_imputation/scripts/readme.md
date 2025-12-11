# IRT Imputation Scripts

This folder contains scripts used to perform **IRT-based imputation** for the VAE–IRT simulation study.  
The imputation procedure is implemented using a **2PL IRT model** fitted to the observed response data (`X_obs`), and missing entries are imputed using the model-predicted probabilities.

- Loads the simulated datasets (`X_obs`, `X_full`, `X_mask`)
- Fits a **2PL IRT model** using the `mirt` package
- Imputes missing responses based on these probabilities
- Excludes examinees with 100% missing responses from RMSE evaluation
- Saves the imputed response matrix (`*_X_IRT_imputed.csv`)
- Reports RMSE on missing entries

---

##  How to Run the Imputation

1. Place all data files (e.g., `MCAR40_X_obs.csv`, `MCAR40_X_full.csv`, `MCAR40_mask.csv`) in the working directory.  
2. Open and knit/run `irt_imputation.Rmd` **or** source the function inside it.

Example (in R):

```r
source("irt_imputation.Rmd")

for (p in c("MCAR40", "MCAR50", "MCAR60", "MCAR70")) {
  irt_impute_scenario(p)
}
```

---

##  Output

Example output:

```
Running IRT imputation for: MCAR40
Saved IRT imputed matrix to: MCAR40_X_IRT_imputed.csv
MCAR40 | IRT RMSE on missing cells: 0.4231
```

---

##  Notes

- Imputation uses **expected probabilities** rather than hard 0/1 classification.  
- Examinees with no observed responses cannot receive θ estimates; they are excluded from RMSE computation.  
