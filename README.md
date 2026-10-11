# TwinBeat — Arrhythmia Detection

**A notebook-based machine-learning study of ECG features and classification using PTB-XL.**

Maintained by [Tanisha Jain](https://github.com/tanisha-jain19). This repository presents the supplied final experiment notebook; it does not include a website, Flask backend, or deployed application.

## Explore the work

**[Open Arrhythmia.ipynb](Arrhythmia.ipynb)** · [Dataset instructions](docs/DATASET.md) · [Methodology and limitations](docs/METHODOLOGY.md) · [Research references](docs/REFERENCES.md)

The notebook loads 12-lead ECG recordings at 500 Hz, extracts handcrafted features, compares six classifiers, and combines XGBoost, Random Forest and LightGBM with a logistic-regression stacking model. It also includes confusion-matrix, ROC, feature-importance, and model-export code.

## Important interpretation

This is a historical research prototype, **not a clinically validated detector**. The original pipeline applies SMOTE and scaling before its random train/test split. It also labels every record outside its SR/AFIB/AFLT rules as `VA`, which does not establish ventricular arrhythmia. These issues limit the meaning of the saved performance numbers. The experiment logic is preserved and explicitly documented rather than silently changing it and retaining old scores.

## Workflow

1. Read PTB-XL metadata and the SCP statement table.
2. Apply the notebook's historical three-label mapping.
3. Load the high-resolution ECG waveforms.
4. Extract 216 features per record with the fast 12-lead feature function.
5. Apply the historical SMOTE/scaling and random split workflow.
6. Fit XGBoost, Random Forest, SVM, KNN, AdaBoost, and LightGBM.
7. Fit and evaluate a stacking ensemble; export models and preprocessing objects.

An earlier NeuroKit prototype extracts 192 features for one record; the subsequent fast function is the one used to build the training feature table.

## Run locally

Use a separate Python 3.11 environment. From the repository folder:

```bash
python -m venv .venv
```

Activate it (`.venv\Scripts\activate` on Windows Command Prompt, or `source .venv/bin/activate` on macOS/Linux), then:

```bash
python -m pip install -r requirements.txt
python -m jupyterlab
```

Download PTB-XL separately following [DATASET.md](docs/DATASET.md), open `Arrhythmia.ipynb`, and run cells in order. The default data directory is `data/ptb-xl`; edit `DATA_DIR` or set `PTBXL_DATA_DIR` to use another location. Generated features, figures, and models are saved to the ignored `outputs/` folder.

The notebook loads all waveforms into memory. Its recorded `(21799, 5000, 12)` array alone requires roughly **10.5 GB at float64**, with additional memory needed during list-to-array conversion and training. Use ample RAM; runtime varies substantially. A streaming rewrite would be separate future work.

Dependency ranges are provided for setup, not claimed as a tested lockfile. The source outputs show mixed Python/package environments. Feature extraction and full training have not been rerun for this publication.

## Recorded results

The source contains a saved stacking accuracy of 96.68%, but **this is not a trustworthy estimate of performance on unseen patients** because of the preprocessing and split issues above. Full historical values are preserved in [RESULTS.md](docs/RESULTS.md), with their provenance and caveats. No new training score or clinical claim is made.

## Files

| File | Purpose |
| --- | --- |
| `Arrhythmia.ipynb` | Final supplied notebook with portable paths and explanatory notes |
| `requirements.txt` | Dependencies, including LightGBM missing from the original install cell |
| `docs/DATASET.md` | Official PTB-XL download, layout, version and licensing information |
| `docs/METHODOLOGY.md` | Label, evaluation, and feature-extraction limitations |
| `docs/RESULTS.md` | Historical metrics and interpretation |
| `docs/REFERENCES.md` | Dataset and relevant research citations |
| `docs/SOURCE.json` | Original notebook hash and publication changes |

## Validation and next steps

The published notebook passed Jupyter schema validation and Python/IPython syntax checks. No ECG dataset, trained weights, website code, or paper PDF is redistributed.

A valid follow-up would define labels from explicit reviewed rhythm annotations, use patient-separated PTB-XL folds, fit preprocessing/resampling within training folds, and rerun every evaluation on untouched real test recordings. This repository does not claim that follow-up has been completed.
