---
title       : Review of Statistics
description : Insert the chapter description here
---
## Biased estimator

```yaml
type: NormalExercise
key: 76c959aa9b
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
## <<<New Exercise>>>

```yaml
type: NormalExercise
key: b75a7ad1f3
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

As an alternative consider the estimator with unequal weighting scheme

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
