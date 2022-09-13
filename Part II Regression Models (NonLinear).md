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


## C8 Regression Trees and Rule-Based Models

## C9 A Summary of Solubility Models
