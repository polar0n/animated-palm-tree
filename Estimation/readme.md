## Table 1 — Main Comparison (Case-by-case): IRT vs Best VAE Method

| Scenario         | MissingRate | IRT_BCE_missing | IRT_RMSE_missing | VAE_best_METHOD | VAE_best_BCE_missing | VAE_best_RMSE_missing | ΔBCE (VAE-IRT) | ΔRMSE (VAE-IRT) |
| ---------------- | ----------: | --------------: | ---------------: | --------------- | -------------------: | --------------------: | -------------: | --------------: |
| MNAR_Y1          |         0.6 |          0.6784 |           0.4848 | enc_dec_ind     |               0.5978 |                0.4551 |        -0.0806 |         -0.0297 |
| MNAR_Y2          |         0.6 |          1.0065 |           0.5887 | enc_dec_ind     |               0.6416 |                0.4760 |        -0.3649 |         -0.1127 |
| NR_simple        |         0.6 |          0.5485 |           0.4304 | enc_ind         |               0.5923 |                0.4513 |        +0.0438 |         +0.0209 |
| NR_speed         |         0.6 |          0.5659 |           0.4384 | enc_dec_ind     |               0.5774 |                0.4446 |        +0.0115 |         +0.0062 |
| Booklet50_MCAR20 |         0.6 |          0.5447 |           0.4288 | zero            |               0.5979 |                0.4539 |        +0.0532 |         +0.0251 |
| DIFMCAR60        |         0.6 |          0.5570 |           0.4354 | zero            |               0.6094 |                0.4603 |        +0.0524 |         +0.0249 |
| DIFMNARth60      |         0.6 |          0.5707 |           0.4426 | enc_dec_ind     |               0.5724 |                0.4420 |        +0.0017 |         -0.0006 |
| GroupMAR60       |         0.6 |          0.5604 |           0.4371 | enc_ind         |               0.6160 |                0.4636 |        +0.0556 |         +0.0265 |
