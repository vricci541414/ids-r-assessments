---
title: 'The Addition Rule'
description: 'In this chapter, you will learn about the addition rule and the Monty Hall problem.'
---

## Exercise 1. The Cavs and the Warriors

```yaml
type: NormalExercise
key: 8292323f6e
lang: r
xp: 100
skills: 1
```

Two teams, say the Cavs and the Warriors, are playing a seven game championship series. The first to win four games wins the series. The teams are equally good, so they each have a 50-50 chance of winning each game. 

If the Cavs lose the first game, what is the probability that they win the series?

`@instructions`
- Assign the number of remaining games to the variable `n`.
- Assign a variable `outcomes` as a vector of possible outcomes in a single game, where 0 indicates a loss and 1 indicates a win for the Cavs.
- Assign a variable `l` to a list of all possible outcomes in all remaining games. Use the `rep` function to create a list of `n` games, where each game consists of `list(outcomes)`.
- Use the `expand.grid` function to create a data frame containing all the combinations of possible outcomes of the remaining games.
- Use the `rowSums` function to identify which combinations of game outcomes result in the Cavs winning the number of games necessary to win the series.
- Use the `mean` function to calculate the proportion of outcomes that result in the Cavs winning the series and print your answer to the console.

`@hint`
- Any combination of 4 or more wins across the 6 remaining games allows the Cavs to win the series.
- The `possibilities` data frame should contain one column for each remaining game.
- The `possibilities` data frame should contain one row for each combination of wins (1) or losses (0) for the next 6 games.
- `results` should be a logical vector.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign a variable 'n' as the number of remaining games.


# Assign a variable `outcomes` as a vector of possible game outcomes, where 0 indicates a loss and 1 indicates a win for the Cavs.


# Assign a variable `l` to a list of all possible outcomes in all remaining games. Use the `rep` function on `list(outcomes)` to create list of length `n`.


# Create a data frame named 'possibilities' that contains all combinations of possible outcomes for the remaining games.


# Create a vector named 'results' that indicates whether each row in the data frame 'possibilities' contains enough wins for the Cavs to win the series.


# Calculate the proportion of 'results' in which the Cavs win the series. Print the outcome to the console.
```

`@solution`
```{r}
# Assign a variable 'n' as the number of remaining games.
n <- 6

# Assign a variable `outcomes` as a vector of possible game outcomes, where 0 indicates a loss and 1 indicates a win for the Cavs.
outcomes <- c(0,1)

# Assign a variable `l` to a list of all possible outcomes in all remaining games. Use the `rep` function on `list(outcomes)` to create list of length `n`. 
l <- rep(list(outcomes), n)

# Create a data frame named 'possibilities' that contains all combinations of possible outcomes for the remaining games.
possibilities <- expand.grid(l)

# Create a vector named 'results' that indicates whether each row in the data frame 'possibilities' contains enough wins for the Cavs to win the series.
results <- rowSums(possibilities)>=4

# Calculate the proportion of 'results' in which the Cavs win the series. Print the outcome to the console.
mean(results)
```

`@sct`
```{r}
test_error()
test_output_contains("0.34375", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are finding possible series outcomes that contain at least 4 games won for the Cavs.")
success_msg("Great work! Let's move on to the next problem.")
```

---

## Exercise 2. The Cavs and the Warriors - Monte Carlo

```yaml
type: NormalExercise
key: 9409bd0725
lang: r
xp: 100
skills: 1
```

Confirm the results of the previous question with a Monte Carlo simulation to estimate the probability of the Cavs winning the series after losing the first game.

`@instructions`
- Use the `replicate` function to replicate the sample code for `B <- 10000` simulations.
- Use the `sample` function to simulate a series of 6 games with random, independent outcomes of either a loss for the Cavs (0) or a win for the Cavs (1) in that order. Use the default probabilities to sample.
- Use the `sum` function to determine whether a simulated series contained at least 4 wins for the Cavs.
- Use the `mean` function to find the proportion of simulations in which the Cavs win at least 4 of the remaining games. Print your answer to the console.

`@hint`
- To use the `replicate` function, provide the number of replications and the code you want to be replicated. You can use {} to include multiple expressions that you'd like to be repeated.
```{r}
results <- replicate(number_of_times_to_replicate, {
  first_command_to_run
  second_command_to_run
})
```

- You can use the `sample` function to simulate a series of 6 games where the outcome is either "0" for a Cav loss or "1" for a Cav win. The probabilities of each outcome are equal and independent.
```{r}
cavs_wins <- sample(c(0,1), 6, replace = TRUE)
```

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# The variable `B` specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Create an object called `results` that replicates for `B` iterations a simulated series and determines whether that series contains at least four wins for the Cavs.




# Calculate the frequency out of `B` iterations that the Cavs won at least four games in the remainder of the series. Print your answer to the console.
```

`@solution`
```{r}
# The variable `B` specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Create an object called `results` that replicates for `B` iterations a simulated series and determines whether that series contains at least four wins for the Cavs.
results <- replicate(B, {
  cavs_wins <- sample(c(0,1), 6, replace = TRUE)
  sum(cavs_wins)>=4 
})

# Calculate the frequency out of `B` iterations that the Cavs won at least four games in the remainder of the series. Print your answer to the console. 
mean(results)
```

`@sct`
```{r}
test_error()
test_output_contains("0.3453", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you sample from `c(0,1)` with replacement without changing default probabilities, and print your answer to the console.")
success_msg("Great work!")
```

---

## Exercise 3. A and B play a series - part 1

```yaml
type: NormalExercise
key: ffff9b2611
lang: r
xp: 100
skills: 1
```

Two teams, $A$ and $B$, are playing a seven series game series. Team $A$ is better than team $B$ and has a $p>0.5$ chance of winning each game.

`@instructions`
- Use the function `sapply` to compute the probability, call it `Pr` of winning for `p <- seq(0.5, 0.95, 0.025)`.
- Then plot the result `plot(p, Pr)`.

`@hint`
- Use the `sapply` function to apply a function over a vector. In this case, your vector is `p`, the sequence of probabilities. Your function is called `prob_win` and has been provided in the sample code.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Let's assign the variable 'p' as the vector of probabilities that team A will win.
p <- seq(0.5, 0.95, 0.025)

# Given a value 'p', the probability of winning the series for the underdog team B can be computed with the following function based on a Monte Carlo simulation:
prob_win <- function(p){
  B <- 10000
  result <- replicate(B, {
    b_win <- sample(c(1,0), 7, replace = TRUE, prob = c(1-p, p))
    sum(b_win)>=4
    })
  mean(result)
}

# Apply the 'prob_win' function across the vector of probabilities that team A will win to determine the probability that team B will win. Call this object 'Pr'.


# Plot the probability 'p' on the x-axis and 'Pr' on the y-axis.
```

`@solution`
```{r}
# Let's assign the variable 'p' as the vector of probabilities that team A will win.
p <- seq(0.5, 0.95, 0.025)

# Given a value 'p', the probability of winning the series for the underdog team B can be computed with the following function based on a Monte Carlo simulation:
prob_win <- function(p){
  B <- 10000
  result <- replicate(B, {
    b_win <- sample(c(1,0), 7, replace = TRUE, prob = c(1-p, p))
    sum(b_win)>=4
    })
  mean(result)
}

# Apply the 'prob_win' function across the vector of probabilities that team A will win to determine the probability that team B will win. Call this object 'Pr'.
Pr <- sapply(p, prob_win)

# Plot the probability 'p' on the x-axis and 'Pr' on the y-axis.
plot(p, Pr)
```

`@sct`
```{r}
test_error()
test_function("sapply",
    not_called_msg = "Make sure you use the `sapply` function to apply the function `prob_win` function across the vector of probabilities that team A will win.")
test_function("plot", not_called_msg = "Make sure you use the `plot` function to generate the plot where 'p' is on the x-axis and 'Pr' is on the y-axis.")
success_msg("Great work! Let's move on to the next example.")
```

---

## Exercise 4. A and B play a series - part 2

```yaml
type: NormalExercise
key: 097cd55746
lang: r
xp: 100
skills: 1
```

Repeat the previous exercise, but now keep the probability that team $A$ wins fixed at `p <- 0.75` and compute the probability for different series lengths. For example, wins in best of 1 game, 3 games, 5 games, and so on through a series that lasts 25 games.

`@instructions`
- Use the `seq` function to generate a list of odd numbers ranging from 1 to 25. 
- Use the function `sapply` to compute the probability, call it `Pr`, of winning during series of different lengths.
- Then plot the result `plot(N, Pr)`.

`@hint`
- Be sure to execute the code that generates the `prob_win` function.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Given a value 'p', the probability of winning the series for the underdog team B can be computed with the following function based on a Monte Carlo simulation:
prob_win <- function(N, p=0.75){
      B <- 10000
      result <- replicate(B, {
        b_win <- sample(c(1,0), N, replace = TRUE, prob = c(1-p, p))
        sum(b_win)>=(N+1)/2
        })
      mean(result)
    }

# Assign the variable 'N' as the vector of series lengths. Use only odd numbers ranging from 1 to 25 games.


# Apply the 'prob_win' function across the vector of series lengths to determine the probability that team B will win. Call this object `Pr`.


# Plot the number of games in the series 'N' on the x-axis and 'Pr' on the y-axis.
```

`@solution`
```{r}
# Given a value 'p', the probability of winning the series for the underdog team $B$ can be computed with the following function based on a Monte Carlo simulation:
prob_win <- function(N, p=0.75){
      B <- 10000
      result <- replicate(B, {
        b_win <- sample(c(1,0), N, replace = TRUE, prob = c(1-p, p))
        sum(b_win)>=(N+1)/2
        })
      mean(result)
    }

# Assign the variable 'N' as the vector of series lengths. Use only odd numbers ranging from 1 to 25 games.
N <- seq(1, 25, 2)

# Apply the 'prob_win' function across the vector of series lengths to determine the probability that team B will win. Call this object `Pr`.
Pr<- sapply(N, prob_win)

# Plot the number of games in the series 'N' on the x-axis and 'Pr' on the y-axis.
plot(N, Pr)
```

`@sct`
```{r}
test_error()
test_function("sapply",
    not_called_msg = "Make sure you use the `sapply` function to apply the function `prob_win` function across the vector of games.")
test_function("plot", not_called_msg = "Make sure you use the `plot` function to generate the plot where 'N' is on the x-axis and 'Pr' is on the y-axis.")
success_msg("Great work!")
```

---

## End of Assessment: The Addition Rule

```yaml
type: PureMultipleChoiceExercise
key: bddcce03c6
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
