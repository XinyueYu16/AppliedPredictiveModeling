# I. 3 Pre-processing  
- Distribution(Skewness)
- Outliers
- Missing Values
  - Informative Missing
  - KNN models
  - MICE
- Whether to Delete
  - Degradate Matrix(single or rare values)
- Adding 
  - e.g. Each predictors' distance from the class centroid
- Binning
  - Easier access to answers in questionnaires
  - good interpretation, low predictive performance

# I. 4 Over-fitting and Model Tuning
## - Methods to tune models
- GirdSearch (Manually pick set of candidates + search optimal)
- **Automatic Search**: [Genetic Algorithm](https://algoritmaonline.com/optimization-with-genetic-algorithm/#:~:text=Genetic%20Algorithm%20is%20an%20optimization%20algorithm%20that%20use,2%20main%20principles%3A%20natural%20selection%20and%20random%20mutation.) (mimicking the natrual selection)
  - (PS. the example for Machine Learnin used an interesting module featuring recipe, juice, bake, whose name is *tidymodels*, similar to *sklearn.pipeline*)
  - Process
    - Binary coding the gene(initial set of candidates), start iterations:
      - Calculate and select best 2 of gene as parent solutions
      - Crossover as the parents give birth to child solutions
      - Mutations may happen with a low propensity
    - choose the best solution according to finess performance
  - Advantage
    - Avoid local optimal
    - Can be parallized
- **Automatic Search**: [Simplex Search Methods](https://blog.csdn.net/weixin_45353822/article/details/105948285)
  - [ref2](https://www.shivajicollege.ac.in/sPanel/uploads/econtent/33dfc039a8d88fa01d763d5abcd1df20.pdf#:~:text=The%20simplex%20method%20provides%20a%20systematic%20search%20so,simplex%20method%20is%20presented%20in%20the%20next%20section.)
 
## - Split the sample data
- Principle: 
  - Better to use resampling than 1 single test set
  - Make sure the test samples are as represenative as possible
- Methods
  - **Single Set**: (Srratified) Random Split (or Group-wise)
  - **Single Set**: [Maximum Dissimilarity Sampling](https://scientistcafe.com/ids/datasplittingresampling.html)
    > - Initialize a single sample as starting test set
    > - Calculate the dissimilarity between this initial sample and each remaining samples in the dataset
    > - Add the most dissimilar unallocated sample to the test set
  - **Resampling**: K Fold CV, Monte Carlo CV(Leave-*group*-out CV, could specify the size of *group*), Bootstraping(can be misleading when sample size is small)
    - fold * iter_time
    - small k (2 or 3) comes with hign variances (typically larger than other methods), if k large (10 is often enough, mostly better than LOOCV in light of computational complexity), the true value can be discovered.
    - small k (2 or 3) has the same level of bias as bootstrap
    - *GCV estimation for linear regression's LOOCV*: models with same MSE but different degrees of freedom would have different GCV, less complex, higher
- Recommended Splitting
  - **Large Dataset**: simple 10-fold CV
  - **Small Dataset**: repeated 10-fold CV
  - **For choosing between models**: bootstraping, has the lowest variance

## How to choose ACROSS models
- **Not only performance but simplicity**: Sometimes paras can be chosen with a tolerance apart from the optimal performance for simplicity
  - one-standard-error: With a standard-error of the peak performance
  - set tolerance(%) threshold
- **Basic Steps**
  - First, complicated models as *performance ceiling*: boosted trees, svm
  - Second, simpler models that are less opaque: MARS, partial least squares, generalized additive models, naive Bayes models
  - Third, use simplest model that approximates the performance of more complex models
  - Then weight your choices: computational time, interpretablity, performance, equation exporting complexity... 
- **Statistical tests** like paired t-test can be used to determine whether there's a significant mean accuracy increase

  
