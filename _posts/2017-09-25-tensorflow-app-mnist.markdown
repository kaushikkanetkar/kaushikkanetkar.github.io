---
layout: post
comments: false
title:  "An App to recognize handwritten digits"
excerpt: "This is an Android application I wrote to classify handwritten digits with the help of the MNIST dataset and ConvNets."
date:   2017-03-01
---


I developed an application that recognizes handwritten digits using the live camera feed of the phone. There were many components that I had to deal with, let's look at them.

## Training

**MNIST**

The MNIST database is a relatively famous dataset of handwritten digits hosted on Yann LeCun's [homepage](http://http://yann.lecun.com/exdb/mnist/).
It contains a training set of 60,000 examples and a test set of 10,000 examples. This is actually a subset of NIST databse. 

The images in the MNIST database are grayscale and their size is 28x28. Good enough for beginners to learn and debug.

I used Tensorflow to train the images in the database using the LeNet 5 model. This ConvNet gave me 99.21%. If I tuned the hyperparameters here and there, I was able to get maybe a 0.1 % bump occasionally, but I was fine with these results. A simple logistic regression model gave me 91.3 % accuracy, which is fine, but isn't that great when I know that ConvNets gave me ~99%.

We'll store this trained file which has all the weights - that activate the computation graphs.


## The Android App

**Camera API**

Here I started by first writing an Android application with live camera feed displayed in a small window. I have written a bunch of apps in the past, it's always fun, reminds me of the [Snake game](https://goo.gl/UJRkrp) I wrote that made it to the PlayStore. The camera part was a little tricky due to the alignments and integration of the Camera API into my native app code.

