# 30-Day Psychiatrically Coded Readmission Prediction

This repository contains the notebook pipeline for an MSc dissertation project predicting 30-day psychiatrically coded hospital readmission from structured MIMIC-IV electronic health record data.

The project constructs an admission-level psychiatric diagnosis cohort, engineers structured predictors from MIMIC-IV hospital and ICU tables, compares statistical, tree-based, gradient-boosting, neural-network, temporal and ensemble models, and evaluates model behaviour using discrimination, calibration, operating thresholds, uncertainty, risk stratification, subgroup analysis and SHAP explainability.

## Data Access

MIMIC-IV is a credentialed clinical dataset and is not included in this repository. To run the notebooks, download MIMIC-IV v3.1 through PhysioNet after completing the required credentialing and place the files locally as:

```text
mimic-iv-3.1/
  hosp/
  icu/
```

The notebooks assume the following local project structure:

```text
DissProject/
  code/
  mimic-iv-3.1/
  outputs/
  reports/
```

Raw MIMIC-IV files, generated patient-level datasets, model binaries, sparse matrices, local environments and temporary files are excluded by `.gitignore`.

## Project Structure

```text
code/
  WP1.ipynb
  WP2/
    WP2_1.ipynb
    WP2_2.ipynb
    WP2_3.ipynb
    WP2_4.ipynb
  WP3/
    WP3_1.ipynb
    WP3_1_model_trial.ipynb
    WP3_2.ipynb
    WP3_3.ipynb
    WP3_4.ipynb
    WP3_5.ipynb
    WP3_6.ipynb
    WP3_7.ipynb
  WP4.ipynb
reports/
  Ahthini_diss_LaTeX/
```

## Notebook Order

Run the notebooks in this order when rebuilding the project from raw MIMIC-IV data.

| Order | Notebook | Purpose |
|---:|---|---|
| 1 | `code/WP1.ipynb` | Inspect MIMIC-IV tables and construct the psychiatric admission/readmission cohort |
| 2 | `code/WP2/WP2_1.ipynb` | Extract admission-level variables and selected table-derived predictors |
| 3 | `code/WP2/WP2_2.ipynb` | Clean extracted data and prepare consistent admission-level inputs |
| 4 | `code/WP2/WP2_3.ipynb` | Engineer final admission-level and hourly clinical sequence datasets |
| 5 | `code/WP2/WP2_4.ipynb` | Exploratory data analysis of cohort, features, missingness, temporal vitals and predictor associations |
| 6 | `code/WP3/WP3_1.ipynb` | Create patient-level train/test split, processed matrices, feature audits and reduced matrix variants |
| 7 | `code/WP3/WP3_1_model_trial.ipynb` | Rapid targeted-boosting check and SHAP-guided reduced feature-set creation |
| 8 | `code/WP3/WP3_2.ipynb` | Logistic regression baseline and tuned logistic regression |
| 9 | `code/WP3/WP3_3.ipynb` | Random Forest modelling |
| 10 | `code/WP3/WP3_4.ipynb` | XGBoost, CatBoost, LightGBM, targeted boosting and calibrated boosting models |
| 11 | `code/WP3/WP3_5.ipynb` | Neural-network comparators, TabNet, transformer-style models and hourly sequence/hybrid models |
| 12 | `code/WP3/WP3_6.ipynb` | Final model comparison, threshold analysis, high-risk strata, clustering, uncertainty and stress checks |
| 13 | `code/WP3/WP3_7.ipynb` | Subgroup performance, error analysis, fairness-related checks, subgroup-specific training and diagnosis cross-testing |
| 14 | `code/WP4.ipynb` | SHAP explainability, local explanations, paired-model explanation, subgroup explanation and hourly sequence occlusion |

## Analysis Design

The primary prediction task is admission-level prediction of 30-day psychiatrically coded hospital readmission, defined using the immediate next recorded hospital admission after discharge.

The main benchmark is a full-record discharge-time setting: structured information recorded up to discharge from the index admission can contribute to prediction, while post-discharge information is excluded. Patient-level train/test separation is used so admissions from the same patient do not appear in both development and held-out evaluation partitions.

PR-AUC is used as the primary comparison metric because the readmission outcome is imbalanced. ROC-AUC, calibration, Brier score, precision, recall, specificity, F1-score, threshold sweeps, risk strata and subgroup analyses are reported as complementary evaluations.

## Environment Setup

Create and activate a Python environment:

```bash
python3 -m venv my_env
source my_env/bin/activate
python -m pip install --upgrade pip setuptools wheel
python -m pip install -r requirements.txt
python -m ipykernel install --user --name dissproject --display-name "DissProject Python"
```

For GPU-enabled neural-network runs on a Linux remote lab, install a CUDA-compatible PyTorch build for that machine, then install the remaining packages from `requirements.txt`.

## Shareable Generated Outputs

The full `outputs/` directory is not intended to be committed because it may contain derived clinical data, identifiers, model artefacts, sparse matrices or large intermediate files. A small shareable subset of aggregate tables and report figures is provided for transparency:

```text
outputs/
  README.md
  summary_tables/
    final_model_comparison.csv
    feature_set_sensitivity.csv
    subgroup_summary.csv
    shap_feature_family_summary.csv
  figures/
    final_model_comparison.png
    calibration_and_risk_strata.png
    subgroup_heatmap.png
    shap_summary.png
```

These files contain aggregate model metrics, feature-set summaries, subgroup summaries, SHAP feature-family summaries and selected report figures only. Full local output workbooks, patient/admission-level outputs, train/test identifiers, model binaries and processed matrices remain excluded by `.gitignore`.


## Reproducibility Notes

- Fixed random seeds are used where supported by the relevant model library.
- WP3.1 audits patient overlap between train and test partitions.
- Preprocessing objects, processed feature names, train/test identifiers and model outputs are saved locally for downstream reuse.
- WP3.6 records final model provenance, leakage checks, threshold choice, uncertainty outputs and stress-test results.
- WP4 reads saved model outputs and processed matrices rather than refitting the primary models.

## Repository Hygiene

Do not commit:

- `mimic-iv-3.1/`
- raw or derived patient-level clinical data
- full local `outputs/` folders outside the curated shareable subset
- local Python environments
- sparse matrices and model binaries
- temporary Office files beginning with `~$`
- LaTeX build artefacts
- `.DS_Store`

The notebooks, dissertation source, compact documentation files and environment specification are the intended repository artefacts.

## Citation

If using or extending this repository, cite the dissertation project and the MIMIC-IV dataset according to the relevant data-use and institutional requirements.
