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
This exercises
In order to illustrate this consider the following simple linear regression model

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
library(AER)
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
ex() %>% check_function("abline") %>% check_arg("reg") %>% check_equal()
success_msg("Although the correlation coefficient suggests that medv and lstat ..., the relationship between them is clearly nonlinear. Hence a simple linear regression specification is inappropriate here.")
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
In the previous exercise we saw that the correlation coefficient is not able to assess whether a linear regression model 
Therefore consider as an alternative the following nonlinear model specification

$$medv\_i = \beta\_0 + \beta\_1\times\log(lstat\_i) + u\_i.$$

The package `MASS` has been loaded.

`@instructions`

- Conduct the regression from above and assign the results to `log_mod`.
- Visualize your results by drawing a scatterplot and adding the corresponding regression line.

`@hint`

- Use `lm()` to conduct a regression.
- As usual you can use `plot()` and `abline()` to visualize regression results.

`@pre_exercise_code`
```{r}
library(AER)
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
success_msg("Although the relationship is not perfectly linear yet, using a log transformation considerably improves our model fit.")
```

---
## 3.

```yaml
type: NormalExercise
key: c77bd54d97
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
