# Machine Learning Concepts

Table of content

- [Machine Learning Concepts](#machine-learning-concepts)
  - [Machine Learning Framework](#machine-learning-framework)
    - [Unsupervised Learning](#unsupervised-learning)
  - [Data Preprocessing](#data-preprocessing)
    - [Normalization](#normalization)
    - [Missing Value](#missing-value)
      - [Options](#options)
    - [Dimensionality Reduction](#dimensionality-reduction)
      - [Factor Analysis](#factor-analysis)
      - [ICA](#ica)
      - [PCA vs SVD](#pca-vs-svd)
    - [Label Encoding](#label-encoding)
    - [Classification Imbalance](#classification-imbalance)
    - [Feature Scaling](#feature-scaling)
  - [Model Expansion](#model-expansion)
    - [Binary to Multi-class](#binary-to-multi-class)
      - [One-vs-rest (one-vs-all) Approaches](#one-vs-rest-one-vs-all-approaches)
      - [Pairwise (one-vs-one, all-vs-all) Approaches](#pairwise-one-vs-one-all-vs-all-approaches)
  - [Model Validation](#model-validation)
    - [Splitting Data](#splitting-data)
    - [Simplest Split](#simplest-split)
    - [Hold-out Validation](#hold-out-validation)
    - [N-Fold Cross-Validation (Repeated Hold-out)](#n-fold-cross-validation-repeated-hold-out)
      - [Hold-one-out Cross-Validation (LOO CV)](#hold-one-out-cross-validation-loo-cv)
    - [Train-Validation-Test](#train-validation-test)
      - [Nested N-Fold Cross-Validation](#nested-n-fold-cross-validation)
    - [Bootstrapping](#bootstrapping)
      - [0.632-bootstrap](#0632-bootstrap)
  - [Model Evaluation](#model-evaluation)
    - [Classification](#classification)
      - [Methods Overview](#methods-overview)
      - [Accuracy (Error Rate)](#accuracy-error-rate)
      - [Confusion Matrix](#confusion-matrix)
      - [Precision, Recall Ratio](#precision-recall-ratio)
      - [ROC curve](#roc-curve)
    - [Regression](#regression)
      - [Mean Absolute Error (MAE)](#mean-absolute-error-mae)
      - [Mean Squared Error (MSE)](#mean-squared-error-mse)
      - [Root Mean Squared Error (RMSE)](#root-mean-squared-error-rmse)
    - [Clustering](#clustering)
      - [Within Groups Sum of Squares](#within-groups-sum-of-squares)
      - [Mean Silhouette Coefficient of all samples](#mean-silhouette-coefficient-of-all-samples)
      - [Calinski and Harabaz score](#calinski-and-harabaz-score)
  - [Fitting and Model Complexity](#fitting-and-model-complexity)
    - [Generalization](#generalization)
    - [Overfitting](#overfitting)
    - [Underfitting](#underfitting)
    - [Occam's Razor Principle](#occams-razor-principle)
    - [Regularization (Weight Decay)](#regularization-weight-decay)
      - [L1 Regularization](#l1-regularization)
      - [L2 Regularization](#l2-regularization)
      - [L1+L2 Regularization](#l1l2-regularization)
  - [Reducing Loss](#reducing-loss)
    - [Common Loss Function](#common-loss-function)
      - [Hinge Loss](#hinge-loss)
      - [Cross Entropy Loss (Negative Log Likelihood)](#cross-entropy-loss-negative-log-likelihood)
    - [Learning Rate](#learning-rate)
    - [Gradient Descent](#gradient-descent)
      - [Stochastic Gradient Descent](#stochastic-gradient-descent)
  - [Other Learning Method](#other-learning-method)
    - [Cost-sensitive Learning](#cost-sensitive-learning)
    - [Lazy Learning](#lazy-learning)
    - [Incremental Learning (Online Learning)](#incremental-learning-online-learning)
    - [Multi-label Classification](#multi-label-classification)

## Machine Learning Framework

Three aspect:

* What is the target?
* The representation?
  * Data
  * Target function
* Algorithms (i.e. ML Method)

Three Spaces

* Input Space/Feature Space: space used to describe each instance
  * Continuous (e.g. Word embedding)
  * Discrete (e.g. Feature engineering)
  * Binary
* Output Space: space of possible output values; very dependent on problem
  * Continuous vs. Discrete
  * Binary vs. Multivalued (in Discrete)
* Hypothesis Space: space of functions that can be selected by the machine learning algorithm (it's the set of all functions *h* that satisfy the goal)

Three Problems

* Accordance Assumption: m examples chosen i.i.d. according to an unknown real world *distribution*
* Modeling: For a *hypotheses*, estimate the parameters based on training data and minimize loss
* Generalization: Accuracy on real data (training & test set)

Goal of ML

* Find a function *h* belonging to hypothesis space H, such that the expected error on new examples is minimal.
* Find a function *h*: $Y = H(X)$, where $D = \{(X, y) | x \in X, y \in Y\}$

Types of ML Problem

* Y = empty set: unsupervised learning
* Y is a set of integer: classification
* If |Y|=2, h is called a concept: concept learning
* Y is a set of real number: regression
* Y are not given for some Ds: semi-supervised learning
* Y is order set: learning for ranking
* ...

Learning Frame

* Describing data with feature (Input Space): Manually designing input feature
* Learning algorihtm (Hypothesis Space): Optimizing the weights on features

Reasons of ML methods fail

* Wrong Bias: best hypothesis is not in H
* Search Failure: best model is in H but search fails to examine it

### Unsupervised Learning

* [Is the test set required for the unsupervised learning?](https://www.quora.com/Is-the-test-set-required-for-the-unsupervised-learning)
  * In a way, no - as there is no ground truth. But often, unsupervised learning is followed by or associated with supervised learning.
    * Word2Vec followed by classification/regression - Text Prediction
    * PCA on TFIDF vectors followed by classification/regression -Text Prediction
    * Clustering on labeled data - if you want to tune the clustering to get the least error
    * Topic Modeling - you use LDA or LSA to get topic models and use the “elbow” to find the optimum number of topics - but now you would like to see if this would generalize well - and then you need a test set.

## Data Preprocessing

[Feature Engineering](FeatureEngineering.md)

### Normalization

TBD

e.g. SVM is better to normalize data between -1 and 1

### Missing Value

* [Scikit Learn - 4.4 Imputation of missing values](http://scikit-learn.org/stable/modules/impute.html#impute)
* [How to Handle Missing Data](https://towardsdatascience.com/how-to-handle-missing-data-8646b18db0d4)

#### Options

* Use the feature’s mean value from all the available data.
* Fill in the unknown with a special value like -1.
* Ignore the instance.
* Use a mean value from similar items.
* Use another machine learning algorithm to predict the value.

### Dimensionality Reduction

Background

* The relevant features may not be explicitly presented in the data.
* We have to identify the relevant features before we can begin to apply other machine learning algorithm

The reasons we want to simplify our data

* Making the dataset easier to use
* Reducing computational cost of many algorithms
* Removing noise
* Making the results easier to understand

#### Factor Analysis

* We assume that some unobservable *latent variables* are generating the data we observe.
* The data we observe is assumed to be a linear combination of the latent variables and some noise
* The number of latent variables is possibly lower than the amount of observed data, which gives us the dimensionality reduction

#### ICA

ICA stands for Independent Component Analysis

* ICA assumes that the data is generated by N sources, which is similar to factor analysis.
* The data is assumed to be a mixture of observations of the sources.
* The sources are assumed to be statically independent, unlike PCA, which assumes the data is uncorrelated.
* If there are fewer sources than the amount of our observed data, we'll get a dimensionality reduction.

#### PCA vs SVD

* PCA
    * find the eigenvalues of a matrix
        * these eigenvalues told us what features were most important in our data set
* SVD
    * find the singular values in $\Sigma$
        * singular values and eigenvlues are related
        * singular vlues are the square root of the eigenvlues of $AA^T$

### Label Encoding

* [Scikit Learn - 4.9 Transforming the prediction target (y)](http://scikit-learn.org/dev/modules/preprocessing_targets.html#preprocessing-targets)

### Classification Imbalance

To alter the data used to train the classifier to deal with imbalanced classification tasks.

* Oversample: means to duplicate examples
* Undersample: means to delete examples

Scenario

* You want to preserve as much information as possible about the rare case (e.g. Credit card fraud)
    * Keep all of the examples form the positive class
    * Undersample or discard examples form the negative class

Drawback

* Deciding which negaive examples to toss out. (You may throw out examples which contain valuable information)

Solution

1. To pick samples to discard that aren't near the decision boundary
2. Use a hybrid approach of undersampling the negative class and oversampling the positive class

(Oversample the positive class have some approaches)

* Replicate the existing examples
* Add new points similar to the existing points
* Add a data point interpolated between existing data points (can lead to overfitting)

### Feature Scaling

aka. Data Normalization (generally performed during the data preprocessing step)

A method used to standardize the range of independent variables or features of data

## Model Expansion

### Binary to Multi-class

* [Wiki - Multiclass classification](https://en.wikipedia.org/wiki/Multiclass_classification)
* [pdf - Lecture 18: Multiclass Support Vector Machines](http://math.arizona.edu/~hzhang/math574m/2017Lect18_msvm.pdf)

While some classification algorithms naturally permit the use of more than two classes, others are by nature binary algorithms; these can, however, be turned into multinomial classifiers by a variety of strategies.

**Main Ideas**

* Decompose the multiclass classification problem into multiple binary classification problems
* Use the majority voting principle (a combined decision from the committee) to predict the label

#### One-vs-rest (one-vs-all) Approaches

Tutorial:

* [Lecture 6.7 — Logistic Regression | MultiClass Classification OneVsAll — [Andrew Ng]](https://www.youtube.com/watch?v=-EIfb6vFJzc)

#### Pairwise (one-vs-one, all-vs-all) Approaches

## Model Validation

### Splitting Data

* Training Set: to get weights (parameters) by training
* Validation Set / Development Set: to determine superparameters and when to stop training (early stop)
* Test Set: to evaluate performance

### Simplest Split

Split data into Training and Test set (usually 2:1)

Problem: the sample might not be representative

### Hold-out Validation

Stratification: sampling for training and testing within classes (this ensures that each class is represented with approximately equal proportions in both subsets)

### N-Fold Cross-Validation (Repeated Hold-out)

> Repeat hold-out process with different subsamples

1. Start with a dataset D of labeled sample
2. Randomly partiiton into N groups (i.e. N-fold)
3. Calculate average n errors

#### Hold-one-out Cross-Validation (LOO CV)

### Train-Validation-Test

Split the Train data into Traintrain and Validation

* Use the validation set to find the best parameters
* Use the test set to estimate the true error

#### Nested N-Fold Cross-Validation

### Bootstrapping

The bootstrap is an estimaiton method that uses sampling with replacement to form the training set

Case where bootstrap does not apply

* Too small datasets: the original sample is not a good approximation of the population
* Dirty data: outliers add variability in our estimations
* Dependence structures (e.g. time series, spatial problems): bootstrap is based on the assumption of independence

#### 0.632-bootstrap

$$
\lim_{n \rightarrow \infty} (1-\frac{1}{n})^n = \frac{1}{e} = 0.368
$$

This means that the training data will contain approximately 63.2% of the examples.

## Model Evaluation

### Classification

Standard classification problem assumes indifvidual cases are disconnected and independent (i.i.d: independently and identically distributed)

We're going to minimize the empirical classification error

#### Methods Overview

* Decision Trees
  * Function space is Boolean formula in Disjunctive Normal Form (DNF)
* Probability Model
  * Function space is dependent on the distribution assumptions of the model
* Discriminant Functions
  * Partition the D dimensional spae with a (D-1) dimensional function
  * Function space is dependent on the function used to discriminate
* Linear Discriminates
  * Partition the D dimensional space with a (D-1) dimensional linear function

#### Accuracy (Error Rate)

* The error rate = the number of misclassified instances / the total number of instances tested.
* Measuring errors this way hides how instances were misclssified.

#### Confusion Matrix

[**Wiki - Confusion Matrix**](https://en.wikipedia.org/wiki/Confusion_matrix)

* With a confusion matrix you get a better understanding of the classification errors.
* If the off-diagonal elements are all zero, then you have a perfect classifier

* Construct a confusion matrix: a table about Actual labels vs. Predicted label

#### Precision, Recall Ratio

These metrics that are more useful than error rate when detection of one class is more important than another class.

Consider a **two-class** problem.
(Confusion matrix with different outcome labeled)

Actual \ Redicted   |+1                 |-1
:------------------:|:-----------------:|:-----------------:
**+1**              |True Positive (TP) |False Negative (FN)
**-1**              |False Positive (FP)|True Negative (TN)

* **Precision** = TP / (TP + FP)
    * Tells us the fraction of records that were positive from the group that the classifier predicted to be positive

* **Recall** = TP / (TP + FN)
    * Measures the fraction of positive examples the classifier got right.
    * Classifiers with a large recall dont have many positive examples classified incorectly.

* **F₁ Score** = 2 × (Precision × Recall) / (Precision + Recall)

Summary:

* You can easily construct a classifier that achieves a high measure of recall or precision but not both.
* If you predicted everything to be in the positive class, you'd have perfect recall but poor precision.

Now consider **multiple classes** problem.

* Macro-average
* Micro-average

#### ROC curve

[Wiki - Receiver operating characteristic](https://en.wikipedia.org/wiki/Receiver_operating_characteristic)

ROC stands for Receiver Operating Characteristic

* The ROC curve shows how the two rates chnge as the threshold changes
* The ROC curve has two lines, a solid one and a dashed one.
    * The solid line:
        * the leftmost point corresponds to classifying everything as the negative class.
        * the rightmost point corresponds to classifying everything in the positive class.
    * The dashed line:
        * the curve you'd get by randomly guessing.
* The ROC curve can be used to compare classifiers and make cost-versus-benefit decisions.
    * Different classifiers may perform better for different threshold values
* The best classifier would be in upper left as much as possible.
    * This would mean that you had a high true positive rate for a low false positive rate.

**AUC** (Area Under the Curve): A metric to compare different ROC

* The AUC gives an average value of the classifier's performance and doesn't substitute for looking at the curve.
* A perfect classifier would have an AUC of 1.0, and random guessing will give you a 0.5.

### Regression

#### Mean Absolute Error (MAE)

#### Mean Squared Error (MSE)

#### Root Mean Squared Error (RMSE)

### Clustering

#### Within Groups Sum of Squares

* Elbow method

#### Mean Silhouette Coefficient of all samples

#### Calinski and Harabaz score

* Max score => the best number of groups (clustes)

## Fitting and Model Complexity

Sample Complexity: A more complex function requires more data to generate an accurate model.

### Generalization

* A good learning program learns something about the data beyond the specific cases that have been presented to it
* Classifier can minimize "i.i.d" error, that is error over future cases (not used in training). Such cases contain both previously encountered as well as new cases.

Error

* Training error: error *on training set*
* Generalization error: expected value of the errors *on testing data*
  * Capacity: ability to fit a wide variety of functions (the expressive power)
    * too low (underfitting): struggle to fit the training set
    * too high (overfitting): overfit by memorizing properties of the training set that do not serve them well on the test set

### Overfitting

In general, over-fitting a model to the data means that we learn non-representative properties of the sample data

> overfitting and poor generalization are synonymous as long as we've learned the training data well.

Overfitting is affected by

* the "simplicity" of the classifier (e.g. straight vs. wiggly line)
* the size of the sample
* the complexity of the function we wish to learn from data
* the amount of noise
* the number of the variable (features)

> Low training set error rate but high validation set error rate

### Underfitting

> High training set error rate

### Occam's Razor Principle

[Wiki - Occam's razor](https://simple.wikipedia.org/wiki/Occam%27s_razor)

Law of Parsimony

### Regularization (Weight Decay)

Used to control the complexity of the model (in case of overfitting)

> let $\theta = (w_1, w_2, \dots, w_n)$ as model parameters

#### L1 Regularization

$$
R(\theta) = ||\theta ||_1 = |w_1| + |w_2| + \cdots + |w_n|
$$

#### L2 Regularization

$$
R(\theta) = ||\theta ||_2^2 = w_1^2 + w_2^2 + \cdots + w_n^2
$$

#### L1+L2 Regularization

$$
R(\theta) = \alpha ||\theta ||_1 + (1-\alpha) ||\theta ||_2^2
$$

## Reducing Loss

### Common Loss Function

#### Hinge Loss

Binary classification

$$
L_{\text{hinge}}(\hat{y}, y) = \max(0, 1-y \cdot \hat{y})
$$

Multi-class classification

$$
L_{\text{hinge}}(\hat{y}, y) = \max(0, 1- (\hat{y}_t - \hat{y}_k)
$$

#### Cross Entropy Loss (Negative Log Likelihood)

Used to measure the similarity between two probability distribution.

$$
H(p, q) = - \sum_x p(x) log q(x)
$$

* $p(x)$ represents the real distribution.
* $q(x)$ represents the model/estimate distribution.

Binary classification

$$
L_{\text{Cross Entropy}}(\hat{y}, y) = -y \log \hat{y} - (1-y) \log (1-\hat{y})
$$

Multi-class classification

$$
L_{\text{Cross Entropy}}(\hat{y}, y) = -\log \hat{y}_t
$$

### Learning Rate

### Gradient Descent

Find the fastest way to minimize the error.

#### Stochastic Gradient Descent

* Random select m example as sample (minibach)
* Use gradient average to estimate the expected gradient of the training set

## Other Learning Method

### Cost-sensitive Learning

* The different incorrect classification will have different costs.
* This gives more weight to the smaller class, which when training the classifier will allow fewer errors in the smaller class
* There are many ways to include the cost information in classification algorithms
    * AdaBoost
        * Adjust the error weight vector D based on the cost function
    * Naive Bayes
        * Predict the class with the lowest expected cost instead of the class with the highest probability
    * SVM
        * Use different C parameters in the cost function for the different classes

### Lazy Learning

### Incremental Learning (Online Learning)

### Multi-label Classification

[Wiki - Multi-label Classification](https://en.wikipedia.org/wiki/Multi-label_classification)
