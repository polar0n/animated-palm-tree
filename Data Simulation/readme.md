# Data Simulation Framework 


This framework is organized into **four main layers**:

---

## 1. Core Simulation Functions

These are reusable across all scenarios:

### **`simulate_irt_data()`**

Generates full response matrices under 2PL/3PL IRT.

### **`apply_missingness()`**

Applies different missing-data mechanisms:

- MCAR (S1)
- MAR (S2A)
- MNAR (S2B)
- booklet/custom designs (S4)

### **`run_scenario()`**

Universal runner that:

1. Simulates IRT data  
2. Applies missingness  
3. Optionally saves CSV outputs  
4. Returns data for VAE/IRT evaluation

This modularity allows easy expansion without breaking previous scenarios.

---

## 2. Scenario Configurations (S0–S4)

Each scenario is defined via a **config object**, specifying:

- sample size  
- number of items  
- latent trait distribution  
- missing-data mechanism  
- file prefix  
- reproducibility seed  

Running a scenario is as simple as:

```r
result <- run_scenario(config_S2B)
```

---

## 3. Data Export

If `save_data = TRUE`, the framework saves:

```
*_X_full.csv
*_X_obs.csv
*_item_params.csv
*_theta.csv
*_mask.csv
```

These files are directly usable by Python VAE pipelines.

---


# Usage Guide

Below is a quick-start guide for running scenarios and understanding settings.

---

## Running Scenarios

```r
result <- run_scenario(config_S0)
str(result, max.level = 1)
```
## Controlling Missingness

Missingness mechanism is set through:

```r
config$missing_mechanism
```

## Saving Output

```r
run_scenario(config_S1, save_data = TRUE)
```

Produces:

```
*_X_full.csv
*_X_obs.csv
*_item_params.csv
*_theta.csv
*_mask.csv
```


---

## Notes

1. **Missingness should only be changed in the scenario config.**  
   Never modify `apply_missingness()` unless you are extending the framework.

2. **Use `save_data = TRUE` only when exporting data**  
   (e.g., for training VAEs in Python or archiving simulation runs).

3. **For MNAR (Scenario S2B), you *must provide your own missingness function*.**  
   Example of a valid MNAR function:

   ```r
   config_S2B$mnar_fun <- function(x, p, i) {
     if (is.na(x) || x == 0) return(0.50)  # low performance → more missing
     return(0.10)                           # high performance → less missing
   }
   ```

   - The function must return a **probability between 0 and 1**.  
   - It is evaluated per person × item.  
   - The MNAR mechanism will fail if the function is missing or incorrectly specified.

4. **For booklet / matrix sampling designs (Scenario S4), you *must supply your own custom mask*.**  
   Example:

   ```r
   mask_custom <- matrix(TRUE, N, I)
   for (p in 1:N) {
     answered <- sample(1:I, I/3)
     mask_custom[p, answered] <- FALSE
   }
   config_S4$custom_mask <- mask_custom
   ```

   - `TRUE` means **missing** (not administered).  
   - `FALSE` means **observed**.  
   - The mask *must* match the dimensions of the response matrix (`N × I`).  
   - If not provided, Scenario S4 cannot run.

5. **The latent trait distribution (theta) should match the scenario.**  

   - S0–S2 use `theta_dist = "normal"`  
   - S3 uses `theta_dist = "mixture"`  
   - If you choose `"custom"`, you must pass a vector `custom_theta` of length `N`.

6. **Item parameters (a, b, c) follow default distributions unless overridden.**  
   Adjust for domain-specific designs using:

   ```r
   a_mean, a_sd, b_mean, b_sd, c_mean, c_sd
   ```

7. **The simulation engine assumes binary items (2PL/3PL).**  

   - Polytomous items (GRM/GPCM) will require extending `simulate_irt_data()`.  
   - Currently not supported.

8. **Scenario names, seeds, and save prefixes should always be unique.**  
   Prevent overwriting output files:

   ```r
   config_S2B$save_prefix <- "S2B_run1"
   ```

9. **The returned object from `run_scenario()` is standardized across all scenarios.**  
   Every scenario returns:

   ```r
   $X_full
   $X_obs
   $mask
   $theta_true
   $item_params_true
   $config
   ```

   This ensures consistent downstream handling (VAE, IRT models, evaluation).
---
