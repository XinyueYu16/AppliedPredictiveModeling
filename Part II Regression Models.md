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
    - E(MSE) = sigma^2(irreducible noise) + (Model Bias)^2 + Model Variance, ***favoring high variance, low bias*
- **Common Errors**
  - overpredict low values, underpredict high ones -- common in *tree-based* models

## C6 Linear Regression and Its Cousins

## C7 Nonlinear Regression Models

## C8 Regression Trees and Rule-Based Models

## C9 A Summary of Solubility Models
