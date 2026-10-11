# Historical results — not independent-test performance

These values come from saved text outputs in the original Downloads notebook. No new model fitting or metric reproduction was performed. SMOTE/scaling before splitting, lack of patient separation, and the residual `VA` label prevent interpreting them as validated arrhythmia detection accuracy.

| Model | Accuracy (%) | Weighted F1 (%) | Weighted precision (%) | Weighted recall (%) |
| --- | ---: | ---: | ---: | ---: |
| XGBoost | 95.78 | 95.77 | 95.85 | 95.78 |
| Random Forest | 94.66 | 94.63 | 94.65 | 94.66 |
| SVM | 90.59 | 90.53 | 90.51 | 90.59 |
| KNN | 82.97 | 81.47 | 85.84 | 82.97 |
| AdaBoost | 74.47 | 74.60 | 74.80 | 74.47 |
| LightGBM | 94.88 | 94.85 | 95.00 | 94.88 |
| Stacking | 96.68 | 96.67 | 96.68 | 96.68 |

The recorded class counts are 16,748 `NSR`, 1,565 `AFib`, and 3,486 residual `VA`, before resampling. SMOTE balances each to 16,748 records; the recorded split then contains 40,195 training rows and 10,049 test rows. These test rows include the consequences of whole-dataset resampling.

The original metric text is preserved in `original_metrics.txt`. Output plots were cleared from the published notebook to avoid displaying the scores without their methodological context. A valid corrected experiment needs new metrics; none are invented here.
