---
title: Exploring the gapminder dataset
description: Visualizing gapminder results with dplyr and ggplot
---

## Exercise 1. Life expectancy vs fertility - part 1

```yaml
type: NormalExercise
key: 2c12ac9e9b
lang: r
xp: 100
skills:
  - 1
```

The Gapminder Foundation (www.gapminder.org) is a non-profit organization based in Sweden that promotes global development through the use of statistics that can help reduce misconceptions about global development.

`@instructions`
- Using ggplot and the points layer, create a scatter plot of life expectancy versus fertility for the African continent in 2012. This means that fertility should be plotted on the x-axis and life expectancy on the y-axis.
- Remember that you can use the R console to explore the gapminder dataset to figure out the names of the columns in the dataframe.
- In this exercise we provide parts of code to get you going. You need to fill out what is missing. But note that going forward, in the next exercises, you will be required to write most of the code.

`@hint`
- You should `filter` for the desired continent and year.
- Make sure that when you call `ggplot(aes(firstvar, secondvar)` that you are replacing `firstvar` and `secondvar` with the appropriate names to plot life expectancy on the y axis and fertility on the x axis.
- You can add the points layer using the call `geom_point`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
## fill out the missing parts in filter and aes
gapminder %>% filter( & ) %>%
  ggplot(aes( , )) +
  geom_point()
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder %>% filter(continent=="Africa" & year == 2012) %>%
  ggplot(aes(fertility, life_expectancy)) +
  geom_point()
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "Don't forget to `filter` by `Africa` and `year` equaling 2012")
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_point", not_called_msg="Did you add the `geom_point()` layer?")
}
success_msg("Great job!")
```

---

## Exercise 2. Life expectancy vs fertility - part 2 - coloring your plot

```yaml
type: NormalExercise
key: ba2e354cea
lang: r
xp: 100
skills:
  - 1
```

Note that there is quite a bit of variability in life expectancy and fertility with some African countries having very high life expectancies. There also appear to be three clusters in the plot.

`@instructions`
Remake the plot from the previous exercises but this time use color to distinguish the different regions of Africa to see if this explains the clusters. Remember that you can explore the gapminder data to see how the regions of Africa are labeled in the data frame!

Use `color` rather than `col` inside your `ggplot` call - while these two forms are equivalent in R, the grader specifically looks for `color`.

`@hint`
Within `aes` there is a `color` variable. Otherwise, your code should stay the same as in the last exercise.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder %>% filter(continent=="Africa" & year == 2012) %>%
  ggplot(aes(fertility, life_expectancy, color = region)) +
  geom_point()
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "Don't forget to `filter` by `Africa` and `year` equaling 2012")
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_point", not_called_msg="Did you add the `geom_point()` layer?")
}
success_msg("Good job!")
```

---

## Exercise 3. Life expectancy vs fertility - part 3 - selecting country and region

```yaml
type: NormalExercise
key: 6f7eef9d12
lang: r
xp: 100
skills:
  - 1
```

While many of the countries in the high life expectancy/low fertility cluster are from Northern Africa, three countries are not.

`@instructions`
- Create a table showing the country and region for the African countries (use `select`) that in 2012 had fertility rates of 3 or less and life expectancies of at least 70.
- Assign your result to a data frame called `df`.

`@hint`
Use `filter` then `select`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
df <- gapminder %>% 
  filter(continent=="Africa" & year == 2012 & fertility <=3 & life_expectancy>=70) %>%
  select(country, region)
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "Don't forget to `filter` by continent, year, fertility and life_expectancy")
test_function("select", incorrect_msg = "Don't forget to `select` country and region")
ex() %>% {
   check_object(.,"df") %>% check_equal()
}
test_student_typed(c("fertility <= 3", "3 >= fertility", "fertility < 4", "4 > fertility"),  
  not_typed_msg = "Remember to restrict to data with fertility at most 3")
test_student_typed(c("life_expectancy >= 70", "70 <= life_expectancy"),
  not_typed_msg = "Remember to restrict to data with life expectancy at least 70")
success_msg("Good job!")
```

---

## Exercise 4. Life expectancy and the Vietnam War - part 1

```yaml
type: NormalExercise
key: 91e3023cfd
lang: r
xp: 100
skills:
  - 1
```

The Vietnam War lasted from 1955 to 1975. Do the data support war having a negative effect on life expectancy? We will create a time series plot that covers the period from 1960 to 2010 of life expectancy for Vietnam and the United States, using color to distinguish the two countries. In this start we start the analysis by generating a table.

`@instructions`
- Use `filter` to create a table with data for the years from 1960 to 2010 in Vietnam and the United States.
- Save the table in an object called `tab`.

`@hint`
- Remember, you are still using the gapminder dataset!
- You can create variables that contain the desired years and countries and use them when you call `filter`. For example, if you wanted data from Mexico and South Africa for all years, you could use `mycountries <- c("Mexico", "South Africa")` and then filter the gapminder dataset using `filter(country %in% mycountries)`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
years <- 1960:2010
countries <- c("United States", "Vietnam")
tab <- gapminder %>% filter(year %in% years & country %in% countries)
```

`@sct`
```{r}
test_error()
test_function("filter", incorrect_msg = "Don't forget to `filter` by country and year")
ex() %>% {
   check_object(.,"tab") %>% check_equal()
}
success_msg("Good job!")
```

---

## Exercise 5. Life expectancy and the Vietnam War - part 2

```yaml
type: NormalExercise
key: 6fe8a21728
lang: r
xp: 100
skills:
  - 1
```

Now that you have created the data table in Exercise 4, it is time to plot the data for the two countries.

`@instructions`
- Use `geom_line` to plot life expectancy vs year for Vietnam and the United States and save the plot as `p`. The data table is stored in `tab`.
- Use color to distinguish the two countries.
- Print the object `p`.

`@hint`
- Again remember that you can look at the gapminder dataset to figure out what different columns are called.
- Year should be plotted on the x axis, and life expectancy should be plotted on the y axis.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
years <- 1960:2010
countries <- c("United States", "Vietnam")
tab <- gapminder %>% filter(year %in% years & country %in% countries)
```

`@sample_code`
```{r}
p <- # code for your plot goes here - the data table is stored as `tab`
p
```

`@solution`
```{r}
p <- tab %>% ggplot(aes(x=year,y=life_expectancy,color=country)) + geom_line()
p
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_line", not_called_msg="Did you add the `geom_line()` layer?")
}
success_msg("Notice the dip in life expectancy during the time of the war.")
```

---

## Exercise 6. Life expectancy in Cambodia

```yaml
type: NormalExercise
key: 1df58235ad
lang: r
xp: 100
skills:
  - 1
```

Cambodia was also involved in this conflict and, after the war, Pol Pot and his communist Khmer Rouge took control and ruled Cambodia from 1975 to 1979. He is considered one of the most brutal dictators in history. Do the data support this claim?

`@instructions`
Use a single line of code to create a time series plot from 1960 to 2010 of life expectancy vs year for Cambodia.

`@hint`
- You can modify your `filter` code from Exercise 4 to create the time series plot for Cambodia instead of for the United States and Vietnam.
- Then feed that output into `ggplot`, again plotting year on the x axis and life expectancy on the y axis.
- Remember to use `geom_line()` to create the plot.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder %>% filter(year >= 1960 & year <= 2010 & country == "Cambodia") %>% 
  ggplot(aes(year, life_expectancy)) + geom_line()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_line", not_called_msg="Did you add the `geom_line()` layer?")
}
success_msg("Good job!")
```

---

## Exercise 7. Dollars per day - part 1

```yaml
type: NormalExercise
key: 6ed3eff502
lang: r
xp: 100
skills:
  - 1
```

Now we are going to calculate and plot dollars per day for African countries in 2010 using GDP data.

In the first part of this analysis, we will create the dollars per day variable.

`@instructions`
- Use `mutate` to create a `dollars_per_day` variable, which is defined as gdp/population/365.
- Create the `dollars_per_day` variable for African countries for the year 2010.
- Remove any `NA` values.
- Save the mutated dataset as `daydollars`.

`@hint`
- First `mutate` and then `filter`.
- You can remove `NA` values using `!is.na(dollars_per_day)`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
daydollars <- # write your code here
```

`@solution`
```{r}
library(dplyr)
library(dslabs)
data(gapminder)
daydollars <- gapminder %>% mutate(dollars_per_day = gdp/population/365) %>% filter(continent == "Africa" & year == 2010 & !is.na(dollars_per_day)) 
```

`@sct`
```{r}
test_error()
ex() %>% check_object("daydollars") %>% check_equal()
test_function("filter", incorrect_msg = "Remember to `filter` by continent and year")
success_msg("Good job!")
```

---

## Exercise 8. Dollars per day - part 2

```yaml
type: NormalExercise
key: 6d64ddb280
lang: r
xp: 100
skills:
  - 1
```

Now we are going to calculate and plot dollars per day for African countries in 2010 using GDP data.

In the second part of this analysis, we will plot the smooth density plot using a log (base 2) x axis.

`@instructions`
- The dataset including the `dollars_per_day` variable is preloaded as `daydollars`.
- Create a smooth density plot of dollars per day from `daydollars`.
- Use `scale_x_continuous` to change the x-axis to a log (base 2) scale.

`@hint`
- Use `ggplot` for the plotting of `dollars_per_day`
- Use `geom_density` to create the smooth density plot.
- Use `scale_x_continuous(trans = "log2")` to transform the x axis.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
daydollars <- gapminder %>% mutate(dollars_per_day = gdp/population/365) %>% filter(continent == "Africa" & year == 2010 & !is.na(dollars_per_day))
```

`@sample_code`
```{r}
# your code here
```

`@solution`
```{r}
daydollars %>% ggplot(aes(dollars_per_day)) + geom_density() + scale_x_continuous(trans = "log2")
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density", not_called_msg="Did you add the `geom_density()` layer?")
   check_function(., "scale_x_continuous") %>% check_arg(., "trans") %>% check_equal(eval = TRUE)
}
success_msg("Good job!")
```

---

## Exercise 9. Dollars per day - part 3 - multiple density plots

```yaml
type: NormalExercise
key: 686da17725
lang: r
xp: 100
skills:
  - 1
```

Now we are going to combine the plotting tools we have used in the past two exercises to create density plots for multiple years.

`@instructions`
- Create the `dollars_per_day` variable as in Exercise 7, but for African countries in the years 1970 and 2010 this time.
    - Make sure you remove any `NA` values.
- Create a smooth density plot of dollars per day for 1970 and 2010 using a log (base 2) scale for the x axis.
- Use `facet_grid` to show a different density plot for 1970 and 2010.

`@hint`
- Change the way you call `filter` to include both years.
- Add `facet_grid(year~.)` at the end to show both plots.
- Everything else stays the same is in the previous exercises!

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year %in% c(1970,2010) & !is.na(dollars_per_day)) %>%
  ggplot(aes(dollars_per_day)) + 
  geom_density() + 
  scale_x_continuous(trans = "log2") + 
  facet_grid(year ~ .)
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
   check_function(., "facet_grid")
}
test_student_typed("scale_x_continuous(trans = \"log2\")",  
  not_typed_msg = "Remember to use a log2 scale on the x-axis")
success_msg("Note the change in the density plots for the two different years.")
```

---

## Exercise 10. Dollars per day - part 4 - stacked density plot

```yaml
type: NormalExercise
key: a73ffee200
lang: r
xp: 100
skills:
  - 1
```

Now we are going to edit the code from Exercise 9 to show a stacked density plot of each region in Africa.

`@instructions`
- Much of the code will be the same as in Exercise 9:
    - Create the `dollars_per_day` variable as in Exercise 7, but for African countries in the years 1970 and 2010 this time.
    - Make sure you remove any `NA` values.
    - Create a smooth density plot of dollars per day for 1970 and 2010 using a log (base 2) scale for the x axis.
    - Use `facet_grid` to show a different density plot for 1970 and 2010. 
- Make sure the densities are smooth by using `bw = 0.5`.
- Use the `fill` and `position` arguments where appropriate to create the stacked density plot of each region.

`@hint`
- Use `fill = region` within `aes`.
- Use `position = "stack"` within `geom_density`, along with `bw = 0.5`.
- Everything else should stay the same!

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)

gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year %in% c(1970,2010) & !is.na(dollars_per_day)) %>%  
  ggplot(aes(dollars_per_day, fill = region)) + 
  geom_density(bw=0.5, position = "stack") + 
  scale_x_continuous(trans = "log2") + 
  facet_grid(year ~ .)
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "fill") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density") %>% {
       check_arg(., "bw") %>% check_equal(eval = FALSE)
       check_arg(., "position") %>% check_equal(eval = FALSE)
   }
   check_function(., "facet_grid")
}
test_student_typed("scale_x_continuous(trans = \"log2\")",  
  not_typed_msg = "Remember to use a log2 scale on the x-axis")
success_msg("Look at the graphs - do different regions of Africa show different patterns?")
```

---

## Exercise 11. Infant mortality scatter plot - part 1

```yaml
type: NormalExercise
key: bb1f9910e7
lang: r
xp: 100
skills:
  - 1
```

We are going to continue looking at patterns in the gapminder dataset by plotting infant mortality rates versus dollars per day for African countries.

`@instructions`
- Generate `dollars_per_day` using `mutate` and `filter` for the year 2010 for African countries.
    - Remember to remove `NA` values for `infant_mortality` and `dollars_per_day`.
- Store the mutated dataset in `gapminder_Africa_2010`.
- Make a scatter plot of `infant_mortality` versus `dollars_per_day` for countries in the African continent.
- Use color to denote the different regions of Africa.

`@hint`
- As in previous exercises, use `mutate` to generate `dollars_per_day`, which is equal to gpd/population/365.
- You should `filter` for both `continent` and `year`.
- Remove `NA` values for `dollars_per_day` and `infant_mortality`.
- `geom_point()` can be used for creating a scatter plot.
- `color = region` belongs within `aes`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder_Africa_2010 <- # create the mutated dataset

# now make the scatter plot
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder_Africa_2010 <- gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year == 2010 & !is.na(dollars_per_day) & !is.na(infant_mortality))

gapminder_Africa_2010 %>%  ggplot(aes(dollars_per_day, infant_mortality, color = region)) +
  geom_point()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_point") 
}
success_msg("Good job! Does there appear to be a relationship between dollars per day and infant mortality?")
```

---

## Exercise 12. Infant mortality scatter plot - part 2 - logarithmic axis

```yaml
type: NormalExercise
key: b50dffa3d0
lang: r
xp: 100
skills:
  - 1
```

Now we are going to transform the x axis of the plot from the previous exercise.

`@instructions`
- The mutated dataset is preloaded as `gapminder_Africa_2010`.
- As in the previous exercise, make a scatter plot of `infant_mortality` versus `dollars_per_day` for countries in the African continent.
- As in the previous exercise, use color to denote the different regions of Africa.
- Transform the x axis to be in the log (base 2) scale.

`@hint`
The plotting code is the same as in the previous exercise - just add the axis transformation using `scale_x_continuous` with the appropriate argument.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder_Africa_2010 <- gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year == 2010 & !is.na(dollars_per_day) & !is.na(infant_mortality))
```

`@sample_code`
```{r}
gapminder_Africa_2010 %>% # your plotting code here
```

`@solution`
```{r}
gapminder_Africa_2010 %>% 
  ggplot(aes(dollars_per_day, infant_mortality, color = region)) +
  geom_point() + 
  scale_x_continuous(trans = "log2")
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_point")
   check_function(., "scale_x_continuous") %>% check_arg(., "trans") %>% check_equal() 
}
success_msg("Good job! Does the transformation help make any relationship between dollars per day and infant mortality clearer?")
```

---

## Exercise 13. Infant mortality scatter plot - part 3 - adding labels

```yaml
type: NormalExercise
key: 2190d733ca
lang: r
xp: 100
skills:
  - 1
```

Note that there is a large variation in infant mortality and dollars per day among African countries.

As an example, one country has infant mortality rates of less than 20 per 1000 and dollars per day of 16, while another country has infant mortality rates over 10% and dollars per day of about 1.

In this exercise, we will remake the plot from Exercise 12 with country names instead of points so we can identify which countries are which.

`@instructions`
- The mutated dataset is preloaded as `gapminder_Africa_2010`.
- As in the previous exercise, make a scatter plot of `infant_mortality` versus `dollars_per_day` for countries in the African continent.
- As in the previous exercise, use color to denote the different regions of Africa.
- As in the previous exercise, transform the x axis to be in the log (base 2) scale.
- Add a `geom_text` layer to display country names instead of points.
- Be sure to call `aes()` within your call to `ggplot()`.

`@hint`
- Use the `geom_text` layer instead of `geom_point` to show country names.
- You will also need `label = country` to get the appropriate labels.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder_Africa_2010 <- gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year == 2010 & !is.na(dollars_per_day) & !is.na(infant_mortality))
```

`@sample_code`
```{r}
gapminder_Africa_2010 %>% # your plotting code here
```

`@solution`
```{r}
gapminder_Africa_2010 %>% 
  ggplot(aes(dollars_per_day, infant_mortality, color = region, label = country)) +
  geom_text() + 
  scale_x_continuous(trans = "log2")
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
       check_arg(., "label") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_text")
   check_function(., "scale_x_continuous") %>% check_arg(., "trans") %>% check_equal() 
}
success_msg("Good job!")
```

---

## Exercise 14. Infant mortality scatter plot - part 4 - comparison of scatter plots

```yaml
type: NormalExercise
key: 94bb0c97d6
lang: r
xp: 100
skills:
  - 1
```

Now we are going to look at changes in the infant mortality and dollars per day patterns African countries between 1970 and 2010.

`@instructions`
- Generate `dollars_per_day` using `mutate` and `filter` for the years 1970 and 2010 for African countries.
    - Remember to remove `NA` values.
- As in the previous exercise, make a scatter plot of `infant_mortality` versus `dollars_per_day` for countries in the African continent.
- As in the previous exercise, use color to denote the different regions of Africa.
- As in the previous exercise, transform the x axis to be in the log (base 2) scale.
- As in the previous exercise, add a layer to display country names in addition to points.
- Use `facet_grid` to show different plots for 1970 and 2010. Align the plots vertically.

`@hint`
Look back at Exercise 9 for a reminder of how to use `facet_grid` if you need help. All of the other code is very similar to everything you have done in the previous exercises.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(gapminder)
gapminder %>% 
  mutate(dollars_per_day = gdp/population/365) %>%
  filter(continent == "Africa" & year %in% c(1970, 2010) & !is.na(dollars_per_day) & !is.na(infant_mortality)) %>%
  ggplot(aes(dollars_per_day, infant_mortality, color = region, label = country)) +
  geom_text() + 
  scale_x_continuous(trans = "log2") +
  facet_grid(year~.)
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
       check_arg(., "label") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_text")
   check_function(., "facet_grid") %>% check_arg(., "rows") %>% check_equal(eval = FALSE)
   check_function(., "scale_x_continuous") %>% check_arg(., "trans") %>% check_equal(eval = FALSE) 
}
success_msg("Good job!")
```

---

## End of Assessment: Exploring the gapminder dataset

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
