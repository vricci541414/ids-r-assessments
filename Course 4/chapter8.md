---
title: Association and Chi-Squared Tests
description: >-
  In this chapter, you will learn about the association tests and the chi-square
  test.
---

## Exercise 1 - Comparing Proportions of Hits

```yaml
type: NormalExercise
key: 8c8fbd5c4f
lang: r
xp: 100
skills:
  - 1
```

In a previous exercise, we determined whether or not each poll predicted the correct winner for their state in the 2016 U.S. presidential election. Each poll was also assigned a grade by the poll aggregator. Now we're going to determine if polls rated A- made better predictions than polls rated C-.

In this exercise, filter the errors data for just polls with grades A- and C-. Calculate the proportion of times each grade of poll predicted the correct winner.

`@instructions`
- Filter `errors` for grades A- and C-.
- Group the data by grade and hit.
- Summarize the number of hits for each grade.
- Generate a two-by-two table containing the number of hits and misses for each grade. Try using the `spread` function to generate this table.
- Calculate the proportion of times each grade was correct.

`@hint`
- After grouping by grade and hit, you can use the `summarize` function to tally up the columns. Then you can use the `spread` function to generate the two-by-two table.

```{r}
summarize(num = n()) %>%
  spread(grade, num)
```

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
library(tidyr)

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
# The 'errors' data have already been loaded. Examine them using the `head` function.
head(errors)

# Generate an object called 'totals' that contains the numbers of good and bad predictions for polls rated A- and C-






# Print the proportion of hits for grade A- polls to the console


# Print the proportion of hits for grade C- polls to the console
```

`@solution`
```{r}
# The 'errors' data have already been loaded. Examine them using the `head` function.
head(errors)

# Generate an object called 'totals' that contains the numbers of good and bad predictions for polls rated A- and C-
totals <- errors %>%
  filter(grade %in% c("A-", "C-")) %>%
  group_by(grade,hit) %>%
  summarize(num = n()) %>%
  spread(grade, num)

# Print the proportion of hits for grade A- polls to the console
totals[[2,3]]/sum(totals[[3]])

# Print the proportion of hits for grade C- polls to the console
totals[[2,2]]/sum(totals[[2]])
```

`@sct`
```{r}
test_error()
test_output_contains(0.8030303, incorrect_msg = "You are not generating the correct proportion of times the grade A- polls were correct. Make sure to filter by grade and divide the number of positive hits by the total number of grade A- polls. Print only the value (no column names).")
test_output_contains(0.8614958, incorrect_msg = "You are not generating the correct proportion of times the grade C- polls were correct. Make sure to filter by grade and divide the number of positive hits by the total number of grade C- polls. Print only the value (no column names).")
success_msg("Great work! Let's see if these proportions are actually different.")
```

---

## Exercise 2 - Chi-squared Test

```yaml
type: NormalExercise
key: cc7bf4c4ff
lang: r
xp: 100
skills:
  - 1
```

We found that the A- polls predicted the correct winner about 80% of the time in their states and C- polls predicted the correct winner about 86% of the time.

Use a chi-squared test to determine if these proportions are different.

`@instructions`
- Use the `chisq.test` function to perform the chi-squared test. Save the results to an object called `chisq_test`.
- Print the p-value of the test to the console.

`@hint`
- Remember to remove the `hit` column from the `totals` data so that your data are in the two-by-two form going into the chi-squared test. You can remove the column using the `select` function as in the sample code below.

```{r}
totals %>% select(-hit)
```

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
library(tidyr)
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
totals <- errors %>%
  filter(grade %in% c("A-", "C-")) %>%
  group_by(grade,hit) %>%
  summarize(num = n()) %>%
  spread(grade, num)
```

`@sample_code`
```{r}
# The 'totals' data have already been loaded. Examine them using the `head` function.
head(totals)

# Perform a chi-squared test on the hit data. Save the results as an object called 'chisq_test'.






# Print the p-value of the chi-squared test to the console
```

`@solution`
```{r}
# The 'totals' data have already been loaded. Examine them using the `head` function.
head(totals)

# Perform a chi-squared test on the hit data. Save the results as an object called 'chisq_test'.
chisq_test <- totals %>% 
  select(-hit) %>%
  chisq.test()
chisq_test

# Print the p-value of the chi-squared test to the console
chisq_test$p.value
```

`@sct`
```{r}
test_error()
test_output_contains(0.1467902, incorrect_msg = "You are not generating the correct p-value for the chi-squared test. Make sure you are printing the entire p-value to the console.")
success_msg("Great work! Let's calculate the odds ratio.")
```

---

## Exercise 3 - Odds Ratio Calculation

```yaml
type: NormalExercise
key: 02122520a8
lang: r
xp: 100
skills:
  - 1
```

It doesn't look like the grade A- polls performed significantly differently than the grade C- polls in their states.

Calculate the odds ratio to determine the magnitude of the difference in performance between these two grades of polls.

`@instructions`
- Calculate the odds that a grade C- poll predicts the correct winner. Save this result to a variable called `odds_C`.
- Calculate the odds that a grade A- poll predicts the correct winner. Save this result to a variable called `odds_A`.
- Calculate the odds ratio that tells us how many times larger the odds of a grade A- poll is at predicting the winner than a grade C- poll.

`@hint`
- Remember the following formula for calculating the odds. In our case, $Y$ represents predicting the winner successfully (1) or not (0) and $X$ represents whether or not the polls are a grade of interest.  

$$\mbox{Pr}(Y=1 \mid X=1) / \mbox{Pr}(Y=0 \mid X=1)$$

- You can use brackets to subset a data frame for cells of interest. For example, the sample code below subsets `data` for the contents in the second row of the first column.

```{r}
data[2,1]
```

`@pre_exercise_code`
```{r}
library(dslabs)
library(dplyr)
library(tidyr)
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
totals <- errors %>%
  filter(grade %in% c("A-", "C-")) %>%
  group_by(grade,hit) %>%
  summarize(num = n()) %>%
  spread(grade, num)
```

`@sample_code`
```{r}
# The 'totals' data have already been loaded. Examine them using the `head` function.
head(totals)

# Generate a variable called `odds_C` that contains the odds of getting the prediction right for grade C- polls




# Generate a variable called `odds_A` that contains the odds of getting the prediction right for grade A- polls




# Calculate the odds ratio to determine how many times larger the odds ratio is for grade A- polls than grade C- polls
```

`@solution`
```{r}
# The 'totals' data have already been loaded. Examine them using the `head` function.
head(totals)

# Generate a variable called `odds_C` that contains the odds of getting the prediction right for grade C- polls
odds_C <- (totals[[2,2]] / sum(totals[[2]])) / 
  (totals[[1,2]] / sum(totals[[2]]))

# Generate a variable called `odds_A` that contains the odds of getting the prediction right for grade A- polls
odds_A <- (totals[[2,3]] / sum(totals[[3]])) / 
  (totals[[1,3]] / sum(totals[[3]]))

# Calculate the odds ratio to determine how many times larger the odds ratio is for grade A- polls than grade C- polls
odds_A/odds_C
```

`@sct`
```{r}
test_error()
test_object("odds_C",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = NULL,
            incorrect_msg = "Something isn't right in `odds_C`. Are you using the correct formula to calculate these odds?")
test_object("odds_A",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = NULL,
            incorrect_msg = "Something isn't right in `odds_A`. Are you using the correct formula to calculate these odds?")
test_output_contains(0.6554539, incorrect_msg = "You are not generating the correct odds ratio. Make sure you divide the odds that the grade A- polls were correct by the odds that the grade C- polls were correct.")
success_msg("Great work! Let's wrap it up.")
```

---

## Exercise 4 - Significance

```yaml
type: MultipleChoiceExercise
key: c596d7b02a
lang: r
xp: 50
skills:
  - 1
```

We did not find meaningful differences between the poll results from grade A- and grade C- polls in this subset of the data, which only contains polls for about a week before the election. Imagine we expanded our analysis to include all election polls and we repeat our analysis. In this hypothetical scenario, we get that the p-value for the difference in prediction success if 0.0015 and the odds ratio describing the effect size of the performance of grade A- over grade B- polls is 1.07.

Based on what we learned in the last section, which statement reflects the best interpretation of this result?

`@possible_answers`
- The p-value is below 0.05, so there is a significant difference. Grade A- polls are significantly better at predicting winners.
- The p-value is too close to 0.05 to call this a significant difference. We do not observe a difference in performance.
- The p-value is below 0.05, but the odds ratio is very close to 1. There is not a scientifically significant difference in performance.
- The p-value is below 0.05 and the odds ratio indicates that grade A- polls perform significantly better than grade C- polls.

`@hint`
- The odds ratio tells you the magnitude of the difference between two groups.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try  again. You also need to consider the magnitude of the difference in performance."
msg2 = "Try again. The p-value is well below 0.05. What else do we think about when comparing performance between two groups?"
msg3 = "Correct!"
msg4 = "Try again. The odds ratio indicates that the two grades perform very similarly."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## End of Assessment

```yaml
type: PureMultipleChoiceExercise
key: 8a8182510f
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
