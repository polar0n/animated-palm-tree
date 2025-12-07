# VAE–IRT Simulation Framework (Scenarios S0–S4)

## Feature Overview

| Feature                 |   S0   |  S1  |  S2  |  S3  |  S4  | Future                   |
| ----------------------- | :----: | :--: | :--: | :--: | :--: | ------------------------ |
| 2PL/3PL data generation |   ✔    |  ✔   |  ✔   |  ✔   |  ✔   | multidimensional?        |
| MAR/MNAR                |        |      |  ✔   |  ✔   |  ✔   | add missing-rule library |
| mixture distributions   |        |      |      |  ✔   |      | mixture of K groups      |
| booklet design          |        |      |      |      |  ✔   | random block design      |
| polytomous items        |   –    |  –   |  –   |  –   |  –   | add GRM/GPCM module      |
| batch simulation        | ✦ easy |      |      |      |      | loop wrapper ready       |
| connect to VAE          |   ✔    |  ✔   |  ✔   |  ✔   |  ✔   | auto export              |

This repository contains a **modular and extensible simulation engine** for studying  
**VAE-based imputation vs. traditional IRT** under controlled data-generating scenarios.

---

# Overview of the Simulation Framework Structure

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

## 4. Extensibility

The system is designed to support future extensions:

- multidimensional IRT  
- graded response / polytomous items  
- booklet forms with multiple blocks  
- wrappers for batch simulation  
- VAE integration modules  

---

# Usage Guide

Below is a quick-start guide for running scenarios and understanding settings.

---

## Running Scenarios

```r
result <- run_scenario(config_S0)
str(result, max.level = 1)
```

---

## Choosing Scenarios

| Scenario | Description               |
| -------- | ------------------------- |
| S0       | Ideal 2PL, no missingness |
| S1       | MCAR                      |
| S2A      | MAR                       |
| S2B      | MNAR                      |
| S3       | Mixture θ                 |
| S4       | Booklet / matrix sampling |

Switch scenario:

```r
result <- run_scenario(config_S3)
```

---

## Controlling Missingness

Missingness mechanism is set through:

```r
config$missing_mechanism
```

### Examples:

#### MCAR (S1)

```r
config_S1$missing_mechanism <- "MCAR"
config_S1$missing_rate <- 0.4
```

#### MAR (S2A)

```r
config_S2A$missing_mechanism <- "MAR"
config_S2A$mar_probs <- seq(0.1, 0.5, length.out = config_S2A$I)
```

#### MNAR (S2B)

```r
config_S2B$missing_mechanism <- "MNAR"
config_S2B$mnar_fun <- function(x,p,i) ifelse(is.na(x)||x==0, 0.5, 0.1)
```

#### Custom booklet (S4)

```r
config_S4$missing_mechanism <- "custom"
config_S4$custom_mask <- mask_custom
```

---

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

## Full Example: Run S2B (MNAR)

```r
result <- run_scenario(config_S2B, save_data = TRUE)
str(result, max.level = 1)
```

---

## Notes & Best Practices

1. **Always begin with S0** to ensure code stability.  
2. **Do not modify core functions** when adding scenarios.  
3. **Missingness should only be changed in config**.  
4. **Use save_data=TRUE only when exporting to VAE**.  
5. **S3 and S4 are realism tests**—expect IRT to misbehave intentionally.  

---

# End of README
