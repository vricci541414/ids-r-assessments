---
title: Data Visualization Principles - Part 1
description: >-
  Show the Data, Ease Comparisons - Use Common Axes, Consider Transformations,
  Ease Comparisons - Compared Visual Cues Should Be Adjacent
---

## Exercise 1: Customizing plots - Pie charts

```yaml
type: MultipleChoiceExercise
key: 2fdba0e6ab
lang: r
xp: 50
skills:
  - 1
```

Pie charts are appropriate:

`@possible_answers`
- When we want to display percentages. 
- When ggplot2 is not available. 
- When I am in a bakery. 
- Never. Barplots and tables are always better.

`@hint`


`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Incorrect. Try again!"
msg2 = "Incorrect. Try again!"
msg3 = "Incorrect. Try again!"
msg4 = "Correct! Good job. Pie charts are not a very effective visualization tool. "
test_mc(4, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 2. Customizing plots - What's wrong?

```yaml
type: MultipleChoiceExercise
key: ca5e3e9a17
lang: r
xp: 50
skills:
  - 1
```

What is the problem with this plot?

`@possible_answers`
- The values are wrong. The final vote was 306 to 232.
- The axis does not start at 0. Judging by the length, it appears Trump received 3 times as many votes when in fact it was about 30% more. 
- The colors should be the same.
- Percentages should be shown as a pie chart.

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
ds_theme_set()

data.frame(candidate=c("Clinton","Trump"), electoral_votes = c(232, 306)) %>% 
  ggplot(aes(candidate, electoral_votes)) + 
  geom_bar(stat = "identity", width=0.5, color =1, fill = c("Blue","Red")) + 
  coord_cartesian(ylim=c(200,310)) + ylab("Electoral Votes") + xlab("") + 
  ggtitle("Result of Presidential Election 2016")
```

`@sct`
```{r}
msg2 = "Correct!  Good Job!"
msg1 = msg3 = msg4 = msg5 = "Incorrect. Try again."
test_mc(2, c(msg1, msg2, msg3, msg4,msg5))
```

---

## Exercise 3: Customizing plots - What's wrong 2?

```yaml
type: MultipleChoiceExercise
key: b3f6829f09
lang: r
xp: 50
skills:
  - 1
```

Take a look at the following two plots. They show the same information: rates of measles by state in the United States for 1928.

`@possible_answers`
- Both plots provide the same information, so they are equally good.
- The plot on the left is better because it orders the states alphabetically.
- The plot on the right is better because it orders the states by disease rate so we can quickly see the states with highest and lowest rates.
- Both plots should be pie charts instead.

`@hint`


`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(gridExtra)
data(us_contagious_diseases)
p1 <- us_contagious_diseases %>% 
  filter(year == 1928 & disease=="Measles" & count>0 & !is.na(population)) %>% 
  mutate(rate = count / population * 10000 * 52 / weeks_reporting) %>%
  ggplot(aes(state, rate)) +
  geom_bar(stat="identity") +
  coord_flip() +
  xlab("")
p2 <- us_contagious_diseases %>% 
  filter(year == 1928 & disease=="Measles" & count>0 & !is.na(population)) %>% 
  mutate(rate = count / population * 10000*52 / weeks_reporting) %>%
  mutate(state = reorder(state, rate)) %>%
  ggplot(aes(state, rate)) +
  geom_bar(stat="identity") +
  coord_flip() +
  xlab("")
grid.arrange(p1, p2, ncol = 2)
```

`@sct`
```{r}
msg3 = "Correct!  Good Job!"
msg1 = msg2 = msg4 = msg5 = "Incorrect. Try again"
test_mc(3, c(msg1, msg2, msg3, msg4,msg5))
```

---

## End of Assessment: Data Visualization Principles, Part 1

```yaml
type: PureMultipleChoiceExercise
key: 38d67dff84
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
