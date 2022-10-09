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

### Support Vector Regression
- Meaning

  ![](https://latex.codecogs.com/svg.image?f(\textbf{u})&space;=&space;\beta_0&space;&plus;&space;\sum_{i=1}^{n}\alpha_iK(\textbf{x}_i,&space;\textbf{u}))
  
  ![](https://latex.codecogs.com/svg.image?K(\textbf{x}_i,&space;\textbf{u})&space;=&space;\sum_{j=i}^{P}x_{ij}u_j&space;=&space;{\textbf{x}_i}'\textbf{u})
  - Robust regression, epsilon-insensitive regression
    - other methods: Huber
  - Developed from SVM Classfication, yet different
    - SVM: to maximize the shortest distances between datapoints and hyperplane (to better divide)
    - SVR: to minimize the longest distances from distances to hyperlane (to better include as many datapoints in the given epsilon tube with the smallest candidate ||w||^2)
  - Kernel tricks
    - make transformations based on all the a > 0 sample data 
    - kernal generalization: polynomial, **radial basis function**, hyperbolic tangent...
  - Loss Function
    - When calculating error: Ignoreing all the datapoints' residuals within given epsilon, however, for datapoints out of *the tube*, use its linear form
    - Target: ![](https://latex.codecogs.com/svg.image?min(\frac{1}{2}||w||^2&space;&plus;&space;C\sum_{i=1}^{n}|\xi&space;_i|))
      - Minimizing the coefficients and loss at the same time
    - Constraint: ![](https://latex.codecogs.com/svg.image?|y&space;-&space;\widehat{y}|&space;\leq&space;&space;\epsilon&space;&plus;&space;|\xi&space;_i|)
- Tuning parameters
  - epsilon
  - cost
  - kernel tricks' parameter
  - best practice: fix epsilon, then tune other kernel parameters
- Pre-processing
  - centering and scaling (for residuals are affected by predictor scales)
- Advantages
  - Handy when detecting anomaly (outside the tube)
  - Good at creating Hyperplanes among different datapoints (see the cow-and-wolf example)
- Disadvantages
- Ref
  - [CN](https://blog.csdn.net/weixin_41940690/article/details/106639347?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-106639347-blog-124145254.pc_relevant_aa&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-106639347-blog-124145254.pc_relevant_aa&utm_relevant_index=2)
  - [EN](https://towardsdatascience.com/an-introduction-to-support-vector-regression-svr-a3ebc1672c2)
  - [when to use-fencing the cows against the wolves](http://www.pybloggers.com/2017/01/why-use-svm/)


## C8 Regression Trees and Rule-Based Models
### Basic Regression Trees
- Pruning: cost-complexity parameter
  - traditional: SSE_cp = SSE + ccp * number of terminal nodes
  -  [sklearn ccp](https://scikit-learn.org/stable/modules/tree.html#minimal-cost-complexity-pruning)
      -  Use alpha_effective to determine whether to maintain certain node, a non-terminal node with the smallest alpha_effective would be pruned if its alpha_effective smaller than the *ccp_alpha*
        - **alpha_effective**: ![](https://latex.codecogs.com/svg.image?\alpha_{eff}(t)=\frac{R(t)-R(T_t)}{|T|-1})
        - R(t) is the impurity of node t, R(Tt) is the weighted sum of impurity of all t's sub-branches, T is the number pf sub-nodes
- Feature Importance
  - Appear higher/ more times
- Advantage
  - Can handle missing data
    - cut at missing data would opt to use surrogate splits
- Disadvantage
  - Complex trees fit better, yet harder to interprete(due to many overlappings)
  - When collinearity exists, splits may be random; and the importance of features tend to be unstable
    - i.e In linear regression, model wouldn't increase the coefficient of a certain feature to increase its performance; but a tree-model might: if the feature is the sole feature seen in data/the number of splits unlimited; **SO**, to underpin the importance of a certain feature, **ensemble methods or CV** should be considered
  - Suffer **SELECTION BIAS**: favor features with higher variance/more distinct values
    - features containing noise sometimes might get more spilts than truely informative ones, after pruning it might lead to no tree at all
  - UNSTABLE (as stated above); performance poor in predicting unseen values
- Adjustments(UNbiased trees) -- Statistical hypothesis does not entail high performance
  - Common places: statistical hypothsis; no need to prune
    - GUIDE model (generalized, unbiased, interaction detection and estimation): use statistical hypothesis to rank importanct features, then split
    - Conditional Inference Trees: Use statistical hypothesis(p-value) to compare the differences between splitted sub-groups

### Regression Model Trees
- M5 (Quinlan 1992) (Similar to the model I deployed in house-price predictions) 
  - Assumption
    - "The functional dependency is not constant in the whole domain, but can be approximated as such on smaller subdomains"
  - Steps
    - **Splitting**: Different splitting criteria(SDR - standard deviation reduction)
    - **Linear Modeling**: Terminal nodes predict the outcome using linear model (with features used in splitting before) as opposed to simple average
    - **Pruning**: After each linear model is built, pruning is done leafmodel-wise, where adjusted error rate is emoployed to determine which *predictor* should be kept 
    - **Smoothing**: Models in parent nodes would be updated (weighted sum) according to its branches, the equation be like:
      ![](https://latex.codecogs.com/svg.image?PV(s)&space;=&space;\frac{n_i\times&space;Si&space;&plus;&space;c\times&space;PV(S)}{n_i&space;&plus;&space;c})
      - This could have significant positive effect in performance when linear models across nodes are very different(either the traning sample is small or high collinearity exists)
      - [python-M5P smoothing implementation](https://github.com/smarie/python-m5p/blob/main/src/m5py/main.py#L414)
  - Advantage
    - Address the fallacy of basic trees' poor predictions in extreme values
    - **Low computation cost**
      > "M5 model tree can simulate the phenomena with very high dimensionality up to hundreds of attributes [13]. This ability sets M5 apart from regression tree learners at the time (like MARS), whose computational cost grows very quickly when the number of features increases."
  - Reference
    - [A Thesis using M5 tree](https://www.un-ihe.org/sites/default/files/solomatinexuem5-model-trees-nn-huai-riverasce-j-hydrolengr2004.pdf)
    - [Model Trees Repo](https://github.com/ankonzoid/LearningX/tree/master/advanced_ML/model_tree)
    - [1992-Quinlan-AI](https://sci2s.ugr.es/keel/pdf/algorithm/congreso/1992-Quinlan-AI.pdf)
    - 
## C9 A Summary of Solubility Models
