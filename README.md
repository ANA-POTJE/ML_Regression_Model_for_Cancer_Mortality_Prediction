# ML_Regression_Models_for_Cancer_Mortality_Prediction
CAPSTONE PROJECT

APPLIED DATA SCIENCE BOOTCAMP - CAMBRIDGE SPARK

Author: Ana Beatriz Potje

Date: 26/03/2020

The objective of this project is to compare results between four machine learning regression models
implemented in Python code, and define the one which best predicts a target variable on a given dataset. 
SHAP (SHapley Additive exPlanations) approach is to be used to explain the feature correlations of the best model.
The best predicting model is then to be compared with "CausaLens ML Prediction Tool" to determine which model returns best
prediction results as well as the most influential features used for the target prediction.

# Scope
“Cancer Mortality Prediction in the US Counties” dataset was provided on the web page:
https://data.world/nrippner/ols-regression-challenge . “TARGET_deathRate” – the target variable – is the mean
per capita (100,000) of cancer mortalities per US county in the period between 2010 and 2016 (or 2013 Census
Estimates). This dataset contains 3,047 rows and 34 features for each of the US counties for this period, which
are described in the document “Capstone Project CausaLens - Ana Potje – APPENDIX”.

cancer_reg.csv : dataset used for model building.

XXXXXXXXXXXXXXXXXXXXXXXX.ipynb: the jupyter notebook containing code.

"Capstone Project CausaLens - Ana Potje.pdf" : final report

"Capstone Project CausaLens - Ana Potje - APPENDIX.pdf" : data dictionary

SHAP_Analysis.png : image displayed in README.md file


This project is organized as follows:

# STEP 1: Exploratory Data Analysis
In order to deploy the best machine learning model to predict our target variable (TARGET_deathRate), the dataset was prepared and unwanted issues removed. The following operations were then performed in a Jupyter Notebook (Python) environment: categorical features mapped to integer values; dropped some categorical features not required; filled in null values; removed Outliers and finally scaled the dataset.

# STEP 2: Train, Test & Evaluate the Data
The dataset was split into train (64%), validation (16%) and test (20%). The regression models used are below:

Regression Model | Package / Class | Parameters | L2 Norm | R-Squared
---------------- | ----------------|------------|---------|----------
Linear Regression (baseline) | Scikit-learn / LinearRegression | default values | 260.79 | 0.4257
Decision Tree Regression | Scikit-learn / DecisionTreeRegressor | P_DTR (below) | 336.70 | 0.3233
Random Forest Regression | Scikit-learn / RandomForestRegressor | P_RFR (below) | 260.03 | 0.4660
SVR | Scikit-learn / SVR | kernel = rbf, C = 0.5 | 262.18 | 0.4511


P_DTR = criterion = mse, max_leaf_nodes = 100, max_depth = 6,min_samples_leaf = 20, min_samples_split = 3

P_RFR = criterion = mse, max_depth = 8, max_leaf_nodes = 100, min_samples_leaf = 10, min_samples_leaf = 5

# Best Model: Random Forest Regression
Random Forest Regression had the highest R-Squared value (0.4660), its Top Features and SHAP analysis are below:

n. | Variable | Importance
---|----------|-----------
1 | PctBachDeg25_Over | 0.32
2 | incidenceRate | 0.22
3 | avgDeathsPerYear | 0.05
4 | medIncome | 0.04

![SHAP Analysis](https://github.com/ANA-POTJE/ML_Regression_Models_for_Cancer_Mortality_Prediction/blob/master/SHAP_Analysis.png)

# CausaLens Best Model: XGBRegressor (0.470 R-Squared)
CausaLens platform was run on the same dataset, data was split into Train (40%), Validation (20%), Test (20%) and Holdout (20%). The tool generated 69 models. The best score was achieved with model ensemble.XGBRegressor (0.470 R-Squared), using 13 features and the parameters: l1 = 0.00, l2 = 0.00, colsample_bytree = 0.50, gamma = 1.00, min_child_weight = 2.00, xgb_extras = {}, max_depth = 2.00, n_boosting_estimators = 145.00, learning_rate = 0.13 and subsample = 0.65.

# Conclusion
Comparing the metrics of models in scope, it can be concluded that the CausaLens model ensemble.XGBRegressor with the given set of parameters provides best predictions, R-Squared metric of 0.470. This metric is found to be better than the Random Forest Regression, the best of four prediction models considered in this project.

The feature contribution to the top 20% of the CausaLens discovered models shows that IncidenceRate and PctBachDeg25_Over are the two most influential features – the same result that came from the Random Forest Regression model, therefore confirming the importance of these features for predicting the target DeathRate feature.
Please refer to file “Capstone Project CausaLens - Ana Potje - APPENDIX.pdf” for data dictionary details.
