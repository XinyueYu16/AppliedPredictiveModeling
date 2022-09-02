# Part II Regression Models

## C5 Measuring Performace in Regression Models
- Principle:
  - relying on solely 1 metric can be problematic
  - utilize visulizations of model fit, redisual plots...
- **Quantitative** Measures
  - RMSE: same unit with original data, average distance between predicted and true values
  - R-square: denote the correlation(*not accuracy!*) between predicted and true values
  - Confidence/Prediction Interval: Confidence is for mean prediction, Prediction is for single datapoints
    - [ref in CN](https://www.jianshu.com/p/47661068ed2d)
    - [x] [how to calculate?](https://www.jianshu.com/p/a18fdbbb0473?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)
- **Quantitative** Measures
- Common Errors:
  - overpredict low values, underpredict high ones -- common in *tree-based* models
