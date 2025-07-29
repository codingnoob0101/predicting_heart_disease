The data can be downloaded through: 'https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction/data'

About This Project:
Cardiovascular disease is very common in daily life, it's seriousness and acute nature of this disease makes it costly if being mistreated.
Early diagnostic of cardiovascular disease is critical for being one step ahead, preventing further progression and worsening of the disease.
This project aims to predict whether the patient has heart disease with 11 variables given.

The data contain 11 variables and 1 target column

The variables are:
- Age: age of the patient [years]
- Sex: sex of the patient [M: Male, F: Female]
- ChestPainType: chest pain type [TA: Typical Angina, ATA: Atypical Angina, NAP: Non-Anginal Pain, ASY: Asymptomatic]
- RestingBP: resting blood pressure [mm Hg]
- Cholesterol: serum cholesterol [mm/dl]
- FastingBS: fasting blood sugar [1: if FastingBS > 120 mg/dl, 0: otherwise]
- RestingECG: resting electrocardiogram results [Normal: Normal, ST: having ST-T wave abnormality (T wave inversions and/or ST elevation or - depression of > 0.05 mV), LVH: showing probable or definite left ventricular hypertrophy by Estes' criteria]
- MaxHR: maximum heart rate achieved [Numeric value between 60 and 202]
- ExerciseAngina: exercise-induced angina [Y: Yes, N: No]
- Oldpeak: oldpeak = ST [Numeric value measured in depression]
- ST_Slope: the slope of the peak exercise ST segment [Up: upsloping, Flat: flat, Down: downsloping]

The target column is: 
- HeartDisease: output class [1: heart disease, 0: Normal]

The workflow is:
1) split the training and testing data (splitting before handling null values to prevent data leakage)
2) drop the only data entry with 0 in 'RestingBP'
3) perform grouped-median imputation to the column 'Cholesterol' (grouping the 'cholesterol' according to heart disease and normal, then compute median of each group for imputation) (only use median from training set for imputation in both training and testing data, to prevent data leakage)
4) Encode the categorical variables with One-Hot Encoding
5) train and finetune Random Forest classifier and XGboost model
    - Random Forest Classifier: trained a model with satisfying result. The model has been saved into the 'model' file. 
    - XGBoost model: Trained a model with satisfying result. The model has been saved into the 'model' file. 
6) evaluate the performance of each model with testing set


Result:

Random Forest Classifier:
- After tuning hyperparameters, the final model acheive Accuracy : 0.8804, Precision : 0.8922, Recall : 0.8922, ROC-AUC: 0.9397
- The hyperparameters selected are: 'criterion': 'gini', 'max_depth': 10, 'max_features': 'log2', 'max_leaf_nodes': 40, 'min_samples_leaf', 2,'min_samples_split': 2, 'n_estimators': 225

XGBoost:
- After tuning hyperparameters, the final model acheive Accuracy : 0.9022, Precision : 0.9118, Recall : 0.9118, ROC-AUC: 0.9534
- The hyperparameters selected are:'colsample_bytree': 0.8, 'learning_rate': 0.1, 'max_depth': 2, 'min_child_weight': 1, 'n_estimators': 95, 'subsample': 0.6

- Given the result above, both models provide sufficient inference power, with XGBoost has better result at 90.22% accuracy vs 88.04% of Random Forest