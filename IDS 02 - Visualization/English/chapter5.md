---
title: Robust Summaries with Outliers
description: 'dplyr, The Dot Placeholder, Group By, Sorting Data Tables'
---

## Exercise 1. Exploring the Galton Dataset - Average and Median

```yaml
type: NormalExercise
key: 00ffbfee10
lang: r
xp: 100
skills:
  - 1
```

For this chapter, we will use height data collected by Francis Galton for his genetics studies. Here we just use height of the children in the dataset:

```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@instructions`
Compute the average and median of these data. Note: do not assign them to a variable.

`@hint`
You can use the `mean` and `median` functions.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@solution`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
mean(x)
median(x)
```

`@sct`
```{r}
test_error()
test_object("x", incorrect_msg = "Did you define `x` appropriately?")
test_function("mean", incorrect_msg = "Are you calculating `mean` on the correct subset?")
test_function("median", incorrect_msg = "Are you calculating `median` on the correct subset?")
success_msg("Nice job! Notice that they are similar.")
```

---

## Exercise 2. Exploring the Galton Dataset - SD and MAD

```yaml
type: NormalExercise
key: a9b75b2e62
lang: r
xp: 100
skills:
  - 1
```

Now for the same data compute the standard deviation and the median absolute deviation (MAD).

`@instructions`
Compute the standard deviation and the median absolute deviation of these data.

`@hint`
Use the `sd` and `mad` functions.

`@pre_exercise_code`
```{r}


```

`@sample_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@solution`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
sd(x)
mad(x)
```

`@sct`
```{r}
test_error()
test_object("x", incorrect_msg = "Did you define `x` appropriately?")
test_function("sd", incorrect_msg = "Are you calculating `sd` on the correct subset?")
test_function("mad", incorrect_msg = "Are you calculating `mad` on the correct subset?")
success_msg("Nice job! Again notice that they are somewhat similar.")
```

---

## Exercise 3. Error impact on average

```yaml
type: NormalExercise
key: c2e9eda61d
lang: r
xp: 100
skills:
  - 1
```

In the previous exercises we saw that the mean and median are very similar and so are the standard deviation and MAD. This is expected since the data is approximated by a normal distribution which has this property. 

Now suppose that Galton made a mistake when entering the first value, forgetting to use the decimal point. You can imitate this error by typing:

```{r}
library(HistData)
data(Galton)
x <- Galton$child
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
```

The data now has an outlier that the normal approximation does not account for. Let's see how this affects the average.

`@instructions`
Report how many inches the average grows after this mistake. Specifically, report the difference between the average of the data with the mistake `x_with_error` and the data without the mistake `x`.

`@hint`
Subtract the means from each other.

`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
```

`@solution`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
mean(x_with_error)- mean(x)
```

`@sct`
```{r}
test_error()
test_object("x", incorrect_msg = "Did you define `x` appropriately?")
test_object("x_with_error", incorrect_msg = "Did you define `x_with_error` appropriately?")
test_function("mean", incorrect_msg = "Are you calculating `mean` on the correct subset?")
test_function("mean",index=2, incorrect_msg = "Are you calculating `mean` on the correct subset?")
test_output_contains("mean(x_with_error)-mean(x)", incorrect_msg = "Are you calculating the difference between the two variables in the order given?")
success_msg("Nice job! Notice the shift in mean.")
```

---

## Exercise 4. Error impact on SD

```yaml
type: NormalExercise
key: bae5b2a5ed
lang: r
xp: 100
skills:
  - 1
```

In the previous exercise we saw how a simple mistake in 1 out of over 900 observations can result in the average of our data increasing more than half an inch, which is a large difference in practical terms. Now let's explore the effect this outlier has on the standard deviation.

`@instructions`
Report how many inches the SD grows after this mistake. Specifically, report the difference between the SD of the data with the mistake `x_with_error` and the data without the mistake `x`.

`@hint`
Subtract the standard deviations from each other.

`@pre_exercise_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@sample_code`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
```

`@solution`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
sd(x_with_error)- sd(x)
```

`@sct`
```{r}
ex() %>% check_predefined_objects("x", incorrect_msg = "Did you define `x` appropriately?")
ex() %>% check_object("x_with_error") %>% check_equal(incorrect_msg = "Did you define `x_with_error` appropriately?")
ex() %>% check_function("sd") %>% check_arg("x") %>% check_equal(incorrect_msg = "Are you calculating `sd` on the correct subset?")
ex() %>% check_function("sd",index=2) %>% check_arg("x") %>% check_equal(incorrect_msg = "Are you calculating `sd` on the correct subset?")
ex() %>% check_output_expr("sd(x_with_error)-sd(x)", missing_msg = "Are you calculating the difference between the two variables in the order given?")
success_msg("Nice job! Notice the increase in the standard deviation.")
```

---

## Exercise 5. Error impact on median

```yaml
type: NormalExercise
key: 3e0ef1c1aa
lang: r
xp: 100
skills:
  - 1
```

In the previous exercises we saw how one mistake can have a substantial effect on the average and the standard deviation. 

Now we are going to see how the median and MAD are much more resistant to outliers. For this reason we say that they are _robust_ summaries.

`@instructions`
Report how many inches the median grows after the mistake. Specifically, report the difference between the median of the data with the mistake `x_with_error` and the data without the mistake `x`.

`@hint`
Subtract the medians from each other.

`@pre_exercise_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@sample_code`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
```

`@solution`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
median(x_with_error)- median(x)
```

`@sct`
```{r}
test_error()
test_object("x", incorrect_msg = "Did you define `x` appropriately?")
test_object("x_with_error", incorrect_msg = "Did you define `x_with_error` appropriately?")
test_function("median", incorrect_msg = "Are you calculating `median` on the correct subset?")
test_function("median",index=2, incorrect_msg = "Are you calculating `median` on the correct subset?")
test_output_contains("median(x_with_error)-median(x)", incorrect_msg = "Are you calculating the difference in the two variables in the order given?")
success_msg("Nice job! Notice the robustness of the median.")
```

---

## Exercise 6. Error impact on MAD

```yaml
type: NormalExercise
key: 7d449b012e
lang: r
xp: 100
skills:
  - 1
```

We saw that the median barely changes. Now let's see how the MAD is affected.

`@instructions`
Report how many inches the MAD grows after the mistake. Specifically, report the difference between the MAD of the data with the mistake `x_with_error` and the data without the mistake `x`.

`@hint`
Subtract the MADs from each other.

`@pre_exercise_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@sample_code`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
```

`@solution`
```{r}
x_with_error <- x
x_with_error[1] <- x_with_error[1]*10
mad(x_with_error)- mad(x)
```

`@sct`
```{r}
test_error()
test_object("x", incorrect_msg = "Did you define `x` appropriately?")
test_object("x_with_error", incorrect_msg = "Did you define `x_with_error` appropriately?")
test_function("mad", incorrect_msg = "Are you calculating `mad` on the correct subset?")
test_function("mad",index=2, incorrect_msg = "Are you calculating `mad` on the correct subset?")
test_output_contains("mad(x_with_error)-mad(x)", incorrect_msg = "Are you calculating the difference in the two variables in the order given?")
success_msg("Nice job! Notice the MAD doesn't change.")
```

---

## Exercise 7. Usefulness of EDA

```yaml
type: MultipleChoiceExercise
key: 754e716c31
lang: r
xp: 50
skills:
  - 1
```

How could you use exploratory data analysis to detect that an error was made?

`@possible_answers`
- Since it is only one value out of many, we will not be able to detect this.
- We would see an obvious shift in the distribution.
- A boxplot, histogram, or qq-plot would reveal a clear outlier.
- A scatter plot would show high levels of measurement error.

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg3 = "Correct! Good Job!"
msg1 = msg2 = msg4 = msg5 = "Incorrect. Try again."
test_mc(3, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Exercise 8. Using EDA to explore changes

```yaml
type: NormalExercise
key: 468a1a1b56
lang: r
xp: 100
skills:
  - 1
```

We have seen how the average can be affected by outliers. But how large can this effect get? This of course depends on the size of the outlier and the size of the dataset.

To see how outliers can affect the average of a dataset, let's write a simple function that takes the size of the outlier as input and returns the average.

`@instructions`
Write a function called `error_avg` that takes a value `k` and returns the average of the vector `x` after the first entry changed to `k`. Show the results for `k=10000` and `k=-10000`.

`@hint`
Your function should replace the first value in the `x` vector with the only argument, `k`, and then calculate the `mean`. And remember to call the function on `k=10000` and `k=-10000`!

`@pre_exercise_code`
```{r}
library(HistData)
data(Galton)
x <- Galton$child
```

`@sample_code`
```{r}
x <- Galton$child
error_avg <- function(k){


}

```

`@solution`
```{r}
x <- Galton$child

error_avg <- function(k){
  x[1] <- k
  mean(x)
}

error_avg(10000)
error_avg(-10000)
```

`@sct`
```{r}
test_error()
msg = "Double check how you're defining the `error_avg()` function."
fun_def <- ex() %>% check_fun_def("error_avg")
fun_def %>% check_arguments()
fun_def %>% check_call(10000) %>% check_result(msg)
fun_def %>% check_body() %>% check_operator('mean')
test_function_result("error_avg",index=1, incorrect_msg = "Are you calculating `error_avg` with `k=10000`?")
test_function_result("error_avg",index=2, incorrect_msg = "Are you calculating `error_avg` with `k=-10000`?")
test_error()
success_msg("Nice job! Notice how changing a single value to a large outlying value can have a large effect on the mean.")
```

---

## End of Assessment: Robust Summaries with Outliers

```yaml
type: PureMultipleChoiceExercise
key: 3dcf2d5987
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
