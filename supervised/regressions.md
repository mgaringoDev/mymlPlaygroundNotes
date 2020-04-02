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
Linear regression models are a good starting point for regression tasks. Such models are popular because they can be fit very quickly, and are very interpretable. You are probably familiar with the simplest form of a linear regression model (i.e., fitting a straight line to data) but such models can be extended to model more complicated data behavior.  For simple linear regression there is, in fact, an optimal solution, however for high dimensional spaces there are none and we need to regard the problem as an optimisation problem. Regression fits a function to the data set, so what we are trying to do is to find a representative function and fit to our data set. Learning takes place as finding the best possible - local optimum - values of the function parameters. Linearity refer to the fact that we are tying to fit either a straight line or a polynomial function (polynomial regression).

### Linear Regression
The model is a straight line in the form $$y=mx+b$$.  We can use **sklearn.linear_model** module to obtain the m and b parameters given list of points [x,y].  The slope and intercept of the data are contained in the model's fit parameters, which in Scikit-Learn are always marked by a trailing underscore. Here the relevant parameters are **coef_** and **intercept_** of the model.

#### Polynomial Basis Function 
One way to adapt linear regression to non-linear relationships between the variables is to transform the data according to some **basis funciton**.  The main idea is to take the multidimension linear model:

$$y=a_0+a_1x_1+a_2x_2+a_3x_3+...+a_nx_n$$

Now we let $$x_n=f_n(x)$$ where $$f_n()$$ is some transformation function.

For instance let $$f_n(x)=x^n$$, the our new model becomes a polynomial regression of the form:

$$y=a_0+a_1x+a_2x^2+a_3x^3+...+a_nx^n$$

Notice that this is still a linear regression because the coefficients $a_0 - a_n$ never multiple or divide one another, rather they are added.  The basic operation above effectively takes 1D **x** values and projected them into a higher dimension, so that a linear fit can fir more complicated relationships between **x** and **y**.

#### Gaussian Basis Functions
Polynomials are **global** basis functions, each affecting the prediction over the whole input space.  Sometimes, **local** basis fucntions are more approriate. One example is using functions proportional to Gaussian probability density:

$$\phi_j(x) = exp(\frac{-(x-\mu_j)^2}{2s^2})$$

Like the polynomial basis function we can also do a sum of Gaussian bases.  Where s is the spacing between each gaussian basis function.

### Regularization
Sometimes, though having many basis functions or polynomials can lead to more flexibiilty in the model.  The model quickly leads to over-fitting when this happens.  The reason is that the coefficients of adjacent basis functions blow up and cancel each other out.  We need to limit such spike explictly in the model by penalizing large values of the model parameters.  This introduction of penalty is called **regularization**.


##### Ridge Regression (L2 Regularization)
This regularization penalizes the sum of squares (2-norms) of the model coefficients.

$$P = \alpha\sum_{N}^{n=1}\theta^2_n$$

here $$\alpha$$ is a free parameter that controls the strngth of the penalty. You can think of this as controlling the complexity of the resulting modle.  In the$$\lim_{\alpha\to 0}$$, we recover the standard linear regresion results.  While the $$\lim_{\alpha\to\infty}$$ all model responses will be suppressed.

##### Lasso Regression (L1 Regularization)
This regularization penalizes the sum of absolute values (1-norms) of the model coefficients.

$$P = \alpha\sum_{N}^{n=1}|\theta_n|$$

This type of regularization favours **sparse models** where possible, where it preferentially sets moel coefficients to exactly zero.  With the lasso regression penalty, the majority of the coefficients are exactly zero, with the functional behavior being modeled by a small subset of the available basis functions.


**Ref**
- [In Depth: Linear Regression](https://jakevdp.github.io/PythonDataScienceHandbook/05.06-linear-regression.html)
- [Machine Learning and Big Date](http://www.kareemalkaseer.com/books/ml/linear-regression-intro)
- [Think Stats: Probability and Statistics for Programmers](http://greenteapress.com/thinkstats/thinkstats.pdf)
- [Applied Data Science](https://columbia-applied-data-science.github.io/appdatasci.pdf)
- [Modeling Data with Linear Combinations of Basis Functions](http://www.utstat.utoronto.ca/~radford/sta414.S11/week1b.pdf)