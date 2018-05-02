---
title       : Hypothesis Tests and Confidence Intervals in Multiple Regression
description : Insert the chapter description here
---
## Hypothesis Testing in a Multiple Regression Model - t statistics and p values

```yaml
type: NormalExercise
key: c80d99676b
lang: r
xp: 100
skills: 1
```

Reconsider the `Boston` data set and the following estimated model from the previous chapter:

$$\widehat{medv}\_i = \underset{(0.74)}{32.828} \underset{(0.08)}{-0.994} \times lstat\_i \underset{(0.03)}{-0.083} \times crim\_i + \underset{(0.02)}{0.038} \times age\_i.$$

Just as in the simple linear regression framework we can conduct hypothesis tests for each coefficent in the multiple regression framework as well. To do so assume that we want to test the null $H\_0:\beta\_j=0$ against the alternative $H\_1:\beta\_j\ne 0$ for all $j$.

The packages `AER` and `MASS` have been loaded. The coefficients of the model as well as the corresponding standard errors are already available in `coef` and `se`, respectively.

`@instructions`

- Compute t statistics for each coefficient by using the predefined objects `coef` and `se`. Assign them to `tstat`.
- Compute p values for each coefficient and assign them to `pval`.
- Check with the help of logical operators whether the hypotheses are rejected at a 1% significance level.

`@hint`

- The t statistic for each coefficient is defined as $t=\frac{\widehat{\beta}\_j-\beta\_{j,0}}{SE(\widehat{\beta}\_j)}$.
- The p value can be computed as $2\Phi(-|t^{act}|)$ where $t^{act}$ denotes the computed t statistic.

`@pre_exercise_code`
```{r}
library(AER)
library(MASS)
coef <- summary(lm(medv ~ lstat + crim + age, data = Boston))$coef[, 1]
se   <- summary(lm(medv ~ lstat + crim + age, data = Boston))$coef[, 2]
```

`@sample_code`
```{r}
# Compute t statistics for each coefficient. Assign them to tstat.


# Compute p values for each coefficient. Assign them to pval.


# Check whether the hypotheses are rejected at a 1% significance level.


```

`@solution`
```{r}
# Compute t statistics for each coefficient. Assign them to tstat.
tstat <- coef/se

# Compute p values for each coefficient. Assign them to pval.
pval <- 2*(pnorm(-abs(tstat)))

# Check whether the hypotheses are rejected at a 1% significance level.
pval < 0.01

```

`@sct`
```{r}
test_object("tstat")
test_object("pval")
test_or(test_output_contains("pval < 0.01"), test_output_contains("pval > 0.01"))
success_msg("All but the coefficent for the crime rate (crim) can be rejected at a 1% significance level.")
```

---
## Hypothesis Testing in a Multiple Regression Model - Can we do more robust?

```yaml
type: NormalExercise
key: 3139d6f2f7
lang: r
xp: 100
skills: 1
```


`@instructions`

- 
- 
- 

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
## Hypothesis Testing in a Multiple Regression Model - Confidence Intervals

```yaml
type: NormalExercise
key: e1463dbaad
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
## Joint Hypothesis Testing - F Test I

```yaml
type: NormalExercise
key: eee04905db
lang: r
xp: 100
skills: 1
```

Besides testing single hypotheses we can also test joint hypotheses which impose restrictions on multiple regression coefficients. For example in the model 

$$medv\_i = \beta\_0 + \beta\_1\times lstat\_i + \beta\_2\times crim\_i + \beta\_3\times age\_i + u\_i$$

we could test the null $H\_0: \beta\_2=\beta\_3$ vs. the alternative $H\_1: \beta\_2\ne\beta\_3$ (which in fact is a joint hypothesis as we impose a restriction on two regression coefficients).

The basic idea behind testing such a hypothesis is now to conduct two regressions. For one of the regressions we incorporate the restriction (we call this the restricted model), whereas for the other regression the restriction is left out (we call this the unrestricted model). From this starting point we can then construct a test statistic which, under the null, follows a well known distribution, namely the $F$ distribution (see next exercise).
However in this exercise we start with the initial steps or computations necessary to construct the test statistic. So please do the following:

The packages `AER` and `MASS` have been loaded.

`@instructions`

- Estimate the restricted model, that is, the model where the restriction is assumed to be true. Save it in `model_res`.
- Compute the SSR of the restricted model and assign it to `RSSR`.
- Estimate the unrestricted model, that is, the model where the restriction is assumed to be false. Save it in `model_unres`.
- Compute the SSR of the unrestricted model and assign it to `USSR`.

`@hint`

- The restricted model can be written as $medv\_i = \beta\_0 + \beta\_1\times lstat\_i + \beta\_2\times crim\_i + \beta\_2\times age\_i + u\_i$ which, after rearranging, can be expressed as $medv\_i = \beta\_0 + \beta\_1\times lstat\_i + \beta\_2\times(crim\_i+age\_i) + u\_i$.
- The SSR is defined as the sum of the squared residuals.
- Note that the residuals of a regression model are available as `residuals` in the corresponding `lm` object. So you can access them as usual via the `$`-operator.

`@pre_exercise_code`
```{r}
library(AER)
library(MASS)
```

`@sample_code`
```{r}
# Estimate the restricted model and save it in model_res.


# Compute the SSR of the restricted model and assign it to RSSR.


# Estimate the unrestricted model and save it in model_unres.


# Compute the SSR of the unrestricted model and assign it to USSR.


```

`@solution`
```{r}
# Estimate the restricted model and save it in model_res.
model_res <- lm(medv ~ lstat + I(crim + age), data = Boston)

# Compute the SSR of the restricted model and assign it to RSSR.
RSSR <- sum(model_res$residuals^2)

# Estimate the unrestricted model and save it in model_unres.
model_unres <- lm(medv ~ lstat + crim + age, data = Boston)

# Compute the SSR of the unrestricted model and assign it to USSR.
USSR <- sum(model_unres$residuals^2)

```

`@sct`
```{r}
test_object("model_res")
test_object("RSSR")
test_object("model_unres")
test_object("USSR")
success_msg("Correct! Note that the SSR of the restricted model is always greater or equal than the SSR of the unrestricted model.")
```

---
## Joint Hypothesis Testing - F Test II

```yaml
type: NormalExercise
key: 7b8296af66
lang: r
xp: 100
skills: 1
```
After estimating the necessary models and computing the SSR we can now compute the test statistic and conduct the hypothesis test. As mentioned in the last exercise the test statistic follows the $F$ distribution or to be more precise the 

The packages `AER` and `MASS` have been loaded. Both models (`model_res` and `model_unres`) as well as their SSR (`RSSR` and `USSR`) are available in your working environment.

`@instructions`

- Compute the F statistic and assign it to `Fstat`.
- Compute the p value and assign it to `pval`. 
- Check with the help of logical operators whether the null is rejected at a 1% significance level.
- Verify your result by using `linearHypothesis()` and printing out the results. 

`@hint`

- The F statistic is defined as $\frac{RSSR-USSR/q}{USSR/(n-k-1)}$ where $q$ and $k$ denote the number of restrictions under the null and regressors in the unrestricted model, respectively.
- The p value can be computed as $1-F\_{q,n-k-1}(F^{act})$ where $F\_{q,n-k-1}$ denotes the cdf of the F distribution with degrees of freedom $q$ and $n-k-1$ and $F^{act}$ the computed F statistic.
- `linearHypothesis()` expects the unrestricted model as well as the null hypothesis.

`@pre_exercise_code`
```{r}
library(AER)
library(MASS)
model_res <- lm(medv ~ lstat + I(crim + age), data = Boston)
RSSR <- sum(model_res$residuals^2)
model_unres <- lm(medv ~ lstat + crim + age, data = Boston)
USSR <- sum(model_unres$residuals^2)
```

`@sample_code`
```{r}
# Compute the F statistic and assign it to Fstat.


# Compute the p value and assign it to pval.


# Check whether the null is rejected at a 1% significance level.


# Verify your result with linearHypothesis().


```

`@solution`
```{r}
# Compute the F statistic and assign it to Fstat.
Fstat <- ((RSSR-USSR)/1)/(USSR/(nrow(Boston)-3-1))

# Compute the p value and assign it to pval.
pval <- 1 - pf(Fstat, 1, nrow(Boston)-3-1)

# Check whether the null is rejected at a 1% significance level.
pval < 0.01

# Verify your result with linearHypothesis().
linearHypothesis(model_unres, "age = crim")

```

`@sct`
```{r}
test_object("Fstat")
test_object("pval")
test_or(test_output_contains("pval < 0.01"), test_output_contains("pval > 0.01"))
test_function_result("linearHypothesis")
success_msg("Correct! The hypothesis is rejected at a 1% significance level.")
```

---
## Joint Hypothesis Testing - Confidence Set

```yaml
type: NormalExercise
key: 4fd9af5073
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
