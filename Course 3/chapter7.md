---
title: 'The Big Short'
description: 'In this chapter, you will learn about interest rates and the big short.'
---

## Exercise 1. Bank earnings

```yaml
type: NormalExercise
key: e25fb16d13
lang: r
xp: 100
skills: 1
```

Say you manage a bank that gives out 10,000 loans. The default rate is 0.03 and you lose $200,000 in each foreclosure.

Create a random variable $S$ that contains the earnings of your bank. Calculate the total amount of money lost in this scenario.

`@instructions`
- Using the `sample` function, generate a vector called `defaults` that contains `n` samples from a vector of `c(0,1)`, where `0` indicates a payment and `1` indicates a default
- Multiply the total number of defaults by the loss per foreclosure.

`@hint`
- You can `sample` function to simulate the outcomes of `n` loans. The following code demonstrates the sample function where the `n` outcomes of `a` and `b` occur with probabilities `p_a` and `p_b`, respectively.

```{r}
outcomes <- sample(c(a,b), n, replace = TRUE, prob = c(p_a, p_b))
```#

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Generate a vector called `defaults` that contains the default outcomes of `n` loans


# Generate `S`, the total amount of money lost across all foreclosures. Print the value to the console.



```

`@solution`
```{r}
# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Generate a vector called `defaults` that contains the default outcomes of `n` loans
defaults <- sample( c(0,1), n, replace = TRUE, prob=c(1-p_default, p_default))

# Generate `S`, the total amount of money lost across all foreclosures. Print the value to the console.
S <- sum(defaults * loss_per_foreclosure)
S
```

`@sct`
```{r}
test_error()
test_function("sample", args = c("x", "size", "replace", "prob"),
              not_called_msg = "Have you used `sample` to model the outcome of `n` loans?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of possible outcomes ('0' for payment or '1' for default), the number of times to sample from that vector (`n`), that the sampling should be done with replacement 'replace = TRUE', and the probability of each outcome using 'prob ='.",
              incorrect_msg = "When using `sample`, include a vector of possible outcomes in the order `c(0,1)`, the number of times to sample from that vector, whether replacement should occur, and the chances of each outcome occurring.")

test_function("sum", 
             not_called_msg = "Did you call `sum` to calculate the total money lost across all defaults?")

test_output_contains("-6.3e+07", incorrect_msg = "Your output does not match the correct answer. Multiply the cost of each foreclosure by the number of foreclosures. The final value should be negative. Print the result to the console.")

success_msg("Great work! Let's move on to the next calculation.")
```

---

## Exercise 2. Bank earnings Monte Carlo

```yaml
type: NormalExercise
key: a52b3bc780
lang: r
xp: 100
skills: 1
```

Run a Monte Carlo simulation with 10,000 outcomes for $S$, the sum of losses over 10,000 loans. Make a histogram of the results.

`@instructions`
- Within a `replicate` loop with 10,000 iterations, use `sample` to generate a list of 10,000 loan outcomes: payment (0) or default (1). Use the outcome order `c(0,1)` and probability of default `p_default`.
- Still within the loop, use the function `sum` to count the number of foreclosures multiplied by `loss_per_foreclosure` to return the sum of all losses across the 10,000 loans. _If you do not take the `sum` inside the `replicate` loop, DataCamp may crash with a "Session Expired" error._
- Plot the histogram of values using the function `hist`.

`@hint`
- To use the `replicate` function, provide the number of replications and the code you want to be replicated. You can use {} to include multiple expressions that you'd like to be repeated.

`@pre_exercise_code`
```{r}
n <- 10000
loss_per_foreclosure <- -200000
p_default <- 0.03
```

`@sample_code`
```{r}
# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# The variable `B` specifies the number of times we want the simulation to run
B <- 10000

# Generate a list of summed losses 'S'. Replicate the code from the previous exercise over 'B' iterations to generate a list of summed losses for 'n' loans.  Ignore any warnings for now.





# Plot a histogram of 'S'.  Ignore any warnings for now.

```

`@solution`
```{r}
# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# The variable `B` specifies the number of times we want the simulation to run
B <- 10000

# Generate a list of summed losses 'S'. Replicate the code from the previous exercise over 'B' iterations to generate a list of summed losses for 'n' loans. Ignore any warnings for now.

S <- replicate(B, {
    defaults <- sample( c(0,1), n, prob=c(1-p_default, p_default), replace = TRUE) 
  sum(defaults * loss_per_foreclosure)
})

# Plot a histogram of 'S'. Ignore any warnings for now.
hist(S)
```

`@sct`
```{r}
test_error()
test_function("sample", args = c("x", "size", "replace", "prob"),
              not_called_msg = "Have you used `sample` to model the outcome of 10,000 loans?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of possible outcomes (payment or default), the number of times to sample from that vector ('n'), that replacement should occur, and the probability of each outcome using 'prob ='.",
              incorrect_msg = "Make sure to use the `sample` function. Include a vector of possible outcomes, the number of times to sample from that vector, and the chances of each outcome occurring.")
test_object("S", incorrect_msg = "`S` does not contain the correct values. Did you use `replicate` to repeatedly sample 10,000 loan outcomes, then take the sum of defaults times the loss per foreclosure?")
test_function("hist", args = "x",
              not_called_msg = "Have you used `hist` to model the outcomes of the simulations?",
              args_not_specified = "In the `hist` function, provide a vector of values to plot.",
              incorrect_msg = "Your histogram is not correct. Check your definition of `S`.")
success_msg("Great work! Let's move on to the next example.")
```

---

## Exercise 3. Bank earnings expected value

```yaml
type: NormalExercise
key: 9888076e5a
lang: r
xp: 100
skills: 1
```

What is the expected value of $S$, the sum of losses over 10,000 loans? For now, assume a bank makes no money if the loan is paid.

`@instructions`
- Using the chances of default (`p_default`), calculate the expected losses over 10,000 loans.

`@hint`
- Multiply the cost of the default by the probability of default.
- Multiply this by the total number of loans.

`@pre_exercise_code`
```{r}
n <- 10000
loss_per_foreclosure <- -200000
p_default <- 0.03 
```

`@sample_code`
```{r}
# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Calculate the expected loss due to default out of 10,000 loans

```

`@solution`
```{r}
# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Calculate the expected loss due to default out of 10,000 loans
n*(p_default*loss_per_foreclosure + (1-p_default)*0)
```

`@sct`
```{r}
test_error()
test_output_contains("-6e+07", incorrect_msg = "You are not providing a calculation that gives the correct answer. The expected outcome is the probability of default multiplied by the total number of loans and the cost of each default.")
success_msg("Good job! Let's work on the next problem.")
```

---

## Exercise 4. Bank earnings standard error

```yaml
type: NormalExercise
key: 6521c563f8
lang: r
xp: 100
skills: 1
```

What is the standard error of $S$?

`@instructions`
- Compute the standard error of the random variable `S` you generated in the previous exercise, the summed outcomes of 10,000 loans.

`@hint`
- Assume two possible outcomes, $a$ and $b$, with the probability of $a$ equal to $p$. When outcomes of loans are independent, the standard error of the sum of outcomes is given by the following equation:

$$ \sqrt{\mbox{number of loans }} \times \mid b - a \mid \sqrt{p(1-p)}$$

`@pre_exercise_code`
```{r}
n <- 10000
loss_per_foreclosure <- -200000
p <- 0.03 
```

`@sample_code`
```{r}
# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Compute the standard error of the sum of 10,000 loans

```

`@solution`
```{r}
# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Compute the standard error of the sum of 10,000 loans
sqrt(n) * abs(loss_per_foreclosure) * sqrt(p_default*(1 - p_default))
```

`@sct`
```{r}
test_error()
test_output_contains("3411744", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are using the `sqrt` function twice to calculate this value. The answer should be a positive number.")
success_msg("Great work!")
```

---

## Exercise 5. Bank earnings interest rate - 1

```yaml
type: NormalExercise
key: cd13ccfa5b
lang: r
xp: 100
skills: 1
```

So far, we've been assuming that we make no money when people pay their loans and we lose a lot of money when people default on their loans. Assume we give out loans for $180,000. How much money do we need to make when people pay their loans so that our net loss is $0?

In other words, what interest rate do we need to charge in order to not lose money?

`@instructions`
- If the amount of money lost or gained equals 0, the probability of default times the total loss per default equals the amount earned per probability of the loan being paid.
- Divide the total amount needed per loan by the loan amount to determine the interest rate.

`@hint`
- We want to solve the following equation, where $l$ is the total amount lost per default, $p$ is the default rate, and $x$ is the total amount gained per loan that does not default.

$$ lp + x(1-p) = 0 $$

- This implies that

$$ x = -lp / (1-p) $$
- To convert the total amount of profit to a rate, divide $x$ by the loan amount.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Assign a variable `x` as the total amount necessary to have an expected outcome of $0


# Convert `x` to a rate, given that the loan amount is $180,000. Print this value to the console.

```

`@solution`
```{r}
# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Assign a variable `x` as the total amount necessary to have an expected outcome of $0 
x <- -(loss_per_foreclosure*p_default) / (1 - p_default)

# Convert `x` to an interest rate, given that the loan amount is $180,000. Print this value to the console.
x / 180000
```

`@sct`
```{r}
test_output_contains("0.03436426", incorrect_msg = "You are not providing a calculation that gives the correct answer. Determine the total amount of money needed to offset the 200,000 per loan loss for defaults. Divide this answer by the loan amount to convert to an interest rate. The answer should be a positive number.")
success_msg("Great work!")
```

---

## Exercise 6. Bank earnings interest rate - 2

```yaml
type: NormalExercise
key: 8d285de8d9
lang: r
xp: 100
skills: 1
```

With the interest rate calculated in the last example, we still lose money 50% of the time. What should the interest rate be so that the chance of losing money is 1 in 20? 

In math notation, what should the interest rate be so that $\mbox{Pr}(S<0) = 0.05$?

Remember that we can add a constant to both sides of the equation to get:
$$ \mbox{Pr}\left(\frac{S - \mbox{E}[S]}{\mbox{SE}[S]} < \frac{ - \mbox{E}[S]}{\mbox{SE}[S]}\right) $$

which is

$$ \mbox{Pr}\left(Z < \frac{- { [lp + x(1-p)]}n}{(x-l) \sqrt{np(1-p)}}\right) = 0.05 $$


Let `z = qnorm(0.05)` give us the value of `z` for which:
$$ \mbox{Pr}(Z \leq z) = 0.05 $$

`@instructions`
- Use the `qnorm` function to compute a continuous variable at given quantile of the distribution to solve for `z`.
- In this equation, $l$, $p$, and $n$ are known values. Once you've solved for `z`, solve for `x`.
- Divide `x` by the loan amount to calculate the rate.

`@hint`
- The right side of the complicated equation must be `z = qnorm(0.05)`:
$$ \frac{- { lp + x(1-p)}N}{(x-l) \sqrt{Np(1-p)}} = z$$

- Solve for `x`:
$$ x = - l \frac{ np - z \sqrt{np(1-p)}}{N(1-p) + z \sqrt{np(1-p)}}$$

`@pre_exercise_code`
```{r}
# no pec
```

`@sample_code`
```{r}
# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Generate a variable `z` using the `qnorm` function


# Generate a variable `x` using `z`, `p_default`, `loss_per_foreclosure`, and `n`


# Convert `x` to an interest rate, given that the loan amount is $180,000. Print this value to the console.

```

`@solution`
```{r}
# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Generate a variable `z` using the `qnorm` function
z <- qnorm(0.05)

# Generate a variable `x` using `z`, `p_default`, `loss_per_foreclosure`, and `n`
x <- -loss_per_foreclosure*( n*p_default - z*sqrt(n*p_default*(1 - p_default)))/ ( n*(1 - p_default) + z*sqrt(n*p_default*(1 - p_default)))

# Convert `x` to an interest rate, given that the loan amount is $180,000. Print this value to the console.
x / 180000
```

`@sct`
```{r}
test_error()
test_object("z", incorrect_msg = "Remember that `z = qnorm(0.05)` gives us the value of `z` for which the probability that `Z` is less than `z` equals 5%.")
test_output_contains("0.03768738", incorrect_msg = "You are not providing a calculation that gives the correct answer. The interest rate can be calculated by solving for `z` using `qnorm`, then solving for `x`. Divide the total amount needed by the loan amount to calculate the rate.")
success_msg("Good job! Let's work on another example.")
```

---

## Exercise 7. Bank earnings - minimize money loss

```yaml
type: MultipleChoiceExercise
key: ab0833255f
lang: r
xp: 50
skills: 1
```

The bank wants to minimize the probability of losing money. Which of the following achieves their goal without making interest rates go up?

`@possible_answers`
- A smaller pool of loans
- A larger probability of default
- A reduced default rate
- A larger cost per loan default

`@hint`
- Consider the variables we've been using: the amount of loss per loan, the default rate, the number of loans offered. Which values could be increased or decreased to decrease the probability of losing money?

`@pre_exercise_code`
```{r}
# no pec
```

`@sct`
```{r}
msg1 = "Try again. Offering fewer loans would increase the standard error in per-loan profit."
msg2 = "Read the answer choices carefully. A larger probability of default would increase the odds of losing money."
msg3 = "Well done!"
msg4 = "Try again. A large cost per default would increase the odds of losing money."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## End of Assessment: The Big Short

```yaml
type: PureMultipleChoiceExercise
key: 0bbe75c031
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
