---
title: Introduction to Inference
title_meta: Chapter 2
description: 'In this chapter, you will learn about the central limit theorem in practice.'
---

## Exercise 1. Sample average

```yaml
type: NormalExercise
key: eebd01a5fe
lang: r
xp: 100
skills:
  - 1
```

Write function called `take_sample` that takes the proportion of Democrats $p$ and the sample size $N$ as arguments and returns the sample average of Democrats (1) and Republicans (0).

Calculate the sample average if the proportion of Democrats equals 0.45 and the sample size is 100.

`@instructions`
- Define a function called `take_sample` that takes $p$ and $N$ as arguments.
- Use the `sample` function as the first statement in your function to sample $N$ elements from a vector of options where Democrats are assigned the value '1' and Republicans are assigned the value '0' in that order.
- Use the `mean` function as the second statement in your function to find the average value of the random sample.

`@hint`
- Define a function by specifying the arguments it will take in parentheses and the lines of code to run in brackets, as seen in the example code below:
```{r}
my_function <- function(argument_1, argument_2){
first_statement
second_statement
}
```
- Create a vector using `c()` that contains all possible polling options.
- Use `replace = TRUE` within the `sample` function to indicate that sampling from the vector should occur with replacement.
- Use `prob = ` within the `sample` function to indicate the probabilities of selecting either element within the vector of possibilities.

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# Write a function called `take_sample` that takes `p` and `N` as arguements and returns the average value of a randomly sampled population.





# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# Call the `take_sample` function to determine the sample average of `N` randomly selected people from a population containing a proportion of Democrats equal to `p`. Print this value to the console.


```

`@solution`
```{r}
# Write a function called `take_sample` that takes `p` and `N` as arguements and returns the average value of a randomly sampled population.
take_sample <- function(p, N){
    X <- sample(c(0,1), size = N, replace = TRUE, prob = c(1 - p, p))
    mean(X)
}

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# Call the `take_sample` function to determine the sample average of `N` randomly selected people from a population containing a proportion of Democrats equal to `p`. Print this value to the console.
take_sample(p,N)

```

`@sct`
```{r}
test_error()

test_function("sample", args = c("x", "size", "replace", "prob"),eval=c(NA,T,T,NA),
              not_called_msg = "Have you used `sample` to model the outcome of polling `N` voters?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of possible outcomes ('0' or '1'), the number of times to sample from that vector (`N`), that the sampling should be done with replacement 'replace = TRUE', and the probability of each outcome using 'prob ='.",
              incorrect_msg = "When generating `take_sample`, be sure to use the `sample` function. Include a vector of possible outcomes, the number of times to sample from that vector, whether replacement should occur, and the chances of each outcome occurring.")

test_function("mean", args = "x", eval=NA,
              not_called_msg = "Have you used `mean` to find the average of the population of polled voters where Democrats are specified as '1' and Republicans are specified as '0'?",
              args_not_specified = "Make sure to use the `mean` function to average of the sampled poll.")

test_output_contains("0.46", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are defining the `take_sample` function using the correct vector of possibilities (1 and 0) and vector of probabilities (p and 1-p). Take the mean of the sample average when p = 0.45 and N = 100.")

success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 2. Distribution of errors - 1

```yaml
type: NormalExercise
key: d7b04a475c
lang: r
xp: 100
skills:
  - 1
```

Assume the proportion of Democrats in the population $p$ equals 0.45 and that your sample size $N$ is 100 polled voters. The `take_sample` function you defined previously generates our estimate, $\bar{X}$.

Replicate the random sampling 10,000 times and calculate $p - \bar{X}$ for each random sample. Save these differences as a vector called `errors`. Find the average of `errors` and plot a histogram of the distribution.

`@instructions`
- The function `take_sample` that you defined in the previous exercise has already been run for you.
- Use the `replicate` function to replicate subtracting the result of `take_sample` from the value of $p$ 10,000 times.
- Use the `mean` function to calculate the average of the differences between the sample average and actual value of $p$.

`@hint`
- Our estimate $\bar{X}$ is estimated using `take_sample(p,N)`.
- The `replicate` function requires a number of replications and the expression to be replicated.

`@pre_exercise_code`
```{r}
take_sample <- function(p, N){
    X <- sample(c(0,1), size=N, replace=TRUE, prob=c(1-p, p))
    mean(X)
}
```

`@sample_code`
```{r}
# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# The variable `B` specifies the number of times we want the sample to be replicated
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Create an objected called `errors` that replicates subtracting the result of the `take_sample` function from `p` for `B` replications


# Calculate the mean of the errors. Print this value to the console.


```

`@solution`
```{r}
# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# The variable `B` specifies the number of times we want the sample to be replicated
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Create an objected called `errors` that replicates subtracting the result of the `take_sample` function from `p` for `B` replications
errors <- replicate(B, p - take_sample(p, N))

# Calculate the mean of the errors. Print this value to the console.
mean(errors)


```

`@sct`
```{r}
test_error()

test_function("replicate", args = c("n","expr"), eval=c(NA,NA),
              not_called_msg = "Be sure to use the `replicate` function to replicate the error calculation over `B` iterations.",
              args_not_specified = "Make sure to include the number of replications `B` and the expression to perform",
              incorrect_msg = "Are you supplying the correct number of replications and the correct expression to calculate the diference between 'p' and the output of 'take_sample'?")

test_function("mean", args = "x", eval=NA,
              not_called_msg = "Have you used `mean` to find the average of `errors`?",
              args_not_specified = "Make sure to use the `mean` function to average the errors.")

test_output_contains("-4.9e-05", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you do not delete any lines of code that were already supplied for you. For the purposes of this exercise, subtract the result of `take_sample` from the actual value of `p`.")

success_msg("Great work! Let's continue.")
```

---

## Exercise 3. Distribution of errors - 2

```yaml
type: MultipleChoiceExercise
key: dcade7b703
lang: r
xp: 50
skills:
  - 1
```

In the last exercise, you made a vector of differences between the actual value for $p$ and an estimate, $\bar{X}$. We called these differences between the actual and estimated values `errors`. 

The `errors` object has already been loaded for you. Use the `hist` function to plot a histogram of the values contained in the vector `errors`. Which statement best describes the distribution of the errors?

`@possible_answers`
- The errors are all about 0.05.
- The error are all about -0.05.
- The errors are symmetrically distributed around 0.
- The errors range from -1 to 1.

`@hint`
- The random sample sometimes generated an estimate that was higher than the actual proportion of Democrats and it sometimes estimated a lower proportion.

`@pre_exercise_code`
```{r}
take_sample <- function(p, N){
    X <- sample(c(0,1), size=N, replace=TRUE, prob=c(1-p, p))
    mean(X)
}
p <- 0.45
N <- 100
B <- 10000
set.seed(1)
errors <- replicate(B, p - take_sample(p, N))
```

`@sct`
```{r}
msg1 = "Try again. About half of the errors were negative values."
msg2 = "Try again. About half of the errors were positive values."
msg3 = "Correct! Let's move on to a similar problem."
msg4 = "Try again. The errors ranged from about -0.2 to 0.2."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 4. Average size of error

```yaml
type: NormalExercise
key: 603d39fc33
lang: r
xp: 100
skills:
  - 1
```

The error $p-\bar{X}$ is a random variable. In practice, the error is not observed because we do not know the actual proportion of Democratic voters, $p$. However, we can describe the size of the error by constructing a simulation. 

What is the average size of the error if we define the size by taking the absolute value $\mid p-\bar{X}\mid$ ?

`@instructions`
- Use the sample code to generate `errors`, a vector of $\mid p-\bar{X}\mid$.
- Calculate the absolute value of `errors` using the `abs` function. 
- Calculate the average of these values using the `mean` function.

`@hint`
- Nest the `abs` function within the `mean` function to generate the average of the absolute values in a single line of code.

`@pre_exercise_code`
```{r}
take_sample <- function(p, N){
    X <- sample(c(0,1), size=N, replace=TRUE, prob=c(1-p, p))
    mean(X)
}
```

`@sample_code`
```{r}
# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# The variable `B` specifies the number of times we want the sample to be replicated
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# We generated `errors` by subtracting the estimate from the actual proportion of Democratic voters
errors <- replicate(B, p - take_sample(p, N))

# Calculate the mean of the absolute value of each simulated error. Print this value to the console.


```

`@solution`
```{r}
# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# The variable `B` specifies the number of times we want the sample to be replicated
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# We generated `errors` by subtracting the estimate from the actual proportion of Democratic voters
errors <- replicate(B, p - take_sample(p, N))

# Calculate the mean of the absolute value of each simulated error. Print this value to the console.
mean(abs(errors))

```

`@sct`
```{r}
test_error()
test_function("abs", not_called_msg = "Make sure to use the `abs` function to calculate the absolute values of the simulated errors.")
test_function("mean", not_called_msg = "Be sure to use the `mean` function to find the average of the absolute values of the simulated errors.")
test_output_contains("0.039267", incorrect_msg = "You are not providing a calculation that gives the correct answer. Do not delete any lines of code supplied for you. In one line of code, find the average of the absolute value of the simulated errors.")
success_msg("Great work! Let's move on.")
```

---

## Exercise 5. Standard deviation of the spread

```yaml
type: NormalExercise
key: f0f996e789
lang: r
xp: 100
skills:
  - 1
```

The standard error is related to the typical **size** of the error we make when predicting. We say **size** because, as we just saw, the errors are centered around 0. In that sense, the typical error is 0. For mathematical reasons related to the central limit theorem, we actually use the standard deviation of `errors` rather than the average of the absolute values. 

As we have discussed, the standard error is the square root of the average squared distance $(\bar{X} - p)^2$. The standard deviation is defined as the square root of the distance squared.

Calculate the standard deviation of the spread.

`@instructions`
- Use the sample code to generate `errors`, a vector of $\mid p-\bar{X}\mid$.
- Use `^2` to square the distances.
- Calculate the average squared distance using the `mean` function.
- Calculate the square root of these values using the `sqrt` function.

`@hint`
- Nest the `mean` function within the `sqrt` function to generate the standard deviation in a single line of code.

`@pre_exercise_code`
```{r}
take_sample <- function(p, N){
    X <- sample(c(0,1), size=N, replace=TRUE, prob=c(1-p, p))
    mean(X)
}
```

`@sample_code`
```{r}
# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# The variable `B` specifies the number of times we want the sample to be replicated
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# We generated `errors` by subtracting the estimate from the actual proportion of Democratic voters
errors <- replicate(B, p - take_sample(p, N))

# Calculate the standard deviation of `errors`


```

`@solution`
```{r}
# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# The variable `B` specifies the number of times we want the sample to be replicated
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# We generated `errors` by subtracting the estimate from the actual proportion of Democratic voters
errors <- replicate(B, p - take_sample(p, N))

# Calculate the standard deviation of `errors`
sqrt(mean(errors^2))

```

`@sct`
```{r}
test_error()
test_function("mean", args = "x",
              not_called_msg = "Have you used `mean` to find the average of the squared errors?",
              incorrect_msg = "To calculate the standard deviation, you'll need to square the errors before you take the average.")
test_function("sqrt",
              not_called_msg = "Have you used `sqrt` to calculate the square root of the average squared errors?")
test_output_contains("0.04949939", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are squaring the errors before you take the average. Then calculate the square root of the average.")
success_msg("Great work! Let's continue.")
```

---

## Exercise 6. Estimating the standard error

```yaml
type: NormalExercise
key: 5ec7e49a09
lang: r
xp: 100
skills:
  - 1
```

The theory we just learned tells us what this standard deviation is going to be because it is the standard error of $\bar{X}$. 

Estimate the standard error given an expected value of 0.45 and a sample size of 100.

`@instructions`
- Calculate the standard error using the `sqrt` function

`@hint`
- The standard error is defined using the following equation:
$$ SE=\sqrt{p(1-p)/N} $$

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# Define `p` as the expected value equal to 0.45
p <- 0.45

# Define `N` as the sample size
N <- 100

# Calculate the standard error


```

`@solution`
```{r}
# Define `p` as the expected value equal to 0.45
p <- 0.45

# Define `N` as the sample size
N <- 100

# Calculate the standard error
sqrt(p*(1-p)/N)

```

`@sct`
```{r}
test_error()
test_function("sqrt",
              not_called_msg = "Use the `sqrt` function to calculate the standard error.")
test_output_contains("0.04974937", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are dividing by the sample size before taking the square root.")
success_msg("Great work! Let's keep going.")
```

---

## Exercise 7. Standard error of the estimate

```yaml
type: NormalExercise
key: ecb44f6763
lang: r
xp: 100
skills:
  - 1
```

In practice, we don't know $p$, so we construct an estimate of the theoretical prediction based by plugging in $\bar{X}$ for $p$. Calculate the standard error of the estimate: $$\hat{\mbox{SE}}(\bar{X})$$

`@instructions`
- Simulate a poll `X` using the `sample` function.
- When using the `sample` function, create a vector using `c()` that contains all possible polling options where '1' indicates a Democratic voter and '0' indicates a Republican voter.
- When using the `sample` function, use `replace = TRUE` within the `sample` function to indicate that sampling from the vector should occur with replacement.
- When using the `sample` function, use `prob = ` within the `sample` function to indicate the probabilities of selecting either element (0 or 1) within the vector of possibilities.
- Use the `mean` function to calculate the average of the simulated poll, `X_bar`.
- Calculate the standard error of the `X_bar` using the `sqrt` function and print the result.

`@hint`
- The standard error is defined using the following equation:
$$ \hat{\mbox{SE}}(\bar{X})=\sqrt{\bar{X}(1-\bar{X})/N} $$

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# Define `p` as a proportion of Democratic voters to simulate
p <- 0.45

# Define `N` as the sample size
N <- 100

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define `X` as a random sample of `N` voters with a probability of picking a Democrat ('1') equal to `p`


# Define `X_bar` as the average sampled proportion


# Calculate the standard error of the estimate. Print the result to the console.


```

`@solution`
```{r}
# Define `p` as a proportion of Democratic voters to simulate
p <- 0.45

# Define `N` as the sample size
N <- 100

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define `X` as a random sample of `N` voters with a probability of picking a Democrat ('1') equal to `p`
X <- sample(c(0,1), size=N, replace=TRUE, prob=c(1-p, p))

# Define `X_bar` as the average sampled proportion
X_bar <- mean(X)

# Calculate the standard error of the estimate. Print the result to the console.
sqrt(X_bar*(1-X_bar)/N)

```

`@sct`
```{r}
test_error()

test_function("sample", args = c("x", "size", "replace", "prob"),eval=c(NA,T,T,NA),
              not_called_msg = "Have you used `sample` to model the outcome of polling `N` voters?",
              args_not_specified = "In the function `sample`, be sure to provide a vector of possible outcomes ('0' or '1'), the number of times to sample from that vector (`N`), that the sampling should be done with replacement 'replace = TRUE', and the probability of each outcome using 'prob ='.",
              incorrect_msg = "When generating `X`, be sure to use the `sample` function. Include a vector of possible outcomes, the number of times to sample from that vector, whether replacement should occur, and the chances of each outcome occurring.")

test_function("mean", args = "x", eval=NA,
              not_called_msg = "Have you used `mean` to find the average value of `X`?",
              args_not_specified = "Make sure to use the `mean` function to average the simulated result of `X`.")

test_function("sqrt",
              not_called_msg = "Use the `sqrt` function to calculate the standard error.")

test_output_contains("0.04983974", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are dividing by the sample size before taking the square root.")
```

---

## Exercise 8. Plotting the standard error

```yaml
type: MultipleChoiceExercise
key: 482ee1416c
lang: r
xp: 50
skills:
  - 1
```

The standard error estimates obtained from the Monte Carlo simulation, the theoretical prediction, and the estimate of the theoretical prediction are all very close, which tells us that the theory is working. This gives us a practical approach to knowing the typical error we will make if we predict $p$ with $\hat{X}$. The theoretical result gives us an idea of how large a sample size is required to obtain the precision we need. Earlier we learned that the largest standard errors occur for $p=0.5$. 

Create a plot of the largest standard error for $N$ ranging from 100 to 5,000. Based on this plot, how large does the sample size have to be to have a standard error of about 1%?

```{r}
N <- seq(100, 5000, len = 100)
p <- 0.5
se <- sqrt(p*(1-p)/N)
```

`@possible_answers`
- 100
- 500
- 2,500
- 4,000

`@hint`
- Plot the standard error `se` as a function of the sample size `N`
- You can also solve for $N$ using the following equation:

$$
\sqrt{p(1-p)/N} = 0.01 \Rightarrow p(1-p)/N = 0.0001 \Rightarrow N = 10000 p (1-p)
$$

`@pre_exercise_code`
```{r}
#no pec
```

`@sct`
```{r}
msg1 = "Try again. That sample size isn't big enough."
msg2 = "Try again. That sample size isn't big enough."
msg3 = "Correct! Let's move on."
msg4 = "Try again. That number is larger than we require."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 9. Distribution of X-hat

```yaml
type: MultipleChoiceExercise
key: 10195f11c9
lang: r
xp: 50
skills:
  - 1
```

For $N=100$, the central limit theorem tells us that the distribution of $\hat{X}$ is...

`@possible_answers`
- practically equal to $p$.
- approximately normal with expected value $p$ and standard error $\sqrt{p(1-p)/N}$.
- approximately normal with expected value $\bar{X}$ and standard error $\sqrt{\bar{X}(1-\bar{X})/N}$.
- not a random variable.

`@hint`
- The central limit theorem tells us that the distribution of $\hat{X}$ is normal.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. In this case, our estimate is a random variable."
msg2 = "Correct! Let's continue."
msg3 = "Try again. The expected value is equal to the theoretical value."
msg4 = "Try again. It is a random variable."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 10. Distribution of the errors

```yaml
type: MultipleChoiceExercise
key: ccf27292ab
lang: r
xp: 50
skills:
  - 1
```

We calculated a vector `errors` that contained, for each simulated sample, the difference between the actual value $p$ and our estimate $\hat{X}$.

The errors $\bar{X} - p$ are:

`@possible_answers`
- practically equal to 0.
- approximately normal with expected value $0$ and standard error $\sqrt{p(1-p)/N}$.
- approximately normal with expected value $p$ and standard error $\sqrt{p(1-p)/N}$.
- not a random variable.

`@hint`
- Subtracting a constant only shifts a random variable.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. The errors ranged in value."
msg2 = "Correct! Let's continue."
msg3 = "Try again. Subtracting a constant shifts a random variable."
msg4 = "Try again. It is a random variable."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 11. Plotting the errors

```yaml
type: NormalExercise
key: 0d7fa3da55
lang: r
xp: 100
skills:
  - 1
```

Make a qq-plot of the `errors` you generated previously to see if they follow a normal distribution.

`@instructions`
- Run the supplied code
- Use the `qqnorm` function to produce a qq-plot of the errors.
- Use the `qqline` function to plot a line showing a normal distribution.

`@hint`
- Supply `errors` to the function `qqnorm` and then to the function `qqplot`.

`@pre_exercise_code`
```{r}
take_sample <- function(p, N){
    X <- sample(c(0,1), size=N, replace=TRUE, prob=c(1-p, p))
    mean(X)
}
```

`@sample_code`
```{r}
# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# The variable `B` specifies the number of times we want the sample to be replicated
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Generate `errors` by subtracting the estimate from the actual proportion of Democratic voters
errors <- replicate(B, p - take_sample(p, N))

# Generate a qq-plot of `errors` with a qq-line showing a normal distribution



```

`@solution`
```{r}
# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# The variable `B` specifies the number of times we want the sample to be replicated
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Generate `errors` by subtracting the estimate from the actual proportion of Democratic voters
errors <- replicate(B, p - take_sample(p, N))

# Generate a qq-plot of `errors` with a qq-line showing a normal distribution
qqnorm(errors)
qqline(errors)
```

`@sct`
```{r}
test_error()
test_function("qqnorm", not_called_msg = "Did you use the `qqnorm` function to generate the qq-plot?")
test_function("qqline", not_called_msg = "Did you use the `qqline` function to generate a line showing a normal distribution on the qq-plot?")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 12. Estimating the probability of a specific value of X-bar

```yaml
type: NormalExercise
key: ea1732d8de
lang: r
xp: 100
skills:
  - 1
```

If $p=0.45$ and $N=100$, use the central limit theorem to estimate the probability that $\bar{X}>0.5$.

`@instructions`
- Use `pnorm` to define the probability that a value will be greater than 0.5.

`@hint`
- The expected value of $\bar{X} = p$.
- The standard deviation of $\bar{X} = \sqrt{p(1-p)/N}$ 
- Subtract the probability calculated using `pnorm` from 1 to determine the probability that a value will be greater than 0.5.

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# Calculate the probability that the estimated proportion of Democrats in the population is greater than 0.5. Print this value to the console.



```

`@solution`
```{r}
# Define `p` as the proportion of Democrats in the population being polled
p <- 0.45

# Define `N` as the number of people polled
N <- 100

# Calculate the probability that the estimated proportion of Democrats in the population is greater than 0.5. Print this value to the console.
1 - pnorm(0.5, p, sqrt(p*(1-p)/N))
```

`@sct`
```{r}
test_error()
test_function("pnorm",
              not_called_msg = "Have you used `pnorm` to calculate the probability?",
              args_not_specified = "Make sure to specify the proportion to calculate the probability, the expected value, and the standard deviation.",
              incorrect_msg = "Make sure to use `pnorm`. Include the proportion you want to test, the expected value, and the standard deviation.")
test_output_contains("0.1574393", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are subtracting the probability of the value being less than 0.5 by 1.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 13. Estimating the probability of a specific error size

```yaml
type: NormalExercise
key: c85b58b288
lang: r
xp: 100
skills:
  - 1
```

Assume you are in a practical situation and you don't know $p$. Take a sample of size $N=100$ and obtain a sample average of $\bar{X} = 0.51$. 

What is the CLT approximation for the probability that your error size is equal or larger than 0.01?

`@instructions`
- Calculate the standard error of the sample average using the `sqrt` function.
- Use `pnorm` twice to define the probabilities that a value will be less than -0.01 or greater than 0.01.
- Combine these results to calculate the probability that the error *size* will be 0.01 or larger.

`@hint`
- The standard error of $\hat{X} = \sqrt{\hat{X}(1-\hat{X})/N}$ 
- Recall that the expected value of the error is 0.
- Remember to subtract the probability calculated using `pnorm` from 1 to determine the probability that a value will be 0.01 or higher.
- Don't forget to add the probability that the error will be less than -0.01.

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# Define `N` as the number of people polled
N <-100

# Define `X_hat` as the sample average
X_hat <- 0.51

# Define `se_hat` as the standard error of the sample average


# Calculate the probability that the error is 0.01 or larger


```

`@solution`
```{r}
# Define `N` as the number of people polled
N <-100

# Define `X_hat` as the sample average
X_hat <- 0.51

# Define `se_hat` as the standard error of the sample average
se_hat <- sqrt(X_hat*(1-X_hat)/N)

# Calculate the probability that the error is 0.01 or larger
1 - pnorm(.01, 0, se_hat) + pnorm(-0.01, 0, se_hat)

```

`@sct`
```{r}
test_error()
test_function("pnorm", index=2,
              not_called_msg = "Have you used `pnorm` to calculate the probability?")
test_output_contains("0.8414493", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you account for the probability that the error is less than 0.01 or less than -0.01.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## End of Assessment

```yaml
type: PureMultipleChoiceExercise
key: f8bfad775f
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
