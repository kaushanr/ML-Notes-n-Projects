# ML Project Checklist

### 1. Frame the problem and look at the big picture

  * Define the objective in business terms.
  * How will your solution be used?
  * What are the current solutions/workarounds?
  * How should you frame this problem (supervised/unsupervised, online/offline, etc)
  * How should performance be measured?
  * Is the performance measure aligned with the business objective?
  * What would be the minimum performance needed to reach the business objective?
  * What are the comparable problems? Can you reuse experience or tools?
  * Is human expertise available?
  * How would you solve the problem manually?
  * List the assumptions you have made so far.
  * Verify assumptions if possible.


### 2. Get the data

  * Automate as much as possible so you can easily get fresh data.
  * List the data you need and how much you need.
  * Find and document where you can get that data.
  * Check how much space it will take.
  * Check the legal obligations, and get authorization if necessary.
  * Get access authorizations.
  * Create a workspace (with enough storage space)
  * Get the data.
  * Convert the data to a format you can easily manipulate (without altering the data itself)
  * Ensure sensitive information is deleted or protected (anonymized)
  * Check the size and type of data (time series, geographical, etc)
  * Sample a test set, put it aside, and never look at it!


### 3. Explore the data

  * Try to get insights from a field expert for these steps.
  * Create a copy of the data for exploration (sample down to a manageable size if necessary)
  * Create a Jupyter notebook to keep a record of your data exploration.
  * Study each attribute and its characteristics:
    * Name
    * Type - catergorical, int/float, bounded/unbounded, text, structured, etc
    * % of missing values
    * Noisiness and type of noise - stochastic, outliers, rounding errors, etc
    * Usefulness for the task
    * Type of distribution - Gaussian, uniform, logarithmic, etc
  * For supervised learning tasks, identify the target attributes
  * Visualize the data
  * Stdy the correlations between the attributes
  * Study how you would solve the problem manually
  * Identify the promising transformations you may want to apply
  * Identify extra data that would be useful
  * Document what you have learned

### 4. Prepare the data

  * Notes
      * Work on copies of the data.
      * Write functions for all data transformations you apply, Why?
        * So you can easily prepare the data the next time you get a fresh dataset
        * So you can apply these transformations in future projects
        * To clean and prepare the test set
        * To clean and prepare new data isntances once your solution is live
        * To make it easy to treat your preparation choices as hyperparameters

  * Data cleaning
    * Fix or remove outliers
    * Fill in missing values (with zero, mean, median) or drop their rows/columns
  * Feature selection
    * Drop the attributes that provide  no useful information for the task

  * Feature engineering
    * Discretize continous features
    * Decompose features (categorical, date/time,etc)
    * Add promising transformations of features - log(x), sqrt(x), x^2, etc
    * Agrregate features into promising new features

  * Feature scaling
  * Standardize or normalize features

### 5. Shortlist promising models

  * Notes
    * If the data is huge, you want to sample smaller training sets so you can train many different models in a reasonable time (this penaizes complex models such as large neural nets or Random Forests)

    * Try to automate these steps as much as possible

  * Train many quick-and-dirty models from different categories (linear,naive Bayes, SVM, RF, NN, etc)

  * Measure and compare their performance
    * For each model, use N-fold cross-validation and compute the mean and standard deviation of the performance measure on the N folds

  * Analyse the most significant variables for each algorithm

  * Analyse the types of errors the models make
    * What data would a human have used to avoid these errors

  * Perform a quick round of feature selection and engineering

  * Perform one or two or more quick iterations of the five previous steps

  * Shortlist the top three to five most promising models, preferring models that make different types of errors

### 6. Fine-tune the system

  * Notes
    * Use as much data as possible for this step, especially as you move towards the end of fine tuning

    * Try to automate as much as possible

  * Fine-tune the hyperparameters using cross-validation

    * Treat your data transformation choices as hyperparameters, especially when you are not sure about them (if you're not sure whether to replace missing values with zeros of with the median value, or to just drop the rows)

    * Unless there are very few hyperparameter values to explore, prefer random search over grid search. If training is very long, you may prefer a Bayesian optimisation approach

  * Try Ensemble methods. Combining your best models will often produce better performance than running them individually

  * Once you are confident about your final model, measure its performance on the test set to estimate the generalization error.

  * Don't tweak your model after measuring the generalization error: you would just start overfitting the test set

### 7. Present your solution

  * Document what you have done

  * Create a nice presentation making sure you highlight the big picture first

  * Explain why your solution achieves the business objective

  * Don't forget to present interesting points you noticed along the way
    * Described what worked and what did not
    * List your assumptions and your system's limitations

  * Ensure your key findings are communicated through beautiful visualizations or easy-to-remember statements

### 8. Launch

  * Get your solution ready for production (plug into production data inputs, write unit tests, etc)

  * Write monitoring code to check your system's live performance at regular intervals and trigger alerts when it drops

    * Beware of slow degradation: models tend to rot as data evolves

    * Measuring performance may require a human pipeline (via crowdsourcing service)

    * monitor your inputs' quality. Particularly important for online learning systems

  * Retrain your models on a regular basis on fresh data
