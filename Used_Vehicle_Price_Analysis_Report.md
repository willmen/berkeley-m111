# Used Vehicle Price Analysis Report

**Client:** Used Vehicle Dealership
**Objective:** Identify key drivers of used vehicle prices and evaluate
predictive modeling approaches

------------------------------------------------------------------------

## 1. Executive Summary

This analysis examined structural drivers of used vehicle pricing using
a dataset of over 426,000 vehicle listings. Ridge regression was
selected as the preferred estimator after cross-validation and hold-out
testing. The model explains approximately 44% of the variance in
log(price), capturing meaningful market signals while highlighting areas
for future refinement.

Brand positioning, title status, vehicle condition, and model year were
identified as the strongest structured price drivers. While predictive
accuracy is moderate, the model provides actionable insight for
inventory acquisition and pricing strategy.

------------------------------------------------------------------------

## 2. Business Understanding

The dealership seeks to:

-   Understand what factors most influence used vehicle pricing
-   Improve acquisition decisions
-   Support structured pricing guidance
-   Identify risk factors that materially reduce resale value

The analysis focuses on structured attributes (year, mileage,
manufacturer, condition, title status, drivetrain, fuel, state) to
determine their contribution to price variation.

------------------------------------------------------------------------

## 3. Data Understanding

The dataset contains 426,880 vehicle listings across multiple states,
with 18 attributes including numeric and categorical fields.

**Key observations:**

-   Significant missingness in some categorical variables (size,
    cylinders, condition)
-   Price distribution exhibits extreme outliers
-   Model field contains highly granular free-text entries

Initial exploration revealed strong dispersion in pricing and high
dimensionality due to categorical encoding.

------------------------------------------------------------------------

## 4. Data Preparation

The following preparation steps were implemented:

-   Removed unrealistic year values (outside 1980--2023)
-   Removed extreme odometer outliers (capped at 99th percentile)
-   Created log(price) target to stabilize variance
-   Encoded categorical variables via one-hot encoding
-   Scaled numeric features
-   Split dataset into 80% training / 20% testing subsets

These steps ensured consistency, comparability, and stable model
convergence.

------------------------------------------------------------------------

## 5. Modeling

Three linear models were evaluated:

-   Linear Regression
-   Ridge Regression (L2 regularization)
-   ElasticNet (L1 + L2 regularization)

Hyperparameters were tuned via 5-fold cross-validation using RMSE on
log(price). Ridge regression achieved the strongest generalization
performance.

------------------------------------------------------------------------

## 6. Evaluation

**Test-set performance (log scale):**

  Model               RMSE    R²
  ------------------- ------- -------
  Ridge               0.897   0.444
  Linear Regression   0.900   0.441
  ElasticNet          0.987   0.328

Ridge regression was selected due to lowest RMSE and highest R².

An R² of 0.44 indicates that structured features explain approximately
44% of observed price variation. The remaining variance likely reflects
trim nuance, seller behavior, market timing, and unstructured listing
details.

Because predictions are made on log(price), the model provides
directional pricing guidance rather than precise automation.

------------------------------------------------------------------------

## 7. Key Price Drivers

### Positive Price Drivers

-   Premium manufacturers (e.g., Porsche, Tesla, Alfa Romeo, Land
    Rover)
-   Clean title status
-   Excellent or like-new condition
-   Newer model year
-   Certain geographic markets

### Negative Price Drivers

-   Salvage or parts-only title status
-   Fair or salvage condition
-   Lower-demand manufacturers
-   Certain regional markets

Model-level one-hot encoding captured detailed trim-level premiums, but
rare categories dominated extreme coefficients, indicating that future
standardization of model names could improve interpretability.

------------------------------------------------------------------------

## 8. Strategic Recommendations

1.  Prioritize premium brand mix in acquisition strategy
2.  Protect clean title documentation as a key valuation driver
3.  Standardize condition grading and presentation practices
4.  Use structured depreciation curves (year-based adjustments) in
    pricing
5.  Incorporate localized pricing adjustments by state

The current model supports structured decision-making but is not
sufficient for fully automated pricing without additional feature
refinement.

------------------------------------------------------------------------

## 9. Limitations & Future Improvements

-   Model-level string granularity introduces volatility
-   Unstructured listing text was not utilized
-   Depreciation curves could be modeled non-linearly
-   Trim-level parsing would improve interpretability
-   Tree-based ensemble models could capture non-linear effects

Future work should focus on feature engineering rather than model
complexity.

------------------------------------------------------------------------

## 10. Conclusion

The analysis confirms that brand, title status, condition, and recency
are the dominant structural drivers of used vehicle prices. Ridge
regression provides stable and interpretable estimates suitable for
strategic decision support.

The dealership can leverage these insights to improve acquisition
selection, pricing consistency, and risk management.
