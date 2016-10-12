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
It seems like a linear function is going to be the right choice so I'm approixmating $$y$$ with
 
$$h_{\theta}(x^{(m)}) = \theta_0 + \theta_1x_1$$

$$m$$ is the m-th example from our training set,it is not an exponent it's should just indicate which example we're using

$$h_{\theta}(x^{(m)})$$ is called hypotheses

$${\theta}_i$$ are our weights

$$x_1$$ is our selected feature

To simplyfiy our notation we're going to introduce $$x_0 = 1$$ so we can write

$$h_{\theta}(x^{(m)}) = \sum_{i=0}^n \theta_ix_i = \theta^Tx$$

$$n$$ is the number of features. Our goal is to choose our weigths so that we get a good prediction.

For our inital weight we're setting the inital $$\theta$$ to 0

## Cost Function 
The cost function gives us an error margin, it tells us how far apart $$h_{\theta}(x_i)$$ and $$y_i$$ are. There are
multiple cost function but I'm going to use the mean squared error (MSE).

$$J(\theta) = \frac{1} {2m} \sum_{i = 1}^{m} (h_{\theta}(x^{(i)})-y^{i})^2$$

We're trying to choose a $$\theta$$ so that $$J(\theta)$$ is small, to achieve this we're using a gradient descent.

## Gradient Descent
A Gradient descent is a method to minimize $$J(\theta)$$, generally speaking it's a method to minimize a function with multiple parameters.

The gradient descent takes steps in the direction of the steepest decrease of $$J(\theta)$$, with the goals to find the local minimum. 
After each steps is taken $$\theta$$ is updated. 

For our case we're going to use the batch gradient descent, it starts with an initial $$\theta$$ and repeadedly performs following step:

$$\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j}J(\theta) $$

$$\alpha$$ is the learning rate, after solving the partial derivate on the right side you get for a single training example $$i$$ 
the following result:

$$\begin{align*}
  \text{repeat until convergence: } \lbrace & \newline 
  \theta_0 := & \theta_0 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m}(h_\theta(x_{i}) - y_{i}) \newline
  \theta_1 := & \theta_1 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m}\left((h_\theta(x_{i}) - y_{i}) x_{i}\right) \newline
  \rbrace&
  \end{align*}$$


$$\theta_j := \theta_j + \alpha(y^{(i)} - h_{\theta}(x^{(i)}))x_j^{(i)}$$

With our current version we're just taking a look at one training example and update $$\theta$$, so we need to modify it a little bit in order 
to look simoultaniously at multiple training examples:

$$\theta_j := \theta_j + \alpha \sum_{i=1}^m(y^{(i)} - h_{\theta}(x^{(i)}))x_j^{(i)}$$

This is our final batch gradient descent, it takes a look at every example from our traing set for every step it takes.
There are other types of gradient descent, but for now I'm just focuing on this one. 

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