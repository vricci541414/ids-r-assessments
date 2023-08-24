---
title: Data Visualization Principles - Part 3
description: Part 3 of data visualization principles exercises
---

## Exercise 1: Tile plot - measles and smallpox

```yaml
type: NormalExercise
key: 41c91866ca
lang: r
xp: 100
skills:
  - 1
```

The sample code given creates a tile plot showing the rate of measles cases per population. We are going to modify the tile plot to look at smallpox cases instead.

`@instructions`
- Modify the tile plot to show the rate of smallpox cases instead of measles cases.
- Exclude years in which cases were reported in fewer than 10 weeks from the plot.

`@hint`
- The column that has the number of weeks in which cases were reported is called `weeks_reporting`.
- To exclude years with fewer than 10 weeks of reported cases, modify the `filter` you use.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(RColorBrewer)
library(dslabs)
data(us_contagious_diseases)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(RColorBrewer)
library(dslabs)
data(us_contagious_diseases)

the_disease = "Measles"
dat <- us_contagious_diseases %>% 
   filter(!state%in%c("Hawaii","Alaska") & disease == the_disease) %>% 
   mutate(rate = count / population * 10000) %>% 
   mutate(state = reorder(state, rate))

dat %>% ggplot(aes(year, state, fill = rate)) + 
  geom_tile(color = "grey50") + 
  scale_x_continuous(expand=c(0,0)) + 
  scale_fill_gradientn(colors = brewer.pal(9, "Reds"), trans = "sqrt") + 
  theme_minimal() + 
  theme(panel.grid = element_blank()) + 
  ggtitle(the_disease) + 
  ylab("") + 
  xlab("")
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(RColorBrewer)
library(dslabs)
data(us_contagious_diseases)

the_disease = "Smallpox"
dat <- us_contagious_diseases %>% 
   filter(!state%in%c("Hawaii","Alaska") & disease == the_disease & weeks_reporting>=10) %>% 
   mutate(rate = count / population * 10000) %>% 
   mutate(state = reorder(state, rate))

dat %>% ggplot(aes(year, state, fill = rate)) + 
  geom_tile(color = "grey50") + 
  scale_x_continuous(expand=c(0,0)) + 
  scale_fill_gradientn(colors = brewer.pal(9, "Reds"), trans = "sqrt") + 
  theme_minimal() + 
  theme(panel.grid = element_blank()) + 
  ggtitle(the_disease) + 
  ylab("") + 
  xlab("")
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal(eval = TRUE)
  check_function(., "aes") %>% {
    check_arg(., "x") %>% check_equal(eval = FALSE)
    check_arg(., "y") %>% check_equal(eval = FALSE)
    check_arg(., "fill") %>% check_equal(eval = FALSE)
  }
  check_function(., "geom_tile", not_called_msg="Did you add the `geom_tile()` layer?")
  check_function(., "scale_x_continuous") %>% check_arg(., "expand") %>% check_equal(eval = TRUE)
  check_function(., "scale_fill_gradientn") %>% check_arg(., "trans") %>% check_equal(eval = TRUE)
}
success_msg("Good job!")
```

---

## Exercise 2. Time series plot - measles and smallpox

```yaml
type: NormalExercise
key: e01bd5d3b6
lang: r
xp: 100
skills:
  - 1
```

The sample code given creates a time series plot showing the rate of measles cases per population by state. We are going to again modify this plot to look at smallpox cases instead.

`@instructions`
- Modify the sample code for the time series plot to plot data for smallpox instead of for measles.
- Once again, restrict the plot to years in which cases were reported in at least 10 weeks.

`@hint`
- The column that has the number of weeks in which cases were reported is called `weeks_reporting`.
- To exclude years with fewer than 10 weeks of reported cases, modify the `filter` you use.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)

the_disease = "Measles"
dat <- us_contagious_diseases %>%
   filter(!state%in%c("Hawaii","Alaska") & disease == the_disease) %>%
   mutate(rate = count / population * 10000) %>%
   mutate(state = reorder(state, rate))

avg <- us_contagious_diseases %>%
  filter(disease==the_disease) %>% group_by(year) %>%
  summarize(us_rate = sum(count, na.rm=TRUE)/sum(population, na.rm=TRUE)*10000)

dat %>% ggplot() +
  geom_line(aes(year, rate, group = state),  color = "grey50", 
            show.legend = FALSE, alpha = 0.2, size = 1) +
  geom_line(mapping = aes(year, us_rate),  data = avg, size = 1, color = "black") +
  scale_y_continuous(trans = "sqrt", breaks = c(5,25,125,300)) + 
  ggtitle("Cases per 10,000 by state") + 
  xlab("") + 
  ylab("") +
  geom_text(data = data.frame(x=1955, y=50), mapping = aes(x, y, label="US average"), color="black") + 
  geom_vline(xintercept=1963, col = "blue")
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)
the_disease = "Smallpox"

dat <- us_contagious_diseases %>%
   filter(!state%in%c("Hawaii","Alaska") & disease == the_disease & weeks_reporting >= 10) %>%
   mutate(rate = count / population * 10000) %>%
   mutate(state = reorder(state, rate))

avg <- us_contagious_diseases %>%
  filter(disease==the_disease) %>% group_by(year) %>%
  summarize(us_rate = sum(count, na.rm=TRUE)/sum(population, na.rm=TRUE)*10000)

dat %>% ggplot() +
  geom_line(aes(year, rate, group = state),  color = "grey50", 
            show.legend = FALSE, alpha = 0.2, size = 1) +
  geom_line(mapping = aes(year, us_rate),  data = avg, size = 1, color = "black") +
  scale_y_continuous(trans = "sqrt", breaks = c(5,25,125,300)) + 
  ggtitle("Cases per 10,000 by state") + 
  xlab("") + 
  ylab("") +
  geom_text(data = data.frame(x=1955, y=50), mapping = aes(x, y, label="US average"), color="black") + 
  geom_vline(xintercept=1963, col = "blue")
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal(eval = TRUE)
  check_function(., "aes") %>% {
    check_arg(., "x") %>% check_equal(eval = FALSE)
    check_arg(., "y") %>% check_equal(eval = FALSE)
    check_arg(., "group") %>% check_equal(eval = FALSE)
  }
  check_function(., "geom_line", not_called_msg="Did you add the `geom_line()` layer?")
  check_function(., "scale_y_continuous") %>% check_arg(., "trans") %>% check_equal(eval = TRUE)
}
success_msg("Good job!")
```

---

## Exercise 3: Time series plot - all diseases in California

```yaml
type: NormalExercise
key: 77c862e397
lang: r
xp: 100
skills:
  - 1
```

Now we are going to look at the rates of all diseases in one state. Again, you will be modifying the sample code to produce the desired plot.

`@instructions`
- For the state of California, make a time series plot showing rates for all diseases. 
- Include only years with 10 or more weeks reporting. 
- Use a different color for each disease.
- Include your `aes` function inside of `ggplot` rather than inside your `geom` layer.

`@hint`
- You can use `color` within `aes` to plot each disease in a different color.
- The column that has the number of weeks in which cases were reported is called `weeks_reporting`.
- To exclude years with fewer than 10 weeks of reported cases, modify the `filter` you use.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)

us_contagious_diseases %>% filter(state=="California") %>% 
  group_by(year, disease) %>%
  summarize(rate = sum(count)/sum(population)*10000) %>%
  ggplot(aes(year, rate)) + 
  geom_line()
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)

us_contagious_diseases %>% filter(state=="California" & weeks_reporting>=10) %>% 
  group_by(year, disease) %>%
  summarize(rate = sum(count)/sum(population)*10000) %>%
  ggplot(aes(year, rate, color = disease)) + 
  geom_line()
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal(eval = TRUE)
  check_function(., "aes") %>% {
    check_arg(., "x") %>% check_equal(eval = FALSE)
    check_arg(., "y") %>% check_equal(eval = FALSE)
    check_arg(., "color") %>% check_equal(eval = FALSE)
  }
  check_function(., "geom_line", not_called_msg="Did you add the `geom_line()` layer?")
}
test_student_typed("color = disease",  
  not_typed_msg = "Remember to use the disease to set the color")
success_msg("Good job!")
```

---

## Exercise 4: Time series plot - all diseases in the United States

```yaml
type: NormalExercise
key: 5daf3a49ef
lang: r
xp: 100
skills:
  - 1
```

Now we are going to make a time series plot for the rates of all diseases in the United States. For this exercise, we have provided less sample code - you can take a look at the previous exercise to get you started.

`@instructions`
- Compute the US rate by using `summarize` to sum over states. Call the variable `rate`.
    - The US rate for each disease will be the total number of cases divided by the total population. 
    - Remember to convert to cases per 10,000.
- You will need to filter for `!is.na(population)` to get all the data.
- Plot each disease in a different color.

`@hint`
- You can use `color` within `aes` to plot each disease in a different color.
- You don't need to filter for `weeks_reporting` in this exercise.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
library(RColorBrewer)
data(us_contagious_diseases)

us_contagious_diseases %>% filter(!is.na(population)) %>% 
  group_by(year, disease) %>%
  summarize(rate = sum(count)/sum(population)*10000) %>%
  ggplot(aes(year, rate, color = disease)) + 
  geom_line()
```

`@sct`
```{r}
test_error()
ex() %>% {
  check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal(eval = TRUE)
  check_function(., "aes") %>% {
    check_arg(., "x") %>% check_equal(eval = FALSE)
    check_arg(., "y") %>% check_equal(eval = FALSE)
    check_arg(., "color") %>% check_equal(eval = FALSE)
  }
  check_function(., "geom_line", not_called_msg="Did you add the `geom_line()` layer?")
}
success_msg("Good job!")
```

---

## End of Assessment: Data Visualization Principles, Part 3

```yaml
type: PureMultipleChoiceExercise
key: 2ebfaeb28b
xp: 50
skills:
  - 1
```

This is the end of the programming assignments.

You can close this window and return to <a href='https://www.edx.org/course/data-science-visualization-harvardx-ph125-2x'>Data Science: Visualization</a>.

`@hint`
- No hint necessary!

`@possible_answers`
- [Awesome]
- Nope

`@feedback`
- Great! Now navigate back to the course on edX!
- Now navigate back to the course on edX!
