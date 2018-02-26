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
Suppose you are the lottery fairy in a weekly lottery, where $6$ unique numbers out of 49 numbers are drawn.

`@instructions`

- Draw the winning numbers for this week.

`@hint`

- You can use the function `sample()` to draw random numbers.
- The set of elements is $\\{1,...,49\\}$.
- You can specify the numbers to draw via the argument `size`.

`@sample_code`
```{r}
# Draw the winning numbers for this week

```

`@solution`
```{r}
# Draw the winning numbers for this week
sample(1:49, size = 6)
```

`@sct`
```{r}

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
test_function('integrate', args = c('f', 'lower', 'upper'), eval = F)
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
variance <- integrate(VAR, 0, Inf)$value - expected_value^2
```

`@sct`
```{r}
test_function_definition("ex",
                         function_test = {
                           test_expression_result("EV(1)")
                           test_expression_result("EV(4)")
                           test_expression_result("EV(10)")
                           test_expression_result("EV(100)")
                         })
test_function('integrate', args = c('ex', 'lower', 'upper')) 
test_object('expected_value')
test_function_definition("ex2",
                         function_test = {
                           test_expression_result("VAR(1)")
                           test_expression_result("VAR(4)")
                           test_expression_result("VAR(10)")
                           test_expression_result("VAR(100)")
                         })
test_function('integrate', args = c('ex2', 'lower', 'upper'))
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

- Compute $P(-1.96\leq Z\leq 1.96)$ by using the function `pnorm()`.

`@hint`

- Probabilities of the form $P(a\leq Z\leq b)$ can be computed as $P(Z\leq b)-P(Z\leq a)$. Alternatively you can exploit the symmetry of the standard normal pdf.


`@sample_code`
```{r}
# Compute the probability


```

`@solution`
```{r}
# Compute the probability
pnorm(1.96)-pnorm(-1.96)

```

`@sct`
```{r}
test_function_result('pnorm')
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
## Normal distribution II

```yaml
type: NormalExercise
key: ffe8c2a318
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
## Chi-squared distribution I

```yaml
type: NormalExercise
key: 5152d9a665
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

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# Compute the probability

```

`@solution`
```{r}
# Compute the probability
1-pchisq(10/15, df = 2)
```

`@sct`
```{r}
test_output_contains("1-pchisq(10/15, df = 2)", times = 1, incorrect_msg = "Not correct!)
```

---
## Student t distribution

```yaml
type: NormalExercise
key: d8de148eff
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
## F distribution

```yaml
type: NormalExercise
key: 300c006a17
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
