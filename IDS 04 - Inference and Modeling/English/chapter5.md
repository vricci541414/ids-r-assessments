---
title: Bayesian Statistics
description: 'In this chapter, you will learn about Bayesian statistics.'
---

## Exercise 1 -  Statistics in the Courtroom

```yaml
type: MultipleChoiceExercise
key: 729bda2a7d
lang: r
xp: 50
skills:
  - 1
```

In 1999 in England [Sally Clark](https://en.wikipedia.org/wiki/Sally_Clark) was found guilty of the murder of two of her sons. Both infants were found dead in the morning, one in 1996 and another in 1998, and she claimed the cause of death was sudden infant death syndrome (SIDS). No evidence of physical harm was found on the two infants so the main piece of evidence against her was the testimony of Professor Sir Roy Meadow, who testified that the chances of two infants dying of SIDS was 1 in 73 million. He arrived at this figure by finding that the rate of SIDS was 1 in 8,500 and then calculating that the chance of two SIDS cases was 8,500 $\times$ 8,500 $\approx$ 73 million. 

Based on what we've learned throughout this course, which statement best describes a potential flaw in Sir Meadow's reasoning?

`@possible_answers`
- Sir Meadow assumed the second death was independent of the first son being affected, thereby ignoring possible genetic causes.
- There is no flaw. The multiplicative rule always applies in this way: $\mbox{Pr}(A \mbox{ and } B) =\mbox{Pr}(A)\mbox{Pr}(B)$
- Sir Meadow should have added the probabilities: $\mbox{Pr}(A \mbox{ and } B) =\mbox{Pr}(A)+\mbox{Pr}(B)$
- The rate of SIDS is too low to perform these types of statistics.

`@hint`
- Sir Meadow's calculations assume independence.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Correct! If genetics plays a role then the probability a second case of SIDS is more likely given the first occurrence."
msg2 = "Try again. The multiplicative rule has assumptions."
msg3 = "Try again. Factors other than random chance may have affected these children."
msg4 = "Try again. Sir Meadow's calculations are valid assuming the events are independent."
test_mc(correct = 1, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 2 - Recalculating the SIDS Statistics

```yaml
type: NormalExercise
key: 3b97e25f53
lang: r
xp: 100
skills:
  - 1
```

Let's assume that there is in fact a genetic component to SIDS and the the probability of $\mbox{Pr}(\mbox{second case of SIDS} \mid \mbox{first case of SIDS}) = 1/100$, is much higher than 1 in 8,500. 

What is the probability of both of Sally Clark's sons dying of SIDS?

`@instructions`
- Calculate the probability of both sons dying to SIDS.

`@hint`
- The multiplicative rule applies here.

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# Define `Pr_1` as the probability of the first son dying of SIDS
Pr_1 <- 1/8500

# Define `Pr_2` as the probability of the second son dying of SIDS
Pr_2 <- 1/100

# Calculate the probability of both sons dying of SIDS. Print this value to the console.
```

`@solution`
```{r}
# Define `Pr_1` as the probability of the first son dying of SIDS
Pr_1 <- 1/8500

# Define `Pr_2` as the probability of the second son dying of SIDS
Pr_2 <- 1/100

# Calculate the probability of both sons dying of SIDS. Print this value to the console.
Pr_1*Pr_2
```

`@sct`
```{r}
test_error()
test_output_contains("1.176471e-06", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are using the multiplicative rule.")
success_msg("Great work! Let's think about this case some more.")
```

---

## Exercise 3 - Bayes' Rule in the Courtroom

```yaml
type: MultipleChoiceExercise
key: b557ec49ad
lang: r
xp: 50
skills:
  - 1
```

Many press reports stated that the expert claimed the probability of Sally Clark being innocent as 1 in 73 million. Perhaps the jury and judge also interpreted the testimony this way. This probability can be written like this: 

$$
    \mbox{Pr}(\mbox{mother is a murderer} \mid \mbox{two children found dead with no evidence of harm}) 
$$
    
Bayes' rule tells us this probability is equal to:

Bayes' rule tells us this probability is equal to:

`@possible_answers`
- $$\frac{\mbox{Pr}(\mbox{two children found dead with no evidence of harm}) \mbox{Pr}(\mbox{mother is a murderer})}{\mbox{Pr}(\mbox{two children found dead with no evidence of harm})}$$ 
- $\mbox{Pr}(\mbox{two children found dead with no evidence of harm})\mbox{Pr}(\mbox{mother is a murderer} )$
- $$\frac{\mbox{Pr}(\mbox{two children found dead with no evidence of harm} \mid \mbox{mother is a murderer} ) \mbox{Pr}(\mbox{mother is a murderer})}{\mbox{Pr}(\mbox{two children found dead with no evidence of harm})}$$ 
- 1/8500

`@hint`
- Bayes' rule takes into account the independent probabilities.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. This solution is missing an important term."
msg2 = "Try again. Review Bayes' rule."
msg3 = "Correct!"
msg4 = "Try again. We'll need to take into account the probabilities of each event."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 4 - Calculate the Probability

```yaml
type: NormalExercise
key: d8672efe81
lang: r
xp: 100
skills:
  - 1
```

Assume that the probability of a murderer finding a way to kill her two children without leaving evidence of physical harm is:

$\mbox{Pr}(\mbox{two children found dead with no evidence of harm} \mid \mbox{mother is a murderer} ) = 0.50$

Assume that the murder rate among mothers is 1 in 1,000,000. 

$\mbox{Pr}(\mbox{mother is a murderer} ) = 1/1,000,000$

According to Bayes' rule, what is the probability of:

$$\mbox{Pr}(\mbox{mother is a murderer} \mid \mbox{two children found dead with no evidence of harm})$$

`@instructions`
- Use Bayes' rule to calculate the probability that the mother is a murderer, considering the rates of murdering mothers in the population, the probability that two siblings die of SIDS, and the probability that a murderer kills children without leaving evidence of physical harm.
- Print your result to the console.

`@hint`
- Remember our solution to the previous problem.
$$ \mbox{Pr}(\mbox{mother is a murderer} \mid \mbox{two children found dead with no evidence of harm})  = \frac{\mbox{Pr}(\mbox{two children found dead with no evidence of harm} \mid \mbox{mother is a murderer} ) \mbox{Pr}(\mbox{mother is a murderer})}{\mbox{Pr}(\mbox{two children found dead with no evidence of harm})}$$

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
# Define `Pr_1` as the probability of the first son dying of SIDS
Pr_1 <- 1/8500

# Define `Pr_2` as the probability of the second son dying of SIDS
Pr_2 <- 1/100

# Define `Pr_B` as the probability of both sons dying of SIDS
Pr_B <- Pr_1*Pr_2

# Define Pr_A as the rate of mothers that are murderers
Pr_A <- 1/1000000

# Define Pr_BA as the probability that two children die without evidence of harm, given that their mother is a murderer
Pr_BA <- 0.50

# Define Pr_AB as the probability that a mother is a murderer, given that her two children died with no evidence of physical harm. Print this value to the console.
```

`@solution`
```{r}
# Define `Pr_1` as the probability of the first son dying of SIDS
Pr_1 <- 1/8500

# Define `Pr_2` as the probability of the second son dying of SIDS
Pr_2 <- 1/100

# Define `Pr_B` as the probability of both sons dying of SIDS
Pr_B <- Pr_1*Pr_2

# Define Pr_A as the rate of mothers that are murderers
Pr_A <- 1/1000000

# Define Pr_BA as the probability that two children die without evidence of harm, given that their mother is a murderer
Pr_BA <- 0.50

# Define Pr_AB as the probability that a mother is a murderer, given that her two children died with no evidence of physical harm. Print this value to the console.
Pr_AB <- Pr_BA*Pr_A/Pr_B
Pr_AB
```

`@sct`
```{r}
test_error()
test_output_contains("0.425", incorrect_msg = "You are not providing a calculation that gives the correct answer or you forgot to print the result to the console. Make sure you are using Bayes' rule.")
success_msg("Great work! Let's think about what mistake Sir Meadow made.")
```

---

## Exercise 5 - Misuse of Statistics in the Courts

```yaml
type: MultipleChoiceExercise
key: 0ad03f3a50
lang: r
xp: 50
skills:
  - 1
```

After Sally Clark was found guilty, the Royal Statistical Society issued a statement saying that there was "no statistical basis" for the expert's claim. They expressed concern at the "misuse of statistics in the courts". Eventually, Sally Clark was acquitted in June 2003. 

In addition to misusing the multiplicative rule as we saw earlier, what else did Sir Meadow miss?

`@possible_answers`
- He made an arithmetic error in forgetting to divide by the rate of SIDS in siblings.
- He did not take into account how rare it is for a mother to murder her children.
- He mixed up the numerator and denominator of Bayes' rule.
- He did not take into account murder rates in the population.

`@hint`
- We used an estimate for a very rare event in our calculations of the probability that Sally Clark's children died of SIDS.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. Remember what we included in our calculations."
msg2 = "Correct! After using Bayes' rule, we found a probability closer to 0.5 than 1 in 73 million."
msg3 = "Try again. Sir Meadow did not use Bayes' rule."
msg4 = "Try again. Sir Meadow did not account for something else in his calculations."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 6 - Back to Election Polls

```yaml
type: NormalExercise
key: dd2b7cd72c
lang: r
xp: 100
skills:
  - 1
```

Florida is one of the most closely watched states in the U.S. election because it has many electoral votes and the election is generally close. Create a table with the poll spread results from Florida taken during the last days before the election using the sample code.

The CLT tells us that the average of these spreads is approximately normal. Calculate a spread average and provide an estimate of the standard error.

`@instructions`
- Calculate the average of the spreads. Call this average `avg` in the final table.
- Calculate an estimate of the standard error of the spreads. Call this standard error `se` in the final table.
- Use the `mean` and `sd` functions nested within `summarize` to find the average and standard deviation of the grouped `spread` data.
- Save your results in an object called `results`.

`@hint`
- Use the pipe `%>%` to pass the grouped data to the `summarize` function that reduces grouped values to a single value. 
- Remember that the standard error is the standard deviation divided by the square root of the sample size.
- You can use `n()` within the summarize function to tally the number of observations.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data(polls_us_election_2016)
```

`@sample_code`
```{r}
# Load the libraries and poll data
library(dplyr)
library(dslabs)
data(polls_us_election_2016)

# Create an object `polls` that contains the spread of predictions for each candidate in Florida during the last polling days
polls <- polls_us_election_2016 %>% 
  filter(state == "Florida" & enddate >= "2016-11-04" ) %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)

# Examine the `polls` object using the `head` function
head(polls)

# Create an object called `results` that has two columns containing the average spread (`avg`) and the standard error (`se`). Print the results to the console.


```

`@solution`
```{r}
# Load the libraries and poll data
library(dplyr)
library(dslabs)
data(polls_us_election_2016)

# Create an object `polls` that contains the spread of predictions for each candidate in Florida during the last polling days
polls <- polls_us_election_2016 %>% 
  filter(state == "Florida" & enddate >= "2016-11-04" ) %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)

# Examine the `polls` object using the `head` function
head(polls)

# Create an object called `results` that has two columns containing the average spread (`avg`) and the standard error (`se`). Print the results to the console.
results <- polls %>% summarize(avg = mean(spread),  se = sd(spread)/sqrt(n()))
results

```

`@sct`
```{r}
test_error()
test_function("sd",
              not_called_msg = "Use the `sd` function to find the standard deviations of the spreads. Divide the standard deviation by the square root of the sample size to calculate the standard error.")
test_function("mean",
              not_called_msg = "Use the `mean` function to find the averages of the spreads.")
test_object("results", eq_condition = "equivalent", 
            undefined_msg = "Define an object called `results` that contains 2 columns (avg and se).",
            incorrect_msg = "You have not correctly defined the object `results`. Use the `summarize` functions to summarize the means and standard errors of the spreads.")
success_msg("Great work! Let's continue with our Bayesian approach.")
```

---

## Exercise 7 - The Prior Distribution

```yaml
type: MultipleChoiceExercise
key: b381fa5b7c
lang: r
xp: 50
skills:
  - 1
```

Assume a Bayesian model sets the prior distribution for Florida's election night spread $d$ to be normal with expected value $\mu$ and standard deviation $\tau$. 

What are the interpretations of $\mu$ and $\tau$?

`@possible_answers`
- $\mu$ and $\tau$ are arbitrary numbers that let us make probability statements about $d$.
- $\mu$ and $\tau$ summarize what we would predict for Florida before seeing any polls.
- $\mu$ and $\tau$ summarize what we want to be true. We therefore set $\mu$ at $0.10$ and $\tau$ at $0.01$. 
- The choice of prior has no effect on the Bayesian analysis.

`@hint`
- Remember that in our baseball example, $\mu$ and $\tau$ represented the expected value and standard deviation of all players.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. Remember how we used these values in the baseball example."
msg2 = "Correct! Based on past elections, we would set mu close to 0, because both Republicans and Democrats have won, and tau at about 0.02, because these elections tend to be close."
msg3 = "Try again. We can use existing data to make these estimates."
msg4 = "Try again. The choice of prior does affect the analysis."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 8 - Estimate the Posterior Distribution

```yaml
type: NormalExercise
key: ec6d7d1475
lang: r
xp: 100
skills:
  - 1
```

The CLT tells us that our estimate of the spread $\hat{d}$ has a normal distribution with expected value $d$ and standard deviation $\sigma$, which we calculated in a previous exercise. 

Use the formulas for the posterior distribution to calculate the expected value of the posterior distribution if we set $\mu = 0$ and $\tau = 0.01$.

`@instructions`
- Define $\mu$ and $\tau$
- Identify which elements stored in the object `results` represent $\sigma$ and $Y$
- Estimate `B` using $\sigma$ and $\tau$
- Estimate the posterior distribution using `B`, $\mu$, and $Y$

`@hint`
- B is constructed using the following formula:
$$ \begin{aligned} B &= \frac{\sigma^2}{\sigma^2+\tau^2} \end{aligned} $$

- The posterior distribution has an expected value given by the following formula:
$$ \begin{aligned} \mbox{E}(p \mid y) &= B \mu + (1-B) Y\ \end{aligned} $$

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data(polls_us_election_2016)
polls <- polls_us_election_2016 %>% 
  filter(state == "Florida" & enddate >= "2016-11-04" ) %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
results <- polls %>% summarize(avg = mean(spread),  se = sd(spread)/sqrt(n()))
```

`@sample_code`
```{r}
# The results` object has already been loaded. Examine the values stored: `avg` and `se` of the spread
results

# Define `mu` and `tau`
mu <- 0
tau <- 0.01

# Define a variable called `sigma` that contains the standard error in the object `results`


# Define a variable called `Y` that contains the average in the object `results`


# Define a variable `B` using `sigma` and `tau`. Print this value to the console.


# Calculate the expected value of the posterior distribution

```

`@solution`
```{r}
# The results` object has already been loaded. Examine the values stored: `avg` and `se` of the spread
results

# Define `mu` and `tau`
mu <- 0
tau <- 0.01

# Define a variable called `sigma` that contains the standard error in the object `results`
sigma <- results$se

# Define a variable called `Y` that contains the average in the object `results`
Y <- results$avg

# Define a variable `B` using `sigma` and `tau`. Print this value to the console.
B <- sigma^2 / (sigma^2 + tau^2)
B

# Calculate the expected value of the posterior distribution
B*mu + (1-B)*Y
```

`@sct`
```{r}
test_error()
test_object("B", eq_condition = "equivalent", 
            undefined_msg = "Define a variable `B` using `sigma` and `tau` and print it to the console.",
            incorrect_msg = "You are not providing a calculation that gives the correct value for `B`. Make sure you are using the correct formula for `B`. Also check that your `sigma` object is only a number, not a named vector - the grader will not work correctly if `sigma` has a column name. Take the hint for a reminder on how to calculate `B`.")
test_output_contains("0.002731286", incorrect_msg = "You are not providing a calculation that gives the correct estimate of the posterior distribution. Make sure you are using the correct formula. Take the hint for a reminder.")
success_msg("Great work! Let's keep going.")
```

---

## Exercise 9 - Standard Error of the Posterior Distribution

```yaml
type: NormalExercise
key: 519aac5492
lang: r
xp: 100
skills:
  - 1
```

Compute the standard error of the posterior distribution.

`@instructions`
- Using the variables we have defined so far, calculate the standard error of the posterior distribution.
- Print this value to the console.

`@hint`
- The standard error is calculated as:
$$ \mbox{SE}(p\mid y)^2 = \frac{1}{1/\sigma^2+1/\tau^2}$$

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data(polls_us_election_2016)
polls <- polls_us_election_2016 %>% 
  filter(state == "Florida" & enddate >= "2016-11-04" ) %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
results <- polls %>% summarize(avg = mean(spread),  se = sd(spread)/sqrt(n()))
```

`@sample_code`
```{r}
# Here are the variables we have defined
mu <- 0
tau <- 0.01
sigma <- results$se
Y <- results$avg
B <- sigma^2 / (sigma^2 + tau^2)

# Compute the standard error of the posterior distribution. Print this value to the console.
```

`@solution`
```{r}
# Here are the variables we have defined
mu <- 0
tau <- 0.01
sigma <- results$se
Y <- results$avg
B <- sigma^2 / (sigma^2 + tau^2)

# Compute the standard error of the posterior distribution. Print this value to the console.
sqrt( 1/ (1/sigma^2 + 1/tau^2))
```

`@sct`
```{r}
test_error()
test_function("sqrt", not_called_msg = "Use the `sqrt` function to calculate the standard error")
test_output_contains("0.005853024", incorrect_msg = "You are not providing a calculation that gives the correct standard error. Make sure you are using the correct formula that uses sigma and tau. Take the hint for a reminder.")
success_msg("Great work! Let's use this standard error to create a credible interval.")
```

---

## Exercise 10- Constructing a Credible Interval

```yaml
type: NormalExercise
key: 9285949d79
lang: r
xp: 100
skills:
  - 1
```

Using the fact that the posterior distribution is normal, create an interval that has a 95% of occurring centered at the posterior expected value. Note that we call these credible intervals.

`@instructions`
- Calculate the 95% credible intervals using the `qnorm` function.
- Save the lower and upper confidence intervals as an object called `ci`. Save the lower confidence interval first.

`@hint`
- The center of the 95% credible interval is the expected value of the posterior distribution that we calculated previously:
$$ \begin{aligned} \mbox{E}(p \mid y) &= B \mu + (1-B) Y\ \end{aligned} $$
- Add and subtract from this estimate to construct the credible interval. Use the standard error and the `qnorm` function.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data(polls_us_election_2016)
polls <- polls_us_election_2016 %>% 
  filter(state == "Florida" & enddate >= "2016-11-04" ) %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
results <- polls %>% summarize(avg = mean(spread),  se = sd(spread)/sqrt(n()))
```

`@sample_code`
```{r}
# Here are the variables we have defined in previous exercises
mu <- 0
tau <- 0.01
sigma <- results$se
Y <- results$avg
B <- sigma^2 / (sigma^2 + tau^2)
se <- sqrt( 1/ (1/sigma^2 + 1/tau^2))

# Construct the 95% credible interval. Save the lower and then the upper confidence interval to a variable called `ci`.

```

`@solution`
```{r}
# Here are the variables we have defined in previous exercises
mu <- 0
tau <- 0.01
sigma <- results$se
Y <- results$avg
B <- sigma^2 / (sigma^2 + tau^2)
se <- sqrt( 1/ (1/sigma^2 + 1/tau^2))

# Construct the 95% credible interval. Save the lower and then the upper confidence interval to a variable called `ci`.
ci <- B*mu + (1-B)*Y + c(-1,1)*qnorm(0.975)*sqrt( 1/ (1/sigma^2 + 1/tau^2))

```

`@sct`
```{r}
test_error()

test_function("qnorm", not_called_msg = "Make sure you are using the `qnorm` function. Use a value slightly less than 1 to calculate the 95% credible interval.")

test_object("ci",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Have you made an object called 'ci'?",
            incorrect_msg = "The values contained in the object 'ci' are not correct. Are you using the correct formula to calculate the confidence intervals? Make sure to save the lower confidence interval first.")
            
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 11 - Odds of Winning Florida

```yaml
type: NormalExercise
key: ea31e7e5ad
lang: r
xp: 100
skills:
  - 1
```

According to this analysis, what was the probability that Trump wins Florida?

`@instructions`
- Using the `pnorm` function, calculate the probability that the spread in Florida was less than 0.

`@hint`
- Use the `pnorm` function by supplying the quantile you are interested in (0), the expected value, and the standard error.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data(polls_us_election_2016)
polls <- polls_us_election_2016 %>% 
  filter(state == "Florida" & enddate >= "2016-11-04" ) %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
results <- polls %>% summarize(avg = mean(spread),  se = sd(spread)/sqrt(n()))
mu <- 0
tau <- 0.01
sigma <- results$se
Y <- results$avg
B <- sigma^2 / (sigma^2 + tau^2)
```

`@sample_code`
```{r}
# Assign the expected value of the posterior distribution to the variable `exp_value`
exp_value <- B*mu + (1-B)*Y 

# Assign the standard error of the posterior distribution to the variable `se`
se <- sqrt( 1/ (1/sigma^2 + 1/tau^2))

# Using the `pnorm` function, calculate the probability that the actual spread was less than 0 (in Trump's favor). Print this value to the console.
```

`@solution`
```{r}
# Assign the expected value of the posterior distribution to the variable `exp_value`
exp_value <- B*mu + (1-B)*Y 

# Assign the standard error of the posterior distribution to the variable `se`
se <- sqrt( 1/ (1/sigma^2 + 1/tau^2))

# Using the `pnorm` function, calculate the probability that the actual spread was less than 0 (in Trump's favor). Print this value to the console.
pnorm(0, exp_value, se)
```

`@sct`
```{r}
test_error()
test_function("pnorm", args=c("q","mean","sd"),
              eq_condition = "equivalent",
              not_called_msg = "Use the `pnorm` function to calculate the probability.",
              args_not_specified = "Make sure to provide the value of the spread you are interested in, the expected value, and the standard error to the `pnorm` function.",
              incorrect_msg = "You should supply the quantile (0), the expected value (exp_value), and the standard error (se) to the `pnorm` function.")
test_output_contains("0.3203769", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are using the `pnorm` function. Don't delete any lines of code that have been provided.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 12 - Change the Priors

```yaml
type: NormalExercise
key: 3a2525e0a1
lang: r
xp: 100
skills:
  - 1
```

We had set the prior variance $\tau$ to 0.01, reflecting that these races are often close. 

Change the prior variance to include values ranging from 0.005 to 0.05 and observe how the probability of Trump winning Florida changes by making a plot.

`@instructions`
- Create a vector of values of `taus` by executing the sample code.
- Create a function using `function(){}` called `p_calc` that takes the value `tau` as the only argument,  then calculates `B` from  `tau` and `sigma`, and then calculates the probability of Trump winning, as we did in the previous exercise.
- Apply your `p_calc` function across all the new values of `taus`.
- Use the `plot` function to plot $\tau$ on the x-axis and the new probabilities on the y-axis.

`@hint`
- Create a function by defining the arguments of the function in parentheses and writing the code to run in brackets, with line breaks separating different functions. 
```{r}
my_function <- function(my_argument){
  my_first_statement
  my_second_statement
}
```
- In your function, the first statement should calculate `B` as we have done previously. 
- The second statement should calculate the probability of Trump winning. 
`pnorm(0, B*mu + (1-B)*Y, sqrt( 1/ (1/sigma^2 + 1/tau^2)))`

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data(polls_us_election_2016)
polls <- polls_us_election_2016 %>% 
  filter(state == "Florida" & enddate >= "2016-11-04" ) %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
results <- polls %>% summarize(avg = mean(spread),  se = sd(spread)/sqrt(n()))
```

`@sample_code`
```{r}
# Define the variables from previous exercises
mu <- 0
sigma <- results$se
Y <- results$avg

# Define a variable `taus` as different values of tau
taus <- seq(0.005, 0.05, len = 100)

# Create a function called `p_calc` that generates `B` and calculates the probability of the spread being less than 0





# Create a vector called `ps` by applying the function `p_calc` across values in `taus`


# Plot `taus` on the x-axis and `ps` on the y-axis
```

`@solution`
```{r}
# Define the variables from previous exercises
mu <- 0
sigma <- results$se
Y <- results$avg

# Define a variable `taus` as different values of tau
taus <- seq(0.005, 0.05, len = 100)

# Create a function called `p_calc` that generates `B` and calculates the probability of the spread being less than 0
p_calc <- function(tau){
  B <- sigma^2 / (sigma^2 + tau^2)
  pnorm(0, B*mu + (1-B)*Y, sqrt( 1/ (1/sigma^2 + 1/tau^2)))
}

# Create a vector called `ps` by applying the function `p_calc` across values in `taus`
ps <- p_calc(taus)

# Plot `taus` on the x-axis and `ps` on the y-axis
plot(taus, ps)

```

`@sct`
```{r}
test_error()

test_function_definition("p_calc",
                          function_test = {
                            test_expression_result("p_calc(taus)", 
                            incorrect_msg = "Your `p_calc` function does not generate the correct probabilities when supplied the vector 'taus'. First, estimate 'B' using 'sigma' and 'tau'. Then use the `pnorm` function to estimate the probability that the spread is less than 0.")
                          })

test_function("plot", args = c("x","y"),
              not_called_msg = "Use the `plot` function to plot the values of 'tau' and the probabilities.",
              args_not_specified = "Supply the values to plot on each axis to the `plot` function.",
              incorrect_msg = "You should be plotting `taus` on the x-axis and `ps` on the y-axis.")

success_msg("Great work! Let's work on a similar problem.")

```

---

## End of Assessment

```yaml
type: PureMultipleChoiceExercise
key: e3d83204c6
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
