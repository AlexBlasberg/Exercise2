---
  title: "Hypothesis Tests and Confidence Intervals in Multiple Regression"
  description: "Insert the chapter description here"
---

## Hypothesis Testing in a Multiple Regression Model - t statistics and p values

```yaml
type: NormalExercise 
lang: r
xp: 100 
skills: 1
key: c80d99676b   
```


Reconsider the `Boston` data set and the following estimated model (with homoscedasticity-only standard errors in parentheses) from the previous chapter:

$$\widehat{medv}\_i = \underset{(0.75)}{32.828} \underset{(0.05)}{-0.994} \times lstat\_i \underset{(0.04)}{-0.083} \times crim\_i + \underset{(0.01)}{0.038} \times age\_i.$$

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

```{undefined}
library(AER)
library(MASS)
coef <- summary(lm(medv ~ lstat + crim + age, data = Boston))$coef[, 1]
se   <- summary(lm(medv ~ lstat + crim + age, data = Boston))$coef[, 2]
```

`@sample_code`

```{undefined}
# Compute t statistics for each coefficient. Assign them to tstat.


# Compute p values for each coefficient. Assign them to pval.


# Check whether the hypotheses are rejected at a 1% significance level.
```

`@solution`

```{undefined}
# Compute t statistics for each coefficient. Assign them to tstat.
tstat <- coef/se

# Compute p values for each coefficient. Assign them to pval.
pval <- 2*(pnorm(-abs(tstat)))

# Check whether the hypotheses are rejected at a 1% significance level.
pval < 0.01
```

`@sct`

```{undefined}
test_object("tstat")
test_object("pval")
test_or(test_output_contains("pval < 0.01"), test_output_contains("pval > 0.01"))
success_msg("All but the coefficent for the crime rate (crim) can be rejected at a 1% significance level.")
```

---

## Hypothesis Testing in a Multiple Regression Model - Confidence Intervals

```yaml
type: NormalExercise 
lang: r
xp: 100 
skills: 1
key: e1463dbaad   
```


Again consider the model 

$$\widehat{medv}\_i = \underset{(0.75)}{32.828} \underset{(0.05)}{-0.994} \times lstat\_i \underset{(0.04)}{-0.083} \times crim\_i + \underset{(0.01)}{0.038} \times age\_i.$$

which is available as `mod` in your working environment. The packages `AER` and `MASS` have been loaded.


`@instructions`
- Construct a 99% confidence interval for all model coefficients. Decide whether we can reject the null $H\_0:\beta\_j=0$ for all $j$.

`@hint`
- You can use `confint()` to construct confidence intervals. The confidence level can be set via `level`.

`@pre_exercise_code`

```{undefined}
library(AER)
library(MASS)
mod <- lm(medv ~ lstat + crim + age, data = Boston)
```

`@sample_code`

```{undefined}
# Construct a 99% confidence interval for all coefficients
```

`@solution`

```{undefined}
# Construct a 99% confidence interval for all coefficients
confint(mod, level = 0.99)
```

`@sct`

```{undefined}
test_function('confint', args = c('object', 'level'))
success_msg('Correct! Analogously to the previous exercise we can see that 0 is not an element for all confidence intervals but for the one of the crime rate. Hence, as expected, the test decision remains the same.')
```

---

## Hypothesis Testing in a Multiple Regression Model - Can we do more robust?

```yaml
type: NormalExercise 
lang: r
xp: 100 
skills: 1
key: 3139d6f2f7   
```


`mod`, the `lm` object with the estimated model

$$\widehat{medv}\_i = 32.828 - 0.994 \times lstat\_i - 0.083 \times crim\_i + 0.038 \times age\_i.$$

is available in your working environment. The packages `AER` and `MASS` have been loaded.


`@instructions`
- Print a coefficient summary using heteroscedasticity-robust standard errors.
- Access entries of the matrix created by `coeftest()` to check with the help of logical operators whether the hypotheses are rejected at a 1% significance level.

`@hint`
- Inside of `coeftest()` one can set the argument `vcov.` to force the function to use robust standard errors.
- The p values are contained in the fourth column of the matrix. Use square brackets to access them.

`@pre_exercise_code`

```{undefined}
library(AER)
library(MASS)
mod <- lm(medv ~ lstat + crim + age, data = Boston)
```

`@sample_code`

```{undefined}
# Print a coefficient summary using robust standard errors.


# Check whether the hypotheses are rejected at a 1% significance level.
```

`@solution`

```{undefined}
# Print a coefficient summary using robust standard errors.
coeftest(mod, vcov. = vcovHC)

# Check whether the hypotheses are rejected at a 1% significance level.
coeftest(mod, vcov. = vcovHC)[, 4] < 0.01
```

`@sct`

```{undefined}
test_function_result('coeftest')
test_or(test_output_contains("coeftest(mod, vcov. = vcovHC)[, 4] < 0.01", incorrect_msg = 'Not correct! Please make sure you select the correct entries of the matrix.'), test_output_contains("coeftest(mod, vcov. = vcovHC)[, 4] > 0.01", incorrect_msg = 'Not correct! Please make sure you select the correct entries of the matrix.'))
success_msg('Correct! We see that by using robust standard errors the coefficient for the crime rate (crim) becomes significant, whereas the coefficient for the average age of the buildings (age) becomes insignificant at a 1% significance level.')
```

---

## Joint Hypothesis Testing - F Test I

```yaml
type: NormalExercise 
lang: r
xp: 100 
skills: 1
key: eee04905db   
```


Besides testing single hypotheses we can also test joint hypotheses which impose restrictions on multiple regression coefficients. For example in the model 

$$medv\_i = \beta\_0 + \beta\_1\times lstat\_i + \beta\_2\times crim\_i + \beta\_3\times age\_i + u\_i$$

we could test the null $H\_0: \beta\_2=\beta\_3$ vs. the alternative $H\_1: \beta\_2\ne\beta\_3$ (which in fact is a joint hypothesis as we impose a restriction on two regression coefficients).

The basic idea behind testing such a hypothesis is now to conduct two regressions. For one of the regressions we incorporate the restriction (we call this the restricted model), whereas for the other regression the restriction is left out (we call this the unrestricted model). From this starting point we can then construct a test statistic which, under the null, follows a well known distribution, namely a $F$ distribution (see next exercise).
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

```{undefined}
library(AER)
library(MASS)
```

`@sample_code`

```{undefined}
# Estimate the restricted model and save it in model_res.


# Compute the SSR of the restricted model and assign it to RSSR.


# Estimate the unrestricted model and save it in model_unres.


# Compute the SSR of the unrestricted model and assign it to USSR.
```

`@solution`

```{undefined}
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

```{undefined}
test_or({

test_function('lm', 
             args = c('formula', 'data'),
             not_called_msg = "Funktion nicht oder falsch aufgerufen.",
             args_not_specified_msg = "Funktion nicht oder falsch aufgerufen."
             )
             

},{

sol <- ex() %>% override_solution("model_res <- lm(medv ~ lstat + I(crim + age), data = Boston)")
sol %>% check_function('lm') %>% check_arg('formula') %>% check_equal()

},{

sol <- ex() %>% override_solution("model_res <- lm(Boston$medv ~ Boston$lstat + I(Boston$crim + Boston$age))")
sol %>% check_function('lm') %>% check_arg('formula') %>% check_equal()

})
test_object("model_res", eval = F)
test_object("RSSR")
test_or({

test_function('lm', 
             args = c('formula', 'data'),
             not_called_msg = "Funktion nicht oder falsch aufgerufen.",
             args_not_specified_msg = "Funktion nicht oder falsch aufgerufen."
             )
             

},{

sol <- ex() %>% override_solution("model_unres <- lm(medv ~ lstat + crim + age, data = Boston)")
sol %>% check_function('lm') %>% check_arg('formula') %>% check_equal()

},{

sol <- ex() %>% override_solution("model_unres <- lm(Boston$medv ~ Boston$lstat + Boston$crim + Boston$age)")
sol %>% check_function('lm') %>% check_arg('formula') %>% check_equal()

})
test_object("model_unres", eval = F)
test_object("USSR")
success_msg("Correct! Note that the SSR of the restricted model is always greater or equal than the SSR of the unrestricted model.")
```

---

## Joint Hypothesis Testing - F Test II

```yaml
type: NormalExercise 
lang: r
xp: 100 
skills: 1
key: 7b8296af66   
```


After estimating the necessary models and computing the SSR we can now compute the test statistic and conduct the hypothesis test. As mentioned in the last exercise the test statistic follows a $F$ distribution or more precisely a $F\_{q,n-k-1}$ distribution where $q$ and $k$ denote the number of restrictions under the null and regressors in the unrestricted model, respectively.

The packages `AER` and `MASS` have been loaded. Both models (`model_res` and `model_unres`) as well as their SSR (`RSSR` and `USSR`) are available in your working environment.


`@instructions`
- Compute the F statistic and assign it to `Fstat`.
- Compute the p value and assign it to `pval`. 
- Check with the help of logical operators whether the null is rejected at a 1% significance level.
- Verify your result by using `linearHypothesis()` and printing out the results.

`@hint`
- The F statistic is defined as $\frac{RSSR-USSR/q}{USSR/(n-k-1)}$.
- The p value can be computed as $1-F\_{q,n-k-1}(F^{act})$ where $F\_{q,n-k-1}$ denotes the cdf of the F distribution (`pf()`) with degrees of freedom $q$ and $n-k-1$ and $F^{act}$ the computed F statistic.
- `linearHypothesis()` expects the unrestricted model as well as the null hypothesis.

`@pre_exercise_code`

```{undefined}
library(AER)
library(MASS)
model_res <- lm(medv ~ lstat + I(crim + age), data = Boston)
RSSR <- sum(model_res$residuals^2)
model_unres <- lm(medv ~ lstat + crim + age, data = Boston)
USSR <- sum(model_unres$residuals^2)
```

`@sample_code`

```{undefined}
# Compute the F statistic and assign it to Fstat.


# Compute the p value and assign it to pval.


# Check whether the null is rejected at a 1% significance level.


# Verify your result with linearHypothesis().
```

`@solution`

```{undefined}
# Compute the F statistic and assign it to Fstat.
Fstat <- ((RSSR-USSR)/1)/(USSR/(nrow(Boston)-3-1))

# Compute the p value and assign it to pval.
pval <- 1 - pf(Fstat, df1 = 1, df2 = nrow(Boston)-3-1)

# Check whether the null is rejected at a 1% significance level.
pval < 0.01

# Verify your result with linearHypothesis().
linearHypothesis(model_unres, "age = crim")
```

`@sct`

```{undefined}
test_object("Fstat")
test_object("pval")
test_or(test_output_contains("pval < 0.01"), test_output_contains("pval > 0.01"))
test_function_result("linearHypothesis")
success_msg("Correct! The null hypothesis is rejected at a 1% significance level.")
```

---

## Joint Hypothesis Testing - Confidence Set

```yaml
type: NormalExercise 
lang: r
xp: 100 
skills: 1
key: 4fd9af5073   
```


As you know from previous chapters constructing a confidence set for a single regression coefficient results in a simple confidence interval on the real line. However if we consider $n$ regression coefficients jointly (as we do in a joint hypothesis testing setting) we move from $\mathbb{R}$ to $\mathbb{R}^n$ resulting in a n-dimensional confidence set. For the sake of illustration we then often choose $n=2$, so that we end up with a representable two-dimensional plane.

Now recall the model 

$$\widehat{medv}\_i = \underset{(0.75)}{32.828} \underset{(0.05)}{-0.994} \times lstat\_i \underset{(0.04)}{-0.083} \times crim\_i + \underset{(0.01)}{0.038} \times age\_i.$$

which is available as `mod` in your working environment and assume we want to test the null $H\_0: \beta\_2=\beta\_3=0$ vs. $H\_1: \beta\_2\ne 0$ or $\beta\_3\ne 0$.

The packages `AER` and `MASS` have been loaded.


`@instructions`
- Construct a 99% confidence set for the coefficients of `crim` and `lstat`, that is a two-dimensional confidence set. Can you reject the null stated above?
- Verify your visual inspection by conducting a corresponding F test.

`@hint`
- You can use `confidenceEllipse()` to construct a two dimensional confidence set. Besides the coefficients for which the confidence set shall be constructed (`which.coef`), you have to specify the confidence level (`levels`).
- As usual you can use `linearHypothesis()` to conduct a F test. However note that we test two restrictions now, hence you have to pass a vector consisting of both linear restrictions.

`@pre_exercise_code`

```{undefined}
library(AER)
library(MASS)
mod <- lm(medv ~ lstat + crim + age, data = Boston)
```

`@sample_code`

```{undefined}
# Construct a 99% confidence set for the coefficents of crim and lstat.


# Conduct a corresponding F test.
```

`@solution`

```{undefined}
# Construct a 99% confidence set for crim and lstat.
confidenceEllipse(mod, which.coef = c("crim", "lstat"), levels = 0.99)

# Conduct a corresponding F test.
linearHypothesis(mod, c("crim = 0", "lstat = 0"))
```

`@sct`

```{undefined}
test_or({
  fun <- ex() %>% check_function('confidenceEllipse')
  fun %>% check_arg('model') %>% check_equal()
  fun %>% check_arg('which.coef') %>% check_equal()
  fun %>% check_arg('levels') %>% check_equal()
}, {
  fun <- ex() %>% override_solution('confidenceEllipse(mod, which.coef = c("lstat", "crim"), levels = 0.99)') %>% check_function('confidenceEllipse')
  fun %>% check_arg('model') %>% check_equal()
  fun %>% check_arg('which.coef') %>% check_equal()
  fun %>% check_arg('levels') %>% check_equal()
})
test_function_result('linearHypothesis')
success_msg("Correct! Since (0,0) is not an element of the 99% confidence set, the null hypothesis is rejected at a 1% significance level.")
```
