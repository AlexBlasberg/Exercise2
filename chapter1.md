---
title       : Probability Theory
description : Insert the chapter description here
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

---
## A really bad movie

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
Suppose you are the lottery 

`@instructions`
- Check out the structure of `movie_selection`.

`@hint`
- Use `str()` for the first instruction.



`@sample_code`
```{r}
# Draw the lottery numbers for this week

```

`@solution`
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
```

`@sct`
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```

---
## Chi-squared distribution

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
