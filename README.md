# Election Forecasting from State Polling Data

**Live report:** https://nik8x.github.io/Election-Forecasting/

Predicting which party wins each US state in a presidential election
from pre-election polling data, 145 state-year records across 2004,
2008, and 2012.

The analysis trains on 2004 and 2008 and evaluates on 2012, a genuine
out-of-sample test by year rather than a random split. It formalizes
the multicollinearity among the poll measures with a variance inflation
factor, compares two models against each other and against a simple
baseline, and adds an unsupervised check on the polling data itself.

## Notebooks

1. `00_data_setup_eda.ipynb`: missingness in the two named pollsters,
   correlation between the four poll measures.
2. `01_statistical_testing.ipynb`: how good is the simplest possible
   forecast (the sign of one pollster's margin), and how severe is the
   multicollinearity, checked with an actual VIF instead of a
   correlation eyeball.
3. `02_feature_engineering_selection.ipynb`: iterative imputation
   (scikit-learn's equivalent to R's `mice`) for the missing poll
   values.
4. `03_model_training_evaluation.ipynb`: logistic regression and random
   forest, trained on 2004 and 2008, evaluated on a genuinely unseen
   2012, against the smart baseline.
5. `04_clustering.ipynb`: KMeans and Gaussian mixture clustering by
   poll profile alone, checked against the real outcome afterward.

## Results

Both models reach 97.8% accuracy on the 2012 test states (44 of 45
correct), beating a strong 91.1% baseline of just following one
pollster's sign. Clustering by poll numbers alone recovers the actual
outcome closely (adjusted Rand index 0.77), without the model ever
seeing which party won.

## Future work

- Extend to more election cycles for a larger out-of-sample test set,
  three elections is a thin basis for strong claims.
- Bring in fundamentals-based predictors (incumbency, state partisan
  lean, economic indicators) alongside the poll numbers.
- Try a hierarchical or Bayesian model that pools information across
  states instead of treating each state-year as independent.
