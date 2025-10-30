# Machine Learning-Based Prediction of 28-Day Mortality in Sepsis-Associated Liver Injury (SALI)

**Background:**  
Sepsis-associated liver injury (SALI) is a frequent and severe complication of sepsis, significantly increasing mortality risk. Early detection of high-risk patients is essential but challenging due to the nonspecific and complex nature of SALI. This study applies machine learning (ML) models to predict 28-day mortality within the first 24 hours of ICU admission.

**Methods:**  
A total of **1,157 patients** were included (826 from MIMIC-IV, 225 from MIMIC-III, and 106 from eICU). The MIMIC-IV dataset was divided into training and internal validation sets (7:3), while MIMIC-III and eICU were used for external validation. 30 clinically relevant features were selected. Eight ML algorithms—**Logistic Regression**, **Elastic-Net Logistic Regression (cv-glmnet)**, **Decision Tree**, **Random Forest**, **Support Vector Machine (SVM)**, **Extreme Gradient Boosting (XGBoost)**, **k-Nearest Neighbors (KNN)**, and **Linear Discriminant Analysis (LDA)**—were evaluated using AUROC, accuracy, precision, recall, F1-score, and specificity. Model interpretability was enhanced via **SHAP** and **LIME** analyses.

**Results:**  
XGBoost achieved the best overall performance with an **AUROC of 0.8556 (95% CI: 0.807–0.898)**, **accuracy of 0.7702**, **recall of 0.8469**, and **specificity of 0.7200**.  
Key predictive features identified included **lactate**, **blood urea nitrogen (BUN)**, **heart rate**, **hemoglobin**, and **diastolic blood pressure (DiaBP)**.  
Both SHAP and LIME analyses provided global and patient-level interpretability.

**Conclusion:**  
The proposed XGBoost-based model demonstrates strong predictive capability for early mortality in SALI patients and enhances clinical decision support for ICU management.

---

## 🧩 Dataset Sources

All datasets analyzed during this study are publicly available on PhysioNet:
- [MIMIC-IV v2.2](https://physionet.org/content/mimiciv/2.2/)
- [MIMIC-III v1.4](https://physionet.org/content/mimiciii/1.4/)
- [eICU v2.0](https://physionet.org/content/eicu-crd/2.0/)

Access requires credentialed approval via the [PhysioNet Data Use Agreement](https://physionet.org/about/licenses/).

---

## ⚙️ Methodology Overview

| Step | Description |
|------|--------------|
| **1. Data Extraction (SQL)** | Extracted adult SALI patients (≥18 years) with ICU stay ≥24h from MIMIC-IV, MIMIC-III, and eICU. |
| **2. Feature Selection** | 30 clinical variables, including demographics, vital signs, lab indicators, comorbidities, infection sites, interventions, clinical measurements, and severity scores, were used. |
| **3. Model Training** | Applied eight ML algorithms with 5-fold cross-validation. |
| **4. Model Evaluation** | Evaluated using AUROC, accuracy, precision, recall, F1, and specificity. |
| **5. Interpretability** | Conducted SHAP (global) and LIME (local) analyses for clinical transparency. |

---


## 🧮 Model Performance Summary

---

## 🔍 Model Interpretability

- **SHAP Analysis:** Identified global feature importance; *Lactate*, *BUN*, *Hemoglobin*, *Heart Rate*, and *DiaBP* were top predictors.  
- **LIME Analysis:** Provided case-level interpretability for individual mortality predictions.  
  - Green bars → increased mortality risk  
  - Red bars → protective features
 
---

## Code Availability

The code is provided [here](https://drive.google.com/drive/folders/1vuUVePIsRNfKCt5bVJPKsBdrT7vsfaVq?usp=sharing).



