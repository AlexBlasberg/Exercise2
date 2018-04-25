---
title       : Hypothesis Tests and Confidence Intervals in Multiple Regression
description : Insert the chapter description here
---
## Inference in the Multiple Regression Model - t statistics and p values

```yaml
type: NormalExercise
key: c80d99676b
lang: r
xp: 100
skills: 1
```

Reconsider the following estimated model from the previous chapter:

$$\widehat{medv}\_i = \underset{(0.74)}{32.828} \underset{(0.08)}{-0.994} \times lstat\_i \underset{(0.03)}{-0.083} \times crim\_i + \underset{(0.02)}{0.038} \times age\_i.$$

Just as for the simple linear regression model

The packages `AER` and `MASS` have been loaded. The coefficients as well as the standard errors of the model are already available in `coef` and `se`, respectively.

`@instructions`

- Compute t statistics for each coefficient and assign them to `tstat`.
- Compute p values for each coefficient and assign them to `pval`.
- Check with the help of logical operators whether the hypotheses are rejected at a 1% significance level.

`@hint`

- 
- 

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
pval <- 2*(1-pnorm(abs(tstat)))

# Check whether the hypotheses are rejected at a 1% significance level.
pval < 0.01

```

`@sct`
```{r}
test_object("tstat")
test_object("pval")
test_or(test_output_contains("pval < 0.01"), test_output_contains("pval > 0.01"))
```
