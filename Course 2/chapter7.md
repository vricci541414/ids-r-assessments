---
title: Summarizing with dplyr
description: >-
  We will practice our dplyr skills by will be working with data from the survey
  collected by the United States National Center for Health Statistics (NCHS)
---

## Practice Exercise. National Center for Health Statistics

```yaml
type: MultipleChoiceExercise
key: 2f6ce1c49b
lang: r
xp: 50
skills:
  - 1
```

To practice our dplyr skills we will be working with data from the survey collected by the United States National Center for Health Statistics (NCHS). This center has conducted a series of health and nutrition surveys since the 1960’s.

Starting in 1999, about 5,000 individuals of all ages have been interviewed every year and then they complete the health examination component of the survey. Part of this dataset is made available via the NHANES package which can be loaded this way:

```{r}
library(NHANES)
data(NHANES)
```

The NHANES data has many missing values. Remember that the main summarization function in R will return `NA` if any of the entries of the input vector is an `NA`. Here is an example:

```{r}
library(dslabs)
data(na_example)
mean(na_example)
sd(na_example)
```

To ignore the `NA`s, we can use the `na.rm` argument:

```{r}
mean(na_example, na.rm = TRUE)
sd(na_example, na.rm = TRUE)
```
Try running this code, then let us know you are ready to proceed with the analysis.

`@possible_answers`
- Ready!

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Alrighty!"
test_mc(1,c(msg1))
```

---

## Exercise 1. Blood pressure 1

```yaml
type: NormalExercise
key: be7d33bb10
lang: r
xp: 100
skills:
  - 1
```

Let's explore the NHANES data. We will be exploring blood pressure in this dataset.

First let's select a group to set the standard. We will use 20-29 year old females. Note that the category is coded with ` 20-29`, with a space in front of the `20`! The `AgeDecade` is a categorical variable with these ages.

To know if someone is female, you can look at the `Gender` variable.

`@instructions`
- Filter the `NHANES` dataset so that only 20-29 year old females are included and assign this new data frame to the object `tab`.
- Use the pipe to apply the function `filter`, with the appropriate logicals, to `NHANES`.
    - Remember that this age group is coded with ` 20-29`, which includes a space. You can use `head` to explore the `NHANES` table to construct the correct call to filter.

`@hint`
Use the logical `AgeDecade == " 20-29" & Gender == "female"` within `filter`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
## fill in what is needed
tab <- NHANES %>%
```

`@solution`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
tab <- NHANES %>% filter(AgeDecade == " 20-29" & Gender == "female")
```

`@sct`
```{r}
test_error()
test_pipe(absent_msg = "We want you to use the pipe `%>%` here.")
test_function("filter", incorrect_msg = "Don't forget to `filter` by `AgeDecade` and by `Gender`")
test_object("tab",incorrect_msg = "Make sure to define `tab` and that you filter correctly.")
success_msg("Great job!")
```

---

## Exercise 2. Blood pressure 2

```yaml
type: NormalExercise
key: 2c14b6405a
lang: r
xp: 100
skills:
  - 1
```

Now we will compute the average and standard deviation for the subgroup we defined in the previous exercise (20-29 year old females), which we will use reference for what is typical.

You will determine the average and standard deviation of systolic blood pressure, which are stored in the `BPSysAve` variable in the NHANES dataset.

`@instructions`
- Complete the line of code to save the average and standard deviation of systolic blood pressure as `average` and `standard_deviation` to a variable called `ref`.
- Use the `summarize` function after filtering for 20-29 year old females and connect the results using the pipe `%>%`. When doing this remember there are `NA`s in the data!

`@hint`
- Use `filter` and `summarize` and use the `na.rm=TRUE` argument when computing the average and standard deviation. You can also filter the NA values using `filter`.
- Make sure you name the average and standard deviation correctly within `summarize`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
## complete this line of code.
ref <- NHANES %>% filter(AgeDecade == " 20-29" & Gender == "female") %>%
```

`@solution`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
ref <- NHANES %>%
  filter(AgeDecade == " 20-29" & Gender == "female") %>%
  summarize(average = mean(BPSysAve, na.rm = TRUE), 
            standard_deviation = sd(BPSysAve, na.rm = TRUE))
ref
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "Don't forget to `filter` by `AgeDecade` and by `Gender`.")
test_function("summarize",incorrect_msg = "Are you creating variables named `average` and `standard_deviation`?")
ex() %>% {
  check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
  check_function(., "sd") %>% check_arg(., "na.rm") %>% check_equal()
}
success_msg("Great job!")
```

---

## Exercise 3. Summarizing averages

```yaml
type: NormalExercise
key: 154efca36c
lang: r
xp: 100
skills:
  - 1
```

Now we will repeat the exercise and generate only the average blood pressure for 20-29 year old females. For this exercise, you should review how to use the place holder `.` in dplyr or the `pull` function.

`@instructions`
Modify the line of sample code to assign the average to a numeric variable called `ref_avg` using the `.` or `pull`.

`@hint`
Use the code similar to the sample code and then add the dot: `.$average`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
## modify the code we wrote for previous exercise.
ref_avg <- NHANES %>%
  filter(AgeDecade == " 20-29" & Gender == "female") %>%
  summarize(average = mean(BPSysAve, na.rm = TRUE), 
            standard_deviation = sd(BPSysAve, na.rm=TRUE))
```

`@solution`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
ref_avg <- NHANES %>%
      filter(AgeDecade == " 20-29" & Gender == "female") %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE)) %>%
      .$average
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "Don't forget to `filter` by `AgeDecade` and by `Gender`")
test_function("summarize",incorrect_msg = "Are you creating a variable named `average` and `standard_deviation`?")
ex() %>% {
  check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
}
test_object("ref_avg",incorrect_msg = "Make sure to define `ref_avg`")
success_msg("Great job!")
```

---

## Exercise 4. Min and max

```yaml
type: NormalExercise
key: e0deb31386
lang: r
xp: 100
skills:
  - 1
```

Let's continue practicing by calculating two other data summaries: the minimum and the maximum.

Again we will do it for the `BPSysAve` variable and the group of 20-29 year old females.

`@instructions`
- Report the min and max values for the same group as in the previous exercises.
- Use `filter` and `summarize` connected by the pipe `%>%` again. The functions `min` and `max` can be used to get the values you want.
- Within `summarize`, save the min and max of systolic blood pressure as `minbp` and `maxbp`.

`@hint`
- Take a look at the solution to Exercise 3 - but instead of `mean` and `sd`, we are using `min` and `max`.
- Remember to remove `NA` values in the dataset!

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
## complete the line
NHANES %>%
      filter(AgeDecade == " 20-29"  & Gender == "female") %>%

```

`@solution`
```{r}
library(NHANES)
data(NHANES)
NHANES %>%
      filter(AgeDecade == " 20-29"  & Gender == "female") %>%
      summarize(minbp = min(BPSysAve, na.rm = TRUE), 
                maxbp = max(BPSysAve, na.rm = TRUE))
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "Don't forget to `filter` by `AgeDecade` and by `Gender`")
test_function("summarize",incorrect_msg = "Are you creating a variable named `min` and `max`?")
#test_function("min",incorrect_msg = "Don't forget to include `na.rm`")
#test_function("max",incorrect_msg = "Don't forget to include `na.rm`")
ex() %>% {
   check_function(., "min") %>% check_arg(., "na.rm") %>% check_equal()
   check_function(., "max") %>% check_arg(., "na.rm") %>% check_equal()
}
test_output_contains("NHANES %>% filter(AgeDecade == ' 20-29'  & Gender == 'female') %>% summarize(minbp = min(BPSysAve, na.rm = TRUE),maxbp = max(BPSysAve, na.rm = TRUE))",incorrect_msg="Try again!")
success_msg("Great job!")
```

---

## Exercise 5. group_by

```yaml
type: NormalExercise
key: 39e2ca43e3
lang: r
xp: 100
skills:
  - 1
```

Now let's practice using the `group_by` function. 

What we are about to do is a very common operation in data science: you will split a data table into groups and then compute summary statistics for each group.

We will compute the average and standard deviation of systolic blood pressure for females for each age group separately. Remember that the age groups are contained in `AgeDecade`.

`@instructions`
- Use the functions `filter`, `group_by`, `summarize`, and the pipe `%>%` to compute the average and standard deviation of systolic blood pressure for females for each age group separately.
- Within `summarize`, save the average and standard deviation of systolic blood pressure (`BPSysAve`) as `average` and `standard_deviation`.
- Note: ignore warnings about implicit NAs. This warning will not prevent your code from running or being graded correctly.

`@hint`
- In the `filter` call we only filter on `Gender` not `AgeDecade`.
- `AgeDecade` should be used in the `group_by` function.
- The rest is very similar to the code from previous exercises in which we computed average and standard deviation.
- Don't forget to remove the `NA`s!

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
##complete the line with group_by and summarize
NHANES %>%
      filter(Gender == "female") %>%
```

`@solution`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
NHANES %>%
      filter(Gender == "female") %>%
      group_by(AgeDecade) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE))
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "Don't forget to `filter` by `Gender`")
test_function("group_by", incorrect_msg = "Don't forget to `group_by` by `AgeDecade`")
test_function("summarize",incorrect_msg = "Are you creating a variable named `average` and `standard_deviation`?")
ex() %>% {
   check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
   check_function(., "sd") %>% check_arg(., "na.rm") %>% check_equal()
}
test_output_contains("NHANES %>% filter(Gender == 'female') %>% group_by(AgeDecade) %>% summarize(average = mean(BPSysAve, na.rm = TRUE), standard_deviation = sd(BPSysAve, na.rm=TRUE))",incorrect_msg="Try again!")
success_msg("Great job!")
```

---

## Exercise 6. group_by example 2

```yaml
type: NormalExercise
key: 2b7079d1d7
lang: r
xp: 100
skills:
  - 1
```

Now let's practice using `group_by` some more. We are going to repeat the previous exercise of calculating the average and standard deviation of systolic blood pressure, but for males instead of females.

This time we will not provide much sample code. You are on your own!

`@instructions`
- Calculate the average and standard deviation of systolic blood pressure for males for each age group separately using the same methods as in the previous exercise.
- Save the average and standard deviation of systolic blood pressure (`BPSysAve`) as `average` and `standard_deviation`.

Note: ignore warnings about implicit NAs. This warning will not prevent your code from running or being graded correctly.

`@hint`
Change your filter for `Gender` to reflect the new category - everything else stays the same as in the previous exercise!

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@solution`
```{r}
library(NHANES)
data(NHANES)
NHANES %>%
      filter(Gender == "male") %>%
      group_by(AgeDecade) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE))
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "Don't forget to `filter` by `Gender`")
test_function("group_by", incorrect_msg = "Don't forget to `group_by` by `AgeDecade`")
test_function("summarize",incorrect_msg = "Are you creating a variable named `average` and `standard_deviation`?")
ex() %>% {
   check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
   check_function(., "sd") %>% check_arg(., "na.rm") %>% check_equal()
}
test_output_contains("NHANES%>%filter(Gender=='male')%>%group_by(AgeDecade)%>%summarize(average=mean(BPSysAve,na.rm=TRUE),standard_deviation=sd(BPSysAve,na.rm=TRUE))",incorrect_msg="Try again!")

success_msg("Great job!")
```

---

## Exercise 7. group_by example 3

```yaml
type: NormalExercise
key: f653ffcd3a
lang: r
xp: 100
skills:
  - 1
```

We can actually combine both of these summaries into a single line of code. This is because `group_by` permits us to group by more than one variable.

We can use `group_by(AgeDecade, Gender)` to group by both age decades and gender.

`@instructions`
- Create a single summary table for the average and standard deviation of systolic blood pressure using `group_by(AgeDecade, Gender)`.
    - Note that we no longer have to `filter`!
    - Your code within `summarize` should remain the same as in the previous exercises, and should use the variable names `average` and `standard_deviation`.
- Note: ignore warnings about implicit NAs. This warning will not prevent your code from running or being graded correctly.

`@hint`
This just like the previous exercise except that we do not filter and we change `group_by` to include both age decade and gender.

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(NHANES)
data(NHANES)
```

`@solution`
```{r}
library(NHANES)
data(NHANES)
NHANES %>%
      group_by(AgeDecade, Gender) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE))
```

`@sct`
```{r}
test_error()
test_function("group_by", incorrect_msg = "Don't forget to `group_by` by `AgeDecade` and by `Gender`")
test_function("summarize",incorrect_msg = "Are you creating a variable named `average` and `standard_deviation`?")
ex() %>% {
   check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
   check_function(., "sd") %>% check_arg(., "na.rm") %>% check_equal()
}
test_output_contains("NHANES %>%
      group_by(AgeDecade, Gender) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE))",incorrect_msg="Try again!")
success_msg("Great job!")
```

---

## Exercise 8. Arrange

```yaml
type: NormalExercise
key: 89bb8e55f9
lang: r
xp: 100
skills:
  - 1
```

Now we are going to explore differences in systolic blood pressure across races, as reported in the `Race1` variable.

We will learn to use the `arrange` function to order the outcome acording to one variable. 

Note that this function can be used to order any table by a given outcome. Here is an example that arranges by systolic blood pressure. 

```{r}
NHANES %>% arrange(BPSysAve)
```

If we want it in descending order we can use the `desc` function like this:

```{r}
NHANES %>% arrange(desc(BPSysAve))
```

In this example, we will compare systolic blood pressure across values of the `Race1` variable for males between the ages of 40-49.

`@instructions`
- Compute the average and standard deviation for each value of `Race1` for males in the age decade 40-49. Remember that this age group is coded with ` 40-49`, which includes a space.
- Order the resulting table from lowest to highest average systolic blood pressure.
- Use the functions `filter`, `group_by`, `summarize`, `arrange`, and the pipe `%>%` to do this in one line of code.
- Within `summarize`, save the average and standard deviation of systolic blood pressure as `average` and `standard_deviation`.

`@hint`
- This is very similar to previous exercises, just with different filters and groupings.
- You will need to give a name to your mean in `summarize` or you will not be able to use the `arrange` function to order your data.

`@pre_exercise_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@sample_code`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
```

`@solution`
```{r}
library(dplyr)
library(NHANES)
data(NHANES)
NHANES %>%
      filter(Gender == "male" & AgeDecade==" 40-49") %>%
      group_by(Race1) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE)) %>%
      arrange(average)
```

`@sct`
```{r}
test_function("filter", incorrect_msg = "Don't forget to `filter` by `Gender` and `AgeDecade`")
test_function("group_by", incorrect_msg = "Don't forget to `group_by` by `Race``")
test_function("summarize",incorrect_msg = "Are you creating a variable named `average` and `standard_deviation`?")
ex() %>% {
   check_function(., "mean") %>% check_arg(., "na.rm") %>% check_equal()
   check_function(., "sd") %>% check_arg(., "na.rm") %>% check_equal()
}
test_function("arrange",incorrect_msg = "`arrange` the variables by the `average`")
test_output_contains("NHANES %>%
      filter(Gender == 'male' & AgeDecade==' 40-49') %>%
      group_by(Race1) %>%
      summarize(average = mean(BPSysAve, na.rm = TRUE), 
                standard_deviation = sd(BPSysAve, na.rm=TRUE)) %>%
      arrange(average)",incorrect_msg="Make sure arrange is called on average rather than standard deviation and you have the correct specified age/gender combo!")
success_msg("Great job!")
```

---

## End of Assessment: Summarizing with dplyr

```yaml
type: PureMultipleChoiceExercise
key: 35d4331f57
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
