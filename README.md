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

This project is organized as follows:

# STEP 1: Exploratory Data Analysis
In order to deploy the best machine learning model to predict our target variable (TARGET_deathRate), the dataset was prepared and unwanted issues removed. The following operations were then performed in a Jupyter Notebook (Python) environment: categorical features mapped to integer values; dropped some categorical features not required; filled in null values; removed Outliers and finally scaled the dataset.

# STEP 2: Train, Test & Evaluate the Data
The dataset was split in train (64% of the data), validation (16% of the data) and test subsets (20% of the data). 
The metrics used to evaluate and compare the models were "L2 norm" and "R-Squared".

The regression models used are below:

Regression Model | Package / Class | Parameters | L2 Norm | R-Squared
---------------- | ----------------|------------|---------|----------
Linear Regression (baseline) | Scikit-learn / LinearRegression | default values | 260.79 | 0.4257
Decision Tree Regression | Scikit-learn / DecisionTreeRegressor | P1 | 336.70 | 0.3233
Random Forest Regression | Scikit-learn / RandomForestRegressor | P2 | 260.03 | 0.4660
SVR | Scikit-learn / SVR | kernel = rbf, C = 0.5 | 262.18 | 0.4511

P1 = criterion = mse, max_leaf_nodes = 100, max_depth = 6,min_samples_leaf = 20, min_samples_split = 3
P2 = criterion = mse, max_depth = 8, max_leaf_nodes = 100, min_samples_leaf = 10, min_samples_leaf = 5


