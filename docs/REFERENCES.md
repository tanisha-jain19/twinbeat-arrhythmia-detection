# Research references and credits

## Dataset and evaluation background

1. Wagner, P., Strodthoff, N., Bousseljot, R.-D., Kreiseler, D., Lunze, F. I., Samek, W., and Schaeffter, T. (2020). **PTB-XL, a large publicly available electrocardiography dataset.** Scientific Data, 7, 154. [Paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC7248071/) · [DOI: 10.1038/s41597-020-0495-6](https://doi.org/10.1038/s41597-020-0495-6).
2. **PTB-XL, version 1.0.3**, PhysioNet. [Dataset and citation details](https://physionet.org/content/ptb-xl/1.0.3/) · [DOI: 10.13026/kfzx-aw45](https://doi.org/10.13026/kfzx-aw45).
3. Strodthoff, N., Wagner, P., Schaeffter, T., and Samek, W. **Deep Learning for ECG Analysis: Benchmarks and Insights from PTB-XL.** [Research paper/preprint](https://arxiv.org/abs/2004.13701). Included as evaluation background; TwinBeat does not reproduce its benchmark protocol or results.

## Implementation

The notebook uses WFDB, NeuroKit2, NumPy, pandas, SciPy, scikit-learn, imbalanced-learn, XGBoost, LightGBM, matplotlib, seaborn, tqdm, and joblib. These tools and PTB-XL remain credited to their original authors.

The source notebook did not identify the paper behind a feature-comparison comment. That unsupported comment was removed; no claim is made that TwinBeat improves on a particular publication. Paper PDFs and dataset files are not redistributed, and their original licenses are not replaced by this repository.
