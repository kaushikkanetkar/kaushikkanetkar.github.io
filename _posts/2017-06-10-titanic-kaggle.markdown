---
layout: post
comments: false
title:  "Survival on Titanic - Kaggle"
excerpt: "A binary classification problem to find out who would survive the Titanic"
date:   2017-06-10
---

The **Titanic Survival** problem on Kaggle is one of the most popular and basic one for people new to machine learning.


## Dataset

The dataset provided on Kaggle has the following:

- Training (892)
- Test (419)

Labels have been provided for the training data set (1=Survived, 0=Did not survive). Labels have not been provided for the test data set. They want to use predict survival on the test dataset.

## Feature Engineering

An important aspect of solving this problem is what features get fed into the classifier. Well, we could just feed in the features as-is but they might not lead a clear deduction of the survival.

The features here:
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

Label:
- Survived (0 or 1)

A simple look at the entire training set will not help here. A few modifiications and co-relations are needed to be made with the "Survived" field. Python is very powerful. I used packages like numpy, seaborn and pandas to:
- Read CSVs
- Group features and co-relate with the label field
- Analyze certain parts of the features, if not all
- Plot graphs ; because graphs and plots are always fun to see what's exactly happening.

Here's what I deduced from the features that are affecting the chances of survival:
- Age not known
- Being a child (Age less than 9)
- Family size (between 1 and 3 especially - increases survival)
- Name length
- Title
- Embarked
- First alphabet of the Cabin, which suggests the Cabin type
- Being young (Age less than 30)
- Being a Male and having a bad ticket number. (Bad ticket is subjective - here it corresponding to the first digit of the Ticket no.)

These were now my new features to be sent to the classifier.

## Classifier


