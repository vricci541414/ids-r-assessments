---
title: 'The Central Limit Theorem'
description: 'In this chapter, you will learn about the Central Limit Theorem and compare results from Monte Carlo simulations to those obtained using the Central Limit Theorem for games of chance.'
---

## Exercise 1. American Roulette probability of winning money

```yaml
type: NormalExercise
key: 6bfcfb6d3c
lang: r
xp: 100
skills: 1
```

The exercises in the previous chapter explored winnings in American roulette. In this chapter of exercises, we will continue with the roulette example and add in the Central Limit Theorem.

In the previous chapter of exercises, you created a random variable $S$ that is the sum of your winnings after betting on green a number of times in American Roulette.

What is the probability that you end up winning money if you bet on green 100 times?

`@instructions`
- Execute the sample code to determine the expected value `avg` and standard error `se` as you have done in previous exercises.
- Use the `pnorm` function to determine the probability of winning money.

`@hint`
- The Central Limit Theorem tells us that the sum of expected outcomes is approximated by a normal distribution. Therefore, we can use the `pnorm` function to determine the odds of winning money given the expected value and standard error.
- The probability of winning money is equal to 1 minus the odds of earning less than $0.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 100

# Calculate 'avg', the expected outcome of 100 spins if you win $17 when the ball lands on green and you lose $1 when the ball doesn't land on green
avg <- n * (17*p_green + -1*p_not_green)

# Compute 'se', the standard error of the sum of 100 outcomes
se <- sqrt(n) * (17 - -1)*sqrt(p_green*p_not_green)

# Using the expected value 'avg' and standard error 'se', compute the probability that you win money betting on green 100 times.

```

`@solution`
```{r}
# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 100

# Calculate 'avg', the expected outcome of 100 spins if you win $17 when the ball lands on green and you lose $1 when the ball doesn't land on green
avg <- n * (17*p_green + -1*p_not_green)

# Compute 'se', the standard error of the sum of 100 outcomes
se <- sqrt(n) * (17 - -1)*sqrt(p_green*p_not_green)

# Using the expected value 'avg' and standard error 'se', compute the probability that you win money betting on green 100 times. 
1 - pnorm(0, avg,se)
```

`@sct`
```{r}
test_error()
test_function("pnorm", args = c("q", "mean", "sd"),
              not_called_msg = "Have you used `pnorm` to calculate the probability of winning money?",
              args_not_specified = "To calculate the probability of winning money, use `pnorm` to return the probability of earning less than a given amount from a distribution with a specific expected value and standard error.",
              incorrect_msg = "To calculate probability of winning money, first use `pnorm` to calculate the probability of earning less than $0 given a certain expected value and standard error.")
test_output_contains("0.4479091", incorrect_msg = "Your code does not give the correct answer. Use `pnorm` to compute the probability of losing money (earning less than $0). Then, subtract this value from 1 to determine the probability of winning money.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 2. American Roulette Monte Carlo simulation

```yaml
type: NormalExercise
key: 2e3f830682
lang: r
xp: 100
skills: 1
```

Create a Monte Carlo simulation that generates 10,000 outcomes of $S$, the sum of 100 bets. 

Compute the average and standard deviation of the resulting list and compare them to the expected value (-5.263158) and standard error (40.19344) for $S$ that you calculated previously.

`@instructions`
- Use the `replicate` function to replicate the sample code for `B <- 10000` simulations.
- Within `replicate`, use the `sample` function to simulate `n <- 100` outcomes of either a win (17) or a  loss (-1) for the bet. Use the order `c(17, -1)` and corresponding probabilities. Then, use the `sum` function to add up the winnings over all iterations of the model. _Make sure to include `sum` or DataCamp may crash with a "Session Expired" error._
- Use the `mean` function to compute the average winnings.
- Use the `sd` function to compute the standard deviation of the winnings.

`@hint`
- To use `replicate`, provide the number of replications (`B`) and the code you want to repeat. You can use {} to include multiple expressions to be repeated.

```{r}
results <- replicate(B, {
  command_1
  command_2
})
```

- Use `sample` to simulate the outcomes of `n` bets. The following code demonstrates `sample` with outcomes `a`, `b` given probabilities `p_a` and `p_b`.

```{r}
outcomes <- sample(c(a,b), n, replace = TRUE, prob = c(p_a, p_b))
```

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 100

# The variable `B` specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Create an object called `S` that replicates the sample code for `B` iterations and sums the outcomes.




# Compute the average value for 'S'


# Calculate the standard deviation of 'S'


```

`@solution`
```{r}
# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 100

# The variable `B` specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Create an object called `S` that replicates the sample code for `B` iterations and sums the outcomes.
S <- replicate(B,{  
  X <- sample(c(17,-1), size = n, replace = TRUE, prob = c(p_green, p_not_green))
  sum(X)
})

# Compute the average value for 'S'
mean(S)

# Calculate the standard deviation of 'S'
sd(S)
```

`@sct`
```{r}
test_error()
test_function("set.seed", args = "seed",
             not_called_msg = "Did you call `set.seed(1)` before sampling?",
             incorrect_msg = "The seed should be set to 1.")
test_function("sample", args = c("x", "size", "replace", "prob"),
              not_called_msg = "Have you used `sample` to model the outcome of `n` bets?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of possible outcomes ('-1' for losing or '17' for winning), the number of times to sample from that vector (`n`), that the sampling should be done with replacement 'replace = TRUE', and the probability of each outcome using 'prob ='.",
              incorrect_msg = "When generating `S`, be sure to use the `sample` function. Include a vector of possible outcomes, the number of times to sample from that vector, whether replacement should occur, and the chances of each outcome occurring.")
test_function("mean", args = "x",
              not_called_msg = "Have you used `mean` to compute the average outcome of all bets across 10,000 simulations?",
              args_not_specified = "In the function `mean`, be sure to provide a vector of all modeled outcomes",
              incorrect_msg = "Make sure to use the `mean` function to average all the values in the vector 'S'.")
test_function("sd", args = "x",
              not_called_msg = "Have you used `sd` to compute the standard deviation of 'S'?",
              args_not_specified = "In the function `sd`, be sure to provide a vector of all modeled outcomes, 'S'.",
              incorrect_msg = "Make sure to use the `sd` function to compute the standard deviation of values in the vector 'S'.")
test_output_contains("-5.9086", incorrect_msg = "Your code does not print the correct mean to the console. Make sure your `sample` call is correct and print the result of the `mean` function to the console.")
test_output_contains("40.30608", incorrect_msg = "Your code does not print the correct standard deviation to the console. Make sure your `sample` call is correct and print the result of the `sd` function to the console.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 3. American Roulette Monte Carlo vs CLT

```yaml
type: NormalExercise
key: 58b951feb7
lang: r
xp: 100
skills: 1
```

In this chapter, you calculated the probability of winning money in American roulette using the CLT. 

Now, calculate the probability of winning money from the Monte Carlo simulation. The Monte Carlo simulation from the previous exercise has already been pre-run for you, resulting in the variable `S` that contains a list of 10,000 simulated outcomes.

`@instructions`
- Use the `mean` function to calculate the probability of winning money from the Monte Carlo simulation, `S`.

`@hint`
- The probability of winning money is equal to the proportion of simulated outcomes that result in more than $0 in earnings.
- Use the `mean` function to calculate the proportion of values in `S` that are greater than $0.

`@pre_exercise_code`
```{r}
set.seed(1)
B <- 10000
S <- replicate(B,{  
  X <- sample(c(17,-1), size = 100, replace = TRUE, prob = c(1/19, 18/19))
  sum(X)
})
```

`@sample_code`
```{r}
# Calculate the proportion of outcomes in the vector `S` that exceed $0
```

`@solution`
```{r}
# Calculate the proportion of outcomes in the vector `S` that exceed $0
mean(S>0)
```

`@sct`
```{r}
test_error()
test_function("mean", args = "x",
              not_called_msg = "Have you used `mean` to compute the average outcome of all bets across 10,000 simulations?",
              args_not_specified = "In the function `mean`, be sure to provide a vector of all modeled outcomes",
              incorrect_msg = "Make sure to use the `mean` function to average all the values in the vector 'S' that are greater than 0.")
test_output_contains("0.4232", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you've executed the `mean` command to compute the proportion of outcomes that exceed $0. Print the result of the `mean` function to the console.")
success_msg("Great job! Let's move on.")
```

---

## Exercise 4. American Roulette Monte Carlo vs CLT comparison

```yaml
type: MultipleChoiceExercise
key: 7c50de397b
lang: r
xp: 50
skills: 1
```

The Monte Carlo result and the CLT approximation for the probability of losing money after 100 bets are close, but not that close. What could account for this?

`@possible_answers`
- 10,000 simulations is not enough. If we do more, the estimates will match.
- The CLT does not work as well when the probability of success is small.
- The difference is within rounding error.
- The CLT only works for the averages.

`@hint`
- The odds of success affects the appropriateness of the CLT.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. The CLT has limitations to consider."
msg2 = "Correct! If we make the number of roulette plays bigger, the probabilities will match better."
msg3 = "Try again. The difference between the CLT and Monte Carlo estimates is a consequence of the odds associated with winning."
msg4 = "Try again. The CLT works better under certain conditions."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 5. American Roulette average winnings per bet

```yaml
type: NormalExercise
key: 81bffe1ba3
lang: r
xp: 100
skills: 1
```

Now create a random variable $Y$ that contains your average winnings per bet after betting on green 10,000 times.

`@instructions`
- Run a _single_ Monte Carlo simulation of 10,000 bets using the following steps. (You do _not_ need to `replicate` the `sample` code.)
- Specify `n` as the number of times you want to sample from the possible outcomes.
- Use the `sample` function to return `n` values from a vector of possible values: winning $17 or losing $1. Be sure to assign a probability to each outcome and indicate that you are sampling with replacement.
- Calculate the average result per bet placed using the `mean` function.

`@hint`
- You should sample 10,000 values from the possible values of 17 or -1.
- Use the argument 'replace = TRUE' in the `sample` function to indicate that sampling should be done with replacement.
- Use the argument 'prob' in the `sample` function to indicate the probability of winning $17 or losing $1.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Define the number of bets using the variable 'n'
n <- 10000

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1 - p_green

# Create a vector called `X` that contains the outcomes of `n` bets


# Define a variable `Y` that contains the mean outcome per bet. Print this mean to the console.
```

`@solution`
```{r}
# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Define the number of bets using the variable 'n'
n <- 10000

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1 - p_green

# Create a vector called `X` that contains the outcomes of `n` bets
X <- sample(c(17,-1), size = n, replace = TRUE, prob = c(p_green, p_not_green))

# Define a variable `Y` that contains the mean outcome per bet. Print this mean to the console.
Y <- mean(X)
Y
```

`@sct`
```{r}
test_error()
test_function("sample", args = c("x", "size", "replace", "prob"),eval=c(NA,T,T,NA),
              not_called_msg = "Have you used `sample` to model the outcome of `n` bets?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of possible outcomes (winning $17 or losing $1), the number of times to sample from that vector (`n`), that the sampling should be done with replacement 'replace = TRUE', and the probability of each outcome using 'prob ='.",
              incorrect_msg = "When generating `X`, be sure to use the `sample` function. Include a vector of possible outcomes, the number of times to sample from that vector, whether replacement should occur, and the chances of each outcome occurring.")
test_function("mean", args = "x",eval=NA,
              not_called_msg = "Have you used `mean` to find the average outcome of all 10,000 bets?",
              args_not_specified = "In the function `mean`, be sure to provide a vector of all 10,000 outcomes",
              incorrect_msg = "Make sure to use the `mean` function to average the values contained in the vector `X`.")
test_object("Y", incorrect_msg = "You are not providing a calculation that gives the correct final answer for `Y`. Remember to sample 10,000 outcomes from the possible outcomes: losing $1 or winning $17. Print the average result per bet to the console.")
success_msg("Great work! Let's move on to the next example.")
```

---

## Exercise 6. American Roulette per bet expected value

```yaml
type: NormalExercise
key: 0ca63a9bcc
lang: r
xp: 100
skills: 1
```

What is the expected value of $Y$, the average outcome per bet after betting on green 10,000 times?

`@instructions`
- Using the chances of winning $17 (`p_green`) and the chances of losing $1 (`p_not_green`), calculate the expected outcome of a bet that the ball will land in a green pocket.
- Use the expected value formula rather than a Monte Carlo simulation.
- Print this value to the console (do not assign it to a variable).

`@hint`
- The expected value of the average is the average of the outcomes.
- Multiply the outcome for winning or losing by the odds of each event.
- Add these values to generate the overall expected outcome.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1 - p_green

# Calculate the expected outcome of `Y`, the mean outcome per bet in 10,000 bets
```

`@solution`
```{r}
# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1 - p_green

# Use the expected value formula to calculate the expected outcome of `Y`, the mean outcome per bet in 10,000 bets
17*p_green + -1*p_not_green
```

`@sct`
```{r}
test_error()
test_output_contains("-0.05263158", incorrect_msg = "You are not providing a calculation that gives the correct answer. The expected outcome of a single spin is the sum of the individual outcomes for winning or losing multiplied by their chances of occurring.")
success_msg("Good work! Let's move on to another problem.")
```

---

## Exercise 7. American Roulette per bet standard error

```yaml
type: NormalExercise
key: f196e480ed
lang: r
xp: 100
skills: 1
```

What is the standard error of $Y$, the average result of 10,000 spins?

`@instructions`
- Compute the standard error of $Y$, the average result of 10,000 independent spins.

`@hint`
- Given two possible outcomes, $a$ and $b$, with the probability of $a$ equal to $p$, you can calculate the standard deviation using the equation:

$$\mid b - a \mid \sqrt{p(1-p)}$$
- The standard error of the average of the outcomes is equal to the standard deviation divided by the square root of `n`.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Define the number of bets using the variable 'n'
n <- 10000

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1 - p_green

# Compute the standard error of 'Y', the mean outcome per bet from 10,000 bets.
```

`@solution`
```{r}
# Define the number of bets using the variable 'n'
n <- 10000

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1 - p_green

# Compute the standard error of 'Y', the mean outcome per bet from 10,000 bets.
abs((17 - -1))*sqrt(p_green*p_not_green) / sqrt(n)
```

`@sct`
```{r}
test_error()
test_function("abs", args = "x",eval=NA,
              not_called_msg = "Have you used `abs` to find the absolute value of the difference in payoffs?")
test_function("sqrt", args = "x",eval=NA,
              not_called_msg = "Have you used `sqrt` to calculate the standard error? You need to find the square roots of two differnt values.",
              args_not_specified = "The arguments of the `sqrt` function should match the values you want to find the square root of.",
              incorrect_msg = "To calculate the standard error, you'll need to find the square roots of two values: the number of bets and the product of probabilities.")
test_output_contains("0.04019344", incorrect_msg = "You are not providing a calculation that gives the correct answer. Don't forget to divide by the square root of the number of bets.")
success_msg("Great work! Let's move on.")
```

---

## Exercise 8. American Roulette winnings per game are positive

```yaml
type: NormalExercise
key: 3878f868bb
lang: r
xp: 100
skills: 1
```

What is the probability that your winnings are positive after betting on green 10,000 times?

`@instructions`
- Execute the code that we wrote in previous exercises to determine the average and standard error.
- Use the `pnorm` function to determine the probability of winning more than $0.

`@hint`
- We can use the `pnorm` function to determine the odds of winning money given the expected value and standard error.
- The probability of winning money is equal to 1 minus the odds of earning less than $0.

`@pre_exercise_code`
```{r}
n <- 10000
p_green <- 2/38
p_not_green <- 1-p_green
```

`@sample_code`
```{r}
# We defined the average using the following code
avg <- 17*p_green + -1*p_not_green

# We defined standard error using this equation
se <- 1/sqrt(n) * (17 - -1)*sqrt(p_green*p_not_green)

# Given this average and standard error, determine the probability of winning more than $0. Print the result to the console.

```

`@solution`
```{r}
# We defined the average using the following code
avg <- 17*p_green + -1*p_not_green

# We defined standard error using this equation
se <- 1/sqrt(n) * (17 - -1)*sqrt(p_green*p_not_green)

# Given this average and standard error, determine the probability of winning more than $0. Print the result to the console.
1 - pnorm(0, avg, se)
```

`@sct`
```{r}
test_error()
test_function("pnorm", args = c("q", "mean", "sd"),
              not_called_msg = "Have you used `pnorm` to calculate the probability of winning money?",
              args_not_specified = "To calculate the probability of winning money, use `pnorm` to return the probability of earning less than a given amount from a distribution with a specific average and standard error.",
              incorrect_msg = "To calculate probability of winning money, first use `pnorm` to calculate the probability of earning less than $0 given a certain expected value and standard error.")
test_output_contains("0.0951898", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are using the `pnorm` function twice to compute the probability of earning less than $0. Subtract this probability from 1 to determine the odds of winning money.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 9. American Roulette Monte Carlo again

```yaml
type: NormalExercise
key: 38a796ccfb
lang: r
xp: 100
skills: 1
```

Create a Monte Carlo simulation that generates 10,000 outcomes of $S$, the average outcome from 10,000 bets on green. 

Compute the average and standard deviation of the resulting list to confirm the results from previous exercises using the Central Limit Theorem.

`@instructions`
- Use the `replicate` function to model 10,000 iterations of a series of 10,000 bets.
- Each iteration inside `replicate` should simulate 10,000 bets and determine the average outcome of those 10,000 bets. _If you forget to take the mean, DataCamp will crash with a "Session Expired" error._
- Find the average of the 10,000 average outcomes. Print this value to the console.
- Compute the standard deviation of the 10,000 simulations. Print this value to the console.

`@hint`
- To use the `replicate` function, provide the number of replications and the code you want to be replicated. You can use {} to include multiple expressions that you'd like to be repeated.

`@pre_exercise_code`
```{r}
p_green <- 2/38
p_not_green <- 1-p_green
```

`@sample_code`
```{r}
## Make sure you fully follow instructions, including printing values to the console and correctly running the `replicate` loop. If not, you may encounter "Session Expired" errors.

# The variable `n` specifies the number of independent bets on green
n <- 10000

# The variable `B` specifies the number of times we want the simulation to run
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random number generation
set.seed(1)

# Generate a vector `S` that contains the the average outcomes of 10,000 bets modeled 10,000 times





# Compute the average of `S`


# Compute the standard deviation of `S`

```

`@solution`
```{r}
## Make sure you fully follow instructions, including printing values to the console and correctly running the `replicate` loop. If not, you may encounter "Session Expired" errors.

# The variable `n` specifies the number of independent bets on green
n <- 10000

# The variable `B` specifies the number of times we want the simulation to run
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random number generation
set.seed(1)

# Generate a vector `S` that contains the the average outcomes of 10,000 bets modeled 10,000 times
S <- replicate(B,{  
  X <- sample(c(17,-1), size = n, replace = TRUE, prob = c(p_green, p_not_green))
  mean(X)
})

# Compute the average of `S`. Print this value to the console.
mean(S)

# Compute the standard deviation of `S`. Print this value to the console.
sd(S)
```

`@sct`
```{r}
test_error()
test_function("sample", args = c("x", "size", "replace", "prob"),eval=c(NA,T,T,NA),
              not_called_msg = "Have you used `sample` to model the outcome of `n` bets?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of possible outcomes (winning $17 or losing $1), the number of times to sample from that vector (`n`), that the sampling should be done with replacement 'replace = TRUE', and the probability of each outcome using 'prob ='.",
              incorrect_msg = "When generating `outcomes`, be sure to use the `sample` function. Include a vector of possible outcomes, the number of times to sample from that vector, whether replacement should occur, and the chances of each outcome occurring.")
test_function("mean", args = "x", index = 2,eval=NA,
              not_called_msg = "Have you used `mean` to find the average of the 10,000 simulations?",
              args_not_specified = "Make sure to use the `mean` function to average the results from the 10,000 simulations.",
              incorrect_msg = "Make sure to use the `mean` function to average the from the 10,000 simulations.")
test_function("sd", args = "x",eval=NA,
              not_called_msg = "Have you used `sd` to find the standard deviation of the 10,000 simulations?",
              args_not_specified = "Make sure to use the `sd` function to calculate the standard deviation of `S`.",
              incorrect_msg = "Make sure to use the `sd` function to calculate the standard deviation of `S`.")
test_output_contains("-0.05223142", incorrect_msg = "You are not providing a calculation that gives the correct answer. Remember to average the results of 10,000 simulations. Print the result to the console.")
test_output_contains("0.03996168", incorrect_msg = "You are not providing a calculation that gives the correct answer. Use the `sd` function to find the standard deviation of `S`. Print the result to the console.")
success_msg("Great work! Let's move on to the next calculation.")
```

---

## Exercise 10. American Roulette comparison

```yaml
type: NormalExercise
key: 457a0e7c3e
lang: r
xp: 100
skills: 1
```

In a previous exercise, you found the probability of winning more than $0 after betting on green 10,000 times using the Central Limit Theorem. Then, you used a Monte Carlo simulation to model the average result of betting on green 10,000 times over 10,000 simulated series of bets. 

What is the probability of winning more than $0 as estimated by your Monte Carlo simulation? The code to generate the vector `S` that contains the the average outcomes of 10,000 bets modeled 10,000 times has already been run for you.

`@instructions`
- Calculate the probability of winning more than $0 in the Monte Carlo simulation from the previous exercise using the `mean` function.
- You do _not_ need to run another simulation: the results of the simulation are in your workspace as the vector `S`.

`@hint`
- Use the `mean` function to calculate proportion of outcomes that won more than $0
- You do _not_ need to run another simulation. "Session expired" errors mean that you are incorrectly running another simulation. Use `S`.

`@pre_exercise_code`
```{r}
set.seed(1)
n <- 10000
B <- 10000
S <- replicate(B,{  
  X <- sample(c(17,-1), size = n, replace = TRUE, prob = c(1/19, 18/19))
  mean(X)
})
```

`@sample_code`
```{r}
# Compute the proportion of outcomes in the vector 'S' where you won more than $0

```

`@solution`
```{r}
# Compute the proportion of outcomes in the vector 'S' where you won more than $0
mean(S>0)
```

`@sct`
```{r}
test_error()
test_function("mean", args = "x",
              not_called_msg = "Have you used `mean` to find the proportion of values in `S` where the result is greater than 0?",
              args_not_specified = "Make sure to use the `mean` function to find the proportion of values in `S` where the outcome was more than $0.",
              incorrect_msg = "Make sure to use the `mean` function to find the proportion of values in `S` where the outcome was more than $0.")
test_output_contains("0.0977", incorrect_msg = "You are not providing a calculation that gives the correct answer. Find the proportion of results in `S` where the outcome was more than $0")
success_msg("Great work! Let's move on to the next question.")
```

---

## Exercise 11. American Roulette comparison analysis

```yaml
type: MultipleChoiceExercise
key: 33a1d813b7
lang: r
xp: 50
skills: 1
```

The Monte Carlo result and the CLT approximation are now much closer than when we calculated the probability of winning for 100 bets on green. What could account for this difference?

`@possible_answers`
- We are now computing averages instead of sums.
- 10,000 Monte Carlo simulations was not enough to provide a good estimate.
- The CLT works better when the sample size is larger. 
- It is not closer. The difference is within rounding error.

`@hint`
- With very low probabilities, the CLT requires more data.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. Consider what changed between our first and second estimations."
msg2 = "Try again. We used 10,000 Monte Carlo simulations both times, but we changed the number of bets."
msg3 = "Correct! We increased the sample size from 100 bets to 10,000 bets."
msg4 = "Try again. The values are closer because we changed an important parameter."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## End of Assessment: The Central Limit Theorem

```yaml
type: PureMultipleChoiceExercise
key: 382c4e1c59
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
