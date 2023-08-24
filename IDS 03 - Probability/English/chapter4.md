---
title: 'Continuous Probability'
description: 'In this chapter, you will learn about continuous probability through the use of examples involving the distribution of heights and IQ scores.'
---

## Exercise 1. Distribution of female heights - 1

```yaml
type: NormalExercise
key: 11e7f2f0ae
lang: r
xp: 100
skills: 1
```

Assume the distribution of female heights is approximated by a normal distribution with a mean of 64 inches and a standard deviation of 3 inches. If we pick a female at random, what is the probability that she is 5 feet or shorter?

`@instructions`
- Use `pnorm` to define the probability that a height will take a value less than 5 feet given the stated distribution.

`@hint`
- Make sure you convert the height in feet to match the units of the average and standard deviation.

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is shorter than 5 feet. Print this value to the console.


```

`@solution`
```{r}
# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is shorter than 5 feet. Print this value to the console - do not save it to a variable.
pnorm(5*12, female_avg, female_sd)

```

`@sct`
```{r}
test_error()
test_function("pnorm", args = c("q", "mean", "sd"),
              not_called_msg = "Have you used `pnorm` to calculate the probability?",
              args_not_specified = "Make sure to specify the height to calculate the probability, the average height, and standard deviation.",
              incorrect_msg = "Make sure to use `pnorm`. Include the height you want to test (in inches), the average height, and the standard deviation.")
test_output_contains("0.09121122", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you convert the height in feet to inches when using the `pnorm` function.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 2. Distribution of female heights - 2

```yaml
type: NormalExercise
key: 8410d1762c
lang: r
xp: 100
skills: 1
```

Assume the distribution of female heights is approximated by a normal distribution with a mean of 64 inches and a standard deviation of 3 inches. If we pick a female at random, what is the probability that she is 6 feet or taller?

`@instructions`
- Use `pnorm` to define the probability that a height will take a value of 6 feet or taller.

`@hint`
- Make sure you convert the height in feet to match the units of the average and standard deviation.
- The probability that a randomly selected female is 6 feet or taller equals 1 minus the probability that she is shorter than 6 feet.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is 6 feet or taller. Print this value to the console.

```

`@solution`
```{r}
# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is 6 feet or taller. Print this value to the console.
1 - pnorm(6*12, female_avg, female_sd)
```

`@sct`
```{r}
test_error()
test_function("pnorm", args = c("q", "mean", "sd"),
              not_called_msg = "Have you used `pnorm` to calculate the probability?",
              args_not_specified = "Make sure to specify the height to calculate the probability, the average height, and standard deviation.",
              incorrect_msg = "Make sure to use `pnorm`. Include the height you want to test (in inches), the average height, and the standard deviation.")
test_output_contains("0.003830381", incorrect_msg = "You are not providing a calculation that gives the correct answer. Remember that the `pnorm` function calculates the probability that a randomly chosen height is below the given value.")
success_msg("Great work! Let's work on another example.")
```

---

## Exercise 3. Distribution of female heights - 3

```yaml
type: NormalExercise
key: b5bca841f3
lang: r
xp: 100
skills: 1
```

Assume the distribution of female heights is approximated by a normal distribution with a mean of 64 inches and a standard deviation of 3 inches. If we pick a female at random, what is the probability that she is between 61 and 67 inches?

`@instructions`
- Use `pnorm` to define the probability that a randomly chosen woman will be shorter than 67 inches.
- Subtract the probability that a randomly chosen will be shorter than 61 inches.

`@hint`
- Subtract the probability of a woman being shorter than 61 inches from the probability of her being shorter than 67 inches.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.

```

`@solution`
```{r}
# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.
pnorm(67, female_avg, female_sd) - pnorm(61, female_avg, female_sd)
```

`@sct`
```{r}
test_error()
test_function("pnorm", args = c("q", "mean", "sd"),
              not_called_msg = "Have you used `pnorm` to calculate the probability?",
              args_not_specified = "Make sure to specify the average height and standard deviation in the `pnorm` function.",
              incorrect_msg = "Make sure to use `pnorm`. Include the height you want to test, the average height, and the standard deviation.")
test_output_contains("0.6826895", incorrect_msg = "You are not providing a calculation that gives the correct answer. Remember to subtract the probability of being shorter than 61 inches from the probability of being shorter than 67 inches.")
success_msg("Great job! Let's try another problem.")
```

---

## Exercise 4. Distribution of female heights - 4

```yaml
type: NormalExercise
key: 28e74ae71e
lang: r
xp: 100
skills: 1
```

Repeat the previous exercise, but convert everything to centimeters. That is, multiply every height, including the standard deviation, by 2.54. What is the answer now?

`@instructions`
- Convert the average height and standard deviation to centimeters by multiplying each value by 2.54.
- Repeat the previous calculation using `pnorm` to define the probability that a randomly chosen woman will have a height between 61 and 67 inches, converted to centimeters by multiplying each value by 2.54.

`@hint`
- Remember to multiply all values by 2.54 to convert them to centimeters.
- Use `pnorm` to define the probability that a randomly chosen woman will be shorter than a given height.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign a variable 'female_avg' as the average female height. Convert this value to centimeters.
female_avg <- 64*2.54

# Assign a variable 'female_sd' as the standard deviation for female heights. Convert this value to centimeters.
female_sd <- 3*2.54

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.

```

`@solution`
```{r}
# Assign a variable 'female_avg' as the average female height. Convert this value to centimeters.
female_avg <- 64*2.54

# Assign a variable 'female_sd' as the standard deviation for female heights. Convert this value to centimeters.
female_sd <- 3*2.54

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.
pnorm(67*2.54, female_avg, female_sd) - pnorm(61*2.54, female_avg, female_sd)
```

`@sct`
```{r}
test_error()
test_function("pnorm", args = c("q", "mean", "sd"), index = 1,
              not_called_msg = "Have you used `pnorm` to calculate the probability?",
              args_not_specified = "Make sure to specify the average height and standard deviation in the `pnorm` function.",
              incorrect_msg = "Make sure to use `pnorm`. Include the height you want to test (in cm), the average height, and the standard deviation.")
test_function("pnorm", args = c("q", "mean", "sd"), index = 2,
              not_called_msg = "Have you used `pnorm` a second time to calculate the probability that a woman is shorter than 61 inches?",
              args_not_specified = "Make sure to use `pnorm` to calculate the probability that a randomly selected female is shorter than 61 inches. Include the height you want to test (convert to cm), the average height, and the standard deviation.",
              incorrect_msg = "Make sure to use `pnorm` to calculate the probability that a randomly selected female is shorter than 61 inches. Include the height you want to test (convert to cm), the average height, and the standard deviation.") 
test_output_contains("0.6826895", incorrect_msg = "You are not providing a calculation that gives the correct answer. Remember to convert every value to centimeters by multiplying by 2.54.")
success_msg("Good job! Notice that the answer to the question does not change when you change units. This makes sense because the answer to the question should not be affected by which units we use. In fact, if you look closely, you notice that 61 and 67 are both 1 SD away from the average.")
```

---

## Exercise 5. Probability of 1 SD from average

```yaml
type: NormalExercise
key: 2b5ec0d0c5
lang: r
xp: 100
skills: 1
```

Compute the probability that the height of a randomly chosen female is within 1 SD from the average height.

`@instructions`
- Calculate the values for heights one standard deviation taller and shorter than the average.
- Calculate the probability that a randomly chosen woman will be within 1 SD from the average height.

`@hint`
- Use `pnorm` to define the probability that a randomly chosen woman will be shorter than 1 SD above average.
- Subtract the probability that a randomly chosen will be 1 SD shorter than average.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# To a variable named 'taller', assign the value of a height that is one SD taller than average.


# To a variable named 'shorter', assign the value of a height that is one SD shorter than average.


# Calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.

```

`@solution`
```{r}
# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# To a variable named 'taller', assign the value of a height that is one SD taller than average.
taller <- female_avg+female_sd

# To a variable named 'shorter', assign the value of a height that is one SD shorter than average.
shorter <- female_avg-female_sd

# Calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.
pnorm(taller, female_avg, female_sd) - pnorm(shorter, female_avg, female_sd)
```

`@sct`
```{r}
test_error()
test_function("pnorm", args = c("q", "mean", "sd"), index = 1,
              not_called_msg = "Have you used `pnorm` to calculate the probability?",
              args_not_specified = "Make sure to specify the average height and standard deviation in the `pnorm` function.",
              incorrect_msg = "Make sure to use `pnorm`. Include the height you want to test, the average height, and the standard deviation.")
test_function("pnorm", args = c("q", "mean", "sd"), index = 2,
              not_called_msg = "Have you used `pnorm` a second time to calculate the probability of being shorter than average?",
              args_not_specified = "Make sure to specify the average height and standard deviation in the `pnorm` function.",
              incorrect_msg = "Make sure to use `pnorm` to calculate the probability of being shorter than average. Include the height you want to test, the average height, and the standard deviation.") 
test_output_contains("0.6826895", incorrect_msg = "You are not providing a calculation that gives the correct answer. Remember to subtract the probability of being more than 1 SD shorter than average from the probability of being shorter than 1 SD above average.")
success_msg("Great job! Let's try another problem.")
```

---

## Exercise 6. Distribution of male heights

```yaml
type: NormalExercise
key: 600dc1f164
lang: r
xp: 100
skills: 1
```

Imagine the distribution of male adults is approximately normal with an average of 69 inches and a standard deviation of 3 inches. How tall is a male in the 99th percentile?

`@instructions`
- Determine the height of a man in the 99th percentile, given an average height of 69 inches and a standard deviation of 3 inches.

`@hint`
- The function `qnorm` provides the opposite information as `pnorm`. Instead of calculating the probability of a person being a certain height given a distribution of heights, `qnorm` tells you the height at a given quantile of the distribution.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign a variable 'male_avg' as the average male height.
male_avg <- 69

# Assign a variable 'male_sd' as the standard deviation for male heights.
male_sd <- 3

# Determine the height of a man in the 99th percentile of the distribution.

```

`@solution`
```{r}
# Assign a variable 'male_avg' as the average male height.
male_avg <- 69

# Assign a variable 'male_sd' as the standard deviation for male heights.
male_sd <- 3

# Determine the height of a man in the 99th percentile of the distribution.
qnorm(0.99, male_avg, male_sd)
```

`@sct`
```{r}
test_error()
test_function("qnorm", args = c("p", "mean", "sd"),
              not_called_msg = "Have you used `qnorm` to calculate the value?",
              args_not_specified = "Make sure to specify the percentile, the average height, and the standard deviation in the `qnorm` function.",
              incorrect_msg = "Make sure to use `qnorm`. Include the percentile, the average height, and the standard deviation.")
test_output_contains("75.97904", incorrect_msg = "You are not providing a calculation that gives the correct answer. Remember to include the percentile as a fraction.")
success_msg("Great job! Let's move on.")
```

---

## Exercise 7. Distribution of IQ scores

```yaml
type: NormalExercise
key: 2762d30087
lang: r
xp: 100
skills: 1
```

The distribution of IQ scores is approximately normally distributed. The average is 100 and the standard deviation is 15. Suppose you want to know the distribution of the person with the highest IQ in your school district, where 10,000 people are born each year.

Generate 10,000 IQ scores 1,000 times using a Monte Carlo simulation. Make a histogram of the highest IQ scores.

`@instructions`
- Use the function `rnorm` to generate a random distribution of 10,000 values with a given average and standard deviation.
- Use the function `max` to return the largest value from a supplied vector.
- Repeat the previous steps a total of 1,000 times. Store the vector of the top 1,000 IQ scores as `highestIQ`.
- Plot the histogram of values using the function `hist`.

`@hint`
- To use the `replicate` function, provide the number of replications and the code you want to be replicated. You can use {} to include multiple expressions that you'd like to be repeated.

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# The variable `B` specifies the number of times we want the simulation to run.
B <- 1000

# Use the `set.seed` function to make sure your answer matches the expected result after random number generation.
set.seed(1)

# Create an object called `highestIQ` that contains the highest IQ score from each random distribution of 10,000 people.


# Make a histogram of the highest IQ scores.

```

`@solution`
```{r}
# The variable `B` specifies the number of times we want the simulation to run.
B <- 1000

# Use the `set.seed` function to make sure your answer matches the expected result after random number generation.
set.seed(1)

# Create an object called `highestIQ` that contains the highest IQ score from each random distribution of 10,000 people.
highestIQ <- replicate(B, {
  simulated_data <- rnorm(10000, 100, 15)
  max(simulated_data)
})

# Make a histogram of the highest IQ scores.
hist(highestIQ)
```

`@sct`
```{r}
test_error()
test_function("max",
              not_called_msg = "Have you used `max` to return the highest score from each of the B Monte Carlo simulations?")
test_function("rnorm", args = c("n", "mean", "sd"),
              not_called_msg = "Have you used `rnorm` to generate a distribution of IQ scores?",
              args_not_specified = "Make sure to provide the sample size of the population, the average IQ score, and the standard deviation to the function `rnorm`",
              incorrect_msg = "Make sure to use the function `rnorm` to generate a distribution of 10,000 IQ scores in every iteration.")
test_function("hist",
              not_called_msg = "Have you used `hist` to generate a histogram of IQ scores?",
              args_not_specified = "Make sure to provide a vector of IQ scores to the function `hist`",
              incorrect_msg = "Make a histogram of values stored in `highestIQ` when using the `hist` function.")

test_object("highestIQ", incorrect_msg = "`highestIQ` does not contain the correct values. It should contain the maximum values from each of the `B` Monte Carlo simulations.")

success_msg("Great work!")
```

---

## End of Assessment: Continuous Probability

```yaml
type: PureMultipleChoiceExercise
key: 53e3ca69b3
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
