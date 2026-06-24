# PediAppend-MissXAI

**Missingness-Aware Explainable Machine Learning for Pediatric Appendicitis Diagnosis and Surgical Decision Support**

This repository contains the Google Colab notebook and tabular dataset used for the study **PediAppend-MissXAI**, a missingness-aware and explainable machine-learning framework for pediatric appendicitis decision support using clinical, laboratory, scoring, and ultrasound-summary variables.

The study focuses on three clinically relevant prediction tasks:

1. Pediatric appendicitis diagnosis
2. Surgical versus conservative management prediction
3. Complicated versus uncomplicated appendicitis risk stratification

The workflow emphasizes realistic clinical data availability, missing-value handling, feature-group comparison, threshold optimization, model explainability, and journal-style figure/table generation.

---

## Repository Contents

```text
PediAppend-MissXAI/
│
├── PediAppend-MissXAI.ipynb
├── app_datar1.xlsx
└── README.md
```

### Files

| File                       | Description                                                                                                                   |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `PediAppend-MissXAI.ipynb` | Main Google Colab notebook containing the complete machine-learning, statistical, explainability, and visualization workflow. |
| `app_datar1.xlsx`          | Modified Excel dataset used in this repository. It contains only the `All cases` sheet.                                       |
| `README.md`                | Repository documentation.                                                                                                     |

---

## Dataset Source

The dataset used in this project is derived from the public **Regensburg Pediatric Appendicitis Dataset**.

Original dataset:

* **Dataset name:** Regensburg Pediatric Appendicitis Dataset
* **Version:** 1.03
* **DOI:** 10.5281/zenodo.7711412
* **Zenodo URL:** [https://zenodo.org/records/7711412](https://zenodo.org/records/7711412)

The original Zenodo Excel file was named:

```text
app_data.xlsx
```

For this repository, the original Excel file was modified by removing the `Data Summary` tab and keeping only the main data sheet named:

```text
All cases
```

The modified file included in this repository is named:

```text
app_datar1.xlsx
```

No raw ultrasound image data are included in this repository. This study uses the tabular clinical, laboratory, scoring, and ultrasound-summary variables.

---

## Dataset Citation

Please cite the original dataset as:

```text
Marcinkevičs, R., Reis Wolfertstetter, P., Klimiene, U., Chin-Cheong, K.,
Paschke, A., Zerres, J., Denzinger, M., Niederberger, D., Wellmann, S.,
Ozkan, E., Knorr, C., & Vogt, J. E. (2023).
Regensburg Pediatric Appendicitis Dataset (1.03) [Data set].
Zenodo. https://doi.org/10.5281/zenodo.7711412
```

Associated publication:

```text
Marcinkevičs, R., Reis Wolfertstetter, P., Klimiene, U., Chin-Cheong, K.,
Paschke, A., Zerres, J., Denzinger, M., Niederberger, D., Wellmann, S.,
Ozkan, E., Knorr, C., & Vogt, J. E. (2024).
Interpretable and intervenable ultrasonography-based machine learning models
for pediatric appendicitis. Medical Image Analysis, 91, 103042.
https://doi.org/10.1016/j.media.2023.103042
```

Associated preprint:

```text
arXiv:2302.14460
```

---

## Study Objective

Pediatric appendicitis diagnosis can be difficult because clinical signs, laboratory results, scoring systems, and ultrasound findings may be incomplete or variably available during emergency evaluation. This project develops a missingness-aware explainable machine-learning workflow to support pediatric appendicitis diagnosis and decision-making under realistic tabular data availability.

The study evaluates whether machine-learning models can predict:

* appendicitis versus no appendicitis,
* surgical versus conservative management,
* complicated versus uncomplicated appendicitis among appendicitis cases.

---

## Main Methodological Features

The notebook includes:

* Dataset audit and missingness profiling
* Target variable construction
* Leakage-safe feature selection
* Feature-group comparison
* Classical score-only baseline comparison
* Missingness indicators
* Multiple machine-learning classifiers
* Cross-validation and holdout testing
* Bootstrap confidence intervals
* Threshold optimization
* Severity-specific high-sensitivity threshold analysis
* Calibration curves
* Decision-curve analysis
* Permutation importance
* F2-based permutation importance for severity prediction
* SHAP explainability
* Combined important-feature summary
* Publication-style figures and copyable tables

---

## Feature Groups

The workflow compares several clinically meaningful feature groups:

| Feature group                                     | Description                                                          |
| ------------------------------------------------- | -------------------------------------------------------------------- |
| `Score_only`                                      | Alvarado score and Pediatric Appendicitis Score                      |
| `Clinical_only`                                   | Demographics and clinical symptoms/signs                             |
| `Laboratory_only`                                 | Blood and urine laboratory variables                                 |
| `Ultrasound_summary_only`                         | Expert-derived ultrasound-summary findings                           |
| `Clinical_laboratory`                             | Clinical and laboratory variables                                    |
| `Clinical_laboratory_ultrasound`                  | Clinical, laboratory, and ultrasound-summary variables               |
| `All_safe_tabular`                                | All leakage-safe tabular predictors                                  |
| `Sensitivity_without_scores_or_appendix_diameter` | Sensitivity analysis excluding score variables and appendix diameter |

---

## Prediction Tasks

The notebook automatically checks whether each target contains at least two usable classes. Tasks are constructed only when sufficient class variation exists.

### 1. Diagnosis prediction

```text
appendicitis vs no appendicitis
```

### 2. Surgical management prediction

```text
surgical vs conservative
```

### 3. Severity prediction

```text
complicated vs uncomplicated appendicitis
```

Severity prediction is performed among appendicitis cases only.

---

## Models Used

The notebook evaluates the following machine-learning models:

* Logistic Regression
* Random Forest
* Extra Trees
* HistGradientBoosting
* XGBoost
* LightGBM

Models are evaluated using cross-validation and an independent holdout test split.

---

## Evaluation Metrics

The following performance metrics are reported:

* Accuracy
* Balanced accuracy
* Sensitivity
* Specificity
* Precision / positive predictive value
* Negative predictive value
* F1-score
* F2-score
* Matthews correlation coefficient
* AUROC
* AUPRC
* Brier score
* Log loss
* Bootstrap 95% confidence intervals

---

## Threshold Optimization

The notebook does not rely only on the default probability threshold of 0.50. It also performs task-specific threshold optimization:

* Diagnosis and management tasks use the **Youden index**.
* Severity prediction uses an **F2-score-optimized threshold** to prioritize sensitivity, because missing complicated appendicitis may be clinically more harmful than over-alerting.

This allows severity prediction to be interpreted as a high-sensitivity risk-stratification task rather than a definitive classifier.

---

## Explainability

Explainability is provided using complementary approaches:

1. **Univariate statistical testing**
   Mann–Whitney U tests and chi-square tests with FDR correction.

2. **Permutation importance**
   Model-independent feature importance based on AUROC decrease.

3. **F2-based permutation importance**
   Severity-specific feature importance emphasizing detection of complicated cases.

4. **SHAP explainability**
   SHAP global bar plots, beeswarm plots, and mean absolute SHAP importance tables.

5. **Consensus feature importance**
   Combined ranking from permutation importance and SHAP importance.

---

## Outputs Generated by the Notebook

After execution, the notebook creates:

```text
/content/PediAppend_MissXAI/
│
├── figures/
│   ├── missingness plots
│   ├── target distribution plots
│   ├── model comparison plots
│   ├── feature-set comparison plots
│   ├── confusion matrices
│   ├── ROC curves
│   ├── precision-recall curves
│   ├── calibration curves
│   ├── decision-curve plots
│   ├── permutation-importance plots
│   └── SHAP plots
│
└── tables/
    ├── dataset audit tables
    ├── target distribution tables
    ├── feature-set tables
    ├── model performance tables
    ├── bootstrap confidence interval tables
    ├── threshold optimization tables
    ├── permutation-importance tables
    ├── SHAP importance tables
    └── manuscript-ready summary tables
```

At the end, the notebook exports all results into a compressed ZIP file.

---

## How to Run

### Option 1: Run in Google Colab

1. Open `PediAppend-MissXAI.ipynb` in Google Colab.
2. Run Cell 1 to install required packages.
3. When prompted, upload:

```text
app_datar1.xlsx
```

4. Run all cells in order.
5. Download the generated ZIP output file.

### Option 2: Run locally

Install the required packages:

```bash
pip install openpyxl xgboost lightgbm shap statsmodels tabulate scikit-learn pandas numpy matplotlib scipy
```

Then run the notebook in Jupyter Notebook or JupyterLab.

---

## Requirements

Recommended Python version:

```text
Python 3.10 or higher
```

Main Python libraries:

```text
numpy
pandas
matplotlib
scipy
statsmodels
scikit-learn
xgboost
lightgbm
shap
openpyxl
tabulate
```

---

## Reproducibility

The notebook uses a fixed random seed:

```text
RANDOM_STATE = 42
```

The default split is:

```text
80% training
20% holdout testing
```

Cross-validation uses stratified folds where class counts permit.

---

## Important Notes

This repository is intended for academic research and reproducibility. The models are not intended for direct clinical deployment.

The results should be interpreted as retrospective machine-learning findings from a public dataset. External validation, prospective testing, and clinical workflow evaluation are required before any real-world clinical use.

Severity prediction should be interpreted cautiously as risk stratification, especially because complicated appendicitis is less frequent and threshold choice strongly affects sensitivity and specificity.

---

## Suggested Study Title

```text
PediAppend-MissXAI: Missingness-Aware Explainable Machine Learning for Pediatric Appendicitis Diagnosis and Surgical Decision Support
```

Alternative extended title:

```text
PediAppend-MissXAI: Missingness-Aware Explainable Machine Learning for Pediatric Appendicitis Diagnosis, Surgical Management, and Severity Risk Stratification
```

---

## Author

**Partha Pratim Ray**
Department of Computer Applications
Sikkim University, India

Email:

```text
parthapratimray1986@gmail.com
ppray@cus.ac.in
```

---

## License

Please check the original dataset license and terms of use from the Zenodo record before redistributing or reusing the dataset.

For the code in this repository, a permissive license such as the MIT License may be added if desired.

---

## Disclaimer

This repository is for research and educational purposes only. It does not provide medical advice and should not be used as a clinical decision-making tool without independent validation and regulatory/ethical approval.
