---
title: Data Types
description: In this course we introduce you to the basics of various data types.
free_preview: true
---

## Exercise 1. Variable names

```yaml
type: NormalExercise
key: e70afa5dad
lang: r
xp: 100
skills:
  - 1
```

The type of data we are working with will often influence the data visualization technique we use. 
We will be working with two types of variables: categorical and numeric. Each can be divided into two other groups: categorical can be ordinal or not, whereas numerical variables can be discrete or continuous.

We will review data types using some of the examples provided in the `dslabs` package. For example, the `heights` dataset.

```{r}
library(dslabs)
data(heights)
```

`@instructions`
Let's start by reviewing how to extract the variable names from a dataset using the `names` function.
What are the two variable names used in the `heights` dataset?

`@hint`
Use the `names` function. We did this in the first course for the `murders` dataset:
```{r}
library(murders)
names(murders)
```

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
```

`@solution`
```{r}
library(dslabs)
data(heights)
names(heights)
```

`@sct`
```{r}
test_error()
test_output_contains("names(heights)", incorrect_msg = "Are you calling the function on the correct dataset?")
test_function("names", incorrect_msg = "You should be using a specific function to grab the names of the heights dataset")
success_msg("Nice work!")
```

---

## Exercise 2. Variable type

```yaml
type: MultipleChoiceExercise
key: e6b1d336ad
lang: r
xp: 50
skills:
  - 1
```

We saw that `sex` is the first variable. We know what values are represented by this variable and can confirm this by looking at the first few entires:
```{r}
library(dslabs)
data(heights)
head(heights)
```
What data type is the `sex` variable?

`@possible_answers`
- Continuous
- Categorical
- Ordinal
- None of the above

`@hint`


`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
head(heights)
```

`@sct`
```{r}
msg1 = "Incorrect. Looking at the correct variable?"
msg2 = "Correct! Good Job"
msg3 = "Incorrect. Try again!"
msg4 = "Incorrect. It is one of the above?"
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 3. Numerical values

```yaml
type: NormalExercise
key: 7ea8b2ef03
lang: r
xp: 100
skills:
  - 1
```

Keep in mind that discrete numeric data can be considered ordinal. Although this is technically true, we usually reserve the term ordinal data for variables belonging to a small number of different groups, with each group having many members. 

The `height` variable could be ordinal if, for example, we report a small number of values such as short, medium, and tall. Let's explore how many unique values are used by the heights variable. For this we can use the unique function:

```{r}
x <- c(3, 3, 3, 3, 4, 4, 2)
unique(x)
```

`@instructions`
Use the `unique` and `length` functions to determine how many unique heights were reported.

`@hint`
Here is an example:
```{r}
x <- c(3, 3, 3, 3, 4, 4, 2)
length(unique(x))
```

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height
```

`@solution`
```{r}
library(dslabs)
data(heights)
x <- heights$height
length(unique(x))
```

`@sct`
```{r}
test_error()
test_output_contains("139", incorrect_msg = "Are you calling the function on the correct dataset?")
test_function("unique", incorrect_msg = "You should be using unique for this exercise")
test_function("length", incorrect_msg = "You should be using length for this exercise")
success_msg("Nice work!")
```

---

## Exercise 4. Tables

```yaml
type: NormalExercise
key: 2047247be5
lang: r
xp: 100
skills:
  - 1
```

One of the useful outputs of data visualization is that we can learn about the distribution of variables. For categorical data we can construct this distribution by simply computing the frequency of each unique value. This can be done with the function `table`. Here is an example:

```{r}
x <- c(3, 3, 3, 3, 4, 4, 2)
table(x)
```

`@instructions`
Use the `table` function to compute the frequencies of each unique height value. Because we are using the resulting frequency table in a later exercise we want you to save the results into an object and call it `tab`.

`@hint`
Here is an example
```{r}
x <- c(3, 3, 3, 3, 4, 4, 2)
tab <- table(x)
```

In this exercise we will treat the height values as categorical, more specifically as ordinal, and compute these fequencies.

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
x <- heights$height

```

`@solution`
```{r}
library(dslabs)
data(heights)
x <- heights$height
tab <- table(x)
```

`@sct`
```{r}
test_error()
test_object("tab", incorrect_msg = "Are you calling the `table` function on the correct dataset?")
test_function("table", incorrect_msg = "You should be using table for this exercise")
success_msg("Nice work!")
```

---

## Exercise 5. Indicator variables

```yaml
type: NormalExercise
key: 89f473fdd1
lang: r
xp: 100
skills:
  - 1
```

To see why treating the reported heights as an ordinal value is not useful in practice we note how many values are reported only once.

`@instructions`
In the previous exercise we computed the variable `tab` which reports the number of times each unique value appears. For values reported only once `tab` will be 1. Use logicals and the function `sum` to count the number of times this happens.

`@hint`
Here is an example
```{r}
x <- c(3, 3, 3, 3, 4, 4, 2)
tab <- table(x)
sum(tab==1)
```


Use the function `sum` to count the number of times entries in `tab` are equal to 1.

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
tab <- table(heights$height)
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
tab <- table(heights$height)
```

`@solution`
```{r}
library(dslabs)
data(heights)
tab <- table(heights$height)
sum(tab==1)
```

`@sct`
```{r}
test_error()
test_output_contains("sum(tab==1)", incorrect_msg = "Are you calling the `sum` function on the table you created?")
test_function("sum", incorrect_msg = "You should be using `sum` function for this exercise")
success_msg("Nice work!")
```

---

## Exercise 6. Data types - heights

```yaml
type: MultipleChoiceExercise
key: ce3b6a5f17
lang: r
xp: 50
skills:
  - 1
```

Since there are a finite number of reported heights and technically the height can be considered ordinal, which of the following is true:

`@possible_answers`
- It is more effective to consider heights to be numerical given the number of unique values we observe and the fact that if we keep collecting data even more will be observed.
- It is actually preferable to consider heights ordinal since on a computer there are only a finite number of possibilities.
- This is actually a categorical variable: tall, medium or short.
- This is a numerical variable because numbers are used to represent it.

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Correct!  Good Job!"
msg2 = "Incorrect. Try again"
msg3 = "Incorrect. Try again"
msg4 = "Incorrect. Try again"
test_mc(1, c(msg1, msg2, msg3, msg4))
```

---

## End of Assessment: Data Types

```yaml
type: PureMultipleChoiceExercise
key: e3235fbaae
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
- "Great! Now navigate back to the course on edX!"
- "Now navigate back to the course on edX!"
