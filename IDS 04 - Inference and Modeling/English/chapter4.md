---
title: Statistical Models
description: 'In this chapter, you will learn about different types of probability models'
---

## Exercise 1 - Heights Revisited

```yaml
type: NormalExercise
key: c84db45eda
lang: r
xp: 100
skills:
  - 1
```

We have been using _urn models_ to motivate the use of probability models. However, most data science applications are not related to data obtained from urns. More common are data that come from individuals. Probability plays a role because the data come from a random sample. The random sample is taken from a population and the urn serves as an analogy for the population. 

Let's revisit the heights dataset. For now, consider `x` to be the heights of all males in the data set. Mathematically speaking, `x` is our population. Using the urn analogy, we have an urn with the values of `x` in it. 

What are the population average and standard deviation of our population?

`@instructions`
- Execute the lines of code that create a vector `x` that contains heights for all males in the population.
- Calculate the average of `x`.
- Calculate the standard deviation of `x`.

`@hint`
- Use the `mean` and `sd` functions to calculate the average and standard deviation, respectively.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data(heights)
```

`@sample_code`
```{r}
# Load the 'dslabs' package and data contained in 'heights'
library(dslabs)
data(heights)

# Make a vector of heights from all males in the population
x <- heights %>% filter(sex == "Male") %>%
  .$height

# Calculate the population average. Print this value to the console.


# Calculate the population standard deviation. Print this value to the console.
```

`@solution`
```{r}
# Load the 'dslabs' package and data contained in 'heights'
library(dslabs)
data(heights)

# Make a vector of heights from all males in the population
x <- heights %>% filter(sex == "Male") %>%
  .$height

# Calculate the population average. Print this value to the console.
mean(x)

# Calculate the population standard deviation. Print this value to the console.
sd(x)
```

`@sct`
```{r}
test_error()
test_function("mean", args = "x",
              not_called_msg = "Use the `mean` function to find the average of the population.",
              args_not_specified = "Supply a vector of heights to the `mean` function.",
              incorrect_msg = "You are not supplying the correct vector of heights to the `mean` function.")
test_function("sd", args = "x",
              not_called_msg = "Use the `sd` function to find the standard deviation of the population.",
              args_not_specified = "Supply a vector of heights to the `sd` function.",
              incorrect_msg = "You are not supplying the correct vector of heights to the `sd` function.")
test_output_contains("69.31475", incorrect_msg = "You are not providing a calculation that gives the correct population average. Make sure you are using the `mean` function to find the average of 'x'.")
test_output_contains("3.611024", incorrect_msg = "You are not providing a calculation that gives the correct standard deviation. Make sure you are using the `sd` function to find the standard deviation of 'x'.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 2 - Sample the population of heights

```yaml
type: NormalExercise
key: 1d86aed639
lang: r
xp: 100
skills:
  - 1
```

Call the population average computed above $\mu$ and the standard deviation $\sigma$. Now take a sample of size 50, with replacement, and construct an estimate for $\mu$ and $\sigma$.

`@instructions`
- Use the `sample` function to sample `N` values from `x`.
- Calculate the mean of the sampled heights.
- Calculate the standard deviation of the sampled heights.

`@hint`
- Use the `mean` and `sd` functions to calculate the average and standard deviation, respectively.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data(heights)
x <- heights %>% filter(sex == "Male") %>%
  .$height
```

`@sample_code`
```{r}
# The vector of all male heights in our population `x` has already been loaded for you. You can examine the first six elements using `head`.
head(x)

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define `N` as the number of people measured
N <- 50

# Define `X` as a random sample from our population `x`


# Calculate the sample average. Print this value to the console.


# Calculate the sample standard deviation. Print this value to the console.
```

`@solution`
```{r}
# The vector of all male heights in our population `x` has already been loaded for you. You can examine the first six elements using `head`.
head(x)

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define `N` as the number of people measured
N <- 50

# Define `X` as a random sample from our population `x`
X <- sample(x, N, replace = TRUE)

# Calculate the sample average. Print this value to the console.
mean(X)

# Calculate the sample standard deviation. Print this value to the console.
sd(X)
```

`@sct`
```{r}
test_error()
test_function("sample", args = c("x", "size", "replace"),
              not_called_msg = "Have you used `sample` to randomly select N heights from the population 'x'?",
              args_not_specified = "Supply a population to be sampled, the number of values to sample, and whether or not replacement should occur to the `sample` function.",
              incorrect_msg = "You are not supplying the correct arguments to the `sample` function. Make sure to indicate the vector to sample values from, the number of times you want to sample from that vector, and that replacement should occur.")
test_function("mean", args = "x",
              not_called_msg = "Use the `mean` function to find the average of the sample",
              args_not_specified = "Supply a vector of sampled heights to the `mean` function.",
              incorrect_msg = "You are not supplying the correct vector of sampled heights to the `mean` function.")
test_function("sd", args = "x",
              not_called_msg = "Use the `sd` function to find the standard deviation of the sample",
              args_not_specified = "Supply a vector of sampled heights to the `sd` function.",
              incorrect_msg = "You are not supplying the correct vector of sampled heights to the `sd` function.")
test_output_contains("68.73423", incorrect_msg = "You are not providing a calculation that gives the correct population average. Make sure you are using the `mean` function to find the average of 'X'.")
test_output_contains("3.761344", incorrect_msg = "You are not providing a calculation that gives the correct standard deviation. Make sure you are using the `sd` function to find the standard deviation of 'X'.")
success_msg("Great work! Let's think about how these results relate to theory.")
```

---

## Exercise 3 - Sample and Population Averages

```yaml
type: MultipleChoiceExercise
key: 4af1e81376
lang: r
xp: 50
skills:
  - 1
```

What does the central limit theory tell us about the sample average and how it is related to $\mu$, the population average?

`@possible_answers`
- It is identical to $\mu$.
- It is a random variable with expected value $\mu$ and standard error $\sigma/\sqrt{N}$.
- It is a random variable with expected value $\mu$ and standard error $\sigma$.
- It underestimates $\mu$.

`@hint`
- For a large enough sample size, the probability distribution of the sample average is approximately normal.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. The sample average is a random variable related to the population average."
msg2 = "Correct! Let's move on to a similar problem."
msg3 = "Try again. The sample size must be considered when determining the relationship between the sample average and the population average."
msg4 = "Try again. The sample average is a random variable related to the population average."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 4 - Confidence Interval Calculation

```yaml
type: NormalExercise
key: 1c287a5fba
lang: r
xp: 100
skills:
  - 1
```

We will use $\bar{X}$ as our estimate of the heights in the population from our sample size $N$. We know from previous exercises that the standard estimate of our error $\bar{X}-\mu$ is $\sigma/\sqrt{N}$.

Construct a 95% confidence interval for $\mu$.

`@instructions`
- Use the `sd` and `sqrt` functions to define the standard error `se`
- Calculate the 95% confidence intervals using the `qnorm` function. Save the lower then the upper confidence interval to a variable called `ci`.

`@hint`
- The standard error equals $\sigma/\sqrt{N}$.
- Add and subtract `qnorm(0.975)` multiplied by the standard error to calculate the confidence interval.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data(heights)
x <- heights %>% filter(sex == "Male") %>%
  .$height
```

`@sample_code`
```{r}
# The vector of all male heights in our population `x` has already been loaded for you. You can examine the first six elements using `head`.
head(x)

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define `N` as the number of people measured
N <- 50

# Define `X` as a random sample from our population `x`
X <- sample(x, N, replace = TRUE)

# Define `se` as the standard error of the estimate. Print this value to the console.



# Construct a 95% confidence interval for the population average based on our sample. Save the lower and then the upper confidence interval to a variable called `ci`.


```

`@solution`
```{r}
# The vector of all male heights in our population `x` has already been loaded for you. You can examine the first six elements using `head`.
head(x)

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define `N` as the number of people measured
N <- 50

# Define `X` as a random sample from our population `x`
X <- sample(x, N, replace = TRUE)

# Define `se` as the standard error of the estimate. Print this value to the console.
se <- sd(X)/sqrt(N)
se

# Construct a 95% confidence interval for the population average based on our sample. Save the lower and then the upper confidence interval to a variable called `ci`.
ci <- c(mean(X) - qnorm(0.975)*se, mean(X) + qnorm(0.975)*se)

```

`@sct`
```{r}
test_error()
test_function("qnorm", not_called_msg = "Make sure you are using the `qnorm` function. Use a value slightly less than 1 to calculate the 95% confidence interval.")
test_function("mean", args = "x",
              not_called_msg = "Use the `mean` function to find the average of the sample",
              args_not_specified = "Supply a vector of sampled heights to the `mean` function.",
              incorrect_msg = "You are not supplying the correct vector of sampled heights to the `mean` function.")
test_function("sd", args = "x",
              not_called_msg = "Use the `sd` function to find the standard deviation of the sample",
              args_not_specified = "Supply a vector of sampled heights to the `sd` function.",
              incorrect_msg = "You are not supplying the correct vector of sampled heights to the `sd` function.")
test_function("sqrt", args = "x",
              not_called_msg = "Use the `sqrt` function to calculate the standard error.",
              args_not_specified = "Supply the sample size `N` to the `sqrt` function.",
              incorrect_msg = "You are not supplying the sample size `N` to the `sqrt` function.")
test_output_contains("0.5319343", incorrect_msg = "You are not providing a calculation that gives the correct standard error. The standard error is the standard deviation divided by the square root of the sample size.")


test_object("ci",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Have you made an object called 'ci'?",
            incorrect_msg = "The values contained in the object 'ci' are not correct. Are you using the correct formula to calculate the confidence intervals? Make sure to save the lower confidence interval first.")
            
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 5 - Monte Carlo Simulation for Heights

```yaml
type: NormalExercise
key: 2081d4c729
lang: r
xp: 100
skills:
  - 1
```

Now run a Monte Carlo simulation in which you compute 10,000 confidence intervals as you have just done. What proportion of these intervals include $\mu$?

`@instructions`
- Use the `replicate` function to replicate the sample code for `B <- 10000` simulations. Save the results of the replicated code to a variable called `res`.
The replicated code should complete the following steps:
-1. Use the `sample` function to sample `N` values from `x`. Save the sampled heights as a vector called `X`.
-2. Create an object called `interval` that contains the 95% confidence interval for each of the samples. Use the same formula you used in the previous exercise to calculate this interval.
-3. Use the `between` function to determine if $\mu$ is contained within the confidence interval of that simulation.
- Finally, use the `mean` function to determine the proportion of results in `res` that contain mu.

`@hint`
- The standard error equals $\sigma/\sqrt{N}$.
- Add and subtract `qnorm(0.975)` multiplied by the standard error to calculate the confidence interval.
- To use the `replicate` function, provide the number of replications and the code you want to be replicated. You can use {} to include multiple expressions that you'd like to be repeated.

```{r}
results <- replicate(number_of_times_to_replicate, {
  first_command_to_run
  second_command_to_run
  third_command_to_run
})
```

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data(heights)
x <- heights %>% filter(sex == "Male") %>%
  .$height
```

`@sample_code`
```{r}
# Define `mu` as the population average
mu <- mean(x)

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define `N` as the number of people measured
N <- 50

# Define `B` as the number of times to run the model
B <- 10000

# Define an object `res` that contains a logical vector for simulated intervals that contain mu






# Calculate the proportion of results in `res` that include mu. Print this value to the console.
```

`@solution`
```{r}
# Define `mu` as the population average
mu <- mean(x)

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define `N` as the number of people measured
N <- 50

# Define `B` as the number of times to run the model
B <- 10000

# Define an object `res` that contains a logical vector for simulated intervals that contain mu
res <- replicate(B, {
  X <- sample(x, N, replace=TRUE)
  interval <- mean(X) + c(-1,1)*qnorm(0.975)*sd(X)/sqrt(N)
  between(mu, interval[1], interval[2])
})

# Calculate the proportion of results in `res` that include mu. Print this value to the console.
mean(res)
```

`@sct`
```{r}
test_error()
test_function("replicate", not_called_msg = "Make sure you are using the `replicate` function to replicate the sample code 10,000 times.")
test_function("qnorm", not_called_msg = "Make sure you are using the `qnorm` function. Use a value slightly less than 1 to calculate the 95% confidence interval.")
test_function("sd",
              not_called_msg = "Use the `sd` function to find the standard deviation of the sample")
test_function("sqrt",
              not_called_msg = "Use the `sqrt` function to calculate the standard error.")
test_output_contains("0.9433", incorrect_msg = "You are not providing a calculation that gives the correct proportion of confidence intervals that contain mu. Make sure you use `set.seed(1)` and follow each line in the instructions.")
success_msg("Great work! Let's continue to the polling examples.")
```

---

## Exercise 6 - Visualizing Polling Bias

```yaml
type: NormalExercise
key: 82b1998a8e
lang: r
xp: 100
skills:
  - 1
```

In this section, we used visualization to motivate the presence of pollster bias in election polls. Here we will examine that bias more rigorously. Lets consider two pollsters that conducted daily polls and look at national polls for the month before the election. 

Is there a poll bias? Make a plot of the spreads for each poll.

`@instructions`
- Use `ggplot` to plot the spread for each of the two pollsters.
- Define the x- and y-axes usingusing `aes()` within the `ggplot` function.
- Use `geom_boxplot` to make a boxplot of the data.
- Use `geom_point` to add data points to the plot.

`@hint`
- Use the pipe function to tell ggplot what to plot. Define the ggplot aesthetic, then add layers on top of the plot.

For example:
```{r}
my_data %>% ggplot(aes(my_x_axis, my_y_axis)) + 
  geom_boxplot() + 
  geom_point()
```

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
library(ggplot2)
data("polls_us_election_2016")
```

`@sample_code`
```{r}
# Load the libraries and data you need for the following exercises
library(dslabs)
library(dplyr)
library(ggplot2)
data("polls_us_election_2016")

# These lines of code filter for the polls we want and calculate the spreads
polls <- polls_us_election_2016 %>% 
  filter(pollster %in% c("Rasmussen Reports/Pulse Opinion Research","The Times-Picayune/Lucid") &
           enddate >= "2016-10-15" &
           state == "U.S.") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100) 

# Make a boxplot with points of the spread for each pollster
```

`@solution`
```{r}
# These lines of code filter for the polls we want and calculate the spreads
polls <- polls_us_election_2016 %>% 
  filter(pollster %in% c("Rasmussen Reports/Pulse Opinion Research","The Times-Picayune/Lucid") &
           enddate >= "2016-10-15" &
           state == "U.S.") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100) 

# Make a boxplot with points of the spread for each pollster
polls %>% ggplot(aes(pollster, spread)) + 
  geom_boxplot() + 
  geom_point()
```

`@sct`
```{r}
test_error()
test_function("ggplot", not_called_msg = "Make sure to call `ggplot` to make your plot.")
test_function("geom_boxplot", not_called_msg = "Make sure to layer `geom_point` on your ggplot to add the boxplot.")
test_function("geom_point", not_called_msg = "Make sure to layer `geom_point` on your ggplot to add data points.")
success_msg("Great work! Let's answer some questions about pollster bias.")
```

---

## Exercise 7 - Defining Pollster Bias

```yaml
type: MultipleChoiceExercise
key: 8c861b813d
lang: r
xp: 50
skills:
  - 1
```

The data do seem to suggest there is a difference between the pollsters. However, these data are subject to variability. Perhaps the differences we observe are due to chance. Under the urn model, both pollsters should have the same expected value: the election day difference, $d$. 
  
We will model the observed data $Y_{ij}$ in the following way:

$$Y\_{ij}=d+b\_i+\varepsilon\_{ij}$$

with $i=1,2$ indexing the two pollsters, $b\_i$ the bias for pollster $i$, and $\varepsilon\_{ij}$ poll to poll chance variability. We assume the $\varepsilon$ are independent from each other, have expected value $0$ and standard deviation $\sigma_i$ regardless of $j$. 

Which of the following statements best reflects what we need to know to determine if our data fit the urn model?

`@possible_answers`
- Is $\varepsilon_{ij} = 0$?
- How close are $Y_{ij}$ to $d$?
- Is $b\_1 \neq b\_2$?
- Are $b\_1 = 0$ and $b\_2 = 0$?

`@hint`
- Under the urn model, the estimates both have the same expected result, $d$.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. Our assumption about the poll to poll variability do not tell us if our data fit the urn model."
msg2 = "Try again. We want to know if the bias for the two pollsters are different."
msg3 = "Correct!"
msg4 = "Try again. We want to know how these bias values are different."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 8 -  Derive Expected Value

```yaml
type: MultipleChoiceExercise
key: c912da1fdc
lang: r
xp: 50
skills:
  - 1
```

We modelled the observed data $Y_{ij}$ as:

$$Y\_{ij} = d + b\_i + \varepsilon\_{ij}$$

On the right side of this model, only $\varepsilon\_{ij}$ is a random variable. The other two values are constants. 

What is the expected value of $Y_{1j}$?

`@possible_answers`
- $d + b\_1$
- $b\_1 + \varepsilon\_{ij}$
- $d$
- $d + b\_1 + \varepsilon\_{ij}$

`@hint`
- The expected value of $\varepsilon\_{ij}$ is 0. Remember that $d$ and $b\_1$ are constants.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Correct! Let's move on to a similar problem."
msg2 = "Try again. Remember that the expected value of the poll-to-poll variance is zero."
msg3 = "Try again. Remember that the bias for poll 1 is a constant."
msg4 = "Try again. Remember that the expected value of the poll-to-poll variance is zero."
test_mc(correct = 1, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 9 - Expected Value and Standard Error of Poll 1

```yaml
type: MultipleChoiceExercise
key: c25be4efb9
lang: r
xp: 50
skills:
  - 1
```

Suppose we define $\bar{Y}\_1$ as the average of poll results from the first poll and $\sigma\_1$ as the standard deviation of the first poll.

What is the expected value and standard error of $\bar{Y}_1$?

`@possible_answers`
- The expected value is $d+b\_1$ and the standard error is $\sigma\_1$
- The expected value is $d$ and the standard error is $\sigma\_1/\sqrt{N\_1}$
- The expected value is $d+b\_1$ and the standard error is $\sigma\_1/\sqrt{N\_1}$
- The expected value is $d$ and the standard error is $\sigma\_1+\sqrt{N\_1}$

`@hint`
- The sample average is the same as the urn average.
- The standard error involves the standard deviation and the sample size.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. The standard error is divided by the square root of the sample size."
msg2 = "Try again. The expected value includes the poll bias."
msg3 = "Correct!"
msg4 = "Try again. The standard error is divided by the square root of the sample size."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 10 - Expected Value and Standard Error of Poll 2

```yaml
type: MultipleChoiceExercise
key: f2002276aa
lang: r
xp: 50
skills:
  - 1
```

Now we define $\bar{Y}\_2$ as the average of poll results from the second poll.

What is the expected value and standard error of $\bar{Y}\_2$?

`@possible_answers`
- The expected value is $d+b\_2$ and the standard error is $\sigma\_2$
- The expected value is $d$ and the standard error is $\sigma\_2/\sqrt{N\_2}$
- The expected value is $d+b\_2$ and the standard error is $\sigma\_2/\sqrt{N\_2}$
- The expected value is $d$ and the standard error is $\sigma\_2+\sqrt{N\_2}$

`@hint`
- The sample average is the same as the urn average.
- The standard error involves the standard deviation and the sample size.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. The standard error is divided by the square root of the sample size."
msg2 = "Try again. The expected value includes the poll bias."
msg3 = "Correct!"
msg4 = "Try again. The standard error is divided by the square root of the sample size."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 11 - Difference in Expected Values Between Polls

```yaml
type: MultipleChoiceExercise
key: 7e69247c6c
lang: r
xp: 50
skills:
  - 1
```

Using what we learned by answering the previous questions, what is the expected value of $\bar{Y}\_{2} - \bar{Y}\_1$?

`@possible_answers`
- $$(b\_2 - b\_1)^2$$
- $$b\_2 - b\_1/\sqrt(N)$$
- $$b\_2 + b\_1$$
- $$b\_2 - b\_1$$

`@hint`
- Remember that  $\mbox{E}[\bar{Y}\_i] = d + b\_i$.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. The difference between the polls is not squared."
msg2 = "Try again. The sample size is not in the equation."
msg3 = "Try again. You are finding the difference between the polls."
msg4 = "Correct!"
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 12 - Standard Error of the Difference Between Polls

```yaml
type: MultipleChoiceExercise
key: 27b0d9c911
lang: r
xp: 50
skills:
  - 1
```

Using what we learned by answering the questions above, what is the standard error of $\bar{Y}\_{2} - \bar{Y}\_1$?

`@possible_answers`
- $\sqrt{\sigma\_2^2/N\_2 + \sigma\_1^2/N_1}$
- $\sqrt{\sigma\_2/N\_2 + \sigma\_1/N\_1}$
- $(\sigma\_2^2/N\_2 + \sigma\_1^2/N\_1)^2$
- $\sigma\_2^2/N\_2 + \sigma\_1^2/N\_1$

`@hint`
- Here's a hint to the first step: 
$\mbox{SE}[\bar{Y}\_{2} - \bar{Y}\_1] = \sqrt{\mbox{SE}[\bar{Y}\_{2}]^2 + \mbox{SE}[\bar{Y}_1]^2}$
- Remember that the standard error is the standard deviation divided by the square root of the sample size.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Correct!"
msg2 = "Try again. Remember that the standard error is equal to the sigma divided by the square root of N."
msg3 = "Try again. The solution is not squared."
msg4 = "Try again. Think about the relationship between standard error and standard deviation."
test_mc(correct = 1, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 13 - Compute the Estimates

```yaml
type: NormalExercise
key: 30c8ba7827
lang: r
xp: 100
skills:
  - 1
```

The answer to the previous question depends on $\sigma\_1$ and $\sigma\_2$, which we don't know. We learned that we can estimate these values using the sample standard deviation. 

Compute the estimates of $\sigma\_1$ and $\sigma\_2$.

`@instructions`
- Group the data by pollster.
- Summarize the standard deviation of the spreads for each of the two pollsters. Name the standard deviation `s`.
- Store the pollster names and standard deviations of the spreads ($\sigma$) in an object called `sigma`.

`@hint`
- Use the pipe `%>%` to pass the data in `polls` to the `group_by` function that groups the data by a variable of interest (such as "pollster").
- Use the pipe `%>%` to pass the grouped data to the `summarize` function that reduces grouped values to a single value. Use the `sd` function nested within `summarize` to find the standard deviation of the grouped 'spread' data.
- The `sigma` object should contain two columns and two rows. Name the standard deviation column `s`.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(pollster %in% c("Rasmussen Reports/Pulse Opinion Research","The Times-Picayune/Lucid") &
           enddate >= "2016-10-15" &
           state == "U.S.") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
```

`@sample_code`
```{r}
# The `polls` data have already been loaded for you. Use the `head` function to examine them.
head(polls)

# Create an object called `sigma` that contains a column for `pollster` and a column for `s`, the standard deviation of the spread



# Print the contents of sigma to the console
```

`@solution`
```{r}
# The `polls` data have already been loaded for you. Use the `head` function to examine them.
head(polls)

# Create an object called `sigma` that contains a column for `pollster` and a column for `s`, the standard deviation of the spread
sigma <- polls %>% group_by(pollster) %>%
  summarize(s = sd(spread))

# Print the contents of sigma to the console
sigma
```

`@sct`
```{r}
test_error()
test_function("sd",
              not_called_msg = "Use the `sd` function to find the standard deviation of the spread")
test_object("sigma", eq_condition = "equivalent", 
            undefined_msg = "Define an object called `sigma` that contains 2 columns (pollster and standard deviation) and two rows (one for each pollster).",
            incorrect_msg = "You have not correctly defined the object `sigma`. Use the `group_by` and `summarize` functions to group `polls` by pollster and summarize the standard deviation of the spread as `s`.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 14 - Probability Distribution of the Spread

```yaml
type: MultipleChoiceExercise
key: cbc1022f28
lang: r
xp: 50
skills:
  - 1
```

What does the central limit theorem tell us about the distribution of the differences between the pollster averages, $\bar{Y}\_2 - \bar{Y}\_1$?

`@possible_answers`
- The central limit theorem cannot tell us anything because this difference is not the average of a sample.
- Because $Y\_{ij}$ are approximately normal, the averages are normal too.
- If we assume $N\_2$ and $N\_1$ are large enough, $\bar{Y}\_2$ and $\bar{Y}\_1$, and their difference, are approximately normal.
- These data do not contain vectors of 0 and 1, so the central limit theorem does not apply.

`@hint`
- The probability distribution of a sample average $\bar{X}$ is approximately normal, with expected value $\mu$ and standard error $\sigma/\sqrt{N}$.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. Read the answer choices carefully."
msg2 = "Try again. Recall what we learned in the previous exercises."
msg3 = "Correct!"
msg4 = "Try again. The central limit theorem does apply here."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 15 - Calculate the 95% Confidence Interval of the Spreads

```yaml
type: NormalExercise
key: 8da72f3965
lang: r
xp: 100
skills:
  - 1
```

We have constructed a random variable that has expected value $b\_2 - b\_1$, the pollster bias difference. If our model holds, then this random variable has an approximately normal distribution. The standard error of this random variable depends on $\sigma\_1$ and $\sigma\_2$, but we can use the sample standard deviations we computed earlier. We have everything we need to answer our initial question: is $b\_2 - b\_1$ different from 0? 

Construct a 95% confidence interval for the difference $b\_2$ and $b\_1$. Does this interval contain zero?

`@instructions`
- Use pipes `%>%` to pass the data `polls` on to functions that will group by pollster and summarize the average spread, standard deviation, and number of polls per pollster.
- Calculate the estimate by subtracting the average spreads. Save this estimate to a variable called `estimate`.
- Calculate the standard error using the standard deviations of the spreads and the sample size. Save this value to a variable called `se_hat`.
- Calculate the 95% confidence intervals using the `qnorm` function. Save the lower and then the upper confidence interval to a variable called `ci`.

`@hint`
- Recall the formula for the standard error:
$\mbox{SE}[\bar{Y}\_{2} - \bar{Y}\_1] = \sqrt{\sigma\_2^2/N\_2 + \sigma\_1^2/N\_1}$

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(pollster %in% c("Rasmussen Reports/Pulse Opinion Research","The Times-Picayune/Lucid") &
           enddate >= "2016-10-15" &
           state == "U.S.") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
```

`@sample_code`
```{r}
# The `polls` data have already been loaded for you. Use the `head` function to examine them.
head(polls)

# Create an object called `res` that summarizes the average, standard deviation, and number of polls for the two pollsters.




# Store the difference between the larger average and the smaller in a variable called `estimate`. Print this value to the console.




# Store the standard error of the estimates as a variable called `se_hat`. Print this value to the console.




# Calculate the 95% confidence interval of the spreads. Save the lower and then the upper confidence interval to a variable called `ci`.


```

`@solution`
```{r}
# The `polls` data have already been loaded for you. Use the `head` function to examine them.
head(polls)

# Create an object called `res` that summarizes the average, standard deviation, and number of polls for the two pollsters.
res <- polls %>% group_by(pollster) %>% 
  summarize(avg = mean(spread), s = sd(spread), N = n()) 

# Store the difference between the larger average and the smaller in a variable called `estimate`. Print this value to the console.
estimate <- res$avg[2] - res$avg[1]
estimate

# Store the standard error of the estimates as a variable called `se_hat`. Print this value to the console.
se_hat <- sqrt(res$s[2]^2/res$N[2] + res$s[1]^2/res$N[1])
se_hat

# Calculate the 95% confidence interval of the spreads. Save the lower and then the upper confidence interval to a variable called `ci`.
ci <- c(estimate - qnorm(0.975)*se_hat, estimate + qnorm(0.975)*se_hat)
```

`@sct`
```{r}
test_error()
test_function("qnorm", not_called_msg = "Make sure you are using the `qnorm` function. Use a value slightly less than 1 to calculate the 95% confidence interval.")

test_object("estimate",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Have you made an object called 'estimate'?",
            incorrect_msg = "The value contained in the object 'estimate' is not correct. Make sure you are subtracting the poll with the smaller average from the poll with the larger average.")

test_object("se_hat",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Have you made an object called 'se_hat'?",
            incorrect_msg = "The value contained in the object 'se_hat' is not correct. Make sure you are using the formula we derived previously.")

test_object("ci",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Have you made an object called 'ci'?",
            incorrect_msg = "The values contained in the object 'ci' are not correct. Are you using the correct formula to calculate the confidence intervals? Make sure to save the lower confidence interval first.")
            
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 16 - Calculate the P-value

```yaml
type: NormalExercise
key: 7632fa8d52
lang: r
xp: 100
skills:
  - 1
```

The confidence interval tells us there is relatively strong pollster effect resulting in a difference of about 5%. Random variability does not seem to explain it. 

Compute a p-value to relay the fact that chance does not explain the observed pollster effect.

`@instructions`
- Use the `pnorm` function to calculate the probability that a random value is larger than the observed ratio of the estimate to the standard error.
- Multiply the probability by 2, because this is the two-tailed test.

`@hint`
- Our quantile is the estimate divided by the standard error.
- The expected value is 0 with a standard deviation of 1.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(pollster %in% c("Rasmussen Reports/Pulse Opinion Research","The Times-Picayune/Lucid") &
           enddate >= "2016-10-15" &
           state == "U.S.") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
```

`@sample_code`
```{r}
# We made an object `res` to summarize the average, standard deviation, and number of polls for the two pollsters.
res <- polls %>% group_by(pollster) %>% 
  summarize(avg = mean(spread), s = sd(spread), N = n()) 

# The variables `estimate` and `se_hat` contain the spread estimates and standard error, respectively.
estimate <- res$avg[2] - res$avg[1]
se_hat <- sqrt(res$s[2]^2/res$N[2] + res$s[1]^2/res$N[1])

# Calculate the p-value
```

`@solution`
```{r}
# We made an object `res` to summarize the average, standard deviation, and number of polls for the two pollsters.
res <- polls %>% group_by(pollster) %>% 
  summarize(avg = mean(spread), s = sd(spread), N = n()) 

# The variables `estimate` and `se_hat` contain the spread estimates and standard error, respectively.
estimate <- res$avg[2] - res$avg[1]
se_hat <- sqrt(res$s[2]^2/res$N[2] + res$s[1]^2/res$N[1])

# Calculate the p-value
2*(1 - pnorm(estimate/se_hat, 0, 1))
```

`@sct`
```{r}
test_error()
test_function("pnorm",
              not_called_msg = "Make sure to use the `pnorm` function to calculate the probability.")
test_output_contains("1.030287e-13", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are subtracting the 'pnorm' result from 1 and multiplying by 2.")
success_msg("Great work! Let's wrap it up.")
```

---

## Exercise 17 - Comparing Within-Poll and Between-Poll Variability

```yaml
type: NormalExercise
key: 8f77dad3f4
lang: r
xp: 100
skills:
  - 1
```

We compute statistic called the _t-statistic_ by dividing our estimate of $b\_2-b\_1$ by its estimated standard error:

$$
\frac{\bar{Y}\_2 - \bar{Y}\_1}{\sqrt{s\_2^2/N\_2 + s\_1^2/N\_1}}
$$
Later we learn will learn of another approximation for the distribution of this statistic for values of $N\_2$ and $N\_1$ that aren't large enough for the CLT. 

Note that our data has more than two pollsters. We can also test for pollster effect using all pollsters, not just two. The idea is to compare the variability across polls to variability within polls. We can construct statistics to test for effects and approximate their distribution. The area of statistics that does this is called Analysis of Variance or ANOVA. We do not cover it here, but ANOVA provides a very useful set of tools to answer questions such as: is there a pollster effect?

Compute the average and standard deviation for each pollster and examine the variability across the averages and how it compares to the variability within the pollsters, summarized by the standard deviation.

`@instructions`
- Group the `polls` data by pollster.
- Summarize the average and standard deviation of the spreads for each pollster.
- Create an object called `var` that contains three columns: pollster, mean spread, and standard deviation.
- Be sure to name the column for mean `avg` and the column for standard deviation `s`.

`@hint`
- Use the pipe `%>%` to pass the data in `polls` to the `group_by` function that groups the data by a variable of interest (such as "pollster").
- Use the pipe `%>%` to pass the grouped data to the `summarize` function that reduces grouped values to a single value. Use the `mean` and `sd` functions nested within `summarize` to find the average and standard deviation of the grouped 'spread' data.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data("polls_us_election_2016")
```

`@sample_code`
```{r}
# Execute the following lines of code to filter the polling data and calculate the spread
polls <- polls_us_election_2016 %>% 
  filter(enddate >= "2016-10-15" &
           state == "U.S.") %>%
  group_by(pollster) %>%
  filter(n() >= 5) %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100) %>%
  ungroup()

# Create an object called `var` that contains columns for the pollster, mean spread, and standard deviation. Print the contents of this object to the console.



```

`@solution`
```{r}
# Execute the following lines of code to filter the polling data and calculate the spread
polls <- polls_us_election_2016 %>% 
  filter(enddate >= "2016-10-15" &
           state == "U.S.") %>%
  group_by(pollster) %>%
  filter(n() >= 5) %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100) %>%
  ungroup()

# Create an object called `var` that contains columns for the pollster, mean spread, and standard deviation. Print the contents of this object to the console.

var <- polls %>% group_by(pollster) %>%
  summarize(avg = mean(spread), s = sd(spread))
var

```

`@sct`
```{r}
test_error()
test_function("sd",
              not_called_msg = "Use the `sd` function to find the standard deviations of the spreads.")
test_function("mean",
              not_called_msg = "Use the `mean` function to find the averages of the spreads.")

test_object("var", eq_condition = "equivalent", 
            undefined_msg = "Define an object called `var` that contains 3 columns (pollster, average, and standard deviation) and eleven rows (one for each pollster).",
            incorrect_msg = "You have not correctly defined the object `var`. Use the `group_by` and `summarize` functions to group `polls` by pollster and summarize the means and standard deviations of the spreads. Be sure to name the column for mean `avg` and the column for standard deviation `s`.")

success_msg("Great work!")
```

---

## End of Assessment

```yaml
type: PureMultipleChoiceExercise
key: adbfa24d5c
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
