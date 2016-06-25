# useR! Machine Learning Tutorial
useR! 2016 Tutorial: [Machine Learning Algorithmic Deep Dive](http://user2016.org/tutorials/10.html)  


This tutorial will cover six popular [supervised learning](https://en.wikipedia.org/wiki/Supervised_learning) methods:

- Classification and Regression Trees (CART)
- Random Forests (RF)
- Gradient Boosting Machines (GBM)
- Generalized Linear Models (GLM)
- Deep Neural Networks (DNN)
- Stacking / Super Learner (SL)

Here are some practical, related topics we will cover for each algorithm:

- Dimensionality Issues
- Sparsity
- Normalizaion
- Categorical Data
- Missing Data
- Class Imbalance
- Software
- Scalability


## Dimensionality Issues
Certain algorithms don't scale well when there are millions of features.  For example, decision trees require computing some sort of metric (to determine the splits) on all the feature values (or some fraction of the values as in Random Forest and Stochastic GBM).  Therefore, computation time is linear in the number of features.  Other algorithms, such as GLM, scale much better to high-dimensional (n << p) and wide data with appropriate regularization (e.g. Lasso, Elastic Net, Ridge).

## Sparsity
Algorithms can deal with data sparsity (where many of the feature values are zero) in different ways.  In some algorithms there are ways to speed up the computations if sparsity is present, so it's good to know if these shortcuts are available. 

## Normalization
Some algorithms such as Deep Neural Nets and GLMs require that data be normalized for effective interpretation of the models.  Tree-based algorithms (Decision Trees, Random Forest, Gradient Boosting Machines) do not require normalization.  Tree-based methods only use information about whether a value is greater than or less than a certain value (e.g. x > 7 vs. x &leq; 7), the values themselves do not matter.

## Categorical Data
Algorithms handle categorical data differently.  Some algorithms such as GLM and Deep Neural Nets require that a categorical variable be expanded into a set of indicator variables, prior to training.  With tree-based methods and software that supports it, there are ways to get around this requirement, which allows the algorithm to handle the categorical features directly.  It is important to be cognizant of the cardinality of your categorical features before training, as additional pre-processing (collapsing categories, etc) may be beneficial with high-cardinality features.

## Missing Data
Assuming the features are missing completely at random, there are a number of ways of handling missing data:

1. Discard observations with any missing values.
2. Rely on the learning algorithm to deal with missing values in its training phase.
3. Impute all missing values before training.

For most learning methods, the imputation approach (3) is necessary. The simplest tactic is to impute the missing value with the mean or median of the nonmissing values for that feature.  If the features have at least some moderate degree of dependence, one can do better by estimating a predictive model for each feature given the other features and then imputing each missing value by its prediction from the model. 

Some software packages handle missing data automatically, although many don't, so it's important to be aware if any pre-processing is required by the user.

## Class Imbalance
Algorithms that optimize a metric such as accuracy may fail to perform well on training sets that contain a significant degree of class imbalance.  Certain algorithms, such as GBM, allow the user to optimize a performance metric of choice, which is useful when you have a highly imbalanced training set.

## Software
For each algorithm, we will provide examples of open source R packages that implement the algorithm.  All implementations are different, so we will provide information on how each of the implementations differ.

## Scalability
We will address scalability issues inherent to the algorithm and discuss algorithmic or technological solutions to scalability concerns for "big data."


# Tutorial Software Pre-requisites

The tutorial uses [Jupyter notebooks](http://jupyter.readthedocs.io/en/latest/index.html) with the R kernel.  If you are using Anaconda Python, you already have [Jupyter intalled](http://jupyter.readthedocs.io/en/latest/install.html).  For non-Anaconda users, you can optionally install Python via Homebrew and then install Jupyter via pip.

#### Install Python

Python is a requirement of Jupyter notebooks.  It should be installed by default on most machines. If you are on a mac, this can easily be done via Homebrew.  This will install Python 2.7.

```bash
# Homebrew
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# Python 2.7
brew install python
brew install python-dev
```

#### Install Jupyter

However, you may have to install [pip](http://stackoverflow.com/questions/17271319/installing-pip-on-mac-os-x):
```
sudo easy_install pip
```

For Python 2.7:
```
pip install -U jupyter
```

For Python 3:
```
pip3 install -U jupyter
```


#### Install IRkernel

Install the IRkernel binary in R.  More info [here](https://irkernel.github.io/installation/).

```r
install.packages(c('repr', 'pbdZMQ', 'devtools'))
library(devtools)
devtools::install_github('IRkernel/IRdisplay')
devtools::install_github('IRkernel/IRkernel')
IRkernel::installspec()
``` 


# Resources

Where to learn more?

- [An Introduction to Statistical Learning with Applications in R](http://www-bcf.usc.edu/~gareth/ISL/) by  Gareth James, Daniela Witten, Trevor Hastie and Robert Tibshirani
- [The Elements of Statistical Learning](http://statweb.stanford.edu/~tibs/ElemStatLearn/) by Trevor Hastie, Rob Tibshirani and Jerome Friedman
- [Practical Data Science with R](http://www.win-vector.com/blog/practical-data-science-with-r/) by John Mount and Nina Zumel
- [Applied Predictive Modeling](http://appliedpredictivemodeling.com/) by Max Kuhn and Kjell Johnson
- [15 hours of expert videos](http://www.dataschool.io/15-hours-of-expert-machine-learning-videos/) by Trevor Hastie and Rob Tibshirani
