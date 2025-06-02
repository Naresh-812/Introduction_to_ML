# Introduction_to_ML
4.2 What is Linear Regression?
The model assumes that the relationship between the input (x) and the output (y) is
linear — that means it can be drawn as a straight line.
Prediction (ˆy) = w · x + b
we have to find w and b
Where:
• w is the slope (how much y changes when x increases),
• b is the intercept (value of y when x = 0),
• x is the input (feature),
• ˆy is the predicted output.
26 Naresh Lankalapalli
Supervised Learning
Where Do We Use It?
• Predicting house prices based on area
• Estimating sales based on advertising budget
• Predicting student performance from study time
Think a Minute
How Do We Know If Our Model Is Good?
After making predictions, we need to check how good they are . We do this using
evaluation metrics.
1. Mean Absolute Error (MAE)
MAE = 1
n
nX
i=1
|yi − ˆyi|
It tells us: “On average, how far off are we?”
• Easy to understand
• Treats all errors equally
2. Mean Squared Error (MSE)
MSE = 1
n
nX
i=1
(yi − ˆyi)2
It penalizes bigger errors more than smaller ones (because of squaring).
3. Root Mean Squared Error (RMSE)
RMSE = √MSE
This is in the same units as the output, making it easier to interpret.
4. R-Squared (R2 Score)
R2 = 1 − SSres
SStot
Where:
27 Naresh Lankalapalli
Supervised Learning
SSres =
nX
i=1
(yi − ˆyi)2 (Residual Sum of Squares)
SStot =
nX
i=1
(yi − ¯y)2 (Total Sum of Squares)
This tells us how much of the variation in the data is explained by the model.
• R2 = 1 means perfect prediction
• R2 = 0 means model is no better than just guessing the average
Think a Minute
If your predictions are close to the actual values, which metric would show the
smallest value? Hint: MAE and RMSE are error values — smaller is better!
Least Squares — Best Fit Line from Math
To find this best line, we use the least squares method, which means:
MSE = 1
n
nX
i=1
(yi − ˆyi)2 = 1
n
nX
i=1
(yi − (b1xi + b0))2
where:
• yi: actual value,
• ˆyi = b1xi + b: predicted value,
• n: number of data points.
The optimal values of b1 and b0 are found by minimizing this error function, typically
using calculus or optimization techniques like gradient descent.
Think a Minute
Have you ever tried guessing someone’s marks based on how much they studied?
Congrats — you’ve already done a form of regression!
4.2.1 Math Behind Linear Regression from Scratch
Objective: We aim to find the best-fit line of the form y = b0 + b1x that minimizes the
total error between actual and predicted values.
28 Naresh Lankalapalli
Supervised Learning
Figure 4.2: Residual vs. actual value vs. predicted value in simple linear regression
Step 1: Residuals
Residual for each point:
εi = yi − (b0 + b1xi)
Sum of squared residuals:
Sr =
nX
i=1
ε2
i =
nX
i=1
(yi − b0 − b1xi)2
Step 2: Minimize the Error
To minimize Sr, take partial derivatives with respect to b0 and b1 and set them to zero.
With respect to b0: ∂Sr
∂b0
= −2 X(yi − b0 − b1xi)
With respect to b1: ∂Sr
∂b1
= −2 X xi(yi − b0 − b1xi)
Step 3: Solve the Equations
From ∂Sr
∂b0 = 0: X yi − nb0 − b1
X xi = 0 ⇒ b0 = ¯y − b1 ¯x
Substitute into the second derivative equation:
X xi(yi − b0 − b1xi) = 0 ⇒ X xi(yi − ¯y + b1 ¯x − b1xi) = 0
⇒ X xi(yi − ¯y) − b1
X xi(xi − ¯x) = 0
29 Naresh Lankalapalli
Supervised Learning
⇒ b1 =
P(xi − ¯x)(yi − ¯y)
P(xi − ¯x)2
Final Formulas
b1 =
P(xi − ¯x)(yi − ¯y)
P(xi − ¯x)2 , b0 = ¯y − b1 ¯x
Useful Identities
X(xi − ¯x)(yi − ¯y) = X xi(yi − ¯y) because X(yi − ¯y) = 0
X(yi − ¯y)2 = X yi(yi − ¯y) by same reason
Karl Pearson’s Coefficient of Correlation
Karl Pearson’s coefficient of correlation, denoted by r, measures the strength and di-
rection of the linear relationship between two variables .i.e measures the quality of
prediction . It is also known as the Product Moment Correlation Coefficient.
1. Formula (Using Deviations):
r =
P(xi − ¯x)(yi − ¯y)
pP(xi − ¯x)2 · P(yi − ¯y)2
2. Formula (Product Method / Raw Scores):
r = n P xiyi − P xi
P yi
p(n P x2
i − (P xi)2)(n P y2
i − (P yi)2)
30 Naresh Lankalapalli
Supervised Learning
3. Interpretation of r:
Value of r Interpretation
r = +1 Perfect positive correlation (x and y increase together exactly)
0.7 ≤ r < 1 Strong positive correlation
0.3 ≤ r < 0.7 Moderate positive correlation
0 < r < 0.3 Weak positive correlation
r = 0 No linear correlation
−0.3 < r < 0 Weak negative correlation
−0.7 < r ≤ −0.3 Moderate negative correlation
−1 < r ≤ −0.7 Strong negative correlation
r = −1 Perfect negative correlation (x increases, y decreases exactly)
4. Conditions for Using Pearson’s r:
• The data must be quantitative and continuous.
• The relationship between the variables should be linear.
• There should be no extreme outliers.
• Both variables should be approximately normally distributed.
Coefficient of Determination R2
The coefficient of determination R2 tells how much of the variance in Y is explained by
X through the regression:
R2 = r2
This means the proportion of variance explained by the regression model is exactly
the square of the correlation coefficient between X and Y .
—
Range:
0 ≤ R2 ≤ 1
where
• R2 = 0 means no variability explained by the model.
• R2 = 1 means perfect fit to the data.
31 Naresh Lankalapalli
Supervised Learning
Avoiding Extrapolation
What is Extrapolation?
Extrapolation is the process of making predictions outside the range of the observed
data used to build a model. For example, if the data for the independent variable X
covers values from 10 to 50, then predicting Y for X = 60 is extrapolation.
Significance of F-value and P-value in Regression
F-value: Overall Model Significance
The F-value is used in an F-test to evaluate the overall significance of a linear regression
model. It compares the model with no predictors (intercept-only model) against your full
model.
F = Explained Variance (Mean Square Regression)
Unexplained Variance (Mean Square Error)
• A high F-value means your model explains a lot more variation than what you’d
expect by chance.
• If the F-value is significantly greater than 1, the model is considered meaningful.
Think a Minute
Imagine you’re testing if studying time predicts exam scores. A high F-value means
studying actually explains the difference in scores across students.
P-value: Feature Significance
The P-value tests the null hypothesis that the coefficient (bi) of a variable is equal to
zero (i.e., no effect).
Null Hypothesis: H0 : bi = 0 vs Alternative Hypothesis: H1 : bi̸ = 0
• A low p-value (typically ≤ 0.05) indicates that you can reject the null hypothesis
— meaning the variable is statistically significant.
• A high p-value means the variable is likely not contributing much to the prediction.
Think a Minute
Suppose you’re predicting house prices. If the P-value for ”number of bathrooms”
is low, it’s a useful predictor. If it’s high, the model might do fine without it.
32 Naresh Lankalapalli
Supervised Learning
Example: Linear Regression by Hand
Given:
x = (95, 85, 80, 70, 60), y = (85, 95, 70, 65, 70)
First, calculate the means:
¯x = 95 + 85 + 80 + 70 + 60
5 = 78, ¯y = 85 + 95 + 70 + 65 + 70
5 = 77
x y x − ¯x y − ¯y (x − ¯x)(y − ¯y) (x − ¯x)2 (y − ¯y)2
95 85 17 8 136 289 64
85 95 7 18 126 49 324
80 70 2 -7 -14 4 49
70 65 -8 -12 96 64 144
60 70 -18 -7 126 324 49
Total 470 730 630
Now calculate the slope b1 and intercept b0:
b1 =
P(x − ¯x)(y − ¯y)
P(x − ¯x)2 = 470
730 ≈ 0.644
b0 = ¯y − b1 ¯x = 77 − (0.644 × 78) ≈ 77 − 50.23 = 26.77
y = 26.77 + 0.644x
This is the estimated regression line.
Correlation Coefficient and Coefficient of Determination
Step 3: Pearson Correlation Coefficient
r =
P(x − ¯x)(y − ¯y)
pP(x − ¯x)2 · P(y − ¯y)2 = 470
√730 · 630
r = 470
√459900 = 470
678.22 ≈ 0.693
Step 4: Coefficient of Determination
R2 = r2 = (0.693)2 ≈ 0.48
33 Naresh Lankalapalli
Supervised Learning
Interpretation: The correlation coefficient r ≈ 0.693 indicates a moderate positive
relationship between x and y. The coefficient of determination R2 ≈ 0.48 suggests that
about 48% of the variability in y can be explained by the linear relationship with x.
