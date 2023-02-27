---
title: 'Random Variables and Sampling Models'
description: 'In this chapter, you will learn about random variables and sampling models exploring an example looking at various aspects of the game of chance American Roulette.'
---

## Exercise 1. American Roulette probabilities

```yaml
type: NormalExercise
key: 17a22bbaee
lang: r
xp: 100
skills: 1
```

An American roulette wheel has 18 red, 18 black, and 2 green pockets. Each red and black pocket is associated with a number from 1 to 36. The two remaining green slots feature "0" and "00". Players place bets on which pocket they think a ball will land in after the wheel is spun. Players can bet on a specific number (0, 00, 1-36) or color (red, black, or green).  

What are the chances that the ball lands in a green pocket?

`@instructions`
- Define a variable `p_green` as the probability of the ball landing in a green pocket.
- Print the value of `p_green`.

`@hint`
- Calculate the proportion of pockets on the wheel that are green and assign that value to the variable `p_green`.
- To print the contents of a variable, write the variable name in a new line of code.

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# The variables `green`, `black`, and `red` contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket


# Print the variable `p_green` to the console

```

`@solution`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Print the variable `p_green` to the console
p_green

```

`@sct`
```{r}
test_error()
test_object("p_green", incorrect_msg = "Make sure that you use `p_green` as your variable name and that you have assigned the correct value to `p_green`.")
test_output_contains("0.05263158", incorrect_msg = "You are not providing a calculation that gives the correct answer. The probability of the ball landing in a green pocket is equal to the proportion of green pockets on the wheel. Make sure you print the value of `p_green` to the console.")
success_msg("Good job! Let's work on a similar problem.")
```

---

## Exercise 2. American Roulette payout

```yaml
type: NormalExercise
key: daff631ea7
lang: r
xp: 100
skills: 1
```

In American roulette, the payout for winning on green is $17. This means that if you bet $1 and it lands on green, you get $17 as a prize.

Create a model to predict your winnings from betting on green one time.

`@instructions`
- Use the `sample` function return a random value from a specified range of values.
- Use the `prob =` argument in the `sample` function to specify a vector of probabilities for returning each of the values contained in the vector of values being sampled.
- Take a single sample (n = 1).

`@hint`
The example code below shows the predicted outcome when betting on red, where the payout is $1. `win_red` and `lose_not_red` could be substituted for 1 and -1 in the `sample` vector.

```{r}
p_red <- 18/38
p_not_red <- 1-prob_red
red_outcome <- sample(c(1,-1), 1, prob = c(p_red, p_not_red))
red_outcome
```

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket


# Create a model to predict the random variable `X`, your winnings from betting on green. Sample one time.


# Print the value of `X` to the console


```

`@solution`
```{r}
# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Create a model to predict the random variable `X`, your winnings from betting on green. Sample one time.
X <- sample(c(17,-1), 1, prob = c(p_green, p_not_green))

# Print the value of `X` to the console
X
```

`@sct`
```{r}
test_error()
test_function("sample", args = c("x", "size", "prob"),eval=c(NA,NA,NA),
              not_called_msg = "Have you used `sample` to model the outcome of the bet?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of possible outcomes (winning $17 or losing $1), the number of times to sample from that vector (once), and the probability of each outcome using 'prob ='.",
              incorrect_msg = "Make sure to use the `sample` function. Include a vector of possible outcomes, the number of times to sample from that vector, and the chances of each outcome occurring.")
test_output_contains("-1", incorrect_msg = "You are not providing a calculation that gives the correct answer. Remember to sample one number from the possible outcomes: losing $1 or winning $17. Print the result to the console.")
success_msg("Great work! Let's move on to the next example.")
```

---

## Exercise 3. American Roulette expected value

```yaml
type: NormalExercise
key: 984c26e7e5
lang: r
xp: 100
skills: 1
```

In American roulette, the payout for winning on green is $17. This means that if you bet $1 and it lands on green, you get $17 as a prize.In the previous exercise, you created a model to predict your winnings from betting on green.

Now, compute the expected value of $X$, the random variable you generated previously.

`@instructions`
- Using the chances of winning $17 (`p_green`) and the chances of losing $1 (`p_not_green`), calculate the expected outcome of a bet that the ball will land in a green pocket.

`@hint`
The formula for expected value of a random variable is `ap + b(1-p)`, which multiples each possible outcome by its probability of occurring.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Calculate the expected outcome if you win $17 if the ball lands on green and you lose $1 if the ball doesn't land on green


```

`@solution`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Calculate the expected outcome if you win $17 if the ball lands on green and you lose $1 if the ball doesn't land on green
17*p_green + -1*p_not_green
```

`@sct`
```{r}
test_error()
test_output_contains("-0.05263158", incorrect_msg = "You are not providing a calculation that gives the correct answer. Use the formula for expected value, which is the sum of the individual outcomes for winning or losing multiplied by their chances of occurring.")
success_msg("Good work! Let's move on to another problem.")
```

---

## Exercise 4. American Roulette standard error

```yaml
type: NormalExercise
key: 6a709000c4
lang: r
xp: 100
skills: 1
```

The standard error of a random variable $X$ tells us the difference between a random variable and its expected value. You calculated a random variable $X$ in exercise 2 and the expected value of that random variable in exercise 3.

Now, compute the standard error of that random variable, which represents a single outcome after one spin of the roulette wheel.

`@instructions`
- Compute the standard error of the random variable you generated in exercise 2, or the outcome of any one spin of the roulette wheel.
- Recall that the payout for winning on green is $17 for a $1 bet.

`@hint`
- Given two possible outcomes, $a$ and $b$, with the probability of $a$ equal to $p$, the standard error of the random variable is given by the following equation:

$$\mid b - a \mid \sqrt{p(1-p)}$$

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Compute the standard error of the random variable

```

`@solution`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Compute the standard error of the random variable
abs((17 - -1))*sqrt(p_green*p_not_green)
```

`@sct`
```{r}
test_error()
test_function("abs",
             not_called_msg = "Remember to use `abs` take the absolute value of the difference in payouts, +$17 when winning and -$1 when losing.")
test_function("sqrt", args = "x",
              not_called_msg = "Have you used `sqrt` to calculate the standard error?",
              args_not_specified = "To calculate the standard error, find the square root of the product of the two probabilities.",
              incorrect_msg = "To calculate the standard error, find the square root of the product of the two probabilities.")
test_output_contains("4.019344", incorrect_msg = "You are not providing a calculation that gives the correct answer. Multiply the absolute value of the difference between the outcomes by the square root of the product of the probabilities of each outcome.")
success_msg("Great work! Let's work on another example.")
```

---

## Exercise 5. American Roulette sum of winnings

```yaml
type: NormalExercise
key: ddbf31d624
lang: r
xp: 100
skills: 1
```

You modeled the outcome of a single spin of the roulette wheel, $X$, in exercise 2. 

Now create a random variable $S$ that sums your winnings after betting on green 1,000 times.

`@instructions`
- Use `set.seed` to make sure the result of your random operation matches the expected answer for this problem.
- Specify the number of times you want to sample from the possible outcomes.
- Use the `sample` function to return a random value from a vector of possible values. 
- Be sure to assign a probability to each outcome and to indicate that you are sampling with replacement.
- Do not use `replicate` as this changes the output of random sampling and your answer will not match the grader.

`@hint`
- You should select 1,000 values from the possible values of 17 or -1.
- Use the argument 'replace = TRUE' in the `sample` function to indicate that sampling should be done with replacement.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define the number of bets using the variable 'n'


# Create a vector called 'X' that contains the outcomes of 1000 samples


# Assign the sum of all 1000 outcomes to the variable 'S'


# Print the value of 'S' to the console

```

`@solution`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define the number of bets using the variable 'n'
n <- 1000

# Create a vector called 'X' that contains the outcomes of 1000 samples
X <- sample(c(17,-1), size = n, replace = TRUE, prob = c(p_green, p_not_green))

# Assign the sum of all 1000 outcomes to the variable 'S'
S <- sum(X)

# Print the value of 'S' to the console
S
```

`@sct`
```{r}
test_error()
test_function("sample", args = c("x", "size", "replace", "prob"),eval=c(NA,T,T,NA),
              not_called_msg = "Have you used `sample` to model the outcome of the bet?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of possible outcomes (winning $17 or losing $1), the number of times to sample from that vector ('n'), that the sampling should be done with replacement 'replace = TRUE', and the probability of each outcome using 'prob ='.",
              incorrect_msg = "Make sure to use the `sample` function. Include a vector of possible outcomes, the number of times to sample from that vector, whether replacement should occur, and the chances of each outcome occurring.")
test_function("sum", args = "...",eval=F,
              not_called_msg = "Have you used `sum` to add up the outcomes of all 1,000 bets?",
              args_not_specified = "In the function `sum`, be sure to provide a vector of all 1,000 outcomes",
              incorrect_msg = "Make sure to use the `sum` function to add up all of the values contained in the vector 'X'.")
test_output_contains("-10", incorrect_msg = "You are not providing a calculation that gives the correct answer. Remember to sample 1,000 outcomes from the possible outcomes: losing $1 or winning $17. Print the result to the console.")
success_msg("Great work! Let's move on to the next example.")
```

---

## Exercise 6. American Roulette winnings expected value

```yaml
type: NormalExercise
key: 03e9dc02d5
lang: r
xp: 100
skills: 1
```

In the previous exercise, you generated a vector of random outcomes, $S$, after betting on green 1,000 times. 

What is the expected value of $S$?

`@instructions`
- Using the chances of winning $17 (`p_green`) and the chances of losing $1 (`p_not_green`), calculate the expected outcome of a bet that the ball will land in a green pocket over 1,000 bets.

`@hint`
- Use the formula for expected value to calculate the expected value of a single spin.
- Multiply the expected value of one spin by the total number of spins.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 1000

# Calculate the expected outcome of 1,000 spins if you win $17 when the ball lands on green and you lose $1 when the ball doesn't land on green

```

`@solution`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 1000

# Calculate the expected outcome of 1,000 spins if you win $17 when the ball lands on green and you lose $1 when the ball doesn't land on green
n * (17*p_green + -1*p_not_green)
```

`@sct`
```{r}
test_error()
test_output_contains("-52.63158", incorrect_msg = "You are not providing a calculation that gives the correct answer. Use the formula for expected value to calculate the expected value for a single spin. The expected value of multiple spins equals the number of spins times the expected value of one spin.")

success_msg("Good work! Let's move on to another problem.")
```

---

## Exercise 7. American Roulette winnings expected value

```yaml
type: NormalExercise
key: a487ce0739
lang: r
xp: 100
skills: 1
```

You generated the expected value of $S$, the outcomes of 1,000 bets that the ball lands in the green pocket, in the previous exercise. 

What is the standard error of $S$?

`@instructions`
- Compute the standard error of the random variable you generated in exercise 5, or the outcomes of 1,000 spins of the roulette wheel.

`@hint`
- Assume two possible outcomes, $a$ and $b$, with the probability of $a$ equal to $p$. When spins are independent, the standard error of the sum of outcomes is given by the following equation:

$$ \sqrt{\mbox{number of spins }} \times \mid b - a \mid \sqrt{p(1-p)}$$

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 1000

# Compute the standard error of the sum of 1,000 outcomes

```

`@solution`
```{r}
# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 1000

# Compute the standard error of the sum of 1,000 outcomes
sqrt(n) * abs((17 - -1))*sqrt(p_green*p_not_green)
```

`@sct`
```{r}
test_error()
test_function("abs", args = "x",eval=NA,
              not_called_msg = "Have you used `abs` to find the absolute value of the difference in payoffs?")
test_output_contains("127.1028", incorrect_msg = "You are not providing a calculation that gives the correct answer. Use the equation from class to calculate the standard error of the sum. To calculate the standard error of the sum, multiply the standard deviation for one roll by the square root of the number of rolls.")
success_msg("Great work!")
```

---

## End of Assessment: Random Variables and Sampling Models

```yaml
type: PureMultipleChoiceExercise
key: cdeb34e7c7
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
