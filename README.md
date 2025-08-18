# 🩺 Pima Indians Diabetes Prediction — End-to-End ML Project

A compact, production-minded pipeline to predict diabetes risk from routine clinical measurements (Pima Indians dataset).  
Covers **data cleaning → EDA → feature engineering → modeling → calibration & cost-aware threshold → interpretation → deployable artifacts**.

---

## 🚀 Main Steps

**Data Cleaning**
- Replace impossible zeros in medical columns (`Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, `BMI`) with `NaN`.
- Median imputation (robust to outliers). Remove duplicates.

**Feature Engineering**
- Age groups, BMI categories.
- Interactions: `Age×BMI`, `Glucose×BMI`, `Pregnancies/Age`.
- All transformations inside a **leakage-safe Pipeline**.

**EDA & Visualization**
- Class imbalance: ~65% non-diabetic vs ~35% diabetic.
- Correlation: **Glucose** strongest with outcome; diabetics tend to have higher **Glucose/BMI/Age**.
- Plotly: Glucose vs BMI clusters by outcome.

**Modeling**
- Baseline: Dummy.  
- Models: **Logistic Regression, Random Forest** (XGBoost if available).  
- **Imbalance**: SMOTE and/or class weights.  
- **5-fold Stratified CV** with Accuracy, Precision, Recall, F1, ROC-AUC.

**Threshold & Calibration (Pro touch)**
- Tune threshold on validation (maximize **F1** for screening).  
- **Isotonic calibration** + **Reliability plot** for trustworthy probabilities.  
- **Cost Curve** to pick an **operating threshold** minimizing expected cost (typically `Cost_FN > Cost_FP`).

**Interpretation**
- **Permutation importance**: key drivers typically **Glucose, BMI, Age, Pregnancies**.
- Learning curves for data sufficiency.

**Deployment Artifacts**
- Export single `joblib` bundle: pipeline + features + thresholds (validation & operating).

---

## 📦 Artifacts
- `artifacts/pima_best_pipeline.joblib`  
  Includes preprocessing, feature engineering, SMOTE, classifier, **validation threshold**, **operating threshold**, feature list, and CV summary.

