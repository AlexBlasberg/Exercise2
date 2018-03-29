---
title       : Review of Statistics
description : Insert the chapter description here
---
## 1. Biased ...

```yaml
type: NormalExercise
key: 76c959aa9b
lang: r
xp: 100
skills: 1
```

Consider the following alternative estimator

$$\widetilde{Y}=\frac{1}{n-1}\sum\limits\_{i=1}^n Y\_i$$

In this exercise we want to illustrate that this estimator is in fact biased.

`@instructions`

- Define a function for the estimator by yourself and name it `Y_tilde`.
- Randomly draw 5 observations from the $\mathcal{N}(10, 25)$ distribution and compute an estimate with `Y_tilde()`. Repeat this procedure 10000 times and store the results in `est_biased`. 
- Plot a histogram of `est_biased`.
- Add a red vertical line at $\mu=10$ using the function `abline()`.

`@hint`

- To compute the sum of a vector you can use `sum()`, to get the length of a vector you can use `length()`.
- Use the function `replicate()` to compute repeatedly estimates of random samples. With the arguments `expr` and `n` you can specify the operation and how often it has to be replicated.
- A histogram can be plotted with the function `hist()`.
- The point on the x-axis as well as the color for the vertical line can be specified via the arguments `v` and `col`.

`@sample_code`
```{r}
# Define a function for the estimator


# Compute repeatedly estimates and store the results in est_biased
set.seed(123)


# Plot a histogram of est_biased


# Add a red vertical line at mu = 10

 
```

`@solution`
```{r}
# Define a function for the estimator
Y_tilde <- function(x){sum(x)/(length(x)-1)}

# Compute repeatedly estimates and store the results in est_biased
set.seed(123)
est_biased <- replicate(n = 10000, expr = Y_tilde(rnorm(5, 10, 5)))

# Plot a histogram of est_biased
hist(est_biased)

# Add a red vertical line at mu = 10
abline(v = 10, col = "red")

```

`@sct`
```{r}
test_function_definition('Y_tilde', function_test = {
                           test_expression_result("Y_tilde(1:10)")
                           test_expression_result("Y_tilde(1:25)")
                           test_expression_result("Y_tilde(seq(0, 1, 0.1))")
                         })
test_object('est_biased')
test_function('hist', args = 'x')
test_function('abline', args = c('v', 'col'))
success_msg('Correct! The estimator is biased.')
```

---
## 2. ... but consistent estimator

```yaml
type: NormalExercise
key: b75a7ad1f3
lang: r
xp: 100
skills: 1
```

Consider again the estimator from the previous exercise which is available in your environment as `Y_tilde()`.
Do the same procedure as in the previous exercise but now increase the number of observations to draw from 5 to 1000. What do you note? What can you say about this estimator?

`@instructions`

- Randomly draw 1000 observations from the $\mathcal{N}(10, 25)$ distribution and compute an estimate with `Y_tilde()`. Repeat this procedure 10000 times and store the results in `est_consistent`. 
- Plot a histogram of `est_consistent`.
- Add a red vertical line at $\mu=10$ using the function `abline()`.

`@hint`

- Use the function `replicate()` to compute repeatedly estimates of random samples. With the arguments `expr` and `n` you can specify the operation and how often it has to be replicated.
- A histogram can be plotted with the function `hist()`.
- The point on the x-axis as well as the color for the vertical line can be specified via the arguments `v` and `col`.

`@pre_exercise_code`
```{r}
Y_tilde <- function(x){sum(x)/(length(x)-1)}
```

`@sample_code`
```{r}
# Compute repeatedly estimates and store the results in est_consistent
set.seed(123)


# Plot a histogram of est_biased


# Add a red vertical line at mu = 10


```

`@solution`
```{r}
# Compute repeatedly estimates and store the results in est_consistent
set.seed(123)
est_consistent <- replicate(n = 10000, expr = Y_tilde(rnorm(1000, 10, 5)))

# Plot a histogram of est_consistent
hist(est_consistent)

# Add a red vertical line at mu = 10
abline(v = 10, col = "red")

```

`@sct`
```{r}
test_object('est_consistent')
test_function('hist', args = 'x')
test_function('abline', args = c('v', 'col'))
success_msg('Correct! Although biased the estimator is consistent.')
```

---
## 3. Efficiency of an estimator

```yaml
type: NormalExercise
key: ac77115a16
lang: r
xp: 100
skills: 1
```

In this exercise we want to illustrate the result that the sample mean

$$\hat{\mu}\_Y=\sum\limits\_{i=1}^{n}a\_iY\_i$$ with equal weighting scheme $a\_i=\frac{1}{n}$ for $i=1,...,n$ is the best linear unbiased estimator (BLUE) of $\mu\_Y$. 

As an alternative consider the estimator

$$\tilde{\mu}\_Y=\sum\limits\_{i=1}^{n}b\_iY\_i$$

where $b\_i$ gives the first $\frac{n}{2}$ observations a higher weighting than the second $\frac{n}{2}$ observations. 

The respective weighting vector is already defined and available as `w` in your working environment.

`@instructions`

- Verify that $\tilde{\mu}$ is unbiased.
- Define the alternative estimator as a function `mu_tilde()`.
- Randomly draw 100 observations from the $\mathcal{N}(5, 10)$ distribution and compute an estimate with both estimators. Repeat this procedure 10000 times and store the results in `est_bar` and `est_tilde`.
- Compute the sample variances of `est_bar` and `est_tilde`. What can you say about both estimators?

`@hint`

- In order to be an unbiased estimator all weights have to sum up to 1.
- Use the function `replicate()` to compute repeatedly estimates of random samples. With the arguments `expr` and `n` you can specify the operation and how often it has to be replicated.
- To compute sample variances you can use `var()`.

`@sample_code`
```{r}
# Verify that the alternative estimator is unbiased
n <- 100
w <- c(rep((1+0.5)/n, n/2), rep((1-0.5)/n, n/2))


# Define the alternative estimator mu_tilde


# Compute repeatedly estimates for both estimators and store the results in est_bar and est_tilde
set.seed(123)



# Compute the sample variances for est_bar and est_tilde



```

`@solution`
```{r}
# Verify that the alternative estimator is unbiased
n <- 100
w <- c(rep((1+0.5)/n, n/2), rep((1-0.5)/n, n/2))
sum(w)

# Define the alternative estimator mu_tilde
mu_tilde <- function(x){sum(w*x)}

# Compute repeatedly estimates for both estimators and store the results in est_bar and est_tilde
set.seed(123)
est_bar <- replicate(expr = mean(rnorm(100, 5, 10)), n = 10000)
est_tilde <- replicate(expr = mu_tilde(rnorm(100, 5, 10)), n = 10000)

# Compute the sample variances for est_bar and est_tilde
var(est_bar)
var(est_tilde)

```

`@sct`
```{r}
test_function_result('sum')
test_function_definition('mu_tilde',
                         function_test = {
                           test_expression_result("mu_tilde(1:100)")
                           test_expression_result("mu_tilde(2:101)")
                         })
test_object('est_bar')
test_object('est_tilde')
test_function_result('var', index = 1)
test_function_result('var', index = 2)
success_msg('Correct! The sample mean is more efficient (that is, has a lower variance) than the alternative estimator.')
```



---
## 4. Hypothesis test - t statistic

```yaml
type: NormalExercise
key: e37112756b
lang: r
xp: 100
skills: 1
```

Consider the CPS data set from Chapter 3.6 again which is available as `cps` in your working environment.

We suppose that the average hourly earnings (in prices of 2012) `ahe12` exceed 23.50 $\frac{\$}{h}$ and wish to test this hypothesis at a significance level of $\alpha=0.05$. For that reason please do the following:

`@instructions`

- Compute the test statistic by hand and assign it to `tstat`.
- Use `tstat` to accept or reject the null hypothesis. Please do so using the normal approximation. 

`@hint`

- We test $H\_0:\mu\_{Y\_{ahe}}\leq 23.5$ vs. $H\_1:\mu\_{Y\_{ahe}}>23.5$. That is, we conduct a right-sided test.
- The t statistic is defined as $\frac{\bar{Y}-\mu\_{Y,0}}{s\_{Y}/\sqrt{n}}$ where $s\_Y$ denotes the sample variance.
- To decide whether the null hypothesis is accepted or rejected you can compare the t statistic with the respective quantile of the standard normal distribution. Use logical operators to check for this.

`@pre_exercise_code`
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
```

`@sample_code`
```{r}
# Compute the t statistic by hand and assign it to tstat
 

# Use tstat to accept or reject the null


```

`@solution`
```{r}
# Compute the t statistic by hand and assign it to tstat
tstat <- (mean(cps$ahe12)-23.5)/(sd(cps$ahe12)/sqrt(length(cps$ahe12)))

# Use tstat to accept or reject the null
tstat > qnorm(0.95)

```

`@sct`
```{r}
test_object('tstat')
test_function_result('qnorm')
test_student_typed('tstat', times = 2)
test_or(test_output_contains('T'), test_output_contains('F'))
```


---
## 5. Hypothesis test - p-value

```yaml
type: NormalExercise
key: 485fd5f536
lang: r
xp: 100
skills: 1
```

Reconsider the test situation from previous exercise. `cps` as well as `tstat` are available in your working environment.

Instead of using the t statistic as decision criterion we can also use the respective p-value. For that reason please do the following:


`@instructions`

- Compute the p-value by hand and assign it to `pval`.
- Use `pval` to accept or reject the null hypothesis.

`@hint`

- The p-value for a right-sided test can be computed as $p=P(t>t^{act}|H\_0)$.
- We reject the null if $p<\alpha$. Use logical operators to check for this.

`@pre_exercise_code`
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
tstat <- (mean(cps$ahe12)-23.5)/(sd(cps$ahe12)/sqrt(length(cps$ahe12)))
```

`@sample_code`
```{r}
# Compute the p-value by hand and assign it to pval


# Use pval to accept or reject the null


```

`@solution`
```{r}
# Compute the p-value by hand and assign it to pval
pval <- 1-pnorm(tstat)

# Use pval to accept or reject the null
pval < 0.05

```

`@sct`
```{r}
test_object('pval')
test_student_typed('pval', times = 2)
test_or(test_output_contains('T'), test_output_contains('F'))
```

---
## 6. Hypothesis test - one sample t-test

```yaml
type: NormalExercise
key: 3f74f18146
lang: r
xp: 100
skills: 1
```

In the last two exercises we discovered two ways of conducting a hypothesis test. In practice these approaches seem very cumbersome and so R provides the function `t.test()` which does most of the work automatically for us. In fact it provides t statistics, p-values and even confidence intervals (more on the latter in later exercises). In addition it also uses the t instead of the normal distribution which becomes important especially for small sample sizes. 

The data set `cps` as well as the variable `pval` from Exercise 3.4 are available in your working environment.

`@instructions`

- Conduct the hypothesis test from previous exercises with the function `t.test()`.
- Extract the t statistic and p-value from the list created by `t.test()`. Assign them to the variables `tstat` and `pvalue`.
- Verify that using the normal approximation here is valid as well by computing the difference between both p-values.

`@hint`

- The type of the test as well as the null hypothesis can be specified via the arguments `alternative` and `mu`.
- t statistic and p-value can be obtained via `$statistic` and `$p.value`, respectively.

`@pre_exercise_code`
```{r}
cps <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = T, sep = ";")
tstat <- (mean(cps$ahe12)-23.5)/(sd(cps$ahe12)/sqrt(length(cps$ahe12)))
pval <- 1-pnorm(tstat)
```

`@sample_code`
```{r}
# Conduct the hypothesis test from previous exercises with t.test()


# Extract t statistic and p-value from list created by t.test()



# Verify that using the normal approximation here is valid as well


```

`@solution`
```{r}
# Conduct the hypothesis test from previous exercises with t.test()
t.test(cps$ahe12, alternative = "greater", mu = 23.5)

# Extract t statistic and p-value from list created by t.test()
tstat <- t.test(cps$ahe12, alternative = "greater", mu = 23.5)$statistic
pvalue <- t.test(cps$ahe12, alternative = "greater", mu = 23.5)$p.value

# Verify that using the normal approximation here is valid as well
pvalue - pval

```

`@sct`
```{r}
test_function_result('t.test')
test_object('tstat')
test_object('pvalue')
test_or(test_student_typed('pvalue - pval'), test_student_typed('pval - pvalue'))
```


---
## 7. Hypothesis Test - two sample t-test

```yaml
type: NormalExercise
key: cb2df0f522
lang: r
xp: 100
skills: 1
```

Consider the annual maximum sea levels at Port Pirie (Southern Australia) and Fremantle (Western Australia) for the last 30 years.

The observations are available in the variables `portpirie` and `fremantle` in your working environment.

`@instructions`

- Test whether there is a significant difference in the annual maximum sea levels at a significance level of $\alpha=0.05$.

`@hint`

- We test $H\_0:\mu\_{P}-\mu\_{F}=0$ vs. $H\_1:\mu\_{P}-\mu\_{F}\ne 0$. That is, we conduct a two sample t-test.
- For a two sample t-test `t.test()` expects two vectors containing the data.

`@pre_exercise_code`
```{r}
set.seed(123)
portpirie <- runif(30, 3.6, 4.6)
fremantle <- runif(30, 1.2, 1.8)
```

`@sample_code`
```{r}
# Conduct a two sample t-test


```

`@solution`
```{r}
# Conduct a two sample t-test
t.test(portpirie, fremantle)

```

`@sct`
```{r}
test_or(test_output_contains('t.test(portpirie, fremantle)'), test_output_contains('t.test(fremantle, portpirie)'))
```

---
## 8. Confidence interval

```yaml
type: NormalExercise
key: 0896ce3d5c
lang: r
xp: 100
skills: 1
```

Reconsider the test situation concerning the annual maximum sea levels at Port Pirie and Fremantle.

The variables `portpirie` and `fremantle` are again available in your working environment.

`@instructions`

- Construct a 95%-confidence interval for the difference in the sea levels using `t.test()`.

`@hint`

- The function `t.test()` computes by default a confidence interval which is accessible via `$conf.int`.

`@pre_exercise_code`
```{r}
set.seed(123)
portpirie <- runif(30, 3.6, 4.6)
fremantle <- runif(30, 1.2, 1.8)
```

`@sample_code`
```{r}
# Construct a confidence interval using t.test()


```

`@solution`
```{r}
# Construct a confidence interval using t.test()
t.test(portpirie, fremantle)$conf.int

```

`@sct`
```{r}
test_or(test_output_contains('t.test(portpirie, fremantle)$conf.int'), test_output_contains('t.test(fremantle, portpirie)$conf.int'))
```
---
## 9. (Co)variance and Correlation I

```yaml
type: NormalExercise
key: 3f55a664d3
lang: r
xp: 100
skills: 1
```

Consider a random sample $(X\_i, Y\_i)$ for $i=1,...,100$.

The respective vectors $X$ and $Y$ are already available in your working environment as `X` and `Y`.

`@instructions`

- Compute the variance of $X$ using the function `cov()`.
- Compute the covariance of $X$ and $Y$.
- Compute the correlation between $X$ and $Y$.

`@hint`

- The variance is just a special case of the covariance.
- `cov()` as well as `cor()` expect a vector for each variable.

`@pre_exercise_code`
```{r}
custom_seed(123)
X <- runif(100, 900, 1000)
Y <- 3*X+rnorm(100, 0, 100)
```

`@sample_code`
```{r}
# Compute the variance of X


# Compute the covariance of X and Y


# Compute the correlation between X and Y


```

`@solution`
```{r}
# Compute the variance of X with cov()
cov(X, X)

# Compute the covariance of X and Y
cov(X, Y)

# Compute the correlation between X and Y
cor(X, Y)

```

`@sct`
```{r}
test_function_result("cov", index = 1)
test_function_result("cov", index = 2)
test_function_result("cor")
```

---
## 10. (Co)variance and Correlation II

```yaml
type: NormalExercise
key: 260ed038f1
lang: r
xp: 100
skills: 1
```

In this exercise we want to examine the limitations of the correlation as a dependency measure. 

Once the session has initialized you will see the plot of 100 realizations from two random variables $X$ and $Y$.

The respective observations are available in the vectors `X` and `Y` in your working environment.

`@instructions`

- Compute the correlation between $X$ and $Y$. Interpret your result critically.

`@hint`

- `cor()` expects a vector for each variable.

`@pre_exercise_code`
```{r}
custom_seed(123)
X <- runif(100, 0, 3)
Y <- exp(-X) + rnorm(100, 0, .05)
plot(Y ~ X)
```

`@sample_code`
```{r}
# Compute the correlation between X and Y


```

`@solution`
```{r}
# Compute the correlation between x and y
cor(X, Y)
# The correlation is only able to quantify linear relationships which is not the case here.
```

`@sct`
```{r}
test_function_result("cor")
success_msg('Correct! The correlation is able to capture the negative relationship between both variables. However it only measures linear dependencies, whereas the dependency here is clearly nonlinear (exponential).')
```
