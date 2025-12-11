This folder contains simulated datasets generated for the VAE–IRT imputation experiments under controlled 2PL IRT conditions.
The data were simulated with:

	•	N = 3000 examinees
	•	I = 20 dichotomous items
	•	MCAR missingness levels of 40%, 50%, 60%, and 70%

Each scenario includes the following files:

	•	X_obs — the observed response matrix with missing values (NA); used as input for the VAE.
	•	X_full — the complete response matrix without missingness; used as ground truth for evaluating imputation accuracy.
	•	X_mask — the missingness indicator matrix (TRUE = originally missing).

⸻

Usage for VAE and IRT Imputation

	•	Use X_obs as the model input.
	•	Use X_mask to restrict the reconstruction loss to originally missing entries.
	•	Evaluate imputation quality using:
