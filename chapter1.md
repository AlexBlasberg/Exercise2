---
title       : Probability Theory
description : Insert the chapter description here
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

---
## Sample space

```yaml
type: MultipleChoiceExercise
lang: r
xp: 50
skills: 1
key: cfac5af27c
```

Two coins (H = heads, T = tails) are tossed. What is the sample space $\Omega$ of this random experiment?

`@instructions`

- $\\{H,T\\}$
- $\\{HH,HT,TH,TT\\}$
- There is no sample space available here.
- None of the above.

`@hint`

The sample space consists of all possible outcomes of a random variable.

`@sct`
```{r}
msg_bad <- "That is not correct!"
msg_success <- "Correct!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```
---
## Sampling

```yaml
type: NormalExercise
lang: r
xp: 100
skills: 1
key: 01cb7d9bb1
```
Suppose you are the lottery fairy in a weekly lottery, where $6$ out of $49$ unique numbers are drawn.

`@instructions`

- Draw the winning numbers for this week.

`@hint`

- You can use the function `sample()` to draw random numbers.
- The set of elements is $\\{1,...,49\\}$.
- You can specify the numbers to draw via the argument `size`.


`@sample_code`
```{r}
set.seed(123)
# Draw the winning numbers for this week


```

`@solution`
```{r}
set.seed(123)
# Draw the winning numbers for this week
sample(1:49, size = 6)

```

`@sct`
```{r}
test_output_contains("set.seed(123);sample(1:49, 6)")
```
---
## Probability density function

```yaml
type: NormalExercise
key: 0c7164ab11
lang: r
xp: 100
skills: 1
```

Consider a random variable $X$ with probability density function (pdf)

$$f\_X(x)=\frac{x}{4}e^{-\frac{x^2}{8}},\quad x\geq 0.$$


`@instructions`

- Define the pdf from above as a function `f()`. **Hint:** For the natural exponential function you can use `exp()`.
- Check whether the defined function is indeed a pdf.

`@hint`

- You can use `function()` to define a function.
- In order to be a pdf the integral of `f()` over the whole domain has to be equal to 1. That is, $\int\_0^\infty f\_X(x)dx=1$.
- `integrate()` performs integration in R and with `$value` you can access the numerical value of the computed integral.

`@sample_code`
```{r}
# Define the pdf


# Integrate f over the domain


```

`@solution`
```{r}
# Define the pdf
f <- function(x){x/4*exp(-x^2/8)}

# Integrate f over the domain
integrate(f, 0, Inf)$value
```

`@sct`
```{r}
test_function_definition("f",
                         function_test = {
                           test_expression_result("f(1)")
                           test_expression_result("f(4)")
                           test_expression_result("f(10)")
                           test_expression_result("f(100)")
                         })
test_function('integrate', args = c('f', 'lower', 'upper'), eval = c(F, T, T))
test_output_contains('1', incorrect_msg = 'Did you access the value of the integral?')
```
---
## Expected value and variance

```yaml
type: NormalExercise
key: abb753ed1e
lang: r
xp: 100
skills: 1
```

In this exercise we want to compute the expected value and variance of the random variable $X$ considered in the previous exercise. 

The pdf `f()` from the previous exercise is available in your working environment. 

`@instructions`

- Define a suitable function `ex()`.
- Compute the expected value of $X$. Store the result in `expected_value`.
- Define a suitable function `ex2()`.
- Compute the variance of $X$. Store the result in `variance`.

`@hint`

- The expected value of $X$ is defined as $\mathbb{E}[X]=\int\_0^\infty xf\_X(x)dx$.
- The value of an integral can be obtained via `$value`.
- The variance of $X$ is defined as $Var[X]=\mathbb{E}[X^2]-\mathbb{E}[X]^2$, where $\mathbb{E}[X^2]=\int\_0^\infty x^2f\_X(x)dx$.

`@pre_exercise_code`
```{r}
f <- function(x){(x/4)*exp(-x^2/8)}
```

`@sample_code`
```{r}
# Define the function ex


# Compute the expected value of X


# Define the function ex2


# Compute the variance of X


```

`@solution`
```{r}
# Define the function ex
ex <- function(x){x*f(x)}

# Compute the expected value of X
expected_value <- integrate(ex, 0, Inf)$value

# Define the function ex2
ex2 <- function(x){x^2*f(x)}

# Compute the variance of X
variance <- integrate(ex2, 0, Inf)$value - expected_value^2
```

`@sct`
```{r}
test_function_definition("ex",
                         function_test = {
                           test_expression_result("ex(1)")
                           test_expression_result("ex(4)")
                           test_expression_result("ex(10)")
                           test_expression_result("ex(100)")
                         })
test_function('integrate', args = c('f', 'lower', 'upper'), eval = c(F, T, T)) 
test_object('expected_value')
test_function_definition("ex2",
                         function_test = {
                           test_expression_result("ex2(1)")
                           test_expression_result("ex2(4)")
                           test_expression_result("ex2(10)")
                           test_expression_result("ex2(100)")
                         })
test_function('integrate', args = c('f', 'lower', 'upper'), eval = c(F, T, T))
test_object('variance')
```
---
## Standard normal distribution I

```yaml
type: NormalExercise
key: 54447b11cd
lang: r
xp: 100
skills: 1
```

Let $Z\sim\mathcal{N}(0, 1)$.

`@instructions`

- Compute $\phi(3)$, that is, the value of the standard normal density at $c=3$. 

`@hint`

- To compute values of $\phi(\cdot)$ you can use `dnorm()`.


`@sample_code`
```{r}
# Compute the value of the standard normal density at c=3


```

`@solution`
```{r}
# Compute the value of the standard normal density at c=3
dnorm(3)

```

`@sct`
```{r}
test_function_result('dnorm')
```
---
## Standard normal distribution II

```yaml
type: NormalExercise
key: 95f04b63f5
lang: r
xp: 100
skills: 1
```
Let $Z\sim\mathcal{N}(0, 1)$.

`@instructions`

- Compute $P(|Z|\leq 1.64)$ by using the function `pnorm()`.

`@hint`

- $P(|Z|\leq z)$ can be rewritten as $P(-z \leq Z \leq z)$.
- Probabilities of the form $P(a \leq Z \leq b)$ can be computed as $P(Z\leq b)-P(Z\leq a)=F(b)-F(a)$. Alternatively you can exploit the symmetry of the standard normal distribution.

`@sample_code`
```{r}
# Compute the probability


```

`@solution`
```{r}
# Compute the probability
pnorm(1.64)-pnorm(-1.64)

```

`@sct`
```{r}
test_function("pnorm")
test_output_contains("1 - 2*pnorm(-1.64)", incorrect_msg = "Not correct!")
```

---
## Normal distribution I

```yaml
type: NormalExercise
key: 6a2bd11c98
lang: r
xp: 100
skills: 1
```

Let $Y\sim\mathcal{N}(5, 25)$.

`@instructions`

- Compute the 99% quantile of the given distribution. That is, the value $y$ such that $\Phi(y)=0.99$.

`@hint`

- You can compute quantiles of the normal distribution using the function `qnorm()`.
- Besides the quantile you have to specify $\mu$ and $\sigma^2$. This can be done via the arguments `mean` and `sd`, however note that `sd` requires the standard deviation and **not** the variance.


`@sample_code`
```{r}
# Compute the 99% quantile of a normal distribution with mu = 5 and sigma^2 = 25.


```

`@solution`
```{r}
# Compute the 99% quantile of a normal distribution with mu = 5 and sigma^2 = 25.
qnorm(0.99, mean = 5, sd = sqrt(25))

```

`@sct`
```{r}
test_function_result('qnorm')
```
---
## Normal distribution II

```yaml
type: NormalExercise
key: ffe8c2a318
lang: r
xp: 100
skills: 1
```

Let $Y\sim\mathcal{N}(2, 12)$.

`@instructions`

- Generate 10 random numbers from this distribution.

`@hint`

- You can use `rnorm()` to draw random numbers from a normal distribution.
- Besides the number of draws you have to specify $\mu$ and $\sigma^2$. This can be done via the arguments `mean` and `sd`, however note that `sd` requires the standard deviation and **not** the variance.

`@sample_code`
```{r}
set.seed(123)
# Generate 10 random numbers from the given distribution.


```

`@solution`
```{r}
set.seed(123)
# Generate 10 random numbers from the given distribution.
rnorm(10, mean = 2, sd = sqrt(12))

```

`@sct`
```{r}
test_output_contains("set.seed(123);rnorm(10, mean = 2, sd = sqrt(12))")
```
---
## Chi-squared distribution I

```yaml
type: NormalExercise
key: 5152d9a665
lang: r
xp: 100
skills: 1
```

Let $W\sim\chi^2\_{10}$.

`@instructions`

- Plot the corresponding probability density function (pdf) using the function `curve()`. Specify the range of x-values as $[0,25]$ via the argument `xlim`.

`@hint`

- `curve()` expects the function with their respective parameter(s) (here: degrees of freedom `df`) as an argument.
- The range of x-values in `xlim` can be passed as a vector consisting of both endpoints.

`@sample_code`
```{r}
# Plot the pdf of a chi^2 random variable with df = 10


```

`@solution`
```{r}
# Plot the pdf of a chi^2 random variable with df = 10
curve(dchisq(x, df = 10), xlim = c(0, 25))

```

`@sct`
```{r}
test_function('curve', args = c('expr', 'xlim'), eval = c(NA, T))
test_student_typed('dchisq')
```
---
## Chi-squared distribution II

```yaml
type: NormalExercise
key: 3ff6a52c76
lang: r
xp: 100
skills: 1
```

Let $X\_1,X\_2$ be two independent normally distributed random variables with $\mu=0$ and $\sigma^2=15$.


`@instructions`

Compute $P(X\_1^2+X\_2^2>10)$.

`@hint`

- Note that both random variables are not $\mathcal{N}(0,1)$-distributed but $\mathcal{N}(0,\sigma^2)$. Hence you have to scale appropriately. Afterwards you can use `pchisq()` to compute the probability. 


`@sample_code`
```{r}
# Compute the probability


```

`@solution`
```{r}
# Compute the probability
pchisq(10/15, df = 2, lower.tail = F)

```

`@sct`
```{r}
test_output_contains('pchisq(10/15, df = 2, lower.tail = F)')
```
---
## Student t distribution I

```yaml
type: NormalExercise
key: d8de148eff
lang: r
xp: 100
skills: 1
```

Let $X\sim t\_{10000}$ and $Z\sim\mathcal{N}(0,1)$.

`@instructions`

- Compute the 95% quantile of both distributions. What do you note?

`@hint`

- You can use `qt()` and `qnorm()` to compute quantiles of the given distributions.
- For the t distribution you have to specify the degrees of freedom `df`.

`@sample_code`
```{r}
# Compute the 95% quantile of a t distribution with 10000 degrees of freedom


# Compute the 95% quantile of a standard normal distribution


```

`@solution`
```{r}
# Compute the 95% quantile of a t distribution with 10000 degrees of freedom
qt(0.95, df = 10000)

# Compute the 95% quantile of a standard normal distribution
qnorm(0.95)

# Both values are very close to each other. This is not surprising as for sufficient large degrees of freedom the t distribution can be approximated by the standard normal distribution.
```

`@sct`
```{r}
test_function_result('qt')
test_function_result('qnorm')
```


---
## Student t distribution II

```yaml
type: NormalExercise
key: 4cfe724955
lang: r
xp: 100
skills: 1
```

Let $X\sim t\_1$. Besides you can see the plot of the corresponding pdf.

`@instructions`

- Generate 1000 random numbers from this distribution and assign them to the variable `x`.
- Compute the sample mean of `x`. Can you explain the result? **Hint:** Focus in particular on the degree(s) of freedom.

`@hint`

- You can use `rt()` to draw random numbers from a t distribution.
- Note that the t distribution is fully parameterized through the degree(s) of freedom. Specify them via the argument `df`.
- To compute the sample mean of a vector you can use the function `mean()`.

`@pre_exercise_code`
```{r}
curve(dt(x, df = 1), xlim = c(-4, 4))
```

`@sample_code`
```{r}
set.seed(123)
# Generate 1000 random numbers from the given distribution. Assign them to the variable x.


# Compute the sample mean of x.


```

`@solution`
```{r}
set.seed(123)
# Generate 1000 random numbers from the given distribution. Assign them to the variable x.
x <- rt(1000, df = 1)

# Compute the sample mean of x.
mean(x)

# Although a t distribution with M = 1 is, as every other t distribution, symmetric around zero it actually has no expectation. This explains the highly non-zero value for the sample mean.
```

`@sct`
```{r}
test_object('x')
test_function_result('mean')
```

---
## F distribution I

```yaml
type: NormalExercise
key: 300c006a17
lang: r
xp: 100
skills: 1
```

Let $Y\sim F(10, 4)$.

`@instructions`

- Plot the quantile function of the given distribution using the function `curve()`.

`@hint`

- `curve()` expects the function with their respective parameters (here: degrees of freedom `df1` and `df2`) as an argument.

`@sample_code`
```{r}
# Plot the quantile function of the given distribution


```

`@solution`
```{r}
# Plot the quantile function of the given distribution
curve(qf(x, df1 = 10, df2 = 4))

```

`@sct`
```{r}
test_function('curve', args = 'expr', eval = NA)
test_student_typed('qf')
```

---
## F distribution II

```yaml
type: NormalExercise
key: 7312947efe
lang: r
xp: 100
skills: 1
```

Let $Y\sim F(4,5)$.

`@instructions`

- Compute $P(1<Y<10)$ by integration of the pdf.

`@hint`

- Besides the function that has to be integrated you have to specify lower and upper bounds.
- The additional parameters of the distribution (here `df1` and `df2`) also have to be passed **inside** the `integrate()` function.
- The value of the integral can be obtained via `$value`.

`@sample_code`
```{r}
# Compute the probability by integration


```

`@solution`
```{r}
# Compute the probability by integration
integrate(df, lower = 1, upper = 10, df1 = 4, df2 = 5)$value

```

`@sct`
```{r}
test_function('integrate', args = c('f', 'lower', 'upper', 'df1', 'df2'))
test_output_contains('integrate(df, lower = 1, upper = 10, df1 = 4, df2 = 5)$value')
```

---
## 

```yaml
type: NormalExercise
key: 63b40e5241
lang: r
xp: 100
skills: 1
```

In this exercise we want to v

`@instructions`

- Compute $P(1<Y<10)$ by integration of the pdf.

`@hint`

- Besides the function that has to be integrated you have to specify lower and upper bounds.
- The additional parameters of the distribution (here `df1` and `df2`) also have to be passed **inside** the `integrate()` function.
- The value of the integral can be obtained via `$value`.

`@sample_code`
```{r}
# Compute the probability by integration


```

`@solution`
```{r}
# Compute the probability by integration
integrate(df, lower = 1, upper = 10, df1 = 4, df2 = 5)$value

```

`@sct`
```{r}
test_function('integrate', args = c('f', 'lower', 'upper', 'df1', 'df2'))
test_output_contains('integrate(df, lower = 1, upper = 10, df1 = 4, df2 = 5)$value')
```