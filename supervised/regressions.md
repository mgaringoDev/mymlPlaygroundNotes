---
layout: default
title: Regressions
nav_order: 2
---

# Introduction

## To Do
- **Regression Algorithms**
	- [ ] Ordinary Least Squares Regression (OLSR)
	- [ ] Linear Regression
	- [ ] Logistic Regression
	- [ ] Stepwise Regression
	- [ ] Multivariate Adaptive Regression Splines (MARS)
	- [ ] Locally Estimated Scatterplot Smoothing (LOESS)

## Regression
Linear regression models are a good starting point for regression tasks. Such models are popular because they can be fit very quickly, and are very interpretable. You are probably familiar with the simplest form of a linear regression model (i.e., fitting a straight line to data) but such models can be extended to model more complicated data behavior.  For simple linear regression there is, in fact, an optimal solution, however for high dimensional spaces there are none and we need to regard the problem as an optimization problem. Regression fits a function to the data set, so what we are trying to do is to find a representative function and fit to our data set. Learning takes place as finding the best possible - local optimum - values of the function parameters. Linearity refer to the fact that we are tying to fit either a straight line or a polynomial function (polynomial regression).

This is a **parametric method** which means that there exists a relationship which can be expressed as a **fixed equation form to relate y and X**.  Where y are the output variables or response, and **X** are the input variables also known as covariates, features, independent variables or predictors.  The general form for linear regression is:

$$ y = f(X) + \epsilon$$

Various methods use different $$f(X)$$ and are usually statistical methods.  $$\epsilon$$ are the error terms that independent of $$X$$.  Linear regression then simplifies to identifying the coefficients of $$f(X)$$ by minimizing error based on the given data.

### Linear Regression
The model is a straight line in the form $$f(X)=y=mx+b$$.  We can use **sklearn.linear_model** module to obtain the m and b parameters given list of points [x,y].  The slope and intercept of the data are contained in the model's fit parameters, which in Scikit-Learn are always marked by a trailing underscore. Here the relevant parameters are **coef_** and **intercept_** of the model.

#### Polynomial Basis Function 
One way to adapt linear regression to non-linear relationships between the variables is to transform the data according to some **basis funciton**.  The main idea is to take the multidimension linear model:

$$y=a_0+a_1x_1+a_2x_2+a_3x_3+...+a_nx_n$$

Now we let $$x_n=f_n(x)$$ where $$f_n()$$ is some transformation function.

For instance let $$f_n(x)=x^n$$, the our new model becomes a polynomial regression of the form:

$$y=a_0+a_1x+a_2x^2+a_3x^3+...+a_nx^n$$

Notice that this is still a linear regression because the coefficients $a_0 - a_n$ never multiple or divide one another, rather they are added.  The basic operation above effectively takes 1D **x** values and projected them into a higher dimension, so that a linear fit can fir more complicated relationships between **x** and **y**.

#### Gaussian Basis Functions
Polynomials are **global** basis functions, each affecting the prediction over the whole input space.  Sometimes, **local** basis functions are more appropriate. One example is using functions proportional to Gaussian probability density:

$$\phi_j(x) = exp(\frac{-(x-\mu_j)^2}{2s^2})$$

Like the polynomial basis function we can also do a sum of Gaussian bases.  Where s is the spacing between each Gaussian basis function.

### Regularization
Sometimes, though having many basis functions or polynomials can lead to more flexibility in the model.  The model quickly leads to over-fitting when this happens.  The reason is that the coefficients of adjacent basis functions blow up and cancel each other out.  We need to limit such spike explicitly in the model by penalizing large values of the model parameters.  This introduction of penalty is called **regularization**.


##### Ridge Regression (L2 Regularization)
This regularization penalizes the sum of squares (2-norms) of the model coefficients.

$$P = \alpha\sum_{N}^{n=1}\theta^2_n$$

here $$\alpha$$ is a free parameter that controls the strength of the penalty. You can think of this as controlling the complexity of the resulting model.  In the$$\lim_{\alpha\to 0}$$, we recover the standard linear regression results.  While the $$\lim_{\alpha\to\infty}$$ all model responses will be suppressed.

##### Lasso Regression (L1 Regularization)
This regularization penalizes the sum of absolute values (1-norms) of the model coefficients.

$$P = \alpha\sum_{N}^{n=1}|\theta_n|$$

This type of regularization favours **sparse models** where possible, where it preferentially sets model coefficients to exactly zero.  With the lasso regression penalty, the majority of the coefficients are exactly zero, with the functional behavior being modeled by a small subset of the available basis functions.

## Gradient Decent
### Inser notes here

Notes:
- sensitivity of initialization
- may stay at saddle or local minimas
- step size problems
	- too large of a step size increases the time of convergence because may jump back and forth around the minima
	- too small step of a step size increases the time of convergence because the steps towards the minima are too small
	- some ways in practice to improve step size is to:
		- change it linearly by the iteration
		- Newton's method: look at the second derivative to identify the local curvature of the function and decide of how big or small a step to take in a particular direction

### Stochastic / Online Gradient Descent
The classic gradient decent breaks down to taking the sum squared errors of the residual and update based on the weights of each data point.  For stochastic gradient decent we chose a point at random and use that point to update the gradient $\nabla J$.  In practice you do some sort of random ordering of the data and go through this ordering sequentially updating the parameter $\beta$.  This has the property that on average over the data points the optima $E[\nabla J_n(\beta)] = \nabla J_n(\beta) = 0$

Pros:
- Lots of data = many more updates per pass
- computationally faster especially at the beginning where the error is large.  After only a few passes the updates become significant to reduce the error because the decision plane will move closer to the data cluster in space.
Cons:
- no longer strictly "descent" 
	- harder to debug
	- harder to asses convergence
	- stopping condition may be harder to evaluate
Remedy:
- Mini-batch Updates


**Ref**
- [In Depth: Linear Regression](https://jakevdp.github.io/PythonDataScienceHandbook/05.06-linear-regression.html)
- [Machine Learning and Big Date](http://www.kareemalkaseer.com/books/ml/linear-regression-intro)
- [Think Stats: Probability and Statistics for Programmers](http://greenteapress.com/thinkstats/thinkstats.pdf)
- [Applied Data Science](https://columbia-applied-data-science.github.io/appdatasci.pdf)
- [Modeling Data with Linear Combinations of Basis Functions](http://www.utstat.utoronto.ca/~radford/sta414.S11/week1b.pdf)
- [Linear regression (2): Gradient descent](https://www.youtube.com/watch?v=WnqQrPNYz5Q)
- [Gradient Descent step by step](https://www.youtube.com/watch?v=sDv4f4s2SB8)