---
title: Normal Distributions
description: In this chapter we go over the normal distribution.
---

## Exercise 1. Proportions

```yaml
type: NormalExercise
key: 2615b249e5
lang: r
xp: 100
skills:
  - 1
```

Histograms and density plots provide excellent summaries of a distribution. But can we summarize even further? We often see the average and standard deviation used as summary statistics: a two number summary! To understand what these summaries are and why they are so widely used, we need to understand the normal distribution. 

The normal distribution, also known as the bell curve and as the Gaussian distribution, is one of the most famous mathematical concepts in history. A reason for this is that approximately normal distributions occur in many situations. Examples include gambling winnings, heights, weights, blood pressure, standardized test scores, and experimental measurement errors. Often data visualization is needed to confirm that our data follows a normal distribution.

Here we focus on how the normal distribution helps us summarize data and can be useful in practice.

One way the normal distribution is useful is that it can be used to approximate the distribution of a list of numbers without having access to the entire list. We will demonstrate this with the heights dataset.

Load the height data set and create a vector `x` with just the male heights:

```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
```

`@instructions`
- What proportion of the data is between 69 and 72 inches (taller than 69 but shorter or equal to 72)? A proportion is between 0 and 1.
- Use the `mean` function in your code. Remember that you can use `mean` to compute the proportion of entries of a logical vector that are `TRUE`.

`@hint`
- Remember that you can create a logical vector with logical operators. For example, you can ask which entries of a vector are between 2 and 5 like this:

```{r}
x <- 1:10
x > 2 & x<=5
```
- You can use `mean` to compute the proportion of entries that are `TRUE`.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
```

`@solution`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
mean(x > 69 & x <= 72)
```

`@sct`
```{r}
test_error()
#test_object("x", incorrect_msg = "`x` is not defined correctly.")
test_function("mean", incorrect_msg = "Are you using `mean` on the correct subset?")
test_output_contains("0.3337438", incorrect_msg = "Are you using `mean` using the correct logical expression?, it should be something like `x>a & x<=b`. ")
success_msg("Nice job! Remember the value here, we'll reference it in the future.")
```

---

## Exercise 2. Averages and Standard Deviations

```yaml
type: NormalExercise
key: 0390d2888e
lang: r
xp: 100
skills:
  - 1
```

Suppose all you know about the height data from the previous exercise is the average and the standard deviation and that its distribution is approximated by the normal distribution. We can compute the average and standard deviation like this:

```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex=="Male"]
avg <- mean(x)
stdev <- sd(x)
```

Suppose you only have `avg` and `stdev` below, but no access to `x`, can you approximate the proportion of the data that is between 69 and 72 inches?

Given a normal distribution with a mean `mu` and standard deviation `sigma`, you can calculate the proportion of observations less than or equal to a certain `value` with `pnorm(value, mu, sigma)`. Notice that this is the CDF for the normal distribution. We will learn much more about `pnorm` later in the course series, but you can also learn more now with `?pnorm`.

`@instructions`
- Use the normal approximation to estimate the proportion the proportion of the data that is between 69 and 72 inches.
- Note that you can't use `x` in your code, only `avg` and `stdev`. Also note that R has a function that may prove very helpful here - check out the `pnorm` function (and remember that you can get help by using `?pnorm`).

`@hint`
Use the `pnorm` function with the correct arguments for `mean` and `sd` to predict the proportions to compute the proportion that is below 72 and subtract the proportion that is below 69.

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex=="Male"]
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex=="Male"]
avg <- mean(x)
stdev <- sd(x)
```

`@solution`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex=="Male"]
avg <- mean(x)
stdev <- sd(x)
pnorm(72, avg, stdev) - pnorm(69, avg, stdev)
```

`@sct`
```{r}
test_error()
test_output_contains("0.3061779", incorrect_msg = "Are you using `pnorm` on the correct average and sd? Remember you can estimate the proportion below 72 and subtract the proportion below 69. Use `pnorm` both these estimates.")
success_msg("Nice job! Notice how similar they are.")
```

---

## Exercise 3. Approximations

```yaml
type: NormalExercise
key: 82595c60bc
lang: r
xp: 100
skills:
  - 1
```

Notice that the approximation calculated in the second question is very close to the exact calculation in the first question. The normal distribution was a useful approximation for this case. 

However, the approximation is not always useful. An example is for the more extreme values, often called the "tails" of the distribution. Let's look at an example. We can compute the proportion of heights between 79 and 81.

```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
mean(x > 79 & x <= 81)
```

`@instructions`
- Use normal approximation to estimate the proportion of heights between 79 and 81 inches and save it in an object called `approx`.
- Report how many times bigger the actual proportion is compared to the approximation.

`@hint`
- Remember to calculate the average and standard deviation!
- Then compute the normal approximation using `pnorm`.
- Finally, calculate the ratio of the exact value and the approximation by dividing the two values.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
exact <- mean(x > 79 & x <= 81)
```

`@solution`
```{r}
library(dslabs)
data(heights)
x <- heights$height[heights$sex == "Male"]
avg <- mean(x)
stdev <- sd(x)
exact <- mean(x>79 & x<=81)
approx <- pnorm(81, avg, stdev) - pnorm(79, avg, stdev)
exact/approx
```

`@sct`
```{r}
test_error()
test_output_contains("exact/approx", incorrect_msg = "Calculate the ratio of your two previous assessment answers")
success_msg("Nice job! Notice that at the tails of the distribution, the approximation is not as accurate.")
```

---

## Exercise 4. Seven footers and the NBA

```yaml
type: NormalExercise
key: 4004286f5d
lang: r
xp: 100
skills:
  - 1
```

Someone asks you what percent of seven footers are in the National Basketball Association (NBA). Can you provide an estimate? Let's try using the normal approximation to answer this question.

Given a normal distribution with a mean `mu` and standard deviation `sigma`, you can calculate the proportion of observations less than or equal to a certain `value` with `pnorm(value, mu, sigma)`. Notice that this is the CDF for the normal distribution. We will learn much more about `pnorm` later in the course series, but you can also learn more now with `?pnorm`.

First, we will estimate the proportion of adult men that are taller than 7 feet.

Assume that the distribution of adult men in the world as normally distributed with an average of 69 inches and a standard deviation of 3 inches.

`@instructions`
- Using the normal approximation, estimate the proportion of adult men that are taller than 7 feet, referred to as _seven footers_. Remember that 1 foot equals 12 inches.
- Assume that the distribution of adult men in the world is normally distributed with an average of 69 inches and a standard deviation of 3 inches.
- Use the `pnorm` function. Note that `pnorm` finds the proportion less than or equal to a given value, but you are asked to find the proportion greater than that value.
- Print out your estimate; don't store it in an object.

`@hint`
Use the `pnorm` function. Remember 7 feet is `7*12` inches.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# use pnorm to calculate the proportion over 7 feet (7*12 inches)

```

`@solution`
```{r}
# use pnorm to calculate the proportion over 7 feet (7*12 inches)
1 - pnorm(7*12, 69, 3)
```

`@sct`
```{r}
test_error()
test_output_contains("2.866516e-07", incorrect_msg = "Make sure you are calculating the right tail of the distribution. `1 - your estimate`")
success_msg("Great job!")
```

---

## Exercise 5. Estimating the number seven footers

```yaml
type: NormalExercise
key: 0b85453043
lang: r
xp: 100
skills:
  - 1
```

Now we have an approximation for the proportion, call it `p`, of men that are 7 feet tall or taller.

We know that there are about 1 billion men between the ages of 18 and 40 in the world, the age range for the NBA. 

Can we use the normal distribution to estimate how many of these 1 billion men are at least seven feet tall?

`@instructions`
- Use your answer to the previous exercise to estimate the proportion of men that are seven feet tall or taller in the world and store that value as `p`.
- Then multiply this value by 1 billion (10^9) round the number of 18-40 year old men who are seven feet tall or taller to the nearest integer with `round`. (Do not store this value in an object.)

`@hint`
Use the `pnorm` function as in the previous exercise, but this time store the output in `p`. When you round, remember that 1 billion is 10^9 and then use the `round` function.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}

```

`@solution`
```{r}
p <- 1 - pnorm(7*12, 69, 3)
round(p * 10^9)
```

`@sct`
```{r}
test_error()
test_output_contains("287", incorrect_msg = "Make sure you are rounding to the nearest integer. Try the `round` function.")
success_msg("Great job! Remember this answer - we will use it in the next exercise.")
```

---

## Exercise 6. How many seven footers are in the NBA?

```yaml
type: NormalExercise
key: 9ab25189ea
lang: r
xp: 100
skills:
  - 1
```

There are about 10 National Basketball Association (NBA) players that are 7 feet tall or higher.

`@instructions`
- Use your answer to exercise 4 to estimate the proportion of men that are seven feet tall or taller in the world and store that value as `p`.
- Use your answer to the previous exercise (exercise 5) to round the number of 18-40 year old men who are seven feet tall or taller to the nearest integer and store that value as `N`. Note that R is case-sensitive, so do not use `n`.
- Then calculate the proportion of the world's 18 to 40 year old seven footers that are in the NBA. (Do not store this value in an object.)

`@hint`
Use the `pnorm` function as in exercise 4, but this time store the output in `p`. When you round, remember that 1 billion is 10^9 - and store that object in `N`. Use the information given about the number of NBA players to calculate the proportion!

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}

```

`@solution`
```{r}
p <- 1 - pnorm(7*12, 69, 3)
N <- round(p * 10^9)
10/N
```

`@sct`
```{r}
test_error()
test_output_contains("10/N", incorrect_msg = "Divide the number of NBA 7 footers by your previous answer to get a proportion")
success_msg("Great job! That's a higher percentage than I would have imagined!")
```

---

## Exercise 7. Lebron James' height

```yaml
type: NormalExercise
key: 817a8de36d
lang: r
xp: 100
skills:
  - 1
```

In the previous exerceise we estimated the proportion of seven footers in the NBA using this simple code:

```{r}
p <- 1 - pnorm(7*12, 69, 3)
N <- round(p * 10^9)
10/N
```

Repeat the calculations performed in the previous question for Lebron James' height: 6 feet 8 inches. 
There are about 150 players, instead of 10, that are at least that tall in the NBA.

`@instructions`
Report the estimated proportion of people at least Lebron's height that are in the NBA.

`@hint`
Make sure to modify the code for `p` to reflect Lebron James' height and for the final proportion to reflect the number of NBA players at least that tall in the NBA.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
## Change the solution to previous answer
p <- 1 - pnorm(7*12, 69, 3)
N <- round(p * 10^9)
10/N
```

`@solution`
```{r}
p <- 1 - pnorm(6*12 + 8, 69, 3)
N <- round(p * 10^9)
150/N
```

`@sct`
```{r}
test_error()
test_object("p", incorrect_msg = "Make sure the heights are in inches and it represents Lebron's height. The average and standard deviation are the same since it is the same population.")
test_output_contains("150/N", incorrect_msg = "Did you remember to change the number of people in the NBA that are that height?")
success_msg("Great job! Is it just harder to get into the NBA if you're not 7 feet tall?")
```

---

## Exercise 8. Interpretation

```yaml
type: MultipleChoiceExercise
key: d846ce8d42
lang: r
xp: 50
skills:
  - 1
```

In answering the previous questions, we found that it is not at all rare for a seven footer to become an NBA player. 

What would be a fair critique of our calculations?

`@possible_answers`
- Practice and talent are what make a great basketball player, not height.
- The normal approximation is not appropriate for heights.
- As seen in exercise 3, the normal approximation tends to underestimate the extreme values. It's possible that there are more seven footers than we predicted.
- As seen in exercise 3, the normal approximation tends to overestimate the extreme values. It's possible that there are less seven footers than we predicted.

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg3 = "Correct!  Good Job!"
msg1 = msg2 = msg4 = "Incorrect. Try again"
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## End of Assessment: Normal Distribution

```yaml
type: PureMultipleChoiceExercise
key: 4307faf5ce
xp: 50
skills:
  - 1
```

This is the end of the programming assignment for this section. Please DO NOT click through to additional assessments from this page. WARNING: if you continue the assessments by clicking on the arrow to get the next exercise or by hitting Ctrl-K your assessments may NOT get scored.

You can close this window and return to <a href='https://www.edx.org/course/data-science-visualization-harvardx-ph125-2x'>Data Science: Visualization</a>.

`@hint`
- No hint necessary!

`@possible_answers`
- [Awesome]
- Nope

`@feedback`
- Great! Now navigate back to the course on edX!
- Now navigate back to the course on edX!
