---
title: 'Independence and Multiplication Rule'
description: 'In this chapter, you will learn about independence, conditional probability, and the multiplication rule through examples involving draws from an urn, rolls of a die, and sports series wins.'
---

## Exercise 1. Independence

```yaml
type: MultipleChoiceExercise
key: 9de5f06718
xp: 50
skills: 1
```

Imagine you draw two balls from a box containing colored balls. You either replace the first ball before you draw the second or you leave the first ball out of the box when you draw the second ball. 

Under which situation are the two draws independent of one another?

Remember that two events $A$ and $B$ are independent if $\mbox{Pr}(A \mbox{ and } B) = \mbox{Pr}(A) P(B)$.

`@possible_answers`
- You don't replace the first ball before drawing the next.
- You do replace the first ball before drawing the next.
- Neither situation describes independent events.
- Both situations describe independent events.

`@hint`
Sampling without replacement changes the number of balls remaining in the box when the second ball is drawn.

`@pre_exercise_code`
```{r}
# no pec
```

`@sct`
```{r}
msg1 = "Try again! The box contains fewer balls during the second draw if you don't replace the drawn ball."
msg2 = "Well done. Proceed to the next exercise."
msg3 = "One of the situations describes independent events."
msg4 = "One of these situations describes an event where the second draw depends on the outcome of the first."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 2. Sampling with replacement

```yaml
type: NormalExercise
key: f822ca7dc0
lang: r
xp: 100
skills: 1
```

Say you’ve drawn 5 balls from the a box that has 3 cyan balls, 5 magenta balls, and 7 yellow balls, with replacement, and all have been yellow.

What is the probability that the next one is yellow?

`@instructions`
- Assign the variable `p_yellow` as the probability of choosing a yellow ball on the first draw.
- Using the variable `p_yellow`, calculate the probability of choosing a yellow ball on the sixth draw.

`@hint`
- If the proportion of yellow balls in the box doesn't change, the probability of drawing a yellow ball does not change.
- Use the multiplication rule to determine the probability of multiple events.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
cyan <- 3
magenta <- 5
yellow <- 7

# Assign the variable 'p_yellow' as the probability that a yellow ball is drawn from the box.

# Using the variable 'p_yellow', calculate the probability of drawing a yellow ball on the sixth draw. Print this value to the console.
```

`@solution`
```{r}
cyan <- 3
magenta <- 5
yellow <- 7

# Assign the variable 'p_yellow' as the probability that a yellow ball is drawn from the box.
p_yellow <- yellow/(cyan+magenta+yellow)

# Using the variable 'p_yellow', calculate the probability of drawing a yellow ball on the sixth draw. Print this value to the console.
p_yellow
```

`@sct`
```{r}
test_error()
test_object("p_yellow", incorrect_msg = "Make sure that you use `p_yellow` as your variable name for the probability of choosing a yellow ball from the box.")
test_output_contains("0.4666667", incorrect_msg = "You are not providing a calculation that gives the correct answer. The probability of choosing a yellow ball does not depend on subsequent draws when balls are replaced after each draw.")
success_msg("Great! Let's work on another problem.")
```

---

## Exercise 3. Rolling a die

```yaml
type: NormalExercise
key: ad9aa31ae9
lang: r
xp: 100
skills: 1
```

If you roll a 6-sided die once, what is the probability of not seeing a 6? If you roll a 6-sided die six times, what is the probability of not seeing a 6 on any of those rolls?

`@instructions`
- Assign the variable `p_no6` as the probability of not seeing a 6 on a single roll.
- Then, calculate the probability of not seeing a 6 on six rolls using `p_no6`.

`@hint`
- The probability of rolling a 6 does not change from roll to roll.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign the variable 'p_no6' as the probability of not seeing a 6 on a single roll.


# Calculate the probability of not seeing a 6 on six rolls using `p_no6`. Print your result to the console: do not assign it to a variable.
```

`@solution`
```{r}
# Assign the variable 'p_no6' as the probability of not seeing a 6 on a single roll.
p_no6 <- 1 - (1/6)

# Calculate the probability of not seeing a 6 on six rolls using `p_no6`. Print your result to the console: do not assign it to a variable.
p_no6^6
```

`@sct`
```{r}
test_error()
test_object("p_no6", incorrect_msg = "Make sure that you use `p_no6` as your variable name for the probability of rolling any number other than six on a 6-sided die.")
test_output_contains("0.334898", incorrect_msg = "You are not providing a calculation that gives the correct answer. The probability of rolling any number other than a six does not change from roll to roll.")
success_msg("Great! Let's work on another problem.")
```

---

## Exercise 4. Probability the Celtics win a game

```yaml
type: NormalExercise
key: 804dd954a8
lang: r
xp: 100
skills: 1
```

Two teams, say the Celtics and the Cavs, are playing a seven game series. The Cavs are a better team and have a 60% chance of winning each game. 

What is the probability that the Celtics win at least one game? Remember that the Celtics must win one of the first four games, or the series will be over!

`@instructions`
- Calculate the probability that the Cavs will win the first four games of the series.
- Calculate the probability that the Celtics win at least one game in the first four games of the series.

`@hint`
- The probability that the Cavs win a game does not change throughout the series, regardless of previous outcomes.
- If the Cavs don't win all four games, then the Celtics win at least one game.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign the variable `p_cavs_win4` as the probability that the Cavs will win the first four games of the series.


# Using the variable `p_cavs_win4`, calculate the probability that the Celtics win at least one game in the first four games of the series.
```

`@solution`
```{r}
# Assign the variable `p_cavs_win4` as the probability that the Cavs will win the first four games of the series.
p_cavs_win4 <- 0.6^4

# Using the variable `p_cavs_win4`, calculate the probability that the Celtics win at least one game in the first four games of the series.
1 - p_cavs_win4
```

`@sct`
```{r}
test_error()
test_object("p_cavs_win4", incorrect_msg = "Make sure that you use `p_cavs_win4` as your variable name for the probability of the Cavs winning four games in a row.")
test_output_contains("0.8704", incorrect_msg = "The value of `p_cavs_win4` is incorrect. Assign `p_cavs_win4` as the probability the Cavs win the first four games of the series, given that they have a 60% chance of winning each game.")
success_msg("Great! Let's work on another problem.")
```

---

## Exercise 5. Monte Carlo simulation for Celtics winning a game

```yaml
type: NormalExercise
key: 9b3f311b75
lang: r
xp: 100
skills: 1
```

Create a Monte Carlo simulation to confirm your answer to the previous problem by estimating how frequently the Celtics win at least 1 of 4 games. Use `B <- 10000` simulations.

The provided sample code simulates a single series of four random games, `simulated_games`.

`@instructions`
- Use the `replicate` function for `B <- 10000` simulations of a four game series. The results of `replicate` should be stored to a variable named `celtic_wins`.
- Within each simulation, replicate the sample code to simulate a four-game series named `simulated_games`. Then, use the `any` function to indicate whether the four-game series contains at least one win for the Celtics. Perform these operations in two separate steps.
- Use the `mean` function on `celtic_wins` to find the proportion of simulations that contain at least one win for the Celtics out of four games.

`@hint`
- To use the `replicate` function, provide the number of replications and the code you want to be replicated. You can use {} to include multiple expressions that you'd like to be repeated.

```{r}
celtic_wins <- replicate(number_of_times_to_replicate, {
  first_command_to_run
  second_command_to_run
})
```

- You can use the `any` function to identify instances where any game in a simulated series contains a win.

```{r}
any(simulated_games=="win")
```

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# This line of example code simulates four independent random games where the Celtics either lose or win. Copy this example code to use within the `replicate` function.
simulated_games <- sample(c("lose","win"), 4, replace = TRUE, prob = c(0.6, 0.4))

# The variable 'B' specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Create an object called `celtic_wins` that replicates two steps for B iterations: (1) generating a random four-game series `simulated_games` using the example code, then (2) determining whether the simulated series contains at least one win for the Celtics.





# Calculate the frequency out of B iterations that the Celtics won at least one game. Print your answer to the console.
```

`@solution`
```{r}
# This line of example code simulates four independent random games where the Celtics either lose or win. Copy this example code to use within the `replicate` function.
simulated_games <- sample(c("lose","win"), 4, replace = TRUE, prob = c(0.6, 0.4))

# The variable 'B' specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Create an object called `celtic_wins` that replicates two steps for B iterations: (1) generating a random four-game series `simulated_games` using the example code, then (2) determining whether the simulated series contains at least one win for the Celtics. Put these steps on separate lines.
celtic_wins <- replicate(B, {
  simulated_games <- sample(c("lose","win"), 4, replace = TRUE, prob = c(0.6, 0.4))
  any(simulated_games=="win")
})

# Calculate the frequency out of B iterations that the Celtics won at least one game. Print your answer to the console. 
mean(celtic_wins)
```

`@sct`
```{r}
test_error()
test_output_contains("mean(celtic_wins)", incorrect_msg = "Make sure you use the `mean` function on the `celtic_wins` object.")
test_output_contains("0.8757", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you've executed the `set.seed(1)` command and have replicated the sample code over 10,000 iterations.")
success_msg("Great work!")
```

---

## End of Assessment: Independence and Multiplication Rule

```yaml
type: PureMultipleChoiceExercise
key: 52b168f93e
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
