---
title: 'Introduction to Discrete Probability'
description: 'In this chapter, you will learn about the fundamentals of discrete probability through looking at examples of sampling from an urn with and without replacement.'
free_preview: true
---

## Exercise 1. Probability of cyan - generalized

```yaml
type: NormalExercise
key: c76ada353d
lang: r
xp: 100
skills: 1
```

In the edX exercises for this section, we calculated some probabilities by hand. Now we'll calculate those probabilities using R.

One ball will be drawn at random from a box containing: 3 cyan balls, 5 magenta balls, and 7 yellow balls. 

What is the probability that the ball will be cyan?

`@instructions`
- Define a variable `p` as the probability of choosing a cyan ball from the box.
- Print the value of `p`.

`@hint`
- Calculate the proportion of balls in the box that are cyan and assign that value to the variable `p`.
- To print the contents of a variable, write the variable name in a new line of code.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
cyan <- 3
magenta <- 5
yellow <- 7

# Assign a variable `p` as the probability of choosing a cyan ball from the box


# Print the variable `p` to the console
```

`@solution`
```{r}
cyan <- 3
magenta <- 5
yellow <- 7

# Assign a variable `p` as the probability of choosing a cyan ball from the box
p <- cyan / (cyan + magenta + yellow)

# Print the variable `p` to the console
p
```

`@sct`
```{r}
test_error()
test_object("p", incorrect_msg = "Make sure that you use `p` as your variable name and that you have assigned the correct value to `p`.")
test_output_contains("0.2", incorrect_msg = "This value is incorrect. The probability of choosing a cyan ball is equal to the proportion of cyan balls in the box.")
success_msg("Good job! Let's work on a similar problem.")
```

---

## Exercise 2. Probability of not cyan - generalized

```yaml
type: NormalExercise
key: dfa7d52eeb
lang: r
xp: 100
skills: 1
```

We defined the variable `p` as the probability of choosing a cyan ball from a box containing: 3 cyan balls, 5 magenta balls, and 7 yellow balls.

What is the probability that the ball you draw from the box will NOT be cyan?

`@instructions`
- Using the probability of choosing a cyan ball, `p`, calculate the probability of choosing any other ball.

`@hint`
- The sum of all possibilities is 1.

`@pre_exercise_code`
```{r}
cyan <- 3
magenta <- 5
yellow <- 7

# Assign a variable `p` as the probability of choosing a cyan ball from the box
p <- cyan / (cyan + magenta + yellow)
```

`@sample_code`
```{r}
# `p` is defined as the probability of choosing a cyan ball from a box containing: 3 cyan balls, 5 magenta balls, and 7 yellow balls.
# Using variable `p`, calculate the probability of choosing any ball that is not cyan from the box
```

`@solution`
```{r}
# `p` is defined as the probability of choosing a cyan ball from a box containing: 3 cyan balls, 5 magenta balls, and 7 yellow balls.
# Using variable `p`, calculate the probability of choosing any ball that is not cyan from the box
1 - p
```

`@sct`
```{r}
test_error()
test_output_contains("0.8", incorrect_msg = "You are not providing a calculation that gives the correct answer. The sum of all probabilities equals 1.")
success_msg("Good job! Let's work on the next question.")
```

---

## Exercise 3. Sampling without replacement - generalized

```yaml
type: NormalExercise
key: 0f16dc0d6a
lang: r
xp: 100
skills: 1
```

Instead of taking just one draw, consider taking two draws. You take the second draw without returning the first draw to the box. We call this sampling without replacement. 

What is the probability that the first draw is cyan and that the second draw is not cyan?

`@instructions`
- Calculate the **conditional probability `p_2`** of choosing a ball that is not cyan after one cyan ball has been removed from the box.
- Calculate the **joint probability** of **both** choosing a cyan ball on the first draw **and** a ball that is not cyan on the second draw using `p_1` and `p_2`.

`@hint`
- In a scenario where you sample without replacement, the number of balls decreases after the first draw.
- The probability of selecting a ball that is not cyan on the second draw depends on whether or not you removed a cyan ball on the first draw.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
cyan <- 3
magenta <- 5
yellow <- 7

# The variable `p_1` is the probability of choosing a cyan ball from the box on the first draw.
p_1 <- cyan / (cyan + magenta + yellow)

# Assign a variable `p_2` as the probability of not choosing a cyan ball on the second draw without replacement.

# Calculate the probability that the first draw is cyan and the second draw is not cyan using `p_1` and `p_2`.
```

`@solution`
```{r}
cyan <- 3
magenta <- 5
yellow <- 7

# The variable `p_1` is the probability of choosing a cyan ball from the box on the first draw.
p_1 <- cyan / (cyan + magenta + yellow)

# Assign a variable `p_2` as the probability of not choosing a cyan ball on the second draw without replacement.
p_2 <- 1 - (cyan - 1) / (cyan + magenta + yellow - 1)

# Calculate the probability that the first draw is cyan and the second draw is not cyan.
p_1 * p_2
```

`@sct`
```{r}
test_error()
test_object("p_2", incorrect_msg = "`p_2` is not defined correctly. First, define `p_2` as the probability of choosing a ball that is not cyan on the second draw after removing a cyan ball on the first draw. Then, calculate the probability of both events using `p_1` and `p_2`.")
test_output_contains("0.1714286", incorrect_msg = "You are not providing a calculation that gives the correct answer. Multiply probabilities to calculate the probability that they occur in sequence.")
success_msg("Great! Let's work on another problem.")
```

---

## Exercise 4. Sampling with replacement - generalized

```yaml
type: NormalExercise
key: 529ac47eb5
lang: r
xp: 100
skills: 1
```

Now repeat the experiment, but this time, after taking the first draw and recording the color, return it back to the box and shake the box. We call this sampling with replacement. 

What is the probability that the first draw is cyan and that the second draw is not cyan?

`@instructions`
- Calculate the probability `p_2` of choosing a ball that is not cyan on the second draw, with replacement.
- Next, use `p_1` and `p_2` to calculate the probability of choosing a cyan ball on the first draw and a ball that is not cyan on the second draw (after replacing the first ball).

`@hint`
- The probabilities of drawing a cyan ball and then a ball that is not cyan are independent.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
cyan <- 3
magenta <- 5
yellow <- 7

# The variable 'p_1' is the probability of choosing a cyan ball from the box on the first draw.
p_1 <- cyan / (cyan + magenta + yellow)

# Assign a variable 'p_2' as the probability of not choosing a cyan ball on the second draw with replacement.

# Calculate the probability that the first draw is cyan and the second draw is not cyan using `p_1` and `p_2`.

```

`@solution`
```{r}
cyan <- 3
magenta <- 5
yellow <- 7

# The variable 'p_1' is the probability of choosing a cyan ball from the box on the first draw.
p_1 <- cyan / (cyan + magenta + yellow)

# Assign a variable 'p_2' as the probability of not choosing a cyan ball on the second draw with replacement.
p_2 <- 1 - (cyan) / (cyan + magenta + yellow)

# Calculate the probability that the first draw is cyan and the second draw is not cyan using `p_1` and `p_2`.
p_1 * p_2
```

`@sct`
```{r}
test_error()
test_object("p_2", incorrect_msg = "`p_2` is not defined correctly. First, define `p_2` as the probability of choosing a ball that is not cyan on the second draw after replacing the first ball. Then, calculate the probability of both events using `p_1` and `p_2`.")
test_output_contains("0.16", incorrect_msg = "You are not providing a calculation that gives the correct answer. Multiply independent probabilities to calculate the probability that they occur in sequence.")
success_msg("Great work!")
```

---

## End of Assessment: Introduction to Discrete Probability

```yaml
type: PureMultipleChoiceExercise
key: 92dc47880e
xp: 50
skills: 1
```

This is the end of the programming assignment for this section. Please DO NOT click through to additional assessments from this page. Please DO answer the question on this page. If you do click through, your scores may NOT be recorded.

Click on "Awesome" to get the "points" for this question and then return to the course on edX.

You can close this window and return to <a href='https://www.edx.org/course/data-science-probability-2'>Data Science: Probability</a>.

`@hint`
- No hint necessary!

`@possible_answers`
- [Awesome]
- Nope

`@feedback`
- Great! Now navigate back to the course on edX!
- Now navigate back to the course on edX!
