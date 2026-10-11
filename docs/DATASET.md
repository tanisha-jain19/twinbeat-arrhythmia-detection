# PTB-XL dataset

Download from the official [PTB-XL version 1.0.3 page on PhysioNet](https://physionet.org/content/ptb-xl/1.0.3/). The page provides ZIP and command-line download options and the dataset license. Keep the downloaded directory structure intact.

Expected local layout:

```text
data/ptb-xl/
  ptbxl_database.csv
  scp_statements.csv
  records500/
    00000/
      ..._hr.hea
      ..._hr.dat
    ...
```

The notebook reads the relative `filename_hr` entries, so both WFDB header and signal files must be available. `records100` is not used by this notebook.

PhysioNet distributes this version under **CC BY 4.0**. Retain the dataset license and attribution and cite the dataset/paper when using it. This repository links to the source rather than copying ECG records or patient metadata into GitHub.

The source notebook reports 21,799 records, but does not record a dataset version/checksum. That count alone cannot identify the exact release. Version 1.0.3 is the documented download target here, not a claim that it exactly reproduces the historical input.

PTB-XL provides patient-respecting `strat_fold` assignments. Its recommended protocol uses folds 1–8 for training, 9 for validation, and 10 for testing. The supplied historical notebook does **not** use that protocol; this is a documented limitation, not an implemented correction.

Dataset DOI: [10.13026/kfzx-aw45](https://doi.org/10.13026/kfzx-aw45).
