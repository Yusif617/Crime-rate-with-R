# **Crime Rate Prediction using Regression in R**

This repository contains an R script that performs a regression analysis to predict violent crime rates based on various socioeconomic factors. The script demonstrates data loading, preprocessing, feature selection using Variance Inflation Factor (VIF), fitting a Generalized Linear Model (GLM) using `h2o`, evaluating the model's performance, and visualizing the results.

## **Table of Contents**

* [Project Description](#project-description)
* [Dataset](#dataset)
* [Methodology](#methodology)
* [Prerequisites](#prerequisites)
* [How to Run](#how-to-run)
* [Key Steps in the Code](#key-steps-in-the-code)
* [Results](#results)
* [Visualizations](#visualizations)
* [Future Improvements](#future-improvements)
* [License](#license)

## **Project Description**

This project focuses on building a predictive model for violent crime rates (`ViolentCrimesPerPop`) using a dataset containing various community attributes. The analysis employs a linear regression approach, incorporating steps to handle potential multicollinearity among predictor variables through VIF-based feature selection. The model is trained and evaluated to understand which factors are significant predictors of violent crime and how well the model performs.

## **Dataset**

The project uses a dataset loaded from a CSV file named `crimes.csv`. This dataset is expected to contain various features related to communities, with the target variable being `ViolentCrimesPerPop` (Violent Crimes per 100k population).

The script starts by reading this CSV file into an R dataframe.

## **Methodology**

The analysis follows these main steps:

1. **Load Libraries:** Import necessary R packages for data manipulation, visualization, and modeling.

2. **Load Data:** Read the `crimes.csv` file into a dataframe.

3. **Data Inspection:** Perform initial checks for missing values (`inspect_na`).

4. **Data Preprocessing:**

   * Separate numeric and character (categorical) features.

   * Convert character features to integers using factor levels.

   * Combine the processed numeric and character dataframes.

   * Scale all features (excluding the target variable) to have zero mean and unit variance.

5. **Feature Selection (VIF):**

   * Fit an initial GLM model with all features to identify potential multicollinearity.

   * Iteratively remove features with a Variance Inflation Factor (VIF) greater than 1.5 to reduce multicollinearity, refining the model formula in each step.

   * Select the final set of features based on the VIF analysis.

6. **Model Training:**

   * Initialize `h2o` for distributed computing.

   * Convert the preprocessed data to an `h2o` frame.

   * Split the data into training and testing sets (80/20 split).

   * Train a Generalized Linear Model (GLM) using `h2o.glm` on the training data, using the test set for validation and incorporating 10-fold cross-validation.

7. **Model Evaluation:**

   * Predict on the test set using the trained `h2o` model.

   * Calculate residuals (actual - predicted).

   * Compute the Root Mean Squared Error (RMSE) and R-squared ($R^2$) for the test set.

   * Calculate the Adjusted R-squared for the test set.

   * Evaluate model performance on the training set using the same metrics.

   * Perform an overfitting check using AUC/Gini values from the `h2o` model for training, validation, and cross-validation sets.

8. **Visualization:**

   * Generate scatter plots comparing predicted vs. observed violent crime rates for both the test and training sets.

   * Combine the plots for comparison.

## **Prerequisites**

Make sure you have R and RStudio installed. The following R packages are required:

```R
library(tidyverse)
library(data.table)
library(rstudioapi)
library(skimr)
library(inspectdf)
library(mice)
library(plotly)
library(highcharter)
library(recipes)
library(caret)
library(purrr)
library(graphics)
library(Hmisc)
library(glue)
library(faraway) 
library(h2o)     
