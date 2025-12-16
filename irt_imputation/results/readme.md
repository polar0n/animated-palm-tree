# IRT Imputation Results (RMSE on Missing Cells)

## Varying Missingness Proportion (MCAR)
| Missingness Mechanism | Missing Rate | IRT RMSE |
|----------------------|--------------|----------|
| MCAR                 | 40%          | 0.4231   |
| MCAR                 | 50%          | 0.4452   |
| MCAR                 | 60%          | 0.4455   |
| MCAR                 | 70%          | 0.4403   |
Note: For MCAR70, some examinees have 100% missing responses; RMSE may be unstable depending on exclusion rules.

## Varying Missingness Mechanism (Fixed Missingness ≈ 60%)
| Missingness Mechanism | Missing Rate | IRT RMSE |
|----------------------|--------------|----------|
| MCAR                 | 60%          | 0.4307   |
| MAR                  | 60%          | 0.4324   |
| MNAR                 | 60%          | 0.4529   |

IRT imputation performance is stable under MCAR and MAR conditions, where missingness is ignorable.
Under MNAR missingness depending on latent ability, IRT imputation accuracy deteriorates, reflecting the violation of the ignorability assumption.
