---
title: Distributions
description: An overview of distributions and their characteristics
---

## Exercise 1. Distributions - 1

```yaml
type: MultipleChoiceExercise
key: 54f59fc608
lang: r
xp: 50
skills:
  - 1
```

You may have noticed that numerical data is often summarized with the average value. For example, the quality of a high school is sometimes summarized with one number: the average score on a standardized test. Occasionally, a second number is reported: the standard deviation. So, for example, you might read a report stating that scores were 680 plus or minus 50 (the standard deviation). The report has summarized an entire vector of scores with with just two numbers. Is this appropriate? Is there any important piece of information that we are missing by only looking at this summary rather than the entire list? We are going to learn when these 2 numbers are enough and when we need more elaborate summaries and plots to describe the data.

Our first data visualization building block is learning to summarize lists of factors or numeric vectors. The most basic statistical summary of a list of objects or numbers is its distribution. Once a vector has been summarized as distribution, there are several data visualization techniques to effectively relay this information. In later assessments we will practice to write code for data visualization. Here we start with some multiple choice questions to test your understanding of distributions and related basic plots.

In the murders dataset, the region is a categorical variable and on the right you can see its distribution. To the closet 5%, what proportion of the states are in the North Central region?

`@possible_answers`
- 75% 
- 50%
- 25%
- 5%

`@hint`


`@pre_exercise_code`
```{r, echo=FALSE}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(murders)
murders %>% group_by(region) %>%
  summarize(n = n()) %>%
  mutate(Proportion = n/sum(n), 
         region = reorder(region, Proportion)) %>%
  ggplot(aes(x=region, y=Proportion, fill=region)) + 
  geom_bar(stat = "identity", show.legend = FALSE) + 
  xlab("")
```

`@sct`
```{r}
msg3 = "Correct!  Good Job!"
msg1 = msg2 = msg4 = msg5 = "Incorrect. Try again"
test_mc(3, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Exercise 2. Distributions - 2

```yaml
type: MultipleChoiceExercise
key: 8fcdca7449
lang: r
xp: 50
skills:
  - 1
```

In the murders dataset, the region is a categorical variable and to the right is its distribution.

Which of the following is true:

`@possible_answers`
- The graph is a histogram.
- The graph shows only four numbers with a bar plot.
- Categories are not numbers so it does not make sense to graph the distribution.
- The colors, not the height of the bars, describe the distribution.

`@hint`


`@pre_exercise_code`
```{r, echo=FALSE}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(murders)
murders %>% group_by(region) %>%
  summarize(n = n()) %>%
  mutate(Proportion = n/sum(n), 
         region = reorder(region, Proportion)) %>%
  ggplot(aes(x=region, y=Proportion, fill=region)) + 
  geom_bar(stat = "identity", show.legend = FALSE) + 
  xlab("")
```

`@sct`
```{r}
msg2 = "Correct!  Good Job!"
msg1 = msg3 = msg4 = "Incorrect. Try again"
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 3. Empirical Cumulative Distribution Function (eCDF)

```yaml
type: MultipleChoiceExercise
key: f2bb41e8b9
lang: r
xp: 50
skills:
  - 1
```

The plot shows the eCDF for male heights:

Based on the plot, what percentage of males are shorter than 75 inches?

`@possible_answers`
- 100%
- 95%
- 80%
- 72 inches

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
heights %>% filter(sex=="Male") %>% ggplot(aes(height)) + 
  stat_ecdf() +
  ylab("F(a)") + xlab("a")
```

`@sct`
```{r}
msg2 = "Correct!  Good Job!"
msg1 = msg3 = msg4 = "Incorrect. Try again"
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 4. eCDF Male Heights

```yaml
type: MultipleChoiceExercise
key: beac9cc921
lang: r
xp: 50
skills:
  - 1
```

The plot shows the eCDF for male heights:

To the closest inch, what height `m` has the property that 1/2 of the male students are taller than `m` and 1/2 are shorter?

`@possible_answers`
- 61 inches
- 64 inches
- 69 inches
- 74 inches

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
heights %>% filter(sex=="Male") %>% ggplot(aes(height)) + 
  stat_ecdf() +
  ylab("F(a)") + xlab("a")
```

`@sct`
```{r}
msg3 = "Correct!  Good Job!"
msg1 = msg2 = msg4 = "Incorrect. Try again"
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 5. eCDF of Murder Rates

```yaml
type: MultipleChoiceExercise
key: 33398b09b8
lang: r
xp: 50
skills:
  - 1
```

Here is an eCDF of the murder rates across states.

Knowing that there are 51 states (counting DC) and based on this plot, how many states have murder rates larger than 10 per 100,000 people?

`@possible_answers`
- 1
- 5
- 10
- 50

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(murders)
murders %>% mutate(murder_rate = total/population * 10^5) %>%
  ggplot(aes(murder_rate)) + 
  stat_ecdf() +
  ylab("F(a)") + xlab("a")
```

`@sct`
```{r}
msg1 = "Correct!  Good Job!"
msg3 = msg2 = msg4 = "Incorrect. Try again"
test_mc(1, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 6. eCDF of Murder Rates - 2

```yaml
type: MultipleChoiceExercise
key: 0a8a8bd476
lang: r
xp: 50
skills:
  - 1
```

Here is an eCDF of the murder rates across states:

Based on the eCDF above, which of the following statements are true:

`@possible_answers`
- About half the states have murder rates above 7 per 100,000 and the other half below.
- Most states have murder rates below 2 per 100,000.
- All the states have murder rates above 2 per 100,000.
- With the exception of 4 states, the murder rates are below 5 per 100,000.

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()
data(murders)
murders %>% mutate(murder_rate = total/population * 10^5) %>%
  ggplot(aes(murder_rate)) + 
  stat_ecdf() +
  ylab("F(a)") + xlab("a")
```

`@sct`
```{r}
msg4 = "Correct!  Good Job!"
msg3 = msg2 = msg1 = "Incorrect. Try again"
test_mc(4, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 7. Histograms

```yaml
type: MultipleChoiceExercise
key: 576854fa94
lang: r
xp: 50
skills:
  - 1
```

Here is a histogram of male heights in our `heights` dataset:

Based on this plot, how many males are between 62.5 and 65.5?

`@possible_answers`
- 11
- 29
- 58
- 99

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
heights %>% 
  filter(sex=="Male") %>% 
  ggplot(aes(height)) + 
  geom_histogram(binwidth = 1, color = "black")
```

`@sct`
```{r}
msg3 = "Correct!  Good Job!"
msg4 = msg2 = msg1 = "Incorrect. Try again"
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 8. Histograms - 2

```yaml
type: MultipleChoiceExercise
key: 0e27748ac7
lang: r
xp: 50
skills:
  - 1
```

Here is a histogram of male heights in our `heights` dataset:

About what **percentage** are shorter than 60 inches?

`@possible_answers`
- 1%
- 10%
- 25%
- 50%

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
heights %>% 
  filter(sex=="Male") %>% 
  ggplot(aes(height)) + 
  geom_histogram(binwidth = 1, color = "black")
```

`@sct`
```{r}
msg1 = "Correct!  Good Job!"
msg4 = msg2 = msg3 = "Incorrect. Try again"
test_mc(1, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 9. Density plots

```yaml
type: MultipleChoiceExercise
key: 0ffb36f695
lang: r
xp: 50
skills:
  - 1
```

Based on this density plot, about what proportion of US states have populations larger than 10 million?

`@possible_answers`
- 0.02
- 0.15
- 0.50
- 0.55

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
murders %>% ggplot(aes(x=population/10^6)) + geom_density(fill = "grey") + scale_x_log10() + xlab("Population in millions")
```

`@sct`
```{r}
msg2 = "Correct!  Good Job!"
msg4 = msg1 = msg3 = "Incorrect. Try again"
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 10. Density plots - 2

```yaml
type: MultipleChoiceExercise
key: adff149195
lang: r
xp: 50
skills:
  - 1
```

Here are three density plots. Is it possible that they are from the same dataset? 
Which of the following statements is true:

`@possible_answers`
- It is impossible that they are from the same dataset.
- They are from the same dataset, but different due to code errors.
- They are the same dataset, but the first and second undersmooth and the third oversmooths.
- They are the same dataset, but the first does  not have the x-axis in the log scale, the second undersmooths and the third oversmooths.

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(gridExtra)
library(dslabs)
data(murders)
p1 <- murders %>% ggplot(aes(x=population/10^6)) + geom_density(fill = "grey", bw = 5) + xlab("Population in millions") + ggtitle("1")
p2 <- murders %>% ggplot(aes(x=population/10^6)) + geom_density(fill = "grey", bw = .05) + scale_x_log10() + xlab("Population in millions") + ggtitle("2")
p3 <- murders %>% ggplot(aes(x=population/10^6)) + geom_density(fill = "grey", bw = 1) + scale_x_log10() + xlab("Population in millions") + ggtitle("3")
grid.arrange(p1,p2,p3,ncol=2)
```

`@sct`
```{r}
msg4 = "Correct!  Good Job!"
msg2 = msg1 = msg3 = "Incorrect. Try again"
test_mc(4, c(msg1, msg2, msg3, msg4))
```

---

## End of Assessment: Distributions

```yaml
type: PureMultipleChoiceExercise
key: 79ce49ce08
lang: r
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
