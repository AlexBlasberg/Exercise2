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

Let $Y\sim\mathcal{N}(0,10)$. In this exercise we want to illustrate the result that the sample mean

$$\hat{\mu}\_Y=\sum\limits\_{i=1}^{100}a\_iY\_i$$ with equal weighting scheme $a\_i=\frac{1}{100}$ for $i=1,...,100$ is the best linear unbiased estimator (BLUE) of $\mu\_Y$. 

As an alternative consider the estimator $\tilde{Y}$ with unequal weighting scheme

$$$$a weighting scheme giving the first 50 observations $w\_i=\frac{15}{1000}$ for $i=1,...,100$ and

`@instructions`

- Verify that the alternative estimator $\tilde{Y}$ is unbiased as well.
- Define the alternative estimator as a function `Y_tilde()`.


`@hint`

- In order to be an unbiased estimator all weights have to sum up to 1.
- 

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# Verify that the alternative estimator is unbiased
w <- c(rep((1+0.5)/100, 50), rep((1-0.5)/100, 50))


# Define the alternative estimator Y_tilde


# 
```

`@solution`
```{r}

```

`@sct`
```{r}

```

---
## Hypothesis Test - One sample t-test

```yaml
type: NormalExercise
key: e37112756b
lang: r
xp: 100
skills: 1
```


`@instructions`

`@hint`

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}

```

`@solution`
```{r}

```

`@sct`
```{r}

```

---
## Hypothesis Test - Two sample t-test

```yaml
type: NormalExercise
key: cb2df0f522
lang: r
xp: 100
skills: 1
```


`@instructions`

- Test the null using a two sample t-test.

`@hint`

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}

```

`@solution`
```{r}

```

`@sct`
```{r}

```

---
## (Co)variance and Correlation I

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
## (Co)variance and Correlation II

```yaml
type: NormalExercise
key: 260ed038f1
lang: r
xp: 100
skills: 1
```

Once the session has initialized you will see the plot of $Y$ against $X$.

`@instructions`

- Compute the correlation between $X$ and $Y$. 

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
# Compute the correlation between x and y


```

`@solution`
```{r}
# Compute the correlation between x and y
cor(X, Y)

```

`@sct`
```{r}
test_function_result("cor")
success_msg('Correct! The correlation can only measure linear dependencies. However the dependency is clearly nonlinear (exponential).')
```
