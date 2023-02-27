---
title: Data Visualization Principles - Part 2
description: Part 2 of data visualization principles exercises
---

## Exercise 1: Customizing plots - watch and learn

```yaml
type: NormalExercise
key: d7655f4b4a
lang: r
xp: 100
skills:
  - 1
```

To make the plot on the right in the exercise from the last set of assessments, we had to reorder the levels of the states' variables.

`@instructions`
- Redefine the `state` object so that the levels are re-ordered by rate.
- Print the new object `state` and its levels (using `levels`) so you can see that the vector is now re-ordered by the levels.

`@hint`
- You can use `reorder` to re-order the levels of the state object.
- Remember that you are re-ordering by `rate`.
- Inspect the levels of an object with `levels`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
dat <- us_contagious_diseases %>%
filter(year == 1967 & disease=="Measles" & !is.na(population)) %>% mutate(rate = count / population * 10000 * 52 / weeks_reporting)
state <- dat$state 
rate <- dat$count/(dat$population/10000)*(52/dat$weeks_reporting)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
dat <- us_contagious_diseases %>%
filter(year == 1967 & disease=="Measles" & !is.na(population)) %>% mutate(rate = count / population * 10000 * 52 / weeks_reporting)
state <- dat$state 
rate <- dat$count/(dat$population/10000)*(52/dat$weeks_reporting)
```

`@solution`
```{r}
state <- reorder(state, rate)
print(state)
levels(state)
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(.,"reorder") %>% check_arg("x") %>% check_equal()
  check_function(.,"levels") %>% check_result() %>% check_equal()
}
test_object("state", incorrect_msg = "Did you reorder `state` properly and then print it?")

success_msg("Good job!")
```

---

## Exercise 2: Customizing plots - redefining

```yaml
type: NormalExercise
key: c63feefa1a
lang: r
xp: 100
skills:
  - 1
```

Now we are going to customize this plot a little more by creating a rate variable and reordering by that variable instead.

`@instructions`
- Add a single line of code to the definition of the `dat` table that uses `mutate` to reorder the states by the rate variable.
- The sample code provided will then create a bar plot using the newly defined `dat`.

`@hint`
- The code you need to add is very similar to that used in the previous exercise - you can use `reorder` again.
- Make sure you add the code to the code defining `dat`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(us_contagious_diseases)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(us_contagious_diseases)
dat <- us_contagious_diseases %>% filter(year == 1967 & disease=="Measles" & count>0 & !is.na(population)) %>%
  mutate(rate = count / population * 10000 * 52 / weeks_reporting)
dat %>% ggplot(aes(state, rate)) +
  geom_bar(stat="identity") +
  coord_flip()
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
dat <- us_contagious_diseases %>% filter(year == 1967 & disease=="Measles" & count>0 & !is.na(population)) %>%
 mutate(rate = count / population * 10000 * 52 / weeks_reporting) %>%
 mutate(state = reorder(state, rate))
dat %>% ggplot(aes(state, rate)) +
 geom_bar(stat="identity") +
 coord_flip()
```

`@sct`
```{r}
test_error()
ex() %>% {
check_function(.,"reorder", not_called_msg="Don't forget to reorder the data by rate") 
check_object(.,"dat") %>% check_equal()
}
success_msg("Good job!")
```

---

## Exercise 3: Showing the data and customizing plots

```yaml
type: MultipleChoiceExercise
key: 688855b651
lang: r
xp: 50
skills:
  - 1
```

Say we are interested in comparing gun homicide rates across regions of the US. We see this plot:

```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data("murders")
murders %>% mutate(rate = total/population*100000) %>%
  group_by(region) %>%
  summarize(avg = mean(rate)) %>%
  mutate(region = factor(region)) %>%
  ggplot(aes(region, avg)) +
  geom_bar(stat="identity") +
  ylab("Murder Rate Average")
```
and decide to move to a state in the western region. What is the main problem with this interpretaion?

`@possible_answers`
- The categories are ordered alphabetically.
- The graph does not show standard errors.
- It does not show all the data. We do not see the variability within a region and it's possible that the safest states are not in the West.
- The Northeast has the lowest average.

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data("murders")
murders %>% mutate(rate = total/population*100000) %>%
  group_by(region) %>%
  summarize(avg = mean(rate)) %>%
  mutate(region = factor(region)) %>%
  ggplot(aes(region, avg)) +
  geom_bar(stat="identity") +
  ylab("Murder Rate Average")
```

`@sct`
```{r}
msg3 = "Correct!  Good Job!"
msg1 = msg2 = msg4 = "Incorrect. Try again"
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 4: Making a box plot

```yaml
type: NormalExercise
key: fd7566b82b
lang: r
xp: 100
skills:
  - 1
```

To further investigate whether moving to the western region is a wise decision, let's make a box plot of murder rates by region, showing all points.

`@instructions`
- Order the regions by their median murder rate by using `mutate` and `reorder`.
- Make a box plot of the murder rates by region.
- Show all of the points on the box plot.

`@hint`
- To order the regions by rate, you can use `mutate` and `reorder` to sort the `region` column by `rate`.
- Use `geom_boxplot()` to make a boxplot.
- Use `geom_point()` to show the points.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data("murders")
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data("murders")
murders %>% mutate(rate = total/population*100000)
```

`@solution`
```{r}
murders %>% mutate(rate = total/population*100000) %>%
  mutate(region=reorder(region, rate, FUN=median)) %>%
  ggplot(aes(region, rate)) +
  geom_boxplot() +
  geom_point()
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(., "reorder", not_called_msg="Did you remember to reorder the regions by murder rate?") 
  check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
  check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
  }
  check_function(., "geom_boxplot", not_called_msg="Did you add the `geom_boxplot()` layer?")
  check_function(., "geom_point", not_called_msg="Did you add the `geom_point()` layer?")
}
success_msg("Good job!")
```

---

## End of Assessment: Data Visualization Principles, Part 2

```yaml
type: PureMultipleChoiceExercise
key: 9e62a4982b
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
