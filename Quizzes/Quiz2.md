Ryan Tillis - Data Science - Regression Models - Quiz 2 - Coursera
================
<a href="http://www.ryantillis.com"> Ryan Tillis </a>
August 4, 2016

Quiz 2
------

This is Quiz 2 from Coursera's Regression Models class within the Data Science Specialization. This publication is intended as a learning resource, all answers are documented and explained. Datasets are available in R packages.

<hr>
<font size="+2">**1.** </font>Consider the following data with x as the predictor and y as as the outcome.

``` r
x <- c(0.61, 0.93, 0.83, 0.35, 0.54, 0.16, 0.91, 0.62, 0.62)
y <- c(0.67, 0.84, 0.6, 0.18, 0.85, 0.47, 1.1, 0.65, 0.36)
```

Give a P-value for the two sided hypothesis test of whether β1 from a linear regression model is 0 or not.

<hr>
-   <font size="+1">**0.05296**</font>

<hr>
##### Explanation:

P-value on beta1 coefficient given by summary of the linear model

``` r
x <- c(0.61, 0.93, 0.83, 0.35, 0.54, 0.16, 0.91, 0.62, 0.62)
y <- c(0.67, 0.84, 0.6, 0.18, 0.85, 0.47, 1.1, 0.65, 0.36)

summary(lm(y~x))$coef[8]
```

    ## [1] 0.05296439

<hr>
<font size="+2">**2.** </font> Consider the previous problem, give the estimate of the residual standard deviation.

<hr>
-   <font size="+1">**0.223 **</font>

<hr>
##### Explanation:

Residual standard deviation is given by the square roote of the sum of the squared residuals of degrees of freedom.

``` r
sum(resid(lm(y~x))^2)
```

    ## [1] 0.348097

``` r
sqrt(sum(resid(lm(y~x))^2))
```

    ## [1] 0.5899974

``` r
sqrt(sum(resid(lm(y~x))^2)/7)
```

    ## [1] 0.2229981

<hr>
<font size="+2">3. </font> In the 𝚖𝚝𝚌𝚊𝚛𝚜 data set, fit a linear regression model of weight (predictor) on mpg (outcome). Get a 95% confidence interval for the expected mpg at the average weight. What is the lower endpoint?

<hr>
-   <font size="+1">**18.991**</font>

<hr>
##### Explanation:

Predicting with the lower and upper bounds of the confidence intervals

``` r
dat <- mean(mtcars$wt)
fit <- lm(mpg~wt,mtcars)

predict(fit, data.frame(wt = dat), interval = "confidence")
```

    ##        fit      lwr      upr
    ## 1 20.09062 18.99098 21.19027

<hr>
<font size="+2">**4.** </font> Refer to the previous question. Read the help file for 𝚖𝚝𝚌𝚊𝚛𝚜. What is the weight coefficient interpreted as?

<hr>
-   <font size="+1">**The estimated expected change in mpg per 1,000 lb increase in weight.**</font>

<hr>
##### Explanation:

Mtcars reports the weight in units of 1000 lbs. \[, 6\] wt Weight (1000 lbs)

<hr>
<font size="+2">5. </font> Consider again the 𝚖𝚝𝚌𝚊𝚛𝚜 data set and a linear regression model with mpg as predicted by weight (1,000 lbs). A new car is coming weighing 3000 pounds. Construct a 95% prediction interval for its mpg. What is the upper endpoint?

<hr>
-   <font size="+1">**27.57**</font>

<hr>
##### Explanation:

Using same fit, changing predictor to 3 (in 1000lbs units).

``` r
predict(fit, data.frame(wt = 3.0), interval = "prediction")
```

    ##        fit      lwr      upr
    ## 1 21.25171 14.92987 27.57355

<hr>
<font size="+2">**6.** </font> Consider again the 𝚖𝚝𝚌𝚊𝚛𝚜 data set and a linear regression model with mpg as predicted by weight (in 1,000 lbs). A “short” ton is defined as 2,000 lbs. Construct a 95% confidence interval for the expected change in mpg per 1 short ton increase in weight. Give the lower endpoint.

<hr>
-   <font size="+1">**-12.973**</font>

<hr>
##### Explanation:

Multiplying the estimated change per 1000lbs (beta coef) by 2 and adding the error term\*2.

``` r
summary(fit)$coef[2]*2+2*c(-1,1)*qt(.975,30)*summary(fit)$coef[4]
```

    ## [1] -12.97262  -8.40527

<hr>
<font size="+2">**7.** </font> If my X from a linear regression is measured in centimeters and I convert it to meters what would happen to the slope coefficient?

<hr>
-   <font size="+1">**It would get multiplied by 100.**</font>

<hr>
##### Explanation:

The slope coefficient represents the change in the outcome per unit change in regressor. (outcome/regressor) So if you divide the regressor (m -&gt; cm) you are effectively multiplying the outcome by shrinking the units. If you multiply the regressor it will have the opposite effect. The actual change is not effected, only how it is expressed relative to the units of the regressor.

<hr>
<font size="+2">**8.** </font> I have an outcome, Y, and a predictor, X and fit a linear regression model with Y=β0+β1X+ϵ to obtain β^0 and β^1. What would be the consequence to the subsequent slope and intercept if I were to refit the model with a new regressor, X+c for some constant, c?

<hr>
-   <font size="+1">**The new intercept would be β<sup>0−cβ</sup>1**</font>

<hr>
##### Explanation:

This is a consequence of the least squares criteria.

<hr>
<font size="+2">**9.** </font> Refer back to the mtcars data set with mpg as an outcome and weight (wt) as the predictor. About what is the ratio of the the sum of the squared errors, ∑ni=1(Yi−Y^i)2 when comparing a model with just an intercept (denominator) to the model with the intercept and slope (numerator)?

<hr>
-   <font size="+1">**0.25**</font>

<hr>
##### Explanation:

Fitting a model with just an intercept will always predict at the mean.

``` r
fit2 <- lm(mpg ~ 1,mtcars)
fit <- lm(mpg~wt,mtcars)

sum((predict(fit)-mtcars$mpg)^2)/sum((predict(fit2)-mtcars$mpg)^2)
```

    ## [1] 0.2471672

<hr>
<font size="+2">**10.** </font> Do the residuals always have to sum to 0 in linear regression?

<hr>
-   <font size="+1">**If an intercept is included, then they will sum to 0.**</font>

<hr>
##### Explanation:

Least squares effectively minimizes the sum of the squared residuals. By not including an intercept, the mean of x times beta MUST equal the mean of y. This effectively weights the coefficients so that the line passes through zero.

<hr>
Check out my website at: <http://www.ryantillis.com/>
