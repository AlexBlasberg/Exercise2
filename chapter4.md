---
title       : Nonlinear Regression Functions
description : Insert the chapter description here
---
## 1. Correlation and (Non)linearity I

```yaml
type: NormalExercise
key: 40ca44fb3d
lang: r
xp: 100
skills: 1
```
Consider the following simple linear regression model

$$medv\_i = \beta\_0 + \beta\_1\times lstat\_i + u\_i.$$

with `medv` (median house value) and `lstat` (percent of households with low socioeconomic status) being variables from the already known `Boston` data set.

The package `MASS` has been loaded. The model object from the above regression is available as `mod` in your working environment.

`@instructions`

- Compute the correlation between `medv` and `lstat`.
- Plot `medv` against `lstat` and add the regression line from the model object `mod`. What do you notice?

`@hint`

- You can use `cor()` to compute the correlation between variables.
- As usual you can use `plot()` and `abline()` to visualize regression results.

`@pre_exercise_code`
```{r}
library(MASS)
mod <- lm(medv ~ lstat, data = Boston)
```

`@sample_code`
```{r}
# Compute the correlation between medv and lstat


# Plot medv against lstat and draw the regression line



```

`@solution`
```{r}
# Compute the correlation between medv and lstat
cor(Boston$medv, Boston$lstat)

# Plot medv against lstat and draw the regression line
plot(medv ~ lstat, data = Boston)
abline(mod, col = "red")

```

`@sct`
```{r}
ex() %>% check_function("cor") %>% check_result() %>% check_equal()
test_or(ex() %>% check_function('plot') %>% {
          check_arg(., 'formula') %>% check_equal()
          check_arg(., 'data') %>% check_equal()
        },
        ex() %>% override_solution('plot(Boston$medv, Boston$lstat)') %>% check_function('plot') %>% {
          check_arg(., 'x') %>% check_equal()
          check_arg(., 'y') %>% check_equal()
        },
        ex() %>% override_solution('plot(Boston$medv ~ Boston$lstat)') %>% check_function('plot') %>%
          check_arg('formula') %>% check_equal()
        )
#ex() %>% check_function("abline") %>% check_arg("reg") %>% check_equal()
success_msg("Although the correlation coefficient suggests that medv and lstat are negatively linearly dependent, the relationship between them is clearly nonlinear. Hence a simple linear regression specification is inappropriate here.")
```

---
## 2. Correlation and (Non)linearity II

```yaml
type: NormalExercise
key: 8bb4d4bbe0
lang: r
xp: 100
skills: 1
```
In the previous exercise we saw that the correlation coefficient is not able to properly capture the functional form of a regression model in so far as it suggested a linear form, whereas the true functional form seems to be a nonlinear (e.g. exponential) one.
Therefore consider as an alternative the following nonlinear model specification

$$medv\_i = \beta\_0 + \beta\_1\times\log(lstat\_i) + u\_i.$$

The package `MASS` has been loaded.

`@instructions`

- Conduct the regression from above and assign the results to `log_mod`.
- Visualize your results by drawing a scatterplot and adding the corresponding regression line. In comparison to the previous exercise what do you notice now? 

`@hint`

- Use `lm()` to conduct a regression.
- As usual you can use `plot()` and `abline()` to visualize regression results.

`@pre_exercise_code`
```{r}
library(MASS)
```

`@sample_code`
```{r}
# Conduct the regression and assign it to mod_log


# Draw a scatterplot and add the corresponding regression line



```

`@solution`
```{r}
# Conduct the regression and assign it to mod_log
mod_log <- lm(medv ~ log(lstat), data = Boston)

# Draw a scatterplot and add the corresponding regression line
plot(medv ~ log(lstat), data = Boston)
abline(mod_log, col = "red")

```

`@sct`
```{r}
ex() %>% check_object("mod_log") %>% check_equal()
test_or(ex() %>% check_function('plot') %>% {
          check_arg(., 'formula') %>% check_equal()
          check_arg(., 'data') %>% check_equal()
        },
        ex() %>% override_solution('plot(Boston$medv, log(Boston$lstat))') %>% check_function('plot') %>% {
          check_arg(., 'x') %>% check_equal()
          check_arg(., 'y') %>% check_equal()
        },
        ex() %>% override_solution('plot(Boston$medv ~ log(Boston$lstat))') %>% check_function('plot') %>%
          check_arg('formula') %>% check_equal()
        )
#ex() %>% check_function("abline") %>% check_arg("reg") %>% check_equal()
success_msg("Although the relationship is not perfectly linear yet, using a log transformation considerably improves our model fit and seems to be a reasonable model specification.")
```

---
## 3. Optimal Polynomial Order - Sequential Testing

```yaml
type: NormalExercise
key: c77bd54d97
lang: r
xp: 100
skills: 1
```

From the previous exercise recall the following model

$$medv\_i = \beta\_0 + \beta\_1\times\log(lstat\_i) + u\_i.$$

We already saw that this model specification seems to be a reasonable choice. However we cannot be entirely sure, if a higher polynomial order may be more suited to describe the data. Therefore please do the following:

The packages `AER` and `MASS` have been loaded.

`@instructions`

- Determine the optimal order of the polylog model by the sequential testing approach. Assume a maximum polynomial order of $r=4$. You are more or less free to choose a way to solve this as long as you use a `for()` loop. We recommend the following approach:
    1. Estimate a model, say `mod`, which starts with the highest polynomial order.
    2. Save the p-value (with robust standard errors) for the relevant parameter and compare it with the significance level $\alpha$.
    3. If you cannot reject the null, repeat steps 1 and 2 for the next lowest polynomial order, otherwise stop the loop and print out the polynomial order.
- Extract the $R^2$ of the selected model and assign it to the variable `R2`. 

`@hint`

- The index for the `for()` loop should start at 4 and end at 1.
- You can use `poly()` inside of `lm()` as a generic way of incorporating higher orders of a certain variable in the model. Besides the variable, you have to specify the degree of the polynomial via the argument `degree` and set `raw = TRUE`.
- As usual, you can use `coeftest()` to obtain p-values (with robust standard errors). Use the structure of the resulting object to extract the relevant p-value.
- Use an `if()` statement to check whether the condition for no rejection is fulfilled and stop the `for()` loop with the help of `break` otherwise.
- To obtain the $R^2$, you can use `summary()` and extract it via `$r.squared`.

`@pre_exercise_code`
```{r}
library(AER)
library(MASS)
```

`@sample_code`
```{r}
# Find the optimal polynomial order of the polylog model.









# Extract the R^2 from the selected model and assign it to R2.


```

`@solution`
```{r}
# Find the optimal polynomial order of the polylog model.
for(i in 4:1){
  mod  <- lm(medv ~ poly(log(lstat), i, raw = T), data = Boston)
  pval <- coeftest(mod, vcov = vcovHC)[(i+1), 4]
  if(pval < 0.05){
    print(i)
    break
  }
}

# Extract the R^2 from the selected model and assign it to R2.
R2 <- summary(mod)$r.squared

```

`@sct`
```{r}
ex() %>% check_for()
ex() %>% check_object("R2") %>% check_equal()
```

---
## 4. 

```yaml
type: NormalExercise
key: b768384af2
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
