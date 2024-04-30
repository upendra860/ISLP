# Simple linear regression

y' = b0' + b1' x

where y' is the predicted value of actual y, b0' and b1' are estimated values of true b0 and b1.

y = y' + e

where e is the residual or error

y = b0' + b1' x + e

## Estimating the Coefficients

RSS (Residual Sum of Squares) = e1^2 + e2^2 ... en^2

where e = y - y' or ei = yi - yi'

RSS = (y1 - b0' - b1' x1)^2 + (y2 - b0' - b1' x2)^2 + .... (yn - b0' - b1' xn)^2

In least squares method, the objective function is to find the b0' and b1' such that RSS is minimum. 

y~ = sample mean of y

x~ = sample mean of x

## Assessing the Accuracy of the Coefficient Estimates
The analogy between linear regression and estimation of the mean of a random variable is an apt one based on the concept of bias. If we use the sample mean μ' to estimate μ, this estimate is unbiased, in the sense that on average, we expect μ' to equal μ.

if we could average a huge number of estimates of μ obtained from a huge number of sets of observations, then this average
would exactly equal μ. Hence, an unbiased estimator does not systematically over- or under-estimate the true parameter.

how accurate is the sample mean μ' as an estimate of μ? We have established that the average of μ'’s over many data sets will be very close to μ, but that a single estimate μ' may be a substantial underestimate or overestimate of μ.
How far off will that single estimate of μ' be? In general, we answer this question by computing the standard error of μ', written as SE(μ'). We have well-known formula

Var(μ') = SE(μ')^2 = segma^2/n

where segma is the standard deviation of each of the realizations yi of Y. Roughly speaking, the standard error tells us the average amount that this estimate μ' differs from the actual value of μ. Above Equation also tells us how this deviation shrinks with n—the more observations we have, the smaller the standard error of μ'. In a similar vein, we can wonder how close b0' and b1' are to the true values b0 and b1.

For the SE formulas to be strictly valid, we need to assume that the errors ei for each observation have common variance segma^2 and are uncorrelated. This is generally not true, but the formula still turns out to be a good approximation. Notice in the formula that SE(b1') is smaller when the xi are more spread out; intuitively we have more leverage to estimate a slope when this is the case. We also see that SE(b01) would be the same as SE(μ') if x~ were zero (in which case b0' would be equal to y~). 
In general, segma^2 is not known, but can be estimated from the data. This estimate of  is known as the residual standard error, and is given by the formula 

RSE = $\sqrt {RSS/(n-2)}$

Standard errors can be used to compute confidence intervals. A 95 % confidence confidence interval is defined as a range of values such that with 95% interval probability, the range will contain the true unknown value of the parameter.
The range is defined in terms of lower and upper limits computed from the sample of data. A 95% confidence interval has the following property:
if we take repeated samples and construct the confidence interval for each sample, 95% of the intervals will contain the true unknown value of the parameter. That is, there is approximately a 95 % chance that the interval will contain the true value of b1.

Example: In the case of the advertising data, the 95 % confidence interval for b0 is [6.130, 7.935] and the 95 % confidence interval for b1 is [0.042, 0.053]. Therefore, we can conclude that in the absence of any advertising, sales will, on average, fall somewhere between 6,130 and 7,935 units. Furthermore, for each 1,000 dollar increase in television advertising, there will be an average increase in sales of between 42 and 53 units.

As we can see, b0 same as 'mean' of y when x=0. whereas b1 is 'change' in y with unit change in x. 

Standard errors can also be used to perform hypothesis tests on coefficients. The most common hypothesis test involves testing the null hypothesis of 

H0 : There is no relationship between X and Y: b1=0
Ha : There is some relationship between X and Y : b1 != 0

To test the null hypothesis, we need to determine whether b1', our estimate for b1, is sufficiently far from zero that we can be confident that b1 is non-zero. How far is far enough? This of course depends on the accuracy of b1' — that is, it depends on SE(b1'). If SE(b1') is small, then even relatively small values of b1' may provide strong evidence that b1 != 0, and hence that there is a relationship between X and Y . In contrast, if SE(b1') is large, then b1' must be large in absolute value in order for us to reject the null hypothesis. In practice, we compute a t-statistic

t = (b1'-0)/SE(b1')

which measures the number of standard deviations that b1' is away from 0.

the probability of observing any number equal to |t| or larger in absolute value, assuming b1 = 0. We call this probability
the p-value. Therefore, if p-value is sufficiently small, we reject the null hypothesis and declare that there is association between Y and X.

||Coefficient| Std. error| t-statistic| p-value|
|-|-|-|-|-|
|Intercept| 7.0325| 0.4578| 15.36| < 0.0001|
|TV| 0.0475| 0.0027| 17.67| < 0.0001|

Above table provides details of the least squares model for the regression of number of units sold on TV advertising budget for the Advertising data.
Notice that the coefficients for b0' and b1' are very large relative to their standard errors, so the t-statistics are also large; the probabilities of seeing such values if H0 is true are virtually zero. Hence we can conclude that 
b0 != 0 and b1 != 0

## Assessing the Accuracy of the Model
Once we have rejected the null hypothesis in favor of the alternative hypothesis, it is natural to want to quantify the extent to which the model fits the data. The quality of a linear regression fit is typically assessed using two related quantities: 
the residual standard error (RSE) and 
the R2 statistic.

### Residual Standard Error
Due to the presence of error terms, even if we knew the true regression line (i.e. even if b0 and b1 were known), we would not be able to perfectly predict Y from X. 
The RSE is an estimate of the standard deviation of e. Roughly speaking, it is the average amount that the response
will deviate from the true regression line.

RSE = $\sqrt {RSS \over (n-2)}$

 = $\sqrt {\sum(yi - yi')^2 \over (n-2)}$
 
In the case of the advertising data, we see from the linear regression output that the RSE is 3.26. In other words, actual sales in each market deviate from the true regression line by approximately 3,260 units, on average. 
Another way to think about this is that even if the model were correct and the true values of the unknown coefficients b0
and b1 were known exactly, any prediction of sales on the basis of TV advertising would still be off by about 3,260 units on average. Of course, whether or not 3,260 units is an acceptable prediction error depends on the problem context. In the advertising data set, the mean value of sales over all markets is approximately 14,000 units, and so the percentage error is 3,260/14,000 = 23 %. 

If predictions are closure to actuals, then RSE is lesser, which means the model fits data well.

## R^2 Statistic
The RSE provides an absolute measure of lack of fit of the model to the data. But since it is measured in the units of Y , it is not always clear what constitutes a good RSE. The R2 statistic provides an alternative measure of fit. It takes the form of a proportion—the proportion of variance explained—and so it always takes on a value between 0 and 1, and is independent of the scale of Y.

R2 = (TSS − RSS) / TSS
 = 1− (RSS/TSS)
 
where TSS (total Sum of Squares) = $\sum(y_i - \bar y)^2 $

TSS measures the total variance in the response Y , and can be thought of as the amount of variability inherent in the response before the regression is performed. 
In contrast, RSS measures the amount of variability that is left unexplained after performing the regression. 
Hence, TSS−RSS measures the amount of variability in the response that is explained (or removed) by performing the regression, and R2 measures the proportion of variability in Y that can be explained using X.

A number near 0 indicates that the regression does not explain much of the variability in the response; this might occur
because the linear model is wrong, or the error variance segma^2 is high, or both.

The R2 statistic has an interpretational advantage over the RSE, since unlike the RSE, it always lies between 0 and 1. However, it can still be challenging to determine what is a good R2 value, and in general, this will depend on the application. For instance, in certain problems in physics, we may know that the data truly comes from a linear model with
a small residual error. In this case, we would expect to see an R2 value that is extremely close to 1, and a substantially smaller R2 value might indicate a serious problem with the experiment in which the data were generated. On the other hand, in typical applications in biology, psychology, marketing, and other domains, the linear model (3.5) is at best an extremely rough approximation to the data, and residual errors due to other unmeasured factors are often very large. In this setting, we would expect only a very small proportion of the variance in the response to be explained by the
predictor, and an R2 value well below 0.1 might be more realistic.

The R2 statistic is a measure of the linear relationship between X and Y. Whereas, also a measure of the linear relationship between X and Y. In simple linear regression setting, R2 = r2. In other words, the squared correlation
and the R2 statistic are identical. However, in multiple linear regression problem, in which we use several predictors simultaneously to predict the response. The concept of correlation between the predictors and the response does not extend automatically to this setting, since correlation quantifies the association between a single pair of variables rather than between a larger number of variables. We will see that R2 fills this role.

# Multiple Linear Regression
