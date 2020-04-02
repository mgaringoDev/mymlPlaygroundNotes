---
layout: default
title: Linear Regression Implementatinos
nav_order: 3
---

### sklearn
We can use **sklearn.linear_model** module to obtain the m and b parameters given list of points [x,y].  The slope and intercept of the data are contained in the model's fit parameters, which in Scikit-Learn are always marked by a trailing underscore. Here the relevant parameters are **coef_** and **intercept_** of the model. 

The **LinearRegression** module can also fit in multidimensional linear models of the form $$y=a_0+a_1x_1+a_2x_2+...$$ where multiple $$x$$  values are geometrically the same as fitting a plane to 3D or fitting hyper-plane in higher dimensions.  Though higher dimensions are harder to visualize.

The **PolynomialFeatures** module is also in sklearn. Gaussian Basis Functions is not implemented in sklearn but is implemented in the jupyter notebook below.

Regularization is implemented in sklearn by importing the module **Ridge** from **sklearn.linear_model**.

[Jupyter notebook example](https://jakevdp.github.io/PythonDataScienceHandbook/05.06-linear-regression.html)

**Ref**
- [In Depth: Linear Regression](https://jakevdp.github.io/PythonDataScienceHandbook/05.06-linear-regression.html)
- [Machine Learning and Big Date](http://www.kareemalkaseer.com/books/ml/linear-regression-intro)
- [Think Stats: Probability and Statistics for Programmers](http://greenteapress.com/thinkstats/thinkstats.pdf)
- [Applied Data Science](https://columbia-applied-data-science.github.io/appdatasci.pdf)