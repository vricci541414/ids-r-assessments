---
title: Election Forecasting
description: >-
  In this chapter, you will learn about election forecasting by exploring data
  from the 2016 US Presidential Election.
---

## Exercise 1 - Confidence Intervals of Polling Data

```yaml
type: NormalExercise
key: 96633447a5
lang: r
xp: 100
skills:
  - 1
```

For each poll in the polling data set, use the CLT to create a 95% confidence interval for the spread. Create a new table called `cis` that contains columns for the lower and upper limits of the confidence intervals.

`@instructions`
- Use pipes `%>%` to pass the `poll` object on to the `mutate` function, which creates new variables. 
- Create a variable called `X_hat` that contains the estimate of the proportion of Clinton voters for each poll.
- Create a variable called `se` that contains the standard error of the spread.
- Calculate the confidence intervals using the `qnorm` function and your calculated `se`.
- Use the `select` function to keep the following columns: `state`, `startdate`, `enddate`, `pollster`, `grade`, `spread`, `lower`, `upper`.

`@hint`
- Estimate `X_hat` as $E(\bar{X})=(d+1)/2$, where $d$ is the spread.
- Remember the formula for standard error of the spread:
$$SE(\bar{X})=2\sqrt{\bar{X}(1-\bar{X})/N}$$
- The lower bound of the 95% confidence interval is equal to $\bar{X} - qnorm(0.975)*SE(\bar{X})$.
- The upper bound of the 95% confidence interval is equal to $\bar{X} + qnorm(0.975)*SE(\bar{X})$.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data("polls_us_election_2016")
```

`@sample_code`
```{r}
# Load the libraries and data
library(dplyr)
library(dslabs)
data("polls_us_election_2016")

# Create a table called `polls` that filters by  state, date, and reports the spread
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)

# Create an object called `cis` that has the columns indicated in the instructions
```

`@solution`
```{r}
# Load the libraries and data
library(dplyr)
library(dslabs)
data("polls_us_election_2016")

# Create a table called `polls` that filters by  state, date, and reports the spread
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)

# Create an object called `cis` that columns for the lower and upper confidence intervals. Select the columns indicated in the instructions.
cis <- polls %>% mutate(X_hat = (spread+1)/2, se = 2*sqrt(X_hat*(1-X_hat)/samplesize), 
                 lower = spread - qnorm(0.975)*se, upper = spread + qnorm(0.975)*se) %>%
  select(state, startdate, enddate, pollster, grade, spread, lower, upper)
```

`@sct`
```{r}
test_error()
test_function("qnorm", not_called_msg = "Use the `qnorm` function to calculate the confidence intervals. Use a value slightly less than 1.")
test_function("mutate", not_called_msg = "Use the `mutate` function to create new variables: 'X_hat', 'se_hat', 'upper', and 'lower'.")
test_function("select", not_called_msg = "Use the `select` function to specify which columns to save to `cis`.")
test_object("cis",
            eq_condition = "equivalent",
            undefined_msg = "Remember to create an object called `cis`.",
            incorrect_msg = "The object `cis` should contain columns for the 'state', 'startdate', 'enddate', 'pollster', 'grade', 'spread', 'lower', and 'upper'. If your column names are correct, check that you've properly calculated the standard error of the spread as two times the standard error of `x_hat` when calculating confidence intervals.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 2 - Compare to Actual Results

```yaml
type: NormalExercise
key: 7dd2b8b1b1
lang: r
xp: 100
skills:
  - 1
```

You can add the final result to the `cis` table you just created using the `left_join` function as shown in the sample code.

Now determine how often the 95% confidence interval includes the actual result.

`@instructions`
- Create an object called `p_hits` that contains the proportion of intervals that contain the actual spread using the following two steps.
- Use the `mutate` function to create a new variable called `hit` that contains a logical vector for whether the `actual_spread` falls between the `lower` and `upper` confidence intervals.
- Summarize the proportion of values in `hit` that are true using the `mean` function inside of `summarize`.

`@hint`
- Use pipes `%>%` to pass the `poll` data on to the mutate function to create a new variable. Use logical operators to determine whether the `actual_spread` is between the lower and upper confidence intervals.
- Use `mean` nested within the `summarize` function to determine the proportion of `hits` that are true.
- Make sure your final `p_hits` table has one observation of one variable: the proportion of hits.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
cis <- polls %>% mutate(X_hat = (spread+1)/2, se = 2*sqrt(X_hat*(1-X_hat)/samplesize), 
                 lower = spread - qnorm(0.975)*se, upper = spread + qnorm(0.975)*se) %>%
  select(state, startdate, enddate, pollster, grade, spread, lower, upper)
```

`@sample_code`
```{r}
# Add the actual results to the `cis` data set
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
ci_data <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")

# Create an object called `p_hits` that summarizes the proportion of confidence intervals that contain the actual value. Print this object to the console.
```

`@solution`
```{r}
# Add the actual results to the `cis` data set
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
ci_data <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")

# Create an object called `p_hits` that summarizes the proportion of confidence intervals that contain the actual value. Print this object to the console.
p_hits <- ci_data %>% mutate(hit = lower <= actual_spread & upper >= actual_spread) %>% summarize(proportion_hits = mean(hit))
p_hits
```

`@sct`
```{r}
test_error()
test_object("p_hits",
            eq_condition = "equivalent",
            undefined_msg = "Remember to create an object called `p_hits`.",
            incorrect_msg = "The object `p_hits` should be a data frame containing the proportion of hits.")
success_msg("Great work! Let's continue.")
```

---

## Exercise 3 - Stratify by Pollster and Grade

```yaml
type: NormalExercise
key: 205d3feb3b
lang: r
xp: 100
skills:
  - 1
```

Now find the proportion of hits for each pollster. Show only pollsters with at least 5 polls and order them from best to worst. Show the number of polls conducted by each pollster and the FiveThirtyEight grade of each pollster.

`@instructions`
- Create an object called `p_hits` that contains the proportion of intervals that contain the actual spread using the following steps.
- Use the `mutate` function to create a new variable called `hit` that contains a logical vector for whether the `actual_spread` falls between the `lower` and `upper` confidence intervals.
- Use the `group_by` function to group the data by pollster.
- Use the `filter` function to filter for pollsters that have at least 5 polls.
- Summarize the proportion of values in `hit` that are true as a variable called `proportion_hits`. Also create new variables for the number of polls by each pollster (`n`) using the `n()` function and the grade of each poll (`grade`) by taking the first row of the grade column.
- Use the `arrange` function to arrange the `proportion_hits` in descending order.

`@hint`
- Use `n=n(), grade = grade[1]` in the `summarize` function to include the number of polls and grade.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
cis <- polls %>% mutate(X_hat = (spread+1)/2, se = 2*sqrt(X_hat*(1-X_hat)/samplesize), 
                 lower = spread - qnorm(0.975)*se, upper = spread + qnorm(0.975)*se) %>%
  select(state, startdate, enddate, pollster, grade, spread, lower, upper)
```

`@sample_code`
```{r}
# The `cis` data have already been loaded for you
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
ci_data <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")

# Create an object called `p_hits` that summarizes the proportion of hits for each pollster that has at least 5 polls.
```

`@solution`
```{r}
# The `cis` data have already been loaded for you
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
ci_data <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")

# Create an object called `p_hits` that summarizes the proportion of hits for each pollster that has at least 5 polls. 
p_hits <- ci_data %>% mutate(hit = lower <= actual_spread & upper >= actual_spread) %>% 
  group_by(pollster) %>%
  filter(n() >=  5) %>%
  summarize(proportion_hits = mean(hit), n = n(), grade = grade[1]) %>%
  arrange(desc(proportion_hits))
p_hits
```

`@sct`
```{r}
test_error()
test_object("p_hits",
            eq_condition = "equivalent",
            undefined_msg = "Remember to create an object called `p_hits`.",
            incorrect_msg = "The object `p_hits` should contain columns for the pollster, proportion of hits, number of polls, and grade for 13 polls.")
success_msg("Great work! Let's examine these data further.")
```

---

## Exercise 4 - Stratify by State

```yaml
type: NormalExercise
key: 533cc4578c
lang: r
xp: 100
skills:
  - 1
```

Repeat the previous exercise, but instead of pollster, stratify by state. Here we can't show grades.

`@instructions`
- Create an object called `p_hits` that contains the proportion of intervals that contain the actual spread using the following steps.
- Use the `mutate` function to create a new variable called `hit` that contains a logical vector for whether the `actual_spread` falls between the `lower` and `upper` confidence intervals.
- Use the `group_by` function to group the data by state.
- Use the `filter` function to filter for states that have more than 5 polls.
- Summarize the proportion of values in `hit` that are true as a variable called `proportion_hits`. Also create new variables for the number of polls in each state using the `n()` function.
- Use the `arrange` function to arrange the `proportion_hits` in descending order.

`@hint`
- Use `n=n()` in the `summarize` function to include the number of polls

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
cis <- polls %>% mutate(X_hat = (spread+1)/2, se = 2*sqrt(X_hat*(1-X_hat)/samplesize), 
                 lower = spread - qnorm(0.975)*se, upper = spread + qnorm(0.975)*se) %>%
  select(state, startdate, enddate, pollster, grade, spread, lower, upper)
```

`@sample_code`
```{r}
# The `cis` data have already been loaded for you
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
ci_data <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")

# Create an object called `p_hits` that summarizes the proportion of hits for each state that has more than 5 polls.
```

`@solution`
```{r}
# The `cis` data have already been loaded for you
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
ci_data <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")

# Create an object called `p_hits` that summarizes the proportion of hits for each state that has more than 5 polls. 
p_hits <- ci_data %>% mutate(hit = lower <= actual_spread & upper >= actual_spread) %>% 
  group_by(state) %>%
  filter(n() >=  5) %>%
  summarize(proportion_hits = mean(hit), n = n()) %>%
  arrange(desc(proportion_hits)) 
p_hits
```

`@sct`
```{r}
test_error()
test_object("p_hits",
            eq_condition = "equivalent",
            undefined_msg = "Remember to create an object called `p_hits`.",
            incorrect_msg = "The object `p_hits` should contain columns for the state, proportion of hits, and number of polls for 51 states.")
success_msg("Great work! Let's examine these data further.")
```

---

## Exercise 5- Plotting Prediction Results

```yaml
type: NormalExercise
key: 83b0df8ff1
lang: r
xp: 100
skills:
  - 1
```

Make a barplot based on the result from the previous exercise.

`@instructions`
- Reorder the states in order of the proportion of hits.
- Using `ggplot`, set the aesthetic with state as the x-variable and proportion of hits as the y-variable.
- Use `geom_bar` to indicate that we want to plot a barplot. Specifcy `stat = "identity"` to indicate that the height of the bar should match the value.
- Use `coord_flip` to flip the axes so the states are displayed from top to bottom and proportions are displayed from left to right.

`@hint`
- Use the `reorder` function to reorder the states by proportion of hits.
- Use `stat=identity` when calling the `geom_bar` function.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
cis <- polls %>% mutate(X_hat = (spread+1)/2, se = 2*sqrt(X_hat*(1-X_hat)/samplesize), 
                 lower = spread - qnorm(0.975)*se, upper = spread + qnorm(0.975)*se) %>%
  select(state, startdate, enddate, pollster, grade, spread, lower, upper)
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
cis <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")
p_hits <- cis %>% mutate(hit = lower <= actual_spread & upper >= actual_spread) %>% 
  group_by(state) %>%
  filter(n() >=  5) %>%
  summarize(proportion_hits = mean(hit), n = n()) %>%
  arrange(desc(proportion_hits))
```

`@sample_code`
```{r}
# The `p_hits` data have already been loaded for you. Use the `head` function to examine it.
head(p_hits)

# Make a barplot of the proportion of hits for each state
```

`@solution`
```{r}
# The `p_hits` data have already been loaded for you. Use the `head` function to examine it.
head(p_hits)

# Make a barplot of the proportion of hits for each state
p_hits %>% mutate(state = reorder(state, proportion_hits)) %>%
  ggplot(aes(state, proportion_hits)) + 
  geom_bar(stat = "identity") +
  coord_flip()
```

`@sct`
```{r}
test_error()
test_function("ggplot", not_called_msg = "Use `ggplot` to create this barplot. Be sure to set the aesthetic using `aes(state, proportion_hits).")
test_function("geom_bar", not_called_msg = "Use `geom_bar` to create this barplot.")
test_function("coord_flip", not_called_msg = "Use `coord_flip` to flip the axes so that states are displayed from top to bottom.")
success_msg("Great work! Let's continue.")
```

---

## Exercise 6 - Predicting the Winner

```yaml
type: NormalExercise
key: ad84b98c60
lang: r
xp: 100
skills:
  - 1
```

Even if a forecaster's confidence interval is incorrect, the overall predictions will do better if they correctly called the right winner. 

Add two columns to the `cis` table by computing, for each poll, the difference between the predicted spread and the actual spread, and define a column `hit` that is true if the signs are the same.

`@instructions`
- Use the `mutate` function to add two new variables to the `cis` object: `error` and `hit`.
- For the `error` variable, subtract the actual spread from the spread.
- For the `hit` variable, return "TRUE" if the poll predicted the actual winner. Use the `sign` function to check if their signs match - learn more with `?sign`.
- Save the new table as an object called `errors`.
- Use the `tail` function to examine the last 6 rows of `errors`.

`@hint`
- Use the function `sign` to return the sign of a value.
- Use the logical operator `==` to indicate whether two values are equal.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
cis <- polls %>% mutate(X_hat = (spread+1)/2, se = 2*sqrt(X_hat*(1-X_hat)/samplesize), 
                 lower = spread - qnorm(0.975)*se, upper = spread + qnorm(0.975)*se) %>%
  select(state, startdate, enddate, pollster, grade, spread, lower, upper)
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
cis <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")
```

`@sample_code`
```{r}
# The `cis` data have already been loaded. Examine it using the `head` function.
head(cis)

# Create an object called `errors` that calculates the difference between the predicted and actual spread and indicates if the correct winner was predicted


# Examine the last 6 rows of `errors`
```

`@solution`
```{r}
# The `cis` data have already been loaded. Examine it using the `head` function.
head(cis)

# Create an object called `errors` that calculates the difference between the predicted and actual spread and indicates if the correct winner was predicted
errors <- cis %>% mutate(error = spread - actual_spread, hit = sign(spread) == sign(actual_spread))

# Examine the last 6 rows of `errors`
tail(errors)
```

`@sct`
```{r}
test_error()
test_object("errors",
            eq_condition = "equivalent",
            undefined_msg = "Remember to create an object called `errors`.",
            incorrect_msg = "The object `cis` should contain columns for the 'state', 'startdate', 'enddate', 'pollster', 'grade', 'spread', 'lower', 'upper', 'actual_spread', 'error', and 'hit'.")
success_msg("Great work! Let's plot these data.")
```

---

## Exercise 7 - Plotting Prediction Results

```yaml
type: NormalExercise
key: a28f230534
lang: r
xp: 100
skills:
  - 1
```

Create an object called `p_hits` that contains the proportion of instances when the sign of the actual spread matches the predicted spread for states with 5 or more polls.

Make a barplot based on the result from the previous exercise that shows the proportion of times the sign of the spread matched the actual result for the data in `p_hits`.

`@instructions`
- Use the `group_by` function to group the data by state.
- Use the `filter` function to filter for states that have 5 or more polls.
- Summarize the proportion of values in `hit` that are true as a variable called `proportion_hits`. Also create a variable called `n` for the number of polls in each state using the `n()` function.
- To make the plot, follow these steps:
- Reorder the states in order of the proportion of hits.
- Using `ggplot`, set the aesthetic with state as the x-variable and proportion of hits as the y-variable.
- Use `geom_bar` to indicate that we want to plot a barplot.
- Use `coord_flip` to flip the axes so the states are displayed from top to bottom and proportions are displayed from left to right.

`@hint`
- Use `n=n()` in the `summarize` function to include the number of polls
- Use the `reorder` function to reorder the states by proportion of hits.
- Use `stat=identity` when calling the `geom_bar` function.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
library(ggplot2)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
cis <- polls %>% mutate(X_hat = (spread+1)/2, se = 2*sqrt(X_hat*(1-X_hat)/samplesize), 
                 lower = spread - qnorm(0.975)*se, upper = spread + qnorm(0.975)*se) %>%
  select(state, startdate, enddate, pollster, grade, spread, lower, upper)
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
cis <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")
```

`@sample_code`
```{r}
# Create an object called `errors` that calculates the difference between the predicted and actual spread and indicates if the correct winner was predicted
errors <- cis %>% mutate(error = spread - actual_spread, hit = sign(spread) == sign(actual_spread))

# Create an object called `p_hits` that summarizes the proportion of hits for each state that has 5 or more polls





# Make a barplot of the proportion of hits for each state
```

`@solution`
```{r}
# Create an object called `errors` that calculates the difference between the predicted and actual spread and indicates if the correct winner was predicted
errors <- cis %>% mutate(error = spread - actual_spread, hit = sign(spread) == sign(actual_spread))

# Create an object called `p_hits` that summarizes the proportion of hits for each state that has 5 or more polls
p_hits <- errors %>%  group_by(state) %>%
  filter(n() >=  5) %>%
  summarize(proportion_hits = mean(hit), n = n())

# Make a barplot of the proportion of hits for each state
p_hits %>% mutate(state = reorder(state, proportion_hits)) %>%
  ggplot(aes(state, proportion_hits)) + 
  geom_bar(stat = "identity") +
 coord_flip()
```

`@sct`
```{r}
test_error()
test_object("p_hits",
            eq_condition = "equivalent",
            undefined_msg = "Remember to create an object called `p_hits`.",
            incorrect_msg = "The object `p_hits` is incorrect. Did you filter for states with 5 or more polls, then use `summarize` to create columns named `proportion_hits` and `n`?")
test_function("ggplot", not_called_msg = "Use `ggplot` to create this barplot. Be sure to set the aesthetic using `aes(state, proportion_hits).")
test_function("geom_bar", not_called_msg = "Use `geom_bar` to create this barplot.")
test_function("coord_flip", not_called_msg = "Use `coord_flip` to flip the axes so that states are displayed from top to bottom.")
success_msg("Great work! Let's continue.")
```

---

## Exercise 8 - Plotting the Errors

```yaml
type: NormalExercise
key: 98ba61774d
lang: r
xp: 100
skills:
  - 1
```

In the previous graph, we see that most states' polls predicted the correct winner 100% of the time. Only a few states polls' were incorrect more than 25% of the time. Wisconsin got every single poll wrong. In Pennsylvania and Michigan, more than 90% of the polls had the signs wrong. 

Make a histogram of the errors. What is the median of these errors?

`@instructions`
- Use the `hist` function to generate a histogram of the errors
- Use the `median` function to compute the median error

`@hint`
- The column called `error` in the `errors` object contains the errors for each poll.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
cis <- polls %>% mutate(X_hat = (spread+1)/2, se = 2*sqrt(X_hat*(1-X_hat)/samplesize), 
                 lower = spread - qnorm(0.975)*se, upper = spread + qnorm(0.975)*se) %>%
  select(state, startdate, enddate, pollster, grade, spread, lower, upper)
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
cis <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")
errors <- cis %>% mutate(error = spread - actual_spread, hit = sign(spread) == sign(actual_spread))
```

`@sample_code`
```{r}
# The `errors` data have already been loaded. Examine them using the `head` function.
head(errors)

# Generate a histogram of the error


# Calculate the median of the errors. Print this value to the console.
```

`@solution`
```{r}
# The `errors` data have already been loaded. Examine them using the `head` function.
head(errors)

# Generate a histogram of the error
hist(errors$error)

# Calculate the median of the errors. Print this value to the console.
median(errors$error)
```

`@sct`
```{r}
test_error()
test_function("hist", not_called_msg = "Use the `hist` function to create this histogram. Be sure to plot the errors.")
test_function("median", not_called_msg = "Use the `median` function to compute the median of the errors.")
test_output_contains("0.037", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are using the `median` function to compute the median of `error` in the `errors` object.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 9- Plot Bias by State

```yaml
type: NormalExercise
key: 7a0a51b66f
lang: r
xp: 100
skills:
  - 1
```

We see that, at the state level, the median error was slightly in favor of Clinton. The distribution is not centered at 0, but at 0.037. This value represents the general bias we described in an earlier section. 

Create a boxplot to examine if the bias was general to all states or if it affected some states differently. Filter the data to include only pollsters with grades B+ or higher.

`@instructions`
- Use the `filter` function to filter the data for polls with grades equal to A+, A, A-, or B+.
- Use the `reorder` function to order the state data by error.
- Using `ggplot`, set the aesthetic with state as the x-variable and error as the y-variable.
- Use `geom_boxplot` to indicate that we want to plot a boxplot.
- Use `geom_point` to add data points as a layer.

`@hint`
- Use the following code to filter by grade: 
```{r}
filter(grade %in% c("A+","A","A-","B+") | is.na(grade))
```

- Make the axes labels easier to read with the following code:
```{r}
theme(axis.text.x = element_text(angle = 90, hjust = 1))
```

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
library(ggplot2)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
cis <- polls %>% mutate(X_hat = (spread+1)/2, se = 2*sqrt(X_hat*(1-X_hat)/samplesize), 
                 lower = spread - qnorm(0.975)*se, upper = spread + qnorm(0.975)*se) %>%
  select(state, startdate, enddate, pollster, grade, spread, lower, upper)
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
cis <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")
errors <- cis %>% mutate(error = spread - actual_spread, hit = sign(spread) == sign(actual_spread))
```

`@sample_code`
```{r}
# The `errors` data have already been loaded. Examine them using the `head` function.
head(errors)

# Create a boxplot showing the errors by state for polls with grades B+ or higher
```

`@solution`
```{r}
# The `errors` data have already been loaded. Examine them using the `head` function.
head(errors)

# Create a boxplot showing the errors by state for polls with grades B+ or higher
errors %>% filter(grade %in% c("A+","A","A-","B+") | is.na(grade)) %>%
  mutate(state = reorder(state, error)) %>%
  ggplot(aes(state, error)) + 
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) +
  geom_boxplot() + 
  geom_point()
```

`@sct`
```{r}
test_error()
test_function("ggplot", not_called_msg = "Use `ggplot` to create this boxplot. Be sure to set the aesthetic using `aes(state, error).")
test_function("geom_boxplot", not_called_msg = "Use `geom_boxplot` to create this boxplot.")
test_function("geom_point", not_called_msg = "Use `geom_point` to add points to this plot.")
success_msg("Great work! Let's look at one more thing.")
```

---

## Exercise 10 - Filter Error Plot

```yaml
type: NormalExercise
key: 442b9a9302
lang: r
xp: 100
skills:
  - 1
```

Some of these states only have a few polls. Repeat the previous exercise to plot the errors for each state, but only include states with five good polls or more.

`@instructions`
- Use the `filter` function to filter the data for polls with grades equal to A+, A, A-, or B+.
- Group the filtered data by state using `group_by`.
- Use the `filter` function to filter the data for states with at least 5 polls. Then, use `ungroup` so that polls are no longer grouped by state.
- Use the `reorder` function to order the state data by error.
- Using `ggplot`, set the aesthetic with state as the x-variable and error as the y-variable.
- Use `geom_boxplot` to indicate that we want to plot a boxplot.
- Use `geom_point` to add data points as a layer.

`@hint`
- After you use `group_by` to group by state and `filter` to filter for the number and quality of polls, use the `ungroup` function to ungroup the data for sorting and plotting.
- Use the following code to make the axis text easier to read:

```{r}
theme(axis.text.x = element_text(angle = 90, hjust = 1))
```

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
library(ggplot2)
data("polls_us_election_2016")
polls <- polls_us_election_2016 %>% 
  filter(state != "U.S." & enddate >= "2016-10-31") %>% 
  mutate(spread = rawpoll_clinton/100 - rawpoll_trump/100)
cis <- polls %>% mutate(X_hat = (spread+1)/2, se = 2*sqrt(X_hat*(1-X_hat)/samplesize), 
                 lower = spread - qnorm(0.975)*se, upper = spread + qnorm(0.975)*se) %>%
  select(state, startdate, enddate, pollster, grade, spread, lower, upper)
add <- results_us_election_2016 %>% mutate(actual_spread = clinton/100 - trump/100) %>% select(state, actual_spread)
cis <- cis %>% mutate(state = as.character(state)) %>% left_join(add, by = "state")
errors <- cis %>% mutate(error = spread - actual_spread, hit = sign(spread) == sign(actual_spread))
```

`@sample_code`
```{r}
# The `errors` data have already been loaded. Examine them using the `head` function.
head(errors)

# Create a boxplot showing the errors by state for states with at least 5 polls with grades B+ or higher
```

`@solution`
```{r}
# The `errors` data have already been loaded. Examine them using the `head` function.
head(errors)

# Create a boxplot showing the errors by state for states with at least 5 polls with grades B+ or higher
errors %>% filter(grade %in% c("A+","A","A-","B+") | is.na(grade)) %>%
  group_by(state) %>%
  filter(n() >= 5) %>%
  ungroup() %>%
  mutate(state = reorder(state, error)) %>%
  ggplot(aes(state, error)) + 
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) +
  geom_boxplot() + 
  geom_point()
```

`@sct`
```{r}
test_error()
test_function("ggplot", not_called_msg = "Use `ggplot` to create this barplot. Be sure to set the aesthetic using `aes(state, error).")
test_function("geom_boxplot", not_called_msg = "Use `geom_boxplot` to create this boxplot")
test_function("geom_point", not_called_msg = "Use `geom_point` to add points to this plot.")
success_msg("Great work! You see that the West (Washington, New Mexico, California) underestimated Hillary's performance, while the Midwest (Michigan, Pennsylvania, Wisconsin, Ohio, Missouri) overestimated it. In our simulation in we did not model this behavior since we added general bias, rather than a regional bias. Some pollsters are now modeling correlation between similar states and estimating this correlation from historical data. To learn more about this, you can learn about random effects and mixed models.")
```

---

## End of Assessment

```yaml
type: PureMultipleChoiceExercise
key: bcfe0528c5
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
