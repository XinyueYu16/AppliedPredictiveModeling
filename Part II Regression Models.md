# Part II Regression Models

## C5 Measuring Performace in Regression Models
- Principle:
  - relying on solely 1 metric can be problematic
  - utilize visulizations of model fit, redisual plots...
- **Quantitative** Measures
  - RMSE: same unit with original data, average distance between predicted and true values
  - R-square: denote the correlation(*not accuracy!*) between predicted and true values
    - same MSE but larger variance in responses lead to lower R-square
  - Confidence/Prediction Interval: Confidence is for mean prediction, Prediction is for single datapoints
    - [ref in CN](https://www.jianshu.com/p/47661068ed2d)
    - [how to calculate?](https://www.jianshu.com/p/a18fdbbb0473?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)
  - Spearman Correlation (Depending on your goal: suppose you want to predict the rank as opposed to actual number)
- **Trade-off** between variance and bias
  - Low variance, high bias: robust but not accurate, underfit
  - High variance, low bias: complex, outfitted model, sensitive to new data
    - E(MSE) = sigma^2(irreducible noise) + (Model Bias)^2 + Model Variance, *favoring high variance, low bias*
- **Common Errors**
  - overpredict low values, underpredict high ones -- common in *tree-based* models

## C6 Linear Regression and Its Cousins
### Linear Regression (OLS)
- Meaning of Linear Regression
  - linear parameter(linear relationship)
  - additive
  - generally trys to minimize a function of MSE
  - highly interpretable
  - Based on standard assumptions, it provides, with unbiased coefficient, the lowest MSE (which could be lowered by creating )
  - *Use Case*: signal filtering, use the model variance to identify measured noise, so that underlying true signal(y) could be recovered by y_hat
- **![beta-equation](https://latex.codecogs.com/svg.image?\widehat{\beta}&space;=&space;(X^TX)^{-1}X^Ty)**
  - 2 requirements for ![](https://latex.codecogs.com/svg.image?(X^TX)^{-1}) to have unique inverse
    - full rank = no predictor can be determined from a combination of one or more of other predictors
    - the number of observations larger than the number of predictors
    - IF VIOLATED: conditional inverse can still be attained, but the result is not unique, hence interpretablity stained 
  - **Collinearity**
    - Impact
      - standard errors & coefficients inflated
      - predictive power remained, but significance of predictors drop (Type II Error)
    - How to spot?
      - [VIF(variance inflation factor)](https://corporatefinanceinstitute.com/resources/knowledge/other/variance-inflation-factor-vif/): to assess the correlation
        - ![VIF](https://latex.codecogs.com/svg.image?VIF&space;=&space;\frac{1}{(1-R_i^2)}) 
        - ![](https://latex.codecogs.com/svg.image?R_i^2) is represents the unadjusted coefficient of determination for regressing the ith independent variable on the remaining ones
      - not significant respective T-tests, high R^2
    - How to correct?
      - Delete correlated predictors(p47) to ensure all pairwise correlations are below a certain threshold
        - Find the highest correlation (between A and B)
        - remove the one that has higher average correlation with other variables
        - loop until no pairwise correlation is above threshold
      - PCA, PLS(simultaneouos dimension reduction and regression), Lasso, Ridge
      - Situations that multicollinearity doesn't matter: a. dummy variable; b. control variable(as opposed of variable of interest); c. intersection or power
  - [Assumptions](https://towardsdatascience.com/assumptions-of-linear-regression-fdb71ebeaa8b)
    - a. linear; b. nocollinearity; c. normal errors; d. errors independent of independent IVs(correctly specified model); e. errors constant along DV(homoscedacity == independent observations == no group, no autocorrelation)
  - Drawback: a. only for linear; b. sensitive to outliers (bc they are minimizing SSE)
    - Robust Regression : use *alternatives to SSE* to address the tendency towards outliers
      - Hubert function: Given certain threshold C: when residuals < C, use squared residuals; when >= C, use absolute residual
### Partial Least Squares
- Meaning
  - Similar to PCA, denotes a linear combination of predictors based on their variability
  - Moreover, the combination also *have maximum correlation with the response* (focuses on *covariance* rather than *variance*)
  - A supervised dimension reduction procedure, as opposed to PCA being unsupervised
  - Can deal with *multivariate outcome*
- Drawbacks
  - Cannot deal with too many predictors (Penalty Models still would be more efficient in this scope)
  - Cannot deal with unlinear relationship with ease (Tree and other models recommended)
  - Slow computation, *every* component needs to calculate a new IV and DV matrix
- Resources
  - [Full Read](https://towardsdatascience.com/partial-least-squares-f4e6714452a)
### Penalty Models
- Ridge(*shrinking* model, L2, penalty = ![](https://latex.codecogs.com/svg.image?\lambda&space;\sum_{p}^{j=1}\beta&space;_j^2))
- Lasso(*least absolute shrinkage and selection operation* model, L1, penalty = ![](https://latex.codecogs.com/svg.image?\lambda&space;\sum_{p}^{j=1}|\beta&space;_j|))
- Elastic Net

## C7 Nonlinear Regression Models

## C8 Regression Trees and Rule-Based Models

## C9 A Summary of Solubility Models
