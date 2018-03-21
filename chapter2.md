---
title       : Review of Statistics
description : Insert the chapter description here
---
## Biased ...

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
## ... but consistent estimator

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
## Efficiency of an estimator

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
