---
layout: post
title:  "Implementing Linear Regression"
date:   2016-09-15
categories:
    - Machine Learning
---

Linear regression learns from a provided dataset and tries to predict a number. I'm going to show how
it works with a simple dataset and the goal is to be able to predict housing prices.

I'm going to use a dataset that I got from Andrew Ng's Machine Learning course, it's a simple example
as the main point of this post is to understand the idea of the algorithm.

I'm going to use Matlab to implement it, you can find the source [here](/about).

Here is a small excerpt of the data

| area (feet^2) | #bedrooms | Price  |
|---------------|-----------|--------|
| 2104 | 3 | 399900 |
| 1600 | 3 | 329900 |
| 2400 | 3 | 232000 |

# Plotting the data
To get a better idea about the data I'm going to plot it.
![Data Plot](/images/posts/linear-regression/initialPlot.jpg "Data Plot")

As you can see I've just selected one feature, the living area, I'm keeping it simple.

We're looking for a function that matches our data, it looks like a simple straight line (linear function)
should fit well enough.

# Math for linear regression
It seems like a linear function is going to be the right choice so I'm approximating $$y$$ with

$$
\def\hypothesis{
  h_{\theta}(x^{(i)})
}
$$

$$\hypothesis = \theta_0 + \theta_1 x^{(i)}_1$$

$$x^{(i)}_j$$ is the j-th feature of the i-th example, keep in mind $$i$$ is not a power

$$\hypothesis$$ is called hypotheses
$$
\def\thetaVectorExplicit{
\begin{pmatrix}
  \theta_0 \dots \theta_n
\end{pmatrix}}
$$

$$\theta = \thetaVectorExplicit$$, vector with our weights, initially set to $$0$$

To simplify our notation we're going to introduce $$x_0 = 1$$ so we can write

$$\hypothesis = \sum_{j=0}^n \theta_j x^{(i)}_j = \theta x^{T}$$

$$n$$ is the number of features. Our goal is to choose our weights so that we get a good prediction.

## Cost Function
The cost function gives us an error margin, it tells us how far apart $$\hypothesis$$ and $$y_i$$ are. There are multiple cost function but I'm going to use the mean squared error (MSE).

$$J(\theta) = \frac{1} {2m} \sum_{i = 1}^{m} (\hypothesis-y^{(i)})^2$$

We're trying to choose a $$\theta$$ so that $$J(\theta)$$ is small, to achieve this we're using a gradient descent.

## Gradient Descent
// Place this formula at the right place

$$
\def\gradientDescFThetaMatrix{
\begin{pmatrix}
    \frac{\partial J(\theta)}{\partial \theta_0} \\
    \vdots \\
    \frac{\partial J(\theta)}{\partial \theta_n}
\end{pmatrix}}


\nabla_{\theta} J(\theta)= \gradientDescFThetaMatrix$$

A Gradient descent is a method to minimize $$J(\theta)$$, generally speaking it's a method to minimize a function with multiple parameters.

The gradient descent takes steps in the direction of the steepest decrease of $$J(\theta)$$, with the goals to find the local minimum.
After each steps is taken $$\theta$$ is updated.

For our case we're going to use the batch gradient descent, it starts with an initial $$\theta_i$$ and repeatedly performs following step, where $$\alpha$$ is the learning rate:

$$\theta_i := \theta_i - \alpha \frac{\partial J(\theta)}{\partial \theta_i}$$

after solving the partial derivate for our example, keep in mind we only have $$\theta_0$$ and $$\theta_1$$:

$$
\theta_0 := \theta_0 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m}(\hypothesis - y^{(i)}) x^{(i)}_{0} \\
\theta_1 := \theta_1 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m}(\hypothesis - y^{(i)}) x^{(i)}_{1}
$$

this can be generalized to

$$\theta_i := \theta_i - \alpha \frac{1}{m} \sum\limits_{i=1}^{m}(\hypothesis - y^{(i)}) x^{(i)}_{j}$$


This is our final batch gradient descent, it takes a look at every example from our training set for every step it takes.
There are other types of gradient descent, but for now I'm just focusing on this one. The gradient descent is
repeatedly performed till it reaches it's minimum, and as a result we get $$\theta$$

More information on gradient descent can be found [here](https://www.youtube.com/watch?v=WnqQrPNYz5Q)

## Model definition
-> What is a model, vector with values that helps us make predictions
-> Theta

# Show examples for polynomial model
-> Straight line, $$x^2$$ and a $$5^{th}$$ order polynomial
-> the more features we add the better?
-> underfitting, just right, overfitting
-> show simple model vs overfitted model
-> Why choosing this one not a higher order polynomial

# Fitting the data
-> Show each iteration

# Result

# Using the test  data

# Consclusion
