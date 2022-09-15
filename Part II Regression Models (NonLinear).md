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

### Support Vector Machines
- Meaning
- Advantages
- Disadvantages

## C8 Regression Trees and Rule-Based Models

## C9 A Summary of Solubility Models
