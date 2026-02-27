---
author: Data Science Analysis
date: 2026
output: github_markdown
title: Used Vehicle Price Analysis
---

# Used Vehicle Price Analysis Report

## Table of Contents

-   [Executive Summary](#executive-summary)
-   [Business Understanding](#business-understanding)
-   [Data Understanding](#data-understanding)
-   [Data Preparation](#data-preparation)
-   [Modeling](#modeling)
-   [Evaluation](#evaluation)
-   [Key Price Drivers](#key-price-drivers)
-   [Strategic Recommendations](#strategic-recommendations)
-   [Limitations & Future
    Improvements](#limitations--future-improvements)
-   [Conclusion](#conclusion)
-   [Appendix: Modeling Workflow](#appendix-modeling-workflow)

------------------------------------------------------------------------

## Executive Summary

This analysis evaluated structural drivers of used vehicle pricing
across 426,880 listings. Ridge regression was selected as the preferred
estimator after cross-validation and hold-out testing. The model
explains approximately 44% of the variance in log(price), capturing
meaningful structural market signals.

Brand positioning, title status, vehicle condition, and model year were
identified as primary price drivers. While predictive accuracy is
moderate, the model provides actionable guidance for inventory
acquisition and pricing consistency.

------------------------------------------------------------------------

## Business Understanding

The dealership seeks to:

-   Identify structural drivers of vehicle pricing
-   Improve acquisition and pricing strategy
-   Reduce valuation risk
-   Support data-driven decision making

------------------------------------------------------------------------

## Data Understanding

Dataset characteristics:

-   426,880 vehicle listings
-   18 structured features
-   Significant categorical dimensionality
-   Missingness in condition, size, and cylinders
-   High price dispersion and outliers

*Figure Placeholder: Distribution of Price and Log(Price)*

------------------------------------------------------------------------

## Data Preparation

Key preparation steps:

-   Removed unrealistic year values (1980--2023 filter)
-   Removed extreme odometer outliers (99th percentile cap)
-   Created log(price) target variable
-   One-hot encoded categorical features
-   Scaled numeric variables
-   Split data into 80% training / 20% testing

------------------------------------------------------------------------

## Modeling

Models evaluated:

-   Linear Regression
-   Ridge Regression
-   ElasticNet

Hyperparameters were tuned using 5-fold cross-validation. Ridge
regression demonstrated superior generalization performance.

------------------------------------------------------------------------

## Evaluation

**Test Set Performance (log scale):**

  Model               RMSE    R²
  ------------------- ------- -------
  Ridge               0.897   0.444
  Linear Regression   0.900   0.441
  ElasticNet          0.987   0.328

Ridge regression was selected as the final model.

------------------------------------------------------------------------

## Key Price Drivers

### Positive Drivers

-   Premium manufacturers (Porsche, Tesla, Alfa Romeo, Land Rover)
-   Clean title status
-   Excellent / like-new condition
-   Newer model year
-   Certain geographic markets

### Negative Drivers

-   Salvage or parts-only titles
-   Fair / salvage condition
-   Lower-demand manufacturers
-   Certain regional markets

Model-level granularity revealed rare-category dominance, suggesting
that future standardization of model labels would improve
interpretability.

------------------------------------------------------------------------

## Strategic Recommendations

1.  Optimize inventory mix toward premium brands
2.  Protect clean title documentation integrity
3.  Standardize vehicle condition grading
4.  Implement structured depreciation-based pricing
5.  Apply localized pricing adjustments by state

The model provides structured pricing guidance but is not sufficient for
fully automated pricing deployment.

------------------------------------------------------------------------

## Limitations & Future Improvements

-   Model-level free-text introduces volatility
-   Unstructured listing descriptions were not used
-   Non-linear depreciation curves could improve performance
-   Trim-level parsing would enhance interpretability
-   Tree-based ensemble models may capture additional non-linear effects

------------------------------------------------------------------------

## Conclusion

Brand, title status, condition, and recency are dominant structural
price drivers. Ridge regression provides stable, interpretable estimates
suitable for strategic decision support and inventory optimization.

------------------------------------------------------------------------

## Appendix: Modeling Workflow

1.  Data cleaning and filtering
2.  Feature engineering (log(price))
3.  Train/test split
4.  Preprocessing pipeline (imputation + scaling + encoding)
5.  Cross-validation with GridSearch
6.  Test-set evaluation
7.  Coefficient extraction and interpretation
