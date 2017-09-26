---
layout: post
comments: false
title:  "An App to recognize handwritten digits"
excerpt: "This is an Android application I wrote to classify handwritten digits with the help of the MNIST dataset and ConvNets."
date:   2017-03-31
---


I developed an application that recognizes handwritten digits using the live camera feed of the phone. There were many components that I had to deal with, let's look at them.

## Training

**MNIST**

- The MNIST database is a relatively famous dataset of handwritten digits hosted on Yann LeCun's [homepage](http://http://yann.lecun.com/exdb/mnist/).
It contains a training set of 60,000 examples and a test set of 10,000 examples. This is actually a subset of NIST databse. 

<div style="text-align:center;"><img src="/assets/mnist_digits.png"></div>
</div>
<div class="thecap">Image taken from tensorflow.org</div>
</div>

- The images in the MNIST database are grayscale and their size is 28x28. Good enough for beginners to learn and debug.

- I used Tensorflow to train the images in the database using a modified version of the LeNet 5 model. This ConvNet gave me 99.21%. On tuning the hyperparameters, I was able to get a 0.1 % bump occasionally, but I was fine with the previous results. A simple logistic regression model gave me 91.3 % accuracy, which is fine, but isn't that great when I know that ConvNets gave me ~99%.

> We'll store this trained file which has all the weights - that activate the computation graphs.


## The Android App

**Camera API**

- Here I started by first writing an Android application with live camera feed displayed in a small window. I have written a bunch of apps in the past, it's always fun, reminds me of the [Snake game](https://goo.gl/UJRkrp) I wrote that made it to the PlayStore. The camera part was a little tricky due to the alignments and integration of the Camera API into my native app code.

- Next up was to integrate the incoming camera feed and give them as inputs to the trained model. There were two parts to this. One was to translate the incoming feed into images and their respective formats and to prep them in the core app code. Second was to create a small adapter module code to interact with the trained model file. I felt it was easier to have the integration split into two parts as above, just to keep it clean and easier to debug.

Once I verified that I was sending the images in the right format and getting some classified output back from tensorflow, it was time for my favorite part, fine tuning and processing the image.

## Image Processing

- This was one of the main reasons I developed this application. With the ~99% performance on MNIST, I could have been happy and tried out a few more images using a photo editor software. But I wanted to try out a real world integration of the usage, end to end.

- Basic images captured by the camera in a normal lighted environment have a lot of noise. This becomes really difficult to convert your grayscale image into binary format. Infact one could actually use some of these noisy binary images, throw them into the training set and re-train. Meanwhile, I used a bunch of image morphological techniques and coded them myself without using any image processing library. Since it was a grayscale image, the thresholding was done using Otsu's algorithm, which was reliable.


After denoising the images, and integrating the input feed into the tensorflow API, I was able to recognize the handwritten digits as seen by the camera of my phone.

> Youtube link of the application -- [Demo](https://goo.gl/0FNvXL)

