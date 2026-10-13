# statMatchLCM 2.0
statMatchLCM: An R Package for Statistical Matching Using Latent Class Models ver. 2.0

## Changes in version 2.0 compared with version 1.2

### 2. Revised handling of categorical variables
In version 1.2, several Step 2 functions converted factors into numeric codes using `fact_to_num()`. In version 2.0, both predictive models and matching procedures operate directly on factors. Consequently, categorical variables are treated as distinct levels rather than numerical values, which may lead to different results.
Furthermore, the Gower distance is now explicitly specified in all hot-deck matching functions, whereas previously it was explicitly specified only in `sma2_step2()`.

### 3. Refined imputation selection in Step 1

The selection criterion remains the minimization of the Hellinger distance. However, the comparison now explicitly concerns the target variable `Z`, evaluating the agreement between its synthetic distribution in dataset A and its reference distribution in dataset B. Category levels are aligned before computing the distance.
In the previous CRAN version, the comparison was based on the last column of the dataset, and the distributions were supplied to `comp.prop()` in the reverse order.

### 4. Improved handling of binary model probabilities
The functions `smc2_step2()`, `smc3_step2()`, and `sma2_step2()` have been updated to handle probability outputs from binary classification models. Specifically, the predicted probabilities are converted into a two-column matrix, with column names corresponding to the response categories.

### 5. Substantial revision of `sma3_step2()`
The implementation of `sma3_step2()` has been substantially revised. In the previous CRAN version, dummy variables were constructed manually, and category probabilities were calculated directly from the estimated model coefficients.
In version 2.0, a model of the form `Z ~ other variables` is fitted using dataset B, and the `predict()` function is applied to dataset A to obtain predicted probabilities.
This revision changes the model specification and eliminates the previous inclusion of the target variable in the manually constructed predictor matrix.

