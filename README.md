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

## 📈 Results Summary *(replace with your run)*

| Model               | Accuracy | Precision | Recall | F1   | ROC-AUC |
|---------------------|----------|-----------|--------|------|---------|
| Logistic Regression | **0.72** | 0.59      | **0.69** | **0.63** | 0.81    |
| Random Forest       | 0.71     | 0.58      | 0.59   | 0.59 | **0.82** |
| XGBoost             | 0.73     | 0.61      | 0.63   | 0.62 | 0.81    |

- **Best for screening**: Logistic Regression (higher Recall/F1 at tuned thresholds).  
- **Operating threshold (cost-optimal)**: `<best_thr_cost>` with `Cost_FP=1, Cost_FN=7`.  
- **Test @ operating threshold**: `TP=<TP>, FP=<FP>, FN=<FN>, TN=<TN> | Precision=<P>, Recall=<R>, F1=<F1>, ROC-AUC=<AUC> | Expected cost=<COST>`.

---

## 🔧 Quickstart
1. Run the notebook end-to-end (keeps all steps inside a single Pipeline — no leakage).  
2. Artifacts saved to `./artifacts/pima_best_pipeline.joblib` (pipeline, features, thresholds).  
3. Optional batch scoring: `python inference.py input.csv predictions.csv`  
   - CSV columns: `Pregnancies, Glucose, BloodPressure, SkinThickness, Insulin, BMI, DiabetesPedigreeFunction, Age`.

---

## 📦 Artifacts
- `artifacts/pima_best_pipeline.joblib`  
  Includes preprocessing, feature engineering, SMOTE, classifier, **validation threshold**, **operating threshold**, feature list, and CV summary.

