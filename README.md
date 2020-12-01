# Readme


## Introduction

## Executive Summary

In this report, we construct several model to predict the sale price of an Ames, IA home based on certain numeric and categorical features, rank each model using various metrics, and tune those model parameters to improve model accuracy.  

## Contents

Our work is split into two notebooks. The notebooks and contents are listed below:

- `eda_and_data_cleaning`
 - Data cleaning for train data
  - Identify and fix missing rows (imputation or removal)
  - Identify and fix outliers
  - Identify and remove (categorical) features that are heavily skewed in a single value
 - Data exploration for training data
  - Plot distribution of categorical values
  - Plot relationship between numerical values and `saleprice` 
 - Data cleaning for test data
  - Impute missing data 
- `modeling`
 - Preprocessing takes place here
  - Column transformer was used to scale and one-hot encode data
 - Fit the following models:
  - Linear Regression
  - k-Nearest Neigbors Regressor (KNN)
  - Ridge ($L^2$-norm)
  - LASSO ($L^1$-norm)
 - Grid search to optimize KNN and LASSO hyperparameters

## Datasets and Data Dictionary

Dataset was obtained from https://www.kaggle.com/c/dsi-us-11-project-2-regression-challenge/data for the DSI-11 Regression Challenge hosted on Kaggle. The data we ended up using is as follows:

| Feature        | Type    | Description                                                            |
|----------------|---------|------------------------------------------------------------------------|
| saleprice      | int64   | Target Variable : the property's sale price in dollars                 |
| gr_liv_area    | int64   | Above grade (ground) living area square feet                           |
| year_remod/add | int64   | Remodel date (same as construction date if no remodeling or additions) |
| 1st_flr_sf     | int64   | First Floor square feet                                                |
| overall_qual   | int64   | Overall material and finish quality                                    |
| totrms_abvgrd  | int64   | Total rooms above grade (does not include bathrooms)                   |
| garage_yr_blt  | float64 | Year garage was built                                                  |
| garage_area    | float64 | Size of garage in square feet                                          |
| full_bath      | int64   | Full bathrooms above grade                                             |
| total_bsmt_sf  | float64 | Total square feet of basement area                                     |
| year_built     | int64   | Original construction date                                             |
| mas_vnr_area   | float64 | Masonry veneer area                                                    |
| exterior_1st   | object  | Exterior covering on house                                             |
| lot_shape      | object  | General Shape of property                                              |
| neighborhood   | object  | Physical locations within Ames city limits                             |
| foundation     | object  | Type of foundation                                                     |
| mas_vnr_type   | object  | Masonry veneer type                                                    |
| exter_qual     | object  | Exterior material quality                                              |
| garage_type    | object  | Garage location                                                        |
| bsmtfin_type_1 | object  | Quality of basement finished area                                      |
| exterior_2nd   | object  | Exterior covering on house (if more than one material)                 |
| kitchen_qual   | object  | Kitchen quality                                                        |
| season_sold    | object  | Season sale took place                                                 |
| garage_finish  | object  | Interior finish of the garage                                          |
| heating_qc     | object  | Heating quality and condition                                          |
| fireplace_qu   | object  | Fireplace Quality                                                      |
| bsmt_qual      | object  | Height of the Basement                                                 |
| house_style    | object  | Style of dwelling                                                      |


## Results and Conclusions

The most accurate model is the `KNeighborsRegressor`, but it suffers is less interpretable than one of the other linear regression models, particularly LASSO. LASSO tells you which features are important, and which can be eliminated from the model (these have `coefficient = 0`).

### Key Results

The most accurate model is the `KNeighborsRegressor` with test $R^2$ equal to $~84%$ and mean squared error of $1146395582$ which are the highest and lowest respectively among the models fitted. It suffers is less interpretable than one of the other linear regression models, particularly LASSO. LASSO tells you which features are important, and which can be eliminated from the model (these have `coefficient = 0`).

### Recommendations

This model will likely generalize to other Midestern U.S. cities with sales taking place in a comparable time period and city size since most of the features used in this model is information filed with the paperwork used to obtain building permits. Collecting aggregate climate and economic data for the neighborhood the house is located may help the model generalize beyond Ames.