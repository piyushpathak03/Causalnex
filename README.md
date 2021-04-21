# Causalnex

## Introduction of Causalnex
CausalNex is a Python library that uses Bayesian Networks to combine machine learning and domain expertise for causal reasoning. You can use CausalNex to uncover structural relationships in your data, learn complex distributions, and observe the effect of potential interventions.

## Main features of CausalNex
The CausalNex library has the following features:

1. Deploys state-of-the-art structure learning method, DAG with NO TEARS, to understand conditional dependencies between variables
2. Allows domain knowledge to augment model relationships
3. Builds predictive models based on structural relationships
4. Understands model probability
5. Evaluates model quality with standard statistical checks
6. Visualisation which simplifies how causality is understood
7. Analyses the impact of interventions using Do-calculus

# Steps in Causalnex:--

## Structure Learning
Defining the structure of a Bayesian Network (BN) model can be done based on machine learning, domain knowledge, or a combination of both, where experts and algorithms contribute as equal partners.

Regardless of the approach, it is important to validate the structure by evaluating the BN - this will be covered later in the tutorial. In this section, we will focus on how to define a structure.

## Learning the Structure
As the number of variables grows, or when domain knowledge does not exist, it can be tedious to define a structure manually. We can use CausalNex to learn the structure model from data. The structure learning algorithm we are going to use here is the NOTEARS algorithm.

When learning structure, we can use the entire dataset. Since structure should be considered as a joint effort between machine learning and domain experts, it is not always necessary to use a train / test split.

But before we begin, we have to pre-process the data so that the NOTEARS algorithm can be used.

## Modifying the Structure
To correct erroneous relationships, we can incorporate domain knowledge into the model after structure learning. We can modify the structure model through adding and deleting the edges.

## Fitting the Conditional Distribution of the Bayesian Network
### 1. Preparing the Discretised Data
Bayesian Networks in CausalNex support only discrete distributions. Any continuous features, or features with a large number of categories, should be discretised prior to fitting the Bayesian Network. Models containing variables with many possible values will typically be badly fit, and exhibit poor performance.
CausalNex provides a few helper methods to make discretisation easier. Let’s start by reducing the number of categories in some of the categorical features by combining similar values. We will make numeric features categorical by discretisation, and then give the buckets meaningful labels.

### 2. Cardinality of Categorical Features
To reduce the cardinality of categorical features we can define a map {old_value: new_value}, and use this to update the feature

### 3. Discretising Numeric Features
To make numeric features categorical, they must first be discretised. CausalNex provides a helper class causalnex.discretiser.Discretiser, which supports several discretisation methods.

## Create Labels for Numeric Features
To make the discretised categories more readable, we can map the category labels onto something more meaningful in the same way that we mapped category feature values.

## Train / Test Split
Like many other machine learning models, we will use a train and test split to help us validate our findings.

## Model Probability
With the learnt structure model from earlier and the discretised data, we can now fit the probability distrbution of the Bayesian Network. The first step in this is specifying all of the states that each node can take. This can be done either from data, or providing a dictionary of node values. We use the full dataset here to avoid cases where states in our test set do not exist in the training set. For real-world applications, these states may need to be provided using the dictionary method.

## Fit Conditional Probability Distributions
The fit_cpds method of BayesianNetwork accepts a dataset to learn the conditional probablilty distributions (CPDs) of each node, along with a method of how to do this fit.

## Predict the State given the Input Data
The predict method of BayesianNetwork allows us to make predictions based on the data using the learnt Bayesian Network. For example, we want to predict if a student fails or passes their exam based on the input data. Imagine we have an incoming student data that looks like this:

## Model Quality
To evaluate the quality of the model that has been learned, CausalNex supports two main approaches: Classification Report and Reciever Operating Characteristics (ROC) / Area Under the ROC Curve (AUC). In this section each will be discussed.

### Classification Report
To obtain a classification report using a BN, we need to provide a test set, and the node we are trying to classify. The report will predict the target node for all rows in the test set, and evaluate how well those predictions are made.





