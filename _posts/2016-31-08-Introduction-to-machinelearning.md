---
layout: post
title:  "Introduction to machine learning"
date:   2016-08-31
categories: 
    - Machine Learning
---

I'm currently working through Andrew Ng's machine learning course so I'm writing down the things I'm learning during
this time. This post is for beginners and if somebody has found a mistake shoot me a mail, you can find my address [here](/about)

# What is machine learning
Machine learning is as a group of algorithms that try to learn from available data and try to make predictions. 
In machine learning we use methods by which the pc will come up with it's own solution, if we would try to solve the same problem
with "normal" algorithms we would try to develop software to solve the task directly. 

When can machine learning be used? We can, for example predict the price for a home, detect if a credit card 
transaction is fraudulent and even recommend a movie that you should watch next based on your previous one.

# Supervised vs unsupervised learning
The machine learning algorithms can further be separated in two groups, supervised and unsupervised learning. 
Let's take a look at the different classes.

### Supervised learning
Deciding if a credit card transaction is fraudulent or predicting the price of a home are two use cases for supervised 
learning. We need to teach the algorithm how to learn from the available data, we have a bunch of examples (training data) 
and tell the algorithm the expected output for every input. The data is labeled.
For our credit card fraud detection, this means we have credit card transactions which are labeled as normal or suspicious.
And for our home price example this would mean we have the size of the home and the current price.

Size is a feature.
    
|Size | Price   |
|-----|---------|
|80m² | 100.000€|
|120m²| 350.000€|

Our training set isn't limited to one feature, the number of rooms could be another feature. Some datasets have hundreds of
features and you have to decide which ones are important.

|Size |no. Rooms|Price   |
|-----|---------|--------|
|80m² | 2       |100.000€|
|120m²| 4       |350.000€|

Supervised learning can further be grouped in two different group of algorithms, classification and regression.

### What is classification
In the most simple case your algorithm just needs to decide if the provided data is in one class or not, you get a 
discrete value as the result, 0 or 1. For the credit card fraud example this means the algorithm has to decide if the 
transaction is normal (0) or suspicious (1).

Here is a visualization, we're trying to find a line that separates the two classes, so if any future data is above the 
line we will identify it as a valid transaction.

![Classification Plot](/images/posts/machine-learning-intro/classificationPlot.jpg "Classification Plot")
![Classification Plot with decision boundary](/images/posts/machine-learning-intro/classificationPlotDecisionBoundary.jpg "Classification Plot with decision boundary")

### What is regression
Predicting the price for a home is a use case for regression algorithms, the goal is to predict/estimate a number.
So your expected output is a number and not just a class label as in classification.


![Regression Plot](/images/posts/machine-learning-intro/regressionPlot.jpg "Regression Plot")
![Regression Plot Fitted](/images/posts/machine-learning-intro/regressionPlotFitted.jpg "Regression Plot Fitted")

As you can see we're trying to fit a graph that matches our provided data as closely as possible.

### Unsupervised learning
A possible use case is to recommend the next movie to watch after you've finished the current one.
The goal for unsupervised learning is to discover patterns/structure and to cluster the data into classes.
For supervised learning we're teaching the algorithm how to handle the data, but for unsupervised learning the algorithm
is on its own, there is no labeled data.

# Conclusion
Machine Learning sound really complicated but in the end it's just a collection of algorithms that teaches the PC to learn
from data and make predictions for new data. This post just tries to show the big picture for machine learning, in my next 
post I'll implement linear regression with a simple example.