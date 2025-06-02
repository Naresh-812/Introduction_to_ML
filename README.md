# Introduction_to_ML
1. What is Linear Regression?
The model assumes that the relationship between the input (x) and the output (y) is
linear — that means it can be drawn as a straight line.
4.2.3 Gradient Descent Method
From Statistics to Machine Learning
Gradient Descent is a powerful tool used in many machine learning algorithms, especially
in linear regression and neural networks. But where does it come from?
A Statistical Origin: Minimizing Error
Let’s say we have a simple linear model:
ˆy = b0 + b1x
Our goal is to find the best values of b0 and b1 such that our predicted values ˆy are
as close as possible to the actual y values. One common way to measure this difference
is using the Sum of Squared Errors (SSE):
J(b0, b1) =
nX
i=1
(yi − ˆyi)2 =
nX
i=1
(yi − b0 − b1xi)2
This cost function J comes directly from statistics. It tells us how ”wrong” our
predictions are. We want to find the parameters b0 and b1 that minimize this function.
