`
# Beyond Accuracy: Evaluating Voice-Based Parkinson's Symptom Severity Prediction Across Unseen participants.


## Overview
This Machine Learning project explores whether voice measurments can estimate Parkinson's symptom severity and whether a model performance generalizes to participant not seen during training.

## Data Source
- **Primary target: ** 'total_UPDRS'
- **Task: ** Regression
- **Dataset Origin:** Dataset was obtained from UCI Machine Learning repository *Parkinson's Telemonitoring* (official source: https://archive.ics.uci.edu/dataset/189/parkinsons).
- **Description:** Contains participants' demographic data and voice-based measurements.

## research question
How well can a voice-based measurements estimate 'total_UPDRS' for those participant who were not represented in model training?

## Workflow
### 1. Data Cleaning and preprocessing
- Download data from official source. 
- Check missing values, duplicates, ranges and distribution.

### 2. Exploratory Data Analysis (EDA)
- Describe participants characteristics and 'total_UPDRS' distribution.
- Explores voice measurements and its realtionship with the target.

### 3. Model Selection and Benchmarking
-Split the dataset for training and testing data
-Compare performance of multiple models including linear, Ridge, Lasso, ElasticNet, RandomForest, XGBoost Regressors. 

### 4. Random Row Split
- Random Split the dataset by rows for training and testing data (Run a conventional train_test_split).
- Train and test the models based on random split by rows such that recordings form the same participant may appear in training as well as testing data.
- Random Forest Regressor achieved 0.147 Mean Absolute Error (MAE) and 0.551 RMSE score and outperformed the other models based on given evalutaion metrics.
- It creates Opimistic yet misleading results due to Data Leakage.

### 5. Participant-level GroupKFolds Validation
- Dataset split using GroupKFold (n_split=5) with groups='subject#' for participant-level validation.
- In each fold, fit the models to training participants and predict the rest of participants.
- Compare the same models on the same folds.
- Record MAE, RMSE and R2 score for each fold, Report mean and Std of MAE, RMSE, and R2.

## Key Insights & Feature Importance
- Random Forest regressor outperformed the other models when dataset was split randomnly .
- In GroupKFolds participant-level Validation, No model showing overall superior predictive capability strongly suggest that model is unable to get generalized on unseen participant data.
- Feature Importance Analysis show Age, Sex, test_time and DFA and RPDE appeared to be the most important features for prediction.

## Limitation
- This dataset contain repeated recording form relatively small number of participants.
- Association do not establish causation
- Independant external validation is needed before broader claims.


This is an educational research project, not a diagnostic tool or substitute for clinical assessment.