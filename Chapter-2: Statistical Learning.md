# What is Statistical Learning?

## The relationship
The relationship between dependent and independent variables can be written as:

Y = f(X) + e

Imagine X as matrix or a dataframe with all the vectors/columns of pridictor variables. Imagine Y as a vector/column. 

We predict Y using 

Y' = f'(X)

Where Y' is the resulting prediction of Y. 
f' is our estimator of f (actual relationship)

The accuracy of Y' as a prediction for Y depends on two quantities,
which we will call the reducible error and the irreducible error. 

the **reducible error** comes from f'. We can reduce the error by using most appropreate statistical learning technique. 

Even if we use the perfect fuction for f, we still end up with the **irreducible error** which comes from the other independent variables which are not included in the model. It is important to keep in mind that the
irreducible error will always provide an upper bound on the accuracy of
our prediction for Y . This bound is almost always unknown in practice.

## Inference and prediction
There are two types of problem we have, inference and prediction.

When our goal is understand the association between the Y and X rather than the accuracy Y, that is called inference problem and vice versa is prediction problem. 

Prediction: When the aim is to accurately predict the response for 'future'/'OOS' observations.
Inference: When the aim is to understand the relationship between the response and the predictors using 'given sample'.

Depending on whether our ultimate goal is prediction, inference, or a combination of the two, different methods for estimating f may be appropriate.
For example, linear models allow for relatively simple and interpretable inference, but may not yield as accurate predictions as some other approaches. In contrast, some of the highly non-linear approaches that we discuss in the later chapters of this book can potentially provide quite accurate predictions for Y , but this comes at the expense of a less
interpretable model for which inference is more challenging. 

## Estimating f
Our goal is to apply a statistical learning method to the training data in order to estimate the unknown function f.

most statistical learning methods for this task can be characterized as either parametric or non-parametric.

### Parametric methods
Parametric methods involve a two-step model-based approach.

First, we make an assumption about the functional form, or shape,of f, such as linear form.
After a model has been selected, we need a procedure that uses the training data to fit or train the model, such as Orinary Least Squares.

If the chosen model is too far from the true f, then our estimate will be poor. We can try to address this problem by choosing flexible models that can fit many different possible functional forms for f. But in general, fitting a more flexible model requires estimating a greater number of parameters. These more complex models can lead to a
phenomenon known as overfitting the data, which essentially means they follow the errors, or noise, too closely.
Over-fitting is an undesirable situation because the fit obtained will not yield accurate estimates of the response on new
observations that were not part of the original training data set.

### Non-Parametric Methods
Non-parametric methods do not make explicit assumptions about the functional form of f. Instead they seek an estimate of f that gets as close to the data points as possible without being too rough or wiggly.

By avoiding the assumption of a particular functional form for f, they have the potential to accurately fit a wider range of possible shapes for f.

But non-parametric approaches do suffer from a major disadvantage: since they do not reduce the problem of estimating f to a small number of parameters, a very large number of observations (far more than is typically needed for a parametric approach) is required in order to obtain an accurate estimate for f.

## The Trade-Off Between Prediction Accuracy and Model Interpretability
If we are mainly interested in inference, then restrictive models are much more interpretable. For instance, when inference is the goal, the linear model may be a good choice since it will be quite easy to understand the relationship between Y and X1,X2, . . . ,Xp. In contrast, very flexible approaches, such as the (non-parametric) splines and the boosting methods can
lead to such complicated estimates of f that it is difficult to understand how any individual predictor is associated with the response.

We have established that when inference is the goal, there are clear advantages to using simple and relatively inflexible statistical learning methods. In some settings, however, we are only interested in prediction, and the interpretability of the predictive model is simply not of interest. For instance, if we seek to develop an algorithm to predict the price of a
stock, our sole requirement for the algorithm is that it predict accurately - interpretability is not a concern. In this setting, we might expect that it will be best to use the most flexible model available. Surprisingly, this is not always the case! We will often obtain more accurate predictions using a less flexible method. This phenomenon, which may seem counterintuitive at first glance, has to do with the potential for overfitting in highly flexible methods.

## Supervised Versus Unsupervised Learning
Supervised learning problems will have a response variable to supervise our analysis. Whereas, no such resonse variable is available in unsupervised learning problems. Cluster analysis most common unsupervised leaning technique in which several distinguishable groups are identified based on clusters of observations of several valriables. 

## Regression Versus Classification Problems
We tend to refer to problems with a quantitative response as regression problems, while those involving a qualitative response are often referred to as classification problems.
Despite its name, logistic regression is a classification method. But since it estimates class probabilities, it can be thought of as a regression method as well.

# Assessing Model Accuracy
Model selection is most challenging part of the model buildng. We chose among all the studied methods based on cerain criteria such as model performance or accuracy. 

## Measuring the Quality of Fit
To measure how close the prediction are to the actuals on given data set on which the model is trained, we have sevaral metrics to measure. 

MSE (Mean Squared Error) is mean of squares of differences of actuals and predictions. Think about MSE as variance. 

MSE = ${\Sigma(y_i - f'(x_i))} \over {n}$

This is called training/in-sample MSE. in general, we do not really care how well the method works on the training data. Rather, we are interested in the accuracy of the pre-dictions that we obtain when we apply our method to previously unseen test data. So test/OOS MSE is what we really care about.

In most cases, traning MSE decreases with incease in model fexibility. However, test MSE decreases initially upto certain extent of flexibility but increaes after a thrshold is reached. When a given method yields a small training MSE but a large test MSE, we are said to be overfitting the data. This happens because our statistical learning procedure is working too hard to find patterns in the training data, and may be picking up some patterns that are just caused by random chance rather than by true properties of the unknown function f. When we overfit the training data, the test MSE will be very large because the supposed patterns that the method found in the training data simply don’t exist in the test data. Note that regardless of whether or not overfitting has occurred, we almost always expect the training MSE to be smaller than the test MSE because most statistical learning methods either directly or indirectly seek to minimize the training MSE.

When test data is not available, we use cross-validation, which is a method for estimating the test MSE using the training data.

## The Bias-Variance Trade-Off
In order to minimize the expected test error, we need to select a statistical learning method that simultaneously achieves
low variance and low bias. 

Variance refers to the amount by which f' would change if we estimated it using a different training data set. In general, more flexible statistical methods have higher variance.

bias refers to the error that is introduced by approximating a real-life problem, which may be extremely complicated, by a much simpler model. Generally, more flexible methods result in less bias.
For example, linear regression assumes that there is a linear relationship between Y and X1,X2, . . . ,Xp. It is unlikely that any real-life problem truly has such a simple linear relationship, and so performing linear
regression will undoubtedly result in some bias in the estimate of f.

As a general rule, as we use more flexible methods, the variance will increase and the bias will decrease. The relative rate of change of these two quantities determines whether the test MSE increases or decreases. As we increase the flexibility of a class of methods, the bias tends to initially decrease faster than the variance increases. Consequently, the expected test MSE declines. However, at some point increasing flexibility has little impact on the bias but starts to significantly increase the variance. When this happens the test MSE increases.

The relationship between bias, variance, and test set MSE is referred to as the bias-variance trade-off. 
Good test set performance of a statistical learning method requires low variance as well as low squared bias. This is referred to as a trade-off because it is easy to obtain a method with extremely low bias but high variance (for instance, by drawing a curve that passes through every single training observation) or a method with very low variance but high
bias (by fitting a horizontal line to the data). The challenge lies in finding a method for which both the variance and the squared bias are low.

In a real-life situation in which f is unobserved, it is generally not possible to explicitly compute the test MSE, bias, or variance for a statistical learning method. Nevertheless, one should always keep the bias-variance trade-off in mind.

## The Classification Setting
many of the concepts that we have encountered, such as the bias-variance trade-off, transfer over to the classification setting with only some modifications due to the fact that yi is no longer quantitative.

In classification problem, since the response variable is qualitative, we use 'error rate' to measure the model accuracy. 
The error rate is defined as the ratio of total mis-classified observations to the total observations (Confusion matrix is one way to show these).
