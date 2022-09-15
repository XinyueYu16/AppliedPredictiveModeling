# Part II Regression Models (NonLinear)

## C7 Nonlinear Regression Models
### Neural Networks
- Meaning
  - Process
    - Each hidden unit is a *transformed* linear combination of predictors
    - The transformation function could be Sigmoid, ReLu...
    - If NN has multiple layers, layer Unit L,i is the transformed linear combination of layer L-1
    - Also, the relationship between layers can be two-way
    - The final output is the transformed output of the last layer units
  - However, the linear combination is not like OLS or Lasso..., it has no restrictions
    - It can be slow
    - Using back propagation might lead to local optimum
      - Often cases are that different set of coefficients lead to very similar results
    - Prone to over-fit
- How to prevent over-fitting
  - early stopping: as soon as the accuracy begin to drop, stop it (however, what's the criteria for a drop?)
  - avoid collinearity: pre-processing like PCA; add penalty(*weight decay*) like Ridge or Lasso
  - averaging: effective in producing stabler results

### Multivariate Adaptive Regression Splines(MARS)
- Meaning
  - Use hinge functions to create new features based on original predictors
  - A basic formula would be like:
    - ![](https://latex.codecogs.com/svg.image?\widehat{y_i}&space;=&space;\beta&space;_0&space;&plus;&space;\beta&space;_1(h(X-a))&space;&plus;&space;\beta&space;_2(h(a-X)))
  - One term MARS is additive, they search for the cut point in every step with the optimizing objective of errors
  - 2+ term MARS follows the same pattern, yet different features(hinge parts) could be multiplied together, though less robust than one-term MARS
  - After adding all the features, pruning should be done based on how much the model is improved including this feature according to GCV estimation, pruning is stopped until reaching the number of retained terms
- Advantages
  - Automative feature selection: the estimation do not use all the predictors
  - Interpretability: (p152) Every predictor's contribution could be splitted out
  - Little pre-processing
- Disadvantages
  - Prone to outliers

### [Support Vector Regression](https://towardsdatascience.com/an-introduction-to-support-vector-regression-svr-a3ebc1672c2)
- Meaning
  - Developed form SVM Classfication, nevertheless:
    - SVM: to maximize the shortest distances between datapoints and hyperplane (to better devide)
    - SVR: to minimize the longest distances from distances to hyperlane (to better include as many datapoints in the given epsilon tube with the smallest candidate ||w||^2)
  - Ignoreing all the datapoints' residuals which are within epsilon, for datapoints out of *the tube*, use its linear form
  - Loss Function
    - Target: ![](https://latex.codecogs.com/svg.image?min(\frac{1}{2}||w||^2&space;&plus;&space;C\sum_{i=1}^{n}|\xi&space;_i|))
    - Constraint: ![](https://latex.codecogs.com/svg.image?|y&space;-&space;\widehat{y}|&space;\leq&space;&space;\epsilon&space;&plus;&space;|\xi&space;_i|)
  - ref
    - [CN](https://blog.csdn.net/weixin_41940690/article/details/106639347?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-106639347-blog-124145254.pc_relevant_aa&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-106639347-blog-124145254.pc_relevant_aa&utm_relevant_index=2)
- Advantages
  - Handy when detecting anomaly (outside the tube)
  - 
- Disadvantages

## C8 Regression Trees and Rule-Based Models

## C9 A Summary of Solubility Models
