# Shareable Output Subset

This directory contains a curated subset of aggregate outputs from the dissertation pipeline. These files are intended for repository transparency and do not include raw MIMIC-IV data, patient-level derived datasets, train/test identifiers, sparse matrices, model binaries or admission-level prediction files.

## Summary Tables

| File | Source | Contents |
|---|---|---|
| `summary_tables/final_model_comparison.csv` | `outputs/WP3_6/csv_tables/final_model_comparison.csv` | Aggregate performance metrics for the main model comparison |
| `summary_tables/feature_set_sensitivity.csv` | `outputs/WP3_6/csv_tables/t3_6_reduced_feature_model_performance_comparison.csv` | Aggregate feature-matrix sensitivity results |
| `summary_tables/subgroup_summary.csv` | `outputs/WP3_7/csv_tables/t3_7_key_subgroup_finding_summary.csv` | Selected subgroup performance and error-summary findings |
| `summary_tables/shap_feature_family_summary.csv` | `outputs/WP4/csv_tables/t4_shap_feature_family_importance.csv` | SHAP feature-family contribution summary |

## Figures

| File | Source | Contents |
|---|---|---|
| `figures/final_model_comparison.png` | `outputs/WP3_6/images/t3_6_recommended_model_pr_auc_comparison.png` | Recommended model comparison by PR-AUC |
| `figures/calibration_and_risk_strata.png` | `reports/Ahthini_diss_LaTeX/images/fig4_8.png` | Calibration and high-risk strata summary |
| `figures/subgroup_heatmap.png` | `outputs/WP3_7/figures/t3_7_diagnosis_cross_test_pr_auc_heatmap.png` | Diagnosis-group cross-testing PR-AUC heatmap |
| `figures/shap_summary.png` | `outputs/WP4/images/t4_shap_summary_beeswarm_top20.png` | SHAP summary plot for the Targeted LightGBM model |

The complete local outputs should be regenerated from the notebooks rather than committed.
