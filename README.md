# 🩺 Pima Indians Diabetes Prediction — End-to-End ML Project

A complete machine learning pipeline to predict diabetes risk using the **Pima Indians Diabetes Dataset**.  
Covers data cleaning, exploratory analysis, feature engineering, model building, evaluation, and actionable recommendations.

---

## 🚀 Main Steps
1. **Data Cleaning:**  
   - Replace impossible zeros in medical columns with `NaN`.  
   - Impute missing values using median (robust to outliers).  
2. **Feature Engineering:**  
   - Age groups, BMI categories, and interaction features (Age×BMI, Glucose×BMI, Preg/ Age).  
3. **EDA & Visualization:**  
   - Class distribution (~65% non-diabetic, ~35% diabetic)  
   - Correlation analysis (Glucose most correlated with outcome)  
   - Boxplots & distributions showing higher Glucose/BMI/Age in diabetics  
4. **Modeling:**  
   - Logistic Regression, Random Forest, XGBoost  
   - SMOTE for class balancing  
   - Cross-validation and ROC/PR analysis  
5. **Model Interpretation:**  
   - Feature importance (Glucose, BMI, Age, Pregnancies dominate)  
   - Threshold tuning for recall/precision trade-off  
6. **Error Analysis:**  
   - False negatives cluster in moderate Glucose/BMI range  
   - Lowering threshold from 0.5→0.3 raises recall (69%→89%) at cost of more false positives  

---

## 📈 Results Summary
| Model               | Accuracy | Precision | Recall | F1   | ROC-AUC |
|---------------------|----------|-----------|--------|------|---------|
| Logistic Regression | 0.72     | 0.59      | 0.69   | 0.63 | 0.81    |
| Random Forest       | 0.71     | 0.58      | 0.59   | 0.59 | 0.82    |
| XGBoost             | 0.73     | 0.61      | 0.63   | 0.62 | 0.81    |

**Best for screening:** Logistic Regression (highest recall & F1 at tuned thresholds)  
**Strong discrimination:** All models ROC-AUC > 0.80

---

## 💡 Recommendations
- **Screening policy:** Use Logistic Regression with lowered threshold to capture more diabetics.  
- **High-risk group:** Age ≥ 40 + high BMI + high Glucose.  
- **Model maintenance:** Retrain regularly, monitor drift, and add lifestyle/family history features.  
- **Deployment:** Integrate into clinic workflow for early detection support.

---

## 💵 Business Impact Scenario
- Screening 1000 patients/month (dataset prevalence)  
- Lowered threshold → more early detections → reduced complications (~30% assumption)  
- Net benefit = savings from avoided complications − extra follow-up cost for false positives.  
- Detailed impact table included in the notebook.

---
