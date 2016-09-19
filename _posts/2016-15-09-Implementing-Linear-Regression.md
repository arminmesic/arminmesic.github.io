---
layout: post
title:  "Implementing Linear Regression"
date:   2016-09-15
categories: 
    - Machine Learning
---
#NOTES
* Think about implementing it in Python or just use octave/mathlab


# When to use linear regression

# What are we Implementing
-> using simple example to understand the underlying principle
-> octave focus on the Math
-> using one variable

# Dataset
-> split between training and test data

# Plotting the data
-> what are we looking for

# Feature Selection
-> seems linear so just one variable

# Math for a straight linear
![](https://chrisjmccormick.files.wordpress.com/2014/02/mse_variable_descriptions.png 'tet')
-> simple table to show all the different variables
-> table with data excerpt
-> what is $$x_1$$, $$x^{(i)}$$
It seems like it's a linear function, so we need a function that describes our dataset
as our initial choice we're going to use

$$h_{\theta}(x) = \theta_0 + \theta_1x_1$$

$$h_{\theta} $$ is called our hypothesis, and it's trying to predict future values.

# Basics covered
http://stackoverflow.com/questions/13623113/can-someone-explain-to-me-the-difference-between-a-cost-function-and-the-gradien
## Cost Function 
-> mean squared error
-> why choose MSE

$$J(\theta) = \sum_{i = 1}^{m} (h_{\theta}(x^{(i)}-y^{i}))^2$$

-> purpose of cost function
-> try to minimize, but how -> gradient descent
-> overfitting if it's everytime 0
## Gradient Descent
-> purpose of gradient descent 
-> Steps in the direction of the steepest decrease of J, try to find the local minima
-> What is a Gradient (no calculus required)?
https://www.youtube.com/watch?v=WnqQrPNYz5Q

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