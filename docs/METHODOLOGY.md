# Methodology review

These observations describe the supplied notebook. They are not evidence of a corrected or newly validated model.

## Labels

`assign_label` maps `SR` to `NSR` first, maps `AFIB` or `AFLT` to `AFib` only if `SR` is absent, and maps everything else to `VA`. It ignores code likelihood values and coexisting statements. The residual `VA` group cannot be interpreted as verified ventricular arrhythmia, and an SR code alone does not establish an otherwise normal ECG. The original short names remain in code for provenance.

## Evaluation leakage

SMOTE generates synthetic samples from the entire feature dataset before the train/test split. The scaler is also fit on the full resampled data. Consequently, information crosses the intended evaluation boundary and synthetic examples enter the test set. The random record-level split does not ensure patient separation. The stacking model's internal cross-validation also receives data that were already resampled/scaled outside its folds.

Use patient-separated data partitions first. Fit scaling and any resampling only within training folds, including the stacking cross-validation folds. Evaluate once on an untouched test set of real recordings. [imbalanced-learn's leakage guidance](https://imbalanced-learn.org/stable/common_pitfalls.html) explains why resampling before splitting is problematic.

## Features

- The fast peak finder is a heuristic; fixed offsets before/after detected peaks are amplitude samples, not validated P/ST/T delineation.
- With 500 Hz input and `nperseg=512`, Welch frequency spacing is about 0.977 Hz. None of the positive bins lie in the coded VLF/LF/HF bands below 0.40 Hz. Those band integrals therefore collapse to zero. The 1024-sample prototype also lacks positive bins below 0.40 Hz.
- These are spectra of the ECG waveform, not an interpolated RR-interval tachogram. The low-frequency band names should not be treated as validated HRV measures.
- Integration calls omit the frequency coordinates. A revised implementation would need appropriate spectral resolution, signal definition, and integration spacing; it would require new training and evaluation.
- Short RR sequences can produce NaNs; broad exception handlers, warning suppression, and later zero-filling hide extraction failures. Zero can mean a missing/failed feature as well as a real numerical value.
- The initial prototype's Q-to-S peak interval is not a validated QRS onset-to-offset duration.

## Plots and metrics

Precision, recall and F1 use weighted averaging. The flattened one-vs-rest ROC is micro-averaged. Both are affected by the preceding evaluation issues. Raw feature importances from three different estimators are averaged despite differing scales; that chart is exploratory and not a calibrated or causal explanation.

The publication retains this logic to preserve the final submitted experiment. Rewriting the scientific pipeline and claiming the old result as its performance would be misleading.
