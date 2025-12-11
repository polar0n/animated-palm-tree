This folder contains simulated datasets generated for the VAE–IRT imputation experiments under controlled 2PL IRT conditions, with MCAR missingness levels of 40%, 50%, 60%, and 70%.

	•	X_obs：the observed response matrix with missing values (NA)，for VAE input
	•	X_full：the complete response matrix without missingness，for evaluating imputation accuracy（ground truth）。
	•	X_mask：the missingness indicator matrix (TRUE = originally missing)
--

Usage for VAE Imputation
	•	Use X_obs as the model input
	•	Use mask to restrict the reconstruction loss to originally missing entries
	•	Evaluate imputation quality with:rmse <- sqrt(mean((X_imputed[mask] - X_full[mask])^2))
