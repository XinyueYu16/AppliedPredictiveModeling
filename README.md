# AppliedPredictiveModeling
Notes of Applied Predictive Modeling

## I. 3 Pre-processing  
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

## I. 4 Over-fitting and Model Tuning
### - Methods to tune models
  - GirdSearch (Manually pick set of candidates + search optimal)
  - **Automatic Search** [Genetic Algorithm](https://algoritmaonline.com/optimization-with-genetic-algorithm/#:~:text=Genetic%20Algorithm%20is%20an%20optimization%20algorithm%20that%20use,2%20main%20principles%3A%20natural%20selection%20and%20random%20mutation.) (mimicking the natrual selection)
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
 - **Automatic Search**[Simplex Search Methods](https://blog.csdn.net/weixin_45353822/article/details/105948285)
  - [ref2](https://www.shivajicollege.ac.in/sPanel/uploads/econtent/33dfc039a8d88fa01d763d5abcd1df20.pdf#:~:text=The%20simplex%20method%20provides%20a%20systematic%20search%20so,simplex%20method%20is%20presented%20in%20the%20next%20section.)
 
 ### - Split the sample data
