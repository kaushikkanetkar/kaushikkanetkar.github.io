---
layout: post
comments: true
title:  "An App to recognize handwritten digits"
excerpt: "This is an Android application I wrote to classify handwritten digits with the help of the MNIST dataset and ConvNets."
date:   2017-03-01
---


I developed an application that recognizes handwritten digits using the live camera feed of the phone. There were many components that I had to deal with, let's look at them.

## Training

#MNIST

The MNIST database is a relatively famous dataset of handwritten digits hosted on Yann LeCun's [homepage](http://http://yann.lecun.com/exdb/mnist/).
It contains a training set of 60,000 examples and a test set of 10,000 examples. This is actually a subset of NIST databse. 

The images in the MNIST database are grayscale and their size is 28x28. Good enough for beginners to learn and debug.


