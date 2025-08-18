# 🩺 Pima Indians Diabetes Prediction --- End-to-End ML Project

A complete **machine learning pipeline** to predict diabetes risk using
the **Pima Indians Diabetes Dataset**.\
This notebook covers **data cleaning, EDA, feature engineering, model
building, evaluation, interpretation, and deployment artifacts**.

------------------------------------------------------------------------

## 🚀 Main Steps

**Data Cleaning** - Replace impossible zeros in medical columns
(`Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, `BMI`) with
`NaN`. - Impute missing values using **median** (robust to outliers). -
Check for and remove duplicates.

**Feature Engineering** - Create **Age groups** and **BMI categories**.\
- Add interaction features (`Age×BMI`, `Glucose×BMI`,
`Pregnancies/Age`).\
- Ensure transformations are inside pipelines (no leakage).

**EDA & Visualization** - **Class distribution:** \~65% non-diabetic
vs. 35% diabetic.\
- **Correlation heatmap:** Glucose is the most correlated with
diabetes.\
- **Boxplots/Histograms:** Diabetic patients tend to have **higher
Glucose, BMI, Age**.\
- **Grouped insights:** Diabetes rate increases sharply after 40 and
with obesity.\
- Interactive **Plotly charts** (Glucose vs BMI with outcome clusters).

**Modeling** - Baselines: Dummy classifier (most frequent).\
- Models: **Logistic Regression, Random Forest, XGBoost**.\
- **SMOTE** for handling class imbalance.\
- **5-fold Cross-validation** with multiple metrics (Accuracy,
Precision, Recall, F1, ROC-AUC).

**Threshold Tuning** - Precision--Recall curves for best model.\
- Lowering threshold (0.5 → 0.3) increases **recall** (catching more
diabetics) but raises false positives.

**Model Interpretation** - **Permutation importance:** Top drivers =
Glucose, BMI, Age, Pregnancies.\
- **Error analysis:** False negatives cluster in moderate Glucose/BMI
range.\
- **Learning curves:** indicate model stabilizes with more data.

**Deployment Artifacts** - Save final tuned pipeline (`joblib`) +
optimal threshold for production scoring.

------------------------------------------------------------------------

## 📈 Results Summary

  --------------------------------------------------------------------------------
  Model                  Accuracy    Precision    Recall     F1         ROC-AUC
  ---------------------- ----------- ------------ ---------- ---------- ----------
  Logistic Regression    **0.72**    0.59         **0.69**   **0.63**   0.81

  Random Forest          0.71        0.58         0.59       0.59       **0.82**

  XGBoost                0.73        0.61         0.63       0.62       0.81
  --------------------------------------------------------------------------------

-   **Best for screening:** Logistic Regression (high recall & F1 at
    tuned thresholds).\
-   **Strong discrimination:** All models ROC-AUC \> 0.80.\
-   **Tuned RF/XGB** edge slightly in AUC but at higher cost in
    complexity/runtime.

------------------------------------------------------------------------

## 💡 Recommendations

-   **Clinical screening:** Use Logistic Regression with **lowered
    threshold** to minimize missed diabetics.\
-   **High-risk patients:** Age ≥ 40 with high BMI & Glucose →
    prioritize for early testing.\
-   **Model maintenance:** Retrain quarterly, monitor drift, add
    lifestyle/family history features when available.\
-   **Deployment:** Integrate into clinics via a lightweight scoring API
    (saved `joblib` pipeline).

------------------------------------------------------------------------

## 💵 Business Impact Scenario

-   Screening **1000 patients/month** with dataset prevalence (35%).\
-   Lowering threshold → more early detections → fewer complications.\
-   Assuming \~30% reduction in late-stage complications → **significant
    cost savings** despite extra follow-ups.\
-   Full cost--benefit table included in the notebook.

------------------------------------------------------------------------

## 📦 Artifacts

-   **Final Pipeline:** `artifacts/pima_best_pipeline.joblib`\
-   Includes: preprocessing steps, feature engineering, SMOTE,
    classifier, and optimal threshold.\
-   Ready for **real-world deployment** in clinics or healthcare apps.
