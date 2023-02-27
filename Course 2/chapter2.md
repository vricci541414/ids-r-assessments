---
title: 'Quantiles, Percentiles, and Boxplots'
description: 'Quantile-Quantile Plots, Percentiles, Boxplots, Distribution of Female Heights'
---

## Exercise 1. Vector lengths

```yaml
type: NormalExercise
key: 56141be397
lang: r
xp: 100
skills:
  - 1
```

When analyzing data it's often important to know the number of measurements you have for each category.

`@instructions`
- Define a variable `male` that contains the male heights.
- Define a variable `female` that contains the female heights.
- Report the length of each variable.

`@hint`
Use the `length` function after defining two vectors called `male` and `female` of subsetted heights. You will call length twice, once for each variable.

`@pre_exercise_code`
```{r}
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
library(dslabs)
data(heights)
male <- heights$height[heights$sex=="Male"]
female <- heights$height[heights$sex=="Female"]
```

`@solution`
```{r}
library(dslabs)
data(heights)
male <- heights$height[heights$sex=="Male"]
female <- heights$height[heights$sex=="Female"]

length(male)
length(female)
```

`@sct`
```{r}
test_error()
#test_output("female", incorrect_msg = "Are you subsetting correctly?")
#test_output("male", incorrect_msg = "Are you subsetting correctly?")
test_function("length",index=1, incorrect_msg = "You should be using length twice for this exercise")
test_function("length",index=2, incorrect_msg = "You should be using length twice for this exercise")
success_msg("Nice work!")
```

---

## Exercise 2. Percentiles

```yaml
type: NormalExercise
key: b66abf907d
lang: r
xp: 100
skills:
  - 1
```

Suppose we can't make a plot and want to compare the distributions side by side. If the number of data points is large, listing all the numbers is inpractical. A more practical approach is to look at the percentiles. We can obtain percentiles using the `quantile` function like this

```{r}
library(dslabs)
data(heights)
quantile(heights$height, seq(.01, 0.99, 0.01))
```

`@instructions`
- Create two five row vectors showing the 10th, 30th, 50th, 70th, and 90th percentiles for the heights of each sex called these vectors `female_percentiles` and `male_percentiles`.
- Then create a data frame called `df` with these two vectors as columns. The column names should be `female` and `male` and should appear in that order. As an example consider that if you want a data frame to have column names `names` and `grades`, in that order, you do it like this:

```{r}
df <- data.frame(names = c("Jose", "Mary"), grades = c("B", "A"))
```
- Take a look at the `df` by printing it. This will provide some information on how male and female heights differ.

`@hint`
You'll need to apply `quantile` to the `male` and `female` heights and specify the percentiles.
Afterwards, you need to call `data.frame`. Make sure you have the columns in the specified order! Here is an example with sequences of numbers:

```{r}
male <- 50:80
female <- 45:85
female_percentiles <- quantile(female, seq(0.1, 0.9, 0.2))
male_percentiles <- quantile(male, seq(0.1, 0.9, 0.2))
df <- data.frame(female = female_percentiles, male = male_percentiles)
df
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
male <- heights$height[heights$sex=="Male"]
female <- heights$height[heights$sex=="Female"]
```

`@solution`
```{r}
library(dslabs)
data(heights)
male <- heights$height[heights$sex=="Male"]
female <- heights$height[heights$sex=="Female"]

female_percentiles <- quantile(female, seq(0.1, 0.9, 0.2))
male_percentiles <- quantile(male, seq(0.1, 0.9, 0.2))

df <- data.frame(female = female_percentiles, male = male_percentiles)
df
```

`@sct`
```{r}
test_error()
test_object("female_percentiles", incorrect_msg = "Make sure to use the `quantile` function.")
test_object("male_percentiles", incorrect_msg = "Make sure to use the `quantile` function.")
test_object("df",incorrect_msg = "You should be using `data.frame` to define `df` for this exercise. Make sure the columns are in the order `female`, `male`.")
success_msg("Nice work!")
```

---

## Exercise 3. Interpreting Boxplots - 1

```yaml
type: MultipleChoiceExercise
key: ca5e3e9a17
lang: r
xp: 50
skills:
  - 1
```

Study the boxplots summarizing the distributions of populations sizes by country.

Which continent has the country with the largest population size?

`@possible_answers`
- Africa
- Americas
- Asia
- Europe
- Oceania

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(gapminder)
gapminder %>% 
    filter(year == 2010) %>% 
    group_by(continent) %>% 
    ggplot(aes(x=continent, y=population/10^6)) + 
    geom_boxplot() + 
    scale_y_continuous(trans = "log10", breaks = c(1,10,100,1000)) + 
    ylab("Population in millions")

```

`@sct`
```{r}
msg3 = "Correct!  Good Job!"
msg1 = msg2 = msg4 = msg5 = "Incorrect. Try again"
test_mc(3, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Exercise 4. Interpreting Boxplots - 2

```yaml
type: MultipleChoiceExercise
key: abdc87afbd
lang: r
xp: 50
skills:
  - 1
```

Study the boxplots summarizing the distributions of populations sizes by country.

Which continent has the largest median population?

`@possible_answers`
- Africa
- Americas
- Asia
- Europe
- Oceania

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(gapminder)
gapminder %>% 
    filter(year == 2010) %>% 
    group_by(continent) %>% 
    ggplot(aes(x=continent, y=population/10^6)) + 
    geom_boxplot() + 
    scale_y_continuous(trans = "log10", breaks = c(1,10,100,1000)) + 
    ylab("Population in millions")
```

`@sct`
```{r}
msg1 = "Correct!  Good Job!"
msg2 = msg3 = msg4 = msg5 = "Incorrect. Look very closely at where the medians are."
test_mc(1, c(msg1, msg2, msg3, msg4, msg5))
```

---

## Exercise 5. Interpreting Boxplots - 3

```yaml
type: MultipleChoiceExercise
key: 2481169bf1
lang: r
xp: 50
skills:
  - 1
```

Again, look at the boxplots summarizing the distributions of populations sizes by country. To the nearest million, what is the `median` population size for Africa?

`@possible_answers`
- 100 million
- 25 million
- 10 million
- 5 million
- 1 million

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(gapminder)
gapminder %>% 
    filter(year == 2010) %>% 
    group_by(continent) %>% 
    ggplot(aes(x=continent, y=population/10^6)) + 
    geom_boxplot() + 
    scale_y_continuous(trans = "log10", breaks = c(1,10,100,1000)) + 
    ylab("Population in millions")
```

`@sct`
```{r}
msg3 = "Correct!  Good Job!"
msg1 = msg2 = msg4 = msg5 = "Incorrect. Look very closely at where the medians are."
test_mc(3, c(msg1, msg2, msg3, msg4, msg5))
```

---

## Exercise 6. Low quantiles

```yaml
type: MultipleChoiceExercise
key: 66e045675a
lang: r
xp: 50
skills:
  - 1
```

Examine the following boxplots and report approximately what proportion of countries in Europe have populations below 14 million:

`@possible_answers`
- 0.75
- 0.50
- 0.25
- 0.01

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(gapminder)
gapminder %>% 
    filter(year == 2010) %>% 
    group_by(continent) %>% 
    ggplot(aes(x=continent, y=population/10^6)) + 
    geom_boxplot() + 
    scale_y_continuous(trans = "log10", breaks = c(1,10,100,1000)) + 
    ylab("Population in millions")
```

`@sct`
```{r}
msg2 = "Correct!  Good Job!"
msg1 = msg3 = msg4 = msg5 = "Incorrect. Try again."
test_mc(1, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Exercise 7. Interquantile Range (IQR)

```yaml
type: MultipleChoiceExercise
key: c1b21fa2ad
lang: r
xp: 50
skills:
  - 1
```

Using the boxplot as guidance, which continent shown below has the largest interquartile range for log(population)?

`@possible_answers`
- Africa
- Americas
- Asia
- Europe
- Oceania

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(gapminder)
gapminder %>% 
    filter(year == 2010) %>% 
    group_by(continent) %>% 
    ggplot(aes(x=continent, y=population/10^6)) + 
    geom_boxplot() + 
    scale_y_continuous(trans = "log10", breaks = c(1,10,100,1000)) + 
    ylab("Population in millions")
```

`@sct`
```{r}
msg2 = "Correct!  Good Job!"
msg1 = msg3 = msg4 = msg5 = "Incorrect. Try again"
test_mc(2, c(msg1, msg2, msg3, msg4,msg5))
```

---

## End of Assessment: Quantiles, Percentiles, and Boxplots

```yaml
type: PureMultipleChoiceExercise
key: b90a40700b
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
