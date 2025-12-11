This folder contains simulated datasets generated for the VAE–IRT imputation experiments under controlled 2PL IRT conditions with MCAR missingness levels of 40%, 50%, 60%, and 70%.
	•	Use X_obs as input
	•	Use mask to restrict loss to missing entries
  rmse <- sqrt(mean((X_imputed[mask] - X_full[mask])^2))
