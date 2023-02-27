---
title: The t-distribution
description: 'In this chapter, you will learn about the t-distribution.'
---

## Exercise 1 - Using the t-Distribution

```yaml
type: NormalExercise
key: ac6bf8dbda
lang: r
xp: 100
skills:
  - 1
```

We know that, with a normal distribution, only 5% of values are more than 2 standard deviations away from the mean. 

Calculate the probability of seeing t-distributed random variables being more than 2 in absolute value when the degrees of freedom are 3.

`@instructions`
- Use the `pt` function to calculate the probability of seeing a value less than or equal to the argument. Your output should be a single value.

`@hint`
- Use the `pt` function twice to find the probability of a value being equal to or less than 2 and -2.
- Subtract the probability that the value is equal or less than 2 from 1.
- Add the probability that the value is equal or less than -2.

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# Calculate the probability of seeing t-distributed random variables being more than 2 in absolute value when 'df = 3'.
```

`@solution`
```{r}
# Calculate the probability of seeing t-distributed random variables being more than 2 in absolute value when 'df = 3'. 
1 - pt(2, 3) + pt(-2, 3)
```

`@sct`
```{r}
test_error()
test_output_contains("0.139326", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you subtracting the probability of the value being equal to or lower than 2 from 1 and adding the probability that the value is equal or lower than -2.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 2 - Plotting the t-distribution

```yaml
type: NormalExercise
key: 9a9b45069a
lang: r
xp: 100
skills:
  - 1
```

Now use `sapply` to compute the same probability for degrees of freedom from 3 to 50. 

Make a plot and notice when this probability converges to the normal distribution's 5%.

`@instructions`
- Make a vector called `df` that contains a sequence of numbers from 3 to 50.
- Using `function`,  make a function called `pt_func` that recreates the calculation for the probability that a value is greater than 2 as an absolute value for any given degrees of freedom.
- Use `sapply` to apply the `pt_func` function across all values contained in `df`. Call these probabilities `probs`.
- Use the `plot` function to plot `df` on the x-axis and `probs` on the y-axis.

`@hint`
- You can generate a vector of values a number of ways. For example, use the `seq` function or create vector using `c()` with a range of `3:50`.
- Your function should look like this:
```{r}
pt_func <- function(x) 1 - pt(2, x) + pt(-2, x)
```

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# Generate a vector 'df' that contains a sequence of numbers from 3 to 50


# Make a function called 'pt_func' that calculates the probability that a value is more than |2| for any degrees of freedom 


# Generate a vector 'probs' that uses the `pt_func` function to calculate the probabilities


# Plot 'df' on the x-axis and 'probs' on the y-axis
```

`@solution`
```{r}
# Generate a vector 'df' that contains a sequence of numbers from 3 to 50
df <- seq(3,50)

# Make a function called 'pt_func' that calculates the probability that a value is more than |2| for any degrees of freedom 
pt_func <- function(x) 1 - pt(2, x) + pt(-2, x)

# Generate a vector 'probs' that uses the `pt_func` function to calculate the probabilities
probs <- sapply(df, pt_func)

# Plot 'df' on the x-axis and 'probs' on the y-axis
plot(df, probs)
```

`@sct`
```{r}
test_error()
test_object("df",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Remember to generate a vector called 'df' that contains values from 3 to 50.",
            incorrect_msg = "Your vector called 'df' should contain values from 3 to 50.")
test_object("probs",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Remember to generate a vector called 'probs'.",
            incorrect_msg = "Your vector called 'probs' should contain the probabilities for degrees of freedom ranging from 3 to 50.")
test_function("plot", args = c("x","y"),
              not_called_msg = "Remember to generate the plot using the `plot` function.",
              args_not_specified = "Supply values you want on the x- and y-axes to the `plot` function.",
              incorrect_msg = "Plot 'df' on the x-axis and 'probs' on the y-axis.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 3 - Sampling From the Normal Distribution

```yaml
type: NormalExercise
key: c0fd2757ef
lang: r
xp: 100
skills:
  - 1
```

In a previous section, we repeatedly took random samples of 50 heights from a distribution of heights. We noticed that about 95% of the samples had confidence intervals spanning the true population mean.

Re-do this Monte Carlo simulation, but now instead of $N=50$, use $N=15$. Notice what happens to the proportion of hits.

`@instructions`
- Use the `replicate` function to carry out the simulation. Specify the number of times you want the code to run and, within brackets, the three lines of code that should run.
- First use the `sample` function to randomly sample `N` values from `x`.
- Second, create a vector called `interval` that calculates the 95% confidence interval for the sample. You will use the `qnorm` function.
- Third, use the `between` function to determine if the population mean `mu` is contained between the confidence intervals.
- Save the results of the Monte Carlo function to a vector called `res`.
- Use the `mean` function to determine the proportion of hits in `res`.

`@hint`
- You can generate the 95% confidence intervals using the following code:
```{r}
mean(X) + c(-1,1)*qnorm(0.975)*sd(X)/sqrt(N)
```

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data(heights)
```

`@sample_code`
```{r}
# Load the neccessary libraries and data
library(dslabs)
library(dplyr)
data(heights)

# Use the sample code to generate 'x', a vector of male heights
x <- heights %>% filter(sex == "Male") %>%
  .$height

# Create variables for the mean height 'mu', the sample size 'N', and the number of times the simulation should run 'B'
mu <- mean(x)
N <- 15
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Generate a logical vector 'res' that contains the results of the simulations





# Calculate the proportion of times the simulation produced values within the 95% confidence interval. Print this value to the console.
```

`@solution`
```{r}
# Load the neccessary libraries and data
library(dslabs)
library(dplyr)
data(heights)

# Use the sample code to generate 'x', a vector of male heights
x <- heights %>% filter(sex == "Male") %>%
  .$height

# Create variables for the mean height 'mu', the sample size 'N', and the number of times the simulation should run 'B'
mu <- mean(x)
N <- 15
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Generate a logical vector 'res' that contains the results of the simulations
res <- replicate(B, {
  X <- sample(x, N, replace=TRUE)
  interval <- mean(X) + c(-1,1)*qnorm(0.975)*sd(X)/sqrt(N)
  between(mu, interval[1], interval[2])
})

# Calculate the proportion of times the simulation produced values within the 95% confidence interval. Print this value to the console.
mean(res)
```

`@sct`
```{r}
test_error()
test_function("replicate", 
              not_called_msg = "Use the `replicate` function to generate an object called 'res'.")

test_function("sample", args = c("x", "size", "replace"),
              not_called_msg = "Have you used `sample` to select 'N' heights from the vector 'x'?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of heights, the number of times to sample from that vector, and that the sampling should be done with replacement.",
              incorrect_msg = "Make sure to use `sample` function. Include a vector of heights ('x'), the number of times to sample from that vector ('N'), and that replacement should occur..")

test_function("qnorm", args="p", 
              incorrect_msg = "Use the quantile '0.975' to calculate the confidence intervals.", 
              not_called_msg = "Use the `qnorm` function to calculate the confidence intervals.")

test_function("sqrt", args="x", 
              incorrect_msg = "Find the square root of the sample size in order to calculate the confidence interval.", 
              not_called_msg = "Use the `sqrt` function to calculate the confidence intervals.")

test_output_contains("0.9323", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are using the `mean` function to calculate the proportion of hits.")
success_msg("Great work! Let's try this with the t-distribution.")
```

---

## Exercise 4 - Sampling from the t-Distribution

```yaml
type: NormalExercise
key: 0eabc2016e
lang: r
xp: 100
skills:
  - 1
```

$N=15$ is not that big. We know that heights are normally distributed, so the t-distribution should apply. Repeat the previous Monte Carlo simulation using the t-distribution instead of using the normal distribution to construct the confidence intervals.

What are the proportion of 95% confidence intervals that span the actual mean height now?

`@instructions`
- Use the `replicate` function to carry out the simulation. Specify the number of times you want the code to run and, within brackets, the three lines of code that should run.
- First use the `sample` function to randomly sample `N` values from `x`.
- Second, create a vector called `interval` that calculates the 95% confidence interval for the sample. Remember to use the `qt` function this time to generate the confidence interval.
- Third, use the `between` function to determine if the population mean `mu` is contained between the confidence intervals.
- Save the results of the Monte Carlo function to a vector called `res`.
- Use the `mean` function to determine the proportion of hits in `res`.

`@hint`
- You can generate the 95% confidence intervals using the following code:
```{r}
mean(X) + c(-1,1)*qt(0.975, N-1)*sd(X)/sqrt(N)
```

`@pre_exercise_code`
```{r}
# Load the neccessary libraries and data
library(dslabs)
library(dplyr)
data(heights)

# Use the sample code to generate 'x', a vector of male heights
x <- heights %>% filter(sex == "Male") %>%
  .$height
```

`@sample_code`
```{r}
# The vector of filtered heights 'x' has already been loaded for you. Calculate the mean.
mu <- mean(x)

# Use the same sampling parameters as in the previous exercise.
set.seed(1)
N <- 15
B <- 10000

# Generate a logical vector 'res' that contains the results of the simulations using the t-distribution






# Calculate the proportion of times the simulation produced values within the 95% confidence interval. Print this value to the console.
```

`@solution`
```{r}
# The vector of filtered heights 'x' has already been loaded for you. Calculate the mean.
mu <- mean(x)

# Use the same sampling parameters as in the previous exercise.
set.seed(1)
N <- 15
B <- 10000

# Generate a logical vector 'res' that contains the results of the simulations using the t-distribution
res <- replicate(B, {
  X <- sample(x, N, replace=TRUE)
  interval <- mean(X) + c(-1,1)*qt(0.975, N-1)*sd(X)/sqrt(N)
  between(mu, interval[1], interval[2])
})

# Calculate the proportion of times the simulation produced values within the 95% confidence interval. Print this value to the console.
mean(res)
```

`@sct`
```{r}
test_error()
test_function("replicate", 
              not_called_msg = "Use the `replicate` function to generate an object called 'res'.")

test_function("sample", args = c("x", "size", "replace"),
              not_called_msg = "Have you used `sample` to select 'N' heights from the vector 'x'?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of heights, the number of times to sample from that vector, and that the sampling should be done with replacement.",
              incorrect_msg = "Make sure to use `sample` function. Include a vector of heights ('x'), the number of times to sample from that vector ('N'), and that replacement should occur..")

test_function("qt", args=c("p","df"), 
              incorrect_msg = "Use the quantile '0.975' to calculate the confidence intervals. Remember to specify the degrees of freedom (N-1)", 
              not_called_msg = "Use the `qt` function to calculate the confidence intervals.")

test_function("sqrt", args="x", 
              incorrect_msg = "Find the square root of the sample size in order to calculate the confidence interval.", 
              not_called_msg = "Use the `sqrt` function to calculate the confidence intervals.")
test_output_contains("0.9523", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are using the `mean` function to generate the proportion of hits.")
success_msg("Great work! Let's wrap it up.")
```

---

## Exercise 5 - Why the t-Distribution?

```yaml
type: MultipleChoiceExercise
key: 3ac30a4e89
lang: r
xp: 50
skills:
  - 1
```

Why did the t-distribution confidence intervals work so much better?

`@possible_answers`
- The t-distribution takes the variability into account and generates larger confidence intervals.
- Because the t-distribution shifts the intervals in the direction towards the actual mean.
- This was just a chance occurrence. If we run it again, the CLT will work better.
- The t-distribution is always a better approximation than the normal distribution.

`@hint`
- The tails of the t-distribution are wider when there are fewer degrees of freedom.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Great work! Remember that we saw previously that the t-distribution performs similarly to the normal distribution when sample sizes 30 or larger."
msg2 = "Try again. The t-distribution accounts for standard deviation."
msg3 = "Try again. The t-distribution is appropriate for smaller sample sizes."
msg4 = "Try again. The t-distribution and normal distribution perform similarly for large sample sizes."
test_mc(correct = 1, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## End of Assessment

```yaml
type: PureMultipleChoiceExercise
key: f75e054925
xp: 50
skills:
  - 1
```

This is the end of the programming assignment for this section. Please DO NOT click through to additional assessments from this page. If you do click through, your scores may NOT be recorded.

Click "Got it!" and submit to get the "points" for this question.

You can close this window and return to <a href="https://www.edx.org/course/data-science-inference-and-modeling">Data Science: Inference</a>.

`@hint`
Continue on with the course within the edX platform.

`@possible_answers`
- [Got it!]

`@feedback`
- Great!
