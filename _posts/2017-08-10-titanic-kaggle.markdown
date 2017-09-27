---
layout: post
comments: false
title:  "Survival on Titanic - Kaggle"
excerpt: "A binary classification problem to find out who would survive the Titanic"
date:   2017-08-10
---

Link to the question on Kaggle website - [here.](https://www.kaggle.com/c/titanic)

## Dataset

The dataset provided on Kaggle:  
- Training (892)
- Test (419)

Labels have been provided for the training data set (0=Didn't Survive, 1=Survived).
Labels have not been provided for the test data set.

## Feature Engineering

It's important to decide what features get fed into the classifier. Well, we could just feed the features as-is but that might not give us a high accuracy.

The features, as seen in the training set (X):  
- Pclass (Passenger Class - 1, 2, 3)
- Full Name (including title)
- Sex (Male or Female)
- Age
- SibSp (no. of Siblings + Spouse)
- Parch (Parents + Children)
- Ticket
- Fare
- Cabin
- Embarked (C, S or Q)

Label (Y): 
- Survived (0 or 1)

Python is very powerful. Numpy, seaborn and pandas can help to: 
- Read CSVs
- Plot graphs; because graphs and plots are always fun to see if a particular feature can give some signals.
- Group features and co-relate with the label field (plot an engineered feature "x" v/s "Survived" field)
- Analyze certain parts of the features, if not all (eg: just the title out of a name, or the length of a name)

Here's what I deduced from the features that are affecting the chances of survival: (X_modified)  
- Age not known
- Being a child (Age less than 9)
- Family size (between 1 and 3 especially - increases survival)
- Name length
- Title
- Embarked
- First alphabet of the Cabin, which suggests the Cabin type
- Being young (Age less than 30)
- Being a Male and having a bad ticket number. (Bad ticket is subjective - here it corresponding to the first digit of the Ticket no.)

I split the training data (892) into "train" and "test" sets in a 80-20 split using Python's sklearn.

## Training and Testing

For the features to do the job, it's crucial that we design the model in the right way. We need to make sure our model can extract the signals efficently.

This is a binary classification problem, so our "Y" will have 2 classes (0 and 1).

> Framework used - Tensorflow

**LinearClassifier - "Wide" model**  
*Logistic regression*  
First option is to use a logistic regression model (linear classifier). It's faster and we don't need to worry much about hyperparameter tuning.
Results from LinearClassifier:
- Accuracy on training set = 82%
- Accuracy on test set = 75%

One drawback on linear classifiers is that they don't memorize the interactions of features with each other. For example, in our dataset we know that being a male and in Pclass 1 has a lower chance of survival - (Interaction between "Sex" and "PClass"). The other problem is that linear classifiers don't generalize feature interactions that well.

**DNNClassifier - "Deep" model**  
*Neural Networks*  
Deep models can generalize feature interactions that haven't appeared in the training set.
So, I used the DNNClassifier and built a 3-layer network. After doing the usual hyperparameter tuning, these were the results I got:
- Accuracy on training set = 89%
- Accuracy on test set = 82%

Here we go, quite an improvement.

**Deep and Wide model**
Tensorflow has another classifier called "Deep and Wide".
This model actually combines the LinearClassifier and DNNClassifier to create a DNNLinearCombinedClassifier. Focus here is to use benefits of both models.

More details are presented in this [post](https://www.tensorflow.org/versions/r0.12/tutorials/wide_and_deep/)

> One can make use of "crossed columns" to explicitly notify the classifier about a certain feature interaction. Idea behind this is to reduce feature engineering effort.

Results on the "Deep and Wide" model:
- Accuracy on training set = 91%
- Accuracy on test set = 84%

I was able to get a slightly better accuracy on the "Deep and Wide" model as compared to the "Deep" model.

The code for this is on my [github.](https://github.com/kaushikkanetkar/titanic-kaggle) 

## Issues

- Increasing the no. of hidden layers and units per layer bumped up the training accuracy to 94%, but it reduced the test set accuracy to 78%. A complex model generated high variance and made the model to overfit.
- Decreasing the no. of units per layer got me a training and test set accuracy of ~82%.

