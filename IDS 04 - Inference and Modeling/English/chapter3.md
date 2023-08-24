---
title: Confidence Intervals and p-Values
title_meta: Chapter 3
description: >-
  In this chapter, you will learn about confidence intervals and p-values using
  actual polls from the 2016 US Presidential election.
---

## Exercise 1. Confidence interval for p

```yaml
type: NormalExercise
key: c945ad6aed
lang: r
xp: 100
skills:
  - 1
```

For the following exercises, we will use actual poll data from the 2016 election. The exercises will contain pre-loaded data from the `dslabs` package.

```{r}
library(dslabs)
data("polls_us_election_2016")
```

We will use all the national polls that ended within a few weeks before the election.

Assume there are only two candidates and construct a 95% confidence interval for the election night proportion $p$.

`@instructions`
- Use `filter` to subset the data set for the poll data you want. Include polls that ended on or after October 31, 2016 (`enddate`). Only include polls that took place in the United States. Call this filtered object `polls`.
- Use `nrow` to make sure you created a filtered object `polls` that contains the correct number of rows.
- Extract the sample size `N` from the first poll in your subset object `polls`.
- Convert the percentage of Clinton voters (`rawpoll_clinton`) from the first poll in `polls` to a proportion, `X_hat`. Print this value to the console.
- Find the standard error of `X_hat` given `N`. Print this result to the console.
- Calculate the 95% confidence interval of this estimate using the `qnorm` function.
- Save the lower and upper confidence intervals as an object called `ci`. Save the lower confidence interval first.

`@hint`
- Indicate which object you want to filter by using the object name followed by "%>%" then the function you want to perform. For example
```{r}
new_object <- old_object %in% filter(first_filter_logic & second_filter_logic)
```
- Remember the formula for standard error:
$$SE(\bar{X})=\sqrt{\bar{X}(1-\bar{X})/N}$$
- The lower bound of the 95% confidence interval is equal to $\bar{X} - qnorm(0.975)*SE(\bar{X})$.
- The upper bound of the 95% confidence interval is equal to $\bar{X} + qnorm(0.975)*SE(\bar{X})$.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
```

`@sample_code`
```{r}
# Load the data
data(polls_us_election_2016)

# Generate an object `polls` that contains data filtered for polls that ended on or after October 31, 2016 in the United States


# How many rows does `polls` contain? Print this value to the console.


# Assign the sample size of the first poll in `polls` to a variable called `N`. Print this value to the console.



# For the first poll in `polls`, assign the estimated percentage of Clinton voters to a variable called `X_hat`. Print this value to the console.


# Calculate the standard error of `X_hat` and save it to a variable called `se_hat`. Print this value to the console.


# Use `qnorm` to calculate the 95% confidence interval for the proportion of Clinton voters. Save the lower and then the upper confidence interval to a variable called `ci`.


```

`@solution`
```{r}
# Load the data
data("polls_us_election_2016")

# Generate an object `polls` that contains data filtered for polls that ended on or after October 31, 2016 in the United States
polls <- polls_us_election_2016 %>% filter(enddate >= "2016-10-31" & state == "U.S.") 

# How many rows does `polls` contain? Print this value to the console.
nrow(polls)

# Assign the sample size of the first poll in `polls` to a variable called `N`. Print this value to the console.
N <- polls$samplesize[1]
N

# For the first poll in `polls`, convert the percentage to a proportion of Clinton voters and assign it to a variable called `X_hat`. Print this value to the console.
X_hat <- polls$rawpoll_clinton[1]/100
X_hat

# Calculate the standard error of `X_hat` and save it to a variable called `se_hat`. Print this value to the console.
se_hat <- sqrt(X_hat*(1-X_hat)/N)
se_hat

# Use `qnorm` to calculate the 95% confidence interval for the proportion of Clinton voters. Save the lower and then the upper confidence interval to a variable called `ci`.
ci<- c(X_hat - qnorm(0.975)*se_hat, X_hat + qnorm(0.975)*se_hat)
```

`@sct`
```{r}
test_error()

test_output_contains("70", incorrect_msg = "Your `polls` object does not have the correct number of rows. Be sure to `filter` for 'enddate' greater than or equal to '2016-10-31' and 'state=='U.S.'.")

test_output_contains("2220", incorrect_msg = "Your `N` variable does not contain the correct value or has not been printed. Be sure to subset for only the first poll in `polls`.")

test_output_contains("0.47", incorrect_msg = "Your `X_hat` is not correct or has not been printed. Remember to divide the percentage by 100 to convert to a proportion. Do this only for the first poll in `polls`.")

test_output_contains("0.01059279", incorrect_msg = "Your `se_hat` is not correct or has not been printed. Remember that the formula for standard error equals the square root of the variance divided by the sample size.")

test_object("ci",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Have you made an object called 'ci'?",
            incorrect_msg = "The values contained in the object 'ci' are not correct. Are you using the correct formula to calculate the confidence intervals? Make sure to save the lower confidence interval first.")
            
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 2. Pollster results for p

```yaml
type: NormalExercise
key: 5db70d1fb9
lang: r
xp: 100
skills:
  - 1
```

Create a new object called `pollster_results` that contains the pollster's name, the end date of the poll, the proportion of voters who declared a vote for Clinton, the standard error of this estimate, and the lower and upper bounds of the confidence interval for the estimate.

`@instructions`
- Use the `mutate` function to define four new columns: `X_hat`, `se_hat`, `lower`, and `upper`. Temporarily add these columns to the `polls` object that has already been loaded for you.
- In the `X_hat` column, convert the raw poll results for Clinton to a proportion.
- In the `se_hat` column, calculate the standard error of `X_hat` for each poll using the `sqrt` function.
- In the `lower` column, calculate the lower bound of the 95% confidence interval using the `qnorm` function.
- In the `upper` column, calculate the upper bound of the 95% confidence interval using the `qnorm` function.
- Use the `select` function to select the columns from `polls` to save to the new object `pollster_results`.

`@hint`
- Indicate which object you want to mutate by using the object name followed by "%>%" then the function you want to perform.
- When using the `mutate` function, supply the name of the variable you wish to create and the function to perform. For example:
```{r}
data %>% mutate(double = existing_variable*2, triple = existing_variable*3)
```
- Remember the formula for standard error:
$$SE(\bar{X})=\sqrt{\bar{X}(1-\bar{X})/N}$$
- The lower bound of the 95% confidence interval is equal to $\bar{X} - qnorm(0.975)*SE(\bar{X})$.
- The upper bound of the 95% confidence interval is equal to $\bar{X} + qnorm(0.975)*SE(\bar{X})$.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% filter(enddate >= "2016-10-31" & state == "U.S.")
```

`@sample_code`
```{r}
# The `polls` object that filtered all the data by date and nation has already been loaded. Examine it using the `head` function.
head(polls)

# Create a new object called `pollster_results` that contains columns for pollster name, end date, X_hat, se_hat, lower confidence interval, and upper confidence interval for each poll.
```

`@solution`
```{r}
# The `polls` object that filtered all the data by date and nation has already been loaded. Examine it using the `head` function.
head(polls)

# Create a new object called `pollster_results` that contains columns for pollster name, end date, X_hat, se_hat, lower confidence interval, and upper confidence interval for each poll.

pollster_results <- polls %>% 
                    mutate(X_hat = polls$rawpoll_clinton/100, se_hat = sqrt(X_hat*(1-X_hat)/samplesize), lower = X_hat - qnorm(0.975)*se_hat, upper = X_hat + qnorm(0.975)*se_hat) %>% 
                    select(pollster, enddate, X_hat, se_hat, lower, upper)
```

`@sct`
```{r}
test_error()
test_function("mutate", not_called_msg = "Use the `mutate` function to create new variables: 'X_hat', 'se_hat', 'upper', and 'lower'.")
test_function("select", not_called_msg = "Use the `select` function to specify which columns to save to `pollster_results`: 'pollster', 'enddate', 'X_hat', 'se_hat', 'upper', and 'lower'.")
test_object("pollster_results",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = NULL,
            incorrect_msg = "The contents of 'pollster_results' are not correct. Make sure you are selecting the correct columns and calculating the confidence intervals correctly.")
success_msg("Great work! Let's move along.")
```

---

## Exercise 3. Comparing to actual results - p

```yaml
type: NormalExercise
key: e1864899e4
lang: r
xp: 100
skills:
  - 1
```

The final tally for the popular vote was Clinton 48.2% and Trump 46.1%. Add a column called `hit` to `pollster_results` that states if the confidence interval included the true proportion $p=0.482$ or not. What proportion of confidence intervals included $p$?

`@instructions`
- Finish the code to create a new object called `avg_hit` by following these steps.
- Use the `mutate` function to define a new variable called 'hit'.
- Use logical expressions to determine if each values in `lower` and `upper` span the actual proportion. 
- Use the `mean` function to determine the average value in `hit` and summarize the results using `summarize`.

`@hint`
- Define a 'hit' as a poll where the lower bound was less than or equal to the actual value and the upper bound was greater than or equal to the actual value.
- Use the `mean` function nested within the `summarize` to find the proportion of good hits.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% filter(enddate >= "2016-10-31" & state == "U.S.") 
pollster_results <- polls %>% 
                    mutate(X_hat = polls$rawpoll_clinton/100, se_hat = sqrt(X_hat*(1-X_hat)/samplesize), lower = X_hat - qnorm(0.975)*se_hat, upper = X_hat + qnorm(0.975)*se_hat) %>% 
                    select(pollster, enddate, X_hat, lower, upper)
```

`@sample_code`
```{r}
# The `pollster_results` object has already been loaded. Examine it using the `head` function.
head(pollster_results)

# Add a logical variable called `hit` that indicates whether the actual value exists within the confidence interval of each poll. Summarize the average `hit` result to determine the proportion of polls with confidence intervals include the actual value. Save the result as an object called `avg_hit`.
avg_hit <- 
```

`@solution`
```{r}
# The `pollster_results` object has already been loaded. Examine it using the `head` function.
head(pollster_results)

# Add a logical variable called `hit` that indicates whether the actual value exists within the confidence interval of each poll. Summarize the average `hit` result to determine the proportion of polls with confidence intervals include the actual value. Save the result as an object called `avg_hit`.
avg_hit <- pollster_results %>% mutate(hit = lower<=0.482 & upper>=0.482) %>% summarize(mean(hit))
```

`@sct`
```{r}
test_error()
test_function("mutate", not_called_msg = "Use the `mutate` function to create a new variable called 'hit'.")
test_function("mean", not_called_msg = "Use the `mean` function to find the proportion of polls where 'hit' is true.")

test_object("avg_hit",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = NULL,
            incorrect_msg = "Your object called 'avg_hit' does not contain the correct values. Make sure you are summarizing the results of the `hit` variable using the `mean` and `summarize` functions. You want to find hits where the lower bound is less than or equal to 0.482 and the upper bound is greater than or equal to 0.482.")
            
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 4. Theory of confidence intervals

```yaml
type: MultipleChoiceExercise
key: 0942faa253
lang: r
xp: 50
skills:
  - 1
```

If these confidence intervals are constructed correctly, and the theory holds up, what proportion of confidence intervals should include $p$?

`@possible_answers`
- 0.05
- 0.31
- 0.50
- 0.95

`@hint`
- We calculated 95% confidence intervals for each of the polls.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. We calculated 95% confidence intervals for these values."
msg2 = "Try again. The proportion of intervals that included the actual value was lower than expected."
msg3 = "Try again. We constructed 95% confidence intervals."
msg4 = "Correct!"
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 5. Confidence interval for d

```yaml
type: NormalExercise
key: c987f6ea38
lang: r
xp: 100
skills:
  - 1
```

A much smaller proportion of the polls than expected produce confidence intervals containing $p$. Notice that most polls that fail to include $p$ are underestimating. The rationale for this is that undecided voters historically divide evenly between the two main candidates on election day.

In this case, it is more informative to estimate the spread or the difference between the proportion of two candidates $d$, or $0.482 - 0.461 = 0.021$ for this election.

Assume that there are only two parties and that $d = 2p - 1$. Construct a 95% confidence interval for difference in proportions on election night.

`@instructions`
- Use the `mutate` function to define a new variable called 'd_hat' in `polls` as the proportion of Clinton voters minus the proportion of Trump voters. 
- Extract the sample size `N` from the first poll in your subset object `polls`.
- Extract the difference in proportions of voters `d_hat` from the first poll in your subset object `polls`.
- Use the formula above to calculate $p$ from `d_hat`. Assign $p$ to the variable `X_hat`.
- Find the standard error of the spread given `N`. Save this as `se_hat`.
- Calculate the 95% confidence interval of this estimate of the difference in proportions, `d_hat`, using the `qnorm` function.
- Save the lower and upper confidence intervals as an object called `ci`. Save the lower confidence interval first.

`@hint`
- Remember the formula for standard error of `x_hat`:
$$SE(\bar{X})=\sqrt{\bar{X}(1-\bar{X})/N}$$
- Remember that the standard error of the spread `d_hat` will be two times the standard error of `X_hat`.
- The lower bound of the 95% confidence interval is equal to $\bar{d} - qnorm(0.975)*SE(\bar{X})$, where $\bar{d}$ is the difference.
- The upper bound of the 95% confidence interval is equal to $\bar{d} + qnorm(0.975)*SE(\bar{X})$, where $\bar{d}$ is the difference.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data("polls_us_election_2016")
```

`@sample_code`
```{r}
# Add a statement to this line of code that will add a new column named `d_hat` to `polls`. The new column should contain the difference in the proportion of voters.
polls <- polls_us_election_2016 %>% filter(enddate >= "2016-10-31" & state == "U.S.") 


# Assign the sample size of the first poll in `polls` to a variable called `N`. Print this value to the console.


# Assign the difference `d_hat` of the first poll in `polls` to a variable called `d_hat`. Print this value to the console.


# Assign proportion of votes for Clinton to the variable `X_hat`.


# Calculate the standard error of the spread and save it to a variable called `se_hat`. Print this value to the console.



# Use `qnorm` to calculate the 95% confidence interval for the difference in the proportions of voters. Save the lower and then the upper confidence interval to a variable called `ci`.
```

`@solution`
```{r}
# Add a statement to this line of code that will add a new column named `d_hat` to `polls`. The new column should contain the difference in the proportion of voters.
polls <- polls_us_election_2016 %>% filter(enddate >= "2016-10-31" & state == "U.S.")  %>%
  mutate(d_hat = rawpoll_clinton/100 - rawpoll_trump/100)

# Assign the sample size of the first poll in `polls` to a variable called `N`. Print this value to the console.
N <- polls$samplesize[1]

# Assign the difference `d_hat` of the first poll in `polls` to a variable called `d_hat`. Print this value to the console.
d_hat <- polls$d_hat[1]
d_hat

# Assign proportion of votes for Clinton to the variable `X_hat`.
X_hat <- (d_hat+1)/2

# Calculate the standard error of the spread and save it to a variable called `se_hat`. Print this value to the console.
se_hat <- 2*sqrt(X_hat*(1-X_hat)/N)
se_hat

# Use `qnorm` to calculate the 95% confidence interval for the difference in the proportions of voters. Save the lower and then the upper confidence interval to a variable called `ci`.
ci <- c(d_hat - qnorm(0.975)*se_hat, d_hat + qnorm(0.975)*se_hat)
```

`@sct`
```{r}
test_error()
test_function("mutate", not_called_msg = "Use the `mutate` function to create a new variable called 'd_hat'.")

test_object("d_hat",
            eq_condition = "equal",
            eval = TRUE,
            undefined_msg = "Have you made an object called `d_hat`?",
            incorrect_msg = "The values contained in the object `d_hat` are not correct. Make sure you are calculating the proportion of Clinton voters minus the proportion of Trump voters. You must divide the raw poll results by 100 to obtain the proportions.")

test_object("X_hat",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Have you made an object called `X_hat`?",
            incorrect_msg = "The values contained in the object `X_hat` are not correct. Did you use the formula `X_hat <- (d_hat+1)/2`? Because we want to calculate the spread assuming there are only 2 candidates, we can't use the raw poll values and must calculate them from `d_hat`.")

test_object("se_hat",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Have you made an object called `se_hat`?",
            incorrect_msg = "The values contained in the object `se_hat` are not correct. The standard error of the spread `d_hat` is 2 times the standard error of `X_hat`. Remember that the formula for standard error equals the square root of the variance divided by the sample size.")

test_object("ci",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Have you made an object called 'ci'?",
            incorrect_msg = "The values contained in the object 'ci' are not correct. Are you using the correct formula to calculate the confidence intervals? Make sure to save the lower confidence interval first.")
            
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 6. Pollster results for d

```yaml
type: NormalExercise
key: 7b31fe655a
lang: r
xp: 100
skills:
  - 1
```

Create a new object called `pollster_results` that contains the pollster's name, the end date of the poll, the difference in the proportion of voters who declared a vote either, and the lower and upper bounds of the confidence interval for the estimate.

`@instructions`
- Use the `mutate` function to define four new columns: 'X\_hat', 'se\_hat', 'lower', and 'upper'. Temporarily add these columns to the `polls` object that has already been loaded for you.
- In the `X_hat` column, calculate the proportion of voters for Clinton using `d_hat`.
- In the `se_hat` column, calculate the standard error of the spread for each poll using the `sqrt` function.
- In the `lower` column, calculate the lower bound of the 95% confidence interval using the `qnorm` function.
- In the `upper` column, calculate the upper bound of the 95% confidence interval using the `qnorm` function.
- Use the `select` function to select the `pollster, enddate, d_hat, lower, upper` columns from `polls` to save to the new object `pollster_results`.

`@hint`
- When using the `mutate` function, supply the name of the variable you wish to create and the function to perform. For example:
```{r}
data %>% mutate(double = existing_variable*2, triple = existing_variable*3)
```
- Remember that $d = 2p-1$, $p = \bar{X}$ and $d$ is the difference in proportions.
- Remember the formula for standard error:
$$SE(\bar{X})=\sqrt{\bar{X}(1-\bar{X})/N}$$
- The lower bound of the 95% confidence interval is equal to $\bar{d} - qnorm(0.975)*SE(\bar{X})$.
- The upper bound of the 95% confidence interval is equal to $\bar{d} + qnorm(0.975)*SE(\bar{X})$.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% filter(enddate >= "2016-10-31" & state == "U.S.")  %>%
  mutate(d_hat = rawpoll_clinton/100 - rawpoll_trump/100)
```

`@sample_code`
```{r}
# The subset `polls` data with 'd_hat' already calculated has been loaded. Examine it using the `head` function.
head(polls)

# Create a new object called `pollster_results` that contains columns for pollster name, end date, d_hat, lower confidence interval of d_hat, and upper confidence interval of d_hat for each poll.

```

`@solution`
```{r}
# The subset `polls` data with 'd_hat' already calculated has been loaded. Examine it using the `head` function.
head(polls)

# Create a new object called `pollster_results` that contains columns for pollster name, end date, d_hat, lower confidence interval of d_hat, and upper confidence interval of d_hat for each poll.
pollster_results <-  polls %>% mutate(X_hat = (d_hat+1)/2, se_hat = 2*sqrt(X_hat*(1-X_hat)/samplesize), lower = d_hat - qnorm(0.975)*se_hat, upper = d_hat + qnorm(0.975)*se_hat) %>% select(pollster, enddate, d_hat, lower, upper)
```

`@sct`
```{r}
test_error()
test_object("pollster_results", incorrect_msg = "Make sure your `se_hat` is calculated correctly as 2 times the standard error of `X_hat`, check that you calculated the confidence interval correctly, and make sure you select the five columns in the order specified.")
test_function("mutate", not_called_msg = "Use the `mutate` function to create new variables: 'X_hat', 'se_hat', 'upper', and 'lower'.")

test_function("select", not_called_msg = "Use the `select` function to specify which columns to save to `pollster_results`: 'pollster', 'enddate', 'd_hat', 'upper', and 'lower'.")
success_msg("Great work! We'll use this table in the next exercise.")
```

---

## Exercise 7. Comparing to actual results - d

```yaml
type: NormalExercise
key: d1684767a4
lang: r
xp: 100
skills:
  - 1
```

What proportion of confidence intervals for the difference between the proportion of voters included $d$, the actual difference in election day?

`@instructions`
- Use the `mutate` function to define a new variable within `pollster_results` called `hit`.
- Use logical expressions to determine if each values in `lower` and `upper` span the actual difference in proportions of voters. 
- Use the `mean` function to determine the average value in `hit` and summarize the results using `summarize`.
- Save the result of your entire line of code as an object called `avg_hit`.

`@hint`
- Define a 'hit' as a poll where the lower bound was less than or equal to the actual value and the upper bound was greater than or equal to the actual value.
- Use the `mean` function nested within the `summarize` to find the proportion of good hits.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% filter(enddate >= "2016-10-31" & state == "U.S.")  %>%
  mutate(d_hat = rawpoll_clinton/100 - rawpoll_trump/100)
pollster_results <-  polls %>% mutate(X_hat = (d_hat+1)/2, se_hat = 2*sqrt(X_hat*(1-X_hat)/samplesize), lower = d_hat - qnorm(0.975)*se_hat, upper = d_hat + qnorm(0.975)*se_hat) %>% select(pollster, enddate, d_hat, lower, upper)
```

`@sample_code`
```{r}
# The `pollster_results` object has already been loaded. Examine it using the `head` function.
head(pollster_results)

# Add a logical variable called `hit` that indicates whether the actual value (0.021) exists within the confidence interval of each poll. Summarize the average `hit` result to determine the proportion of polls with confidence intervals include the actual value. Save the result as an object called `avg_hit`.
```

`@solution`
```{r}
# The `pollster_results` object has already been loaded. Examine it using the `head` function.
head(pollster_results)

# Add a logical variable called `hit` that indicates whether the actual value exists within the confidence interval of each poll. Summarize the average `hit` result to determine the proportion of polls with confidence intervals include the actual value. Save the result as an object called `avg_hit`.
avg_hit <- pollster_results %>% mutate(hit = lower<=0.021 & upper>=0.021) %>% summarize(mean(hit))
```

`@sct`
```{r}
test_error()
test_function("mutate", not_called_msg = "Use the `mutate` function to create a new variable called 'hit'.")
test_function("mean", not_called_msg = "Use the `mean` function to find the proportion of polls where 'hit' is true.")
test_object("avg_hit",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = NULL,
            incorrect_msg = "Your object called 'avg_hit' does not contain the correct values. Make sure you are summarizing the results of the `hit` variable using the `mean` and `summarize` functions. You want to find hits where the lower bound is less than or equal to 0.021 and the upper bound is greater than or equal to 0.021.")
success_msg("Great work! Let's continue.")
```

---

## Exercise 8. Comparing to actual results by pollster

```yaml
type: NormalExercise
key: 5000d81548
lang: r
xp: 100
skills:
  - 1
```

Although the proportion of confidence intervals that include the actual difference between the proportion of voters increases substantially, it is still lower that 0.95. In the next chapter, we learn the reason for this. 

To motivate our next exercises, calculate the difference between each poll's estimate $\bar{d}$ and the actual $d=0.021$. Stratify this difference, or error, by pollster in a plot.

`@instructions`
- Define a new variable `errors` that contains the difference between the estimated difference between the proportion of voters and the actual difference on election day, 0.021.
- To create the plot of errors by pollster, add a layer with the function `geom_point`. The aesthetic mappings require a definition of the x-axis and y-axis variables. So the code looks like the example below, but you fill in the variables for x and y.
- The last line of the example code adjusts the x-axis labels so that they are easier to read.

```{r}
data %>% ggplot(aes(x = , y = )) +
  geom_point() +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))
```

`@hint`
- Use the pipe `%>%` to pass the data in `polls` to the `mutate` function that adds a column to calculate the error equal to `d_hat - 0.021`.
- Use the pipe `%>%` to pass the new data along to the function `ggplot` for plotting. Define the aesthetics according to which variable you want on the x- and y-axis.
- Use the sample code to fix your graph axis labels.

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
library(ggplot2)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% filter(enddate >= "2016-10-31" & state == "U.S.")  %>%
  mutate(d_hat = rawpoll_clinton/100 - rawpoll_trump/100)
```

`@sample_code`
```{r}
# The `polls` object has already been loaded. Examine it using the `head` function.
head(polls)

# Add variable called `error` to the object `polls` that contains the difference between d_hat and the actual difference on election day. Then make a plot of the error stratified by pollster.
```

`@solution`
```{r}
# The `polls` object has already been loaded. Examine it using the `head` function.
head(polls)

# Add variable called `error` to the object `polls` that contains the difference between d_hat and the actual difference on election day. Then make a plot of the error stratified by pollster.
polls %>% mutate(error = d_hat - 0.021) %>% 
  ggplot(aes(pollster, error)) +
  geom_point() +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))
```

`@sct`
```{r}
test_error()
test_function("mutate", not_called_msg = "Use the `mutate` function to create a new variable called 'error'.")
test_function("ggplot", not_called_msg = "Make sure to call `ggplot` to make your plot.")
test_function("geom_point", not_called_msg = "Make sure to layer `geom_point` on your ggplot to add data points.")
success_msg("Great work! Let's wrap it up.")
```

---

## Exercise 9. Comparing to actual results by pollster - multiple polls

```yaml
type: NormalExercise
key: 99493aa99e
lang: r
xp: 100
skills:
  - 1
```

Remake the plot you made for the previous exercise, but only for pollsters that took five or more polls. 

You can use dplyr tools `group_by` and `n` to group data by a variable of interest and then count the number of observations in the groups. The function `filter` filters data piped into it by your specified condition.

For example:
```{r}
data %>% group_by(variable_for_grouping) 
    %>% filter(n() >= 5)
```

`@instructions`
- Define a new variable `errors` that contains the difference between the estimated difference between the proportion of voters and the actual difference on election day, 0.021.
- Group the data by pollster using the `group_by` function.
- Filter the data by pollsters with 5 or more polls. 
- Use `ggplot` to create the plot of errors by pollster. 
- Add a layer with the function `geom_point`.

`@hint`
- Use the pipe `%>%` to pass the data in `polls` to the `mutate` function that adds a column to calculate the error equal to `d_hat - 0.021`.
- Use the `group_by` function to group the data by a variable of interest, like 'group_by(pollster)'.
- Use the `filter` function to filter the data by a variable of interest.
- Nest the dplyr function `n` to count the number of observations within the current group within `filter`, as in the example code.
- Use the function `ggplot` for plotting. Define the aesthetics according to which variable you want on the x- and y-axis.
- Use the sample code to fix your graph axis labels.

```{r}
data %>% ggplot(aes(x = , y = )) +
  geom_point() +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))
```

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
library(ggplot2)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% filter(enddate >= "2016-10-31" & state == "U.S.")  %>%
  mutate(d_hat = rawpoll_clinton/100 - rawpoll_trump/100)
pollster_results <-  polls %>% mutate(X_hat = (d_hat+1)/2, se_hat = 2*sqrt(X_hat*(1-X_hat)/samplesize), lower = d_hat - qnorm(0.975)*se_hat, upper = d_hat + qnorm(0.975)*se_hat) %>% select(pollster, enddate, d_hat, lower, upper)
```

`@sample_code`
```{r}
# The `polls` object has already been loaded. Examine it using the `head` function.
head(polls)

# Add variable called `error` to the object `polls` that contains the difference between d_hat and the actual difference on election day. Then make a plot of the error stratified by pollster, but only for pollsters who took 5 or more polls.
```

`@solution`
```{r}
# The `polls` object has already been loaded. Examine it using the `head` function.
head(polls)

# Add variable called `error` to the object `polls` that contains the difference between d_hat and the actual difference on election day. Then make a plot of the error stratified by pollster, but only for pollsters who took 5 or more polls.

polls %>% mutate(error = d_hat - 0.021) %>%
  group_by(pollster) %>%
  filter(n() >= 5) %>%
  ggplot(aes(pollster, error)) +
  geom_point() +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))
```

`@sct`
```{r}
test_error()
test_function("mutate", not_called_msg = "Use the `mutate` function to create a new variable called 'error'.")
test_function("group_by", not_called_msg = "Use the `group_by` function to group the data by pollster.")
test_function("filter", not_called_msg = "Use the `filter` function to filter the data to pollsters with 5 or more polls.")
test_function("ggplot", not_called_msg = "Make sure to call `ggplot` to make your plot.")
test_function("geom_point", not_called_msg = "Make sure to layer `geom_point` on your ggplot to add data points.")
success_msg("Great work!")
```

---

## End of Assessment

```yaml
type: PureMultipleChoiceExercise
key: dcf729c536
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
