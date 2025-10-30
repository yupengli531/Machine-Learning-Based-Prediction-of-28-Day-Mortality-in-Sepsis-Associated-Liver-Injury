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

## Dataset Sources

All datasets analyzed during this study are publicly available on PhysioNet:
- [MIMIC-IV v2.2](https://physionet.org/content/mimiciv/2.2/)
- [MIMIC-III v1.4](https://physionet.org/content/mimiciii/1.4/)
- [eICU v2.0](https://physionet.org/content/eicu-crd/2.0/)

Access requires credentialed approval via the [PhysioNet Data Use Agreement](https://physionet.org/about/licenses/).

---

## Study Population
Criteria:
- Age >= 18
- With Sepsis (Sepsis 3.0 criteria)
- SOFA score >=2
- Infections
- ICU stay >= 24 h
- At least one occurrence of SALI
- TBIL > 2 and INR > 1.5
- With sepsis-related liver injury
- Without other types of liver disease
- Without HIV infection
- Non-pregnant
- With Biochemical and coagulation tests within 24 h of admission to the ICU

![Study Population](https://github.com/yupengli531/Machine-Learning-Based-Prediction-of-28-Day-Mortality-in-Sepsis-Associated-Liver-Injury/blob/71100009449bbca4d77cb6207ff9525bcc1950ec/Study%20Population.png)

---

## Data Collection
Clinical data were extracted from the MIMIC-IV, MIMIC-III, and eICU-CRD databases using **Structured Query Language (SQL)**, **MySQL**, and **Python**. Feature selection was guided by existing literature, clinical relevance, and expert recommendations to capture early physiological status within the first 24 hours of ICU admission.

Diagnoses were identified using the **International Classification of Diseases, Ninth and Tenth Revisions (ICD-9-CM and ICD-10-CM)**. 

A total of **68 clinical features** were initially extracted from MIMIC-IV and organized into **eight categories**:

![Overview of Selected Variables]()

Both **minimum and maximum** values of vital signs and laboratory results were computed to capture physiological fluctuations during the initial 24 hours of ICU stay.

The same feature set was consistently extracted from **MIMIC-III** and **eICU-CRD** to ensure cross-dataset comparability and reduce bias.

---

## Data Preprocessing

Data preprocessing ensured feature comparability and model robustness before training and validation. 

The MIMIC-IV dataset was split into **training (N=578)** and **internal validation (N=248)** cohorts using a **stratified 7:3 split** to prevent data leakage. The class distribution was balanced (61:39), so resampling was not applied.

A total of **103 extracted features** were initially included, and **88 remained** after excluding those with >20% missing values. 

Key preprocessing steps included:

- **Missing Data Handling:** Median imputation for remaining missing values (<20%).  
- **Outlier Treatment:** Winsorization (1st–99th percentile capping).  
- **Normalization:** Log transformation for highly skewed variables.  
- **Multicollinearity Control:** Features with **VIF > 20** were removed.  
- **Correlation Reduction:** Predictors with **correlation > 0.85** were excluded.  
- **Scaling:** Numerical features standardized using `StandardScaler` (fit on training set).  
- **Encoding:** Categorical variables (e.g., gender, race) transformed via label and one-hot encoding.  

---
## Feature Selection

- **Permutation Feature Importance (PFI)** was applied using the **optimized XGBoost model**, tuned via grid search with **10-fold cross-validation**.  
- XGBoost hyperparameters included:
  - `learning_rate = 0.1`  
  - `max_depth = 5`  
  - `n_estimators = 200`  
  - `subsample = 0.8`  
  - `colsample_bytree = 1`

PFI quantified the decrease in model performance after shuffling each feature, providing an unbiased, model-agnostic estimate of predictive contribution.  

The **top 30 features** were retained for final modeling—key variables.

![top 30 features]()

![heatmap]()

---

## Model Performance
Eight machine learning models were developed and compared:
- **Logistic Regression**
- **Elastic-Net Logistic Regression (cv-glmnet)**
- **Decision Tree**, **Random Forest**
- **Support Vector Machine (SVM)**
- **Extreme Gradient Boosting (XGBoost)**
- **k-Nearest Neighbors (KNN)**
- **Linear Discriminant Analysis (LDA)**

Internal Validation (MIMIC-IV):
- **Best Model**: XGBoost: AUROC **0.8556** (95% CI: 0.807-0.898)

![roc curves 1]()

External Validation (MIMIC-III):
- **Best Model**: Random Forest: AUROC **0.8964** (95% CI: 0.845-0.943)

![roc curves 2]()

External Validation (eICU-CRD):
- **Best Model**: XGBoost: AUROC **0.6966** (95% CI: 0.594-0.790)

![roc curves 3]()

---

## Model Interpretability

- **SHAP Analysis:** Identified global feature importance;
- Top 5 key indicators:
    - *Lactate*
    - *BUN*
    - *Hemoglobin*
    - *Heart Rate*
    - *DiaBP*

![shap]()

- **LIME Analysis:** Provided case-level interpretability for individual mortality predictions.  
  - Green bars → increased mortality risk  
  - Red bars → protective features

![lime]()

---

## Code Availability

The code is provided [here](https://drive.google.com/drive/folders/1vuUVePIsRNfKCt5bVJPKsBdrT7vsfaVq?usp=sharing).



