---
title: Introduction to ggplot2
description: >-
  You'll learn how to make use of the powerful R package, ggplot2, for
  visualization
---

## Exercise 1. ggplot2 basics

```yaml
type: NormalExercise
key: 5f0d9213f4
lang: r
xp: 100
skills:
  - 1
```

Start by loading the dplyr and ggplot2 libraries as well as the `murders` data.

```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

Note that you can load both dplyr and ggplot2, as well as other packages, by installing and loading the tidyverse package.

With ggplot2 plots can be saved as objects. For example we can associate a dataset with a plot object like this

```{r}
p <- ggplot(data = murders)
```

Because `data` is the first argument we don't need to spell it out. So we can write this instead:

```{r}
p <- ggplot(murders)
```

or, if we load `dplyr`, we can use the pipe:

```{r}
p <- murders %>% ggplot()
```

Remember the pipe sends the object on the left of `%>%` to be the first argument for the function the right of `%>%`.

Now let's get an introduction to `ggplot`.

`@instructions`
What is the `class` of the object `p`?

`@hint`
Use the `class` function.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
p <- ggplot(murders)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
p <- ggplot(murders)
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
p <- ggplot(murders)
class(p)
```

`@sct`
```{r}
test_error()
test_function_result("class", incorrect_msg = "Make sure `p` is the argument.")
test_function("class", incorrect_msg = "Use the `class` function and make sure that `p` is the argument.")
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
}
success_msg("Nice job!")
```

---

## Exercise 2. Printing

```yaml
type: MultipleChoiceExercise
key: 04b871edcd
lang: r
xp: 50
skills:
  - 1
```

Remember that to print an object you can use the command `print` or simply type the object. For example, instead of 

```{r}
x <- 2
print(x)
```

you can simply type 


```{r}
x <- 2
x
```

Print the object `p` defined in exercise one 

```{r}
p <- ggplot(murders)
```

and describe what you see.

`@possible_answers`
- Nothing happens
- A blank slate plot
- A scatter plot
- A histogram

`@hint`
The libraries and data you need are already pre-loaded, but you will still need to define `p`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
```

`@sct`
```{r}
msg2 = "Correct!  Good Job!"
msg1 = msg3 = msg4 = "Incorrect. Try again."
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 3. Pipes

```yaml
type: NormalExercise
key: 1c5e6b0d1b
lang: r
xp: 100
skills:
  - 1
```

Now we are going to review the use of pipes by seeing how they can be used with `ggplot`.

`@instructions`
Using the pipe `%>%`, create an object `p` associated with the `heights` dataset instead of with the `murders` dataset as in previous exercises.

`@hint`
If we were to use the pipe to create an object associated with the `murders` dataset, we would use the code `p <- murders %>% ggplot()`. The code we want here is very similar.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)

```

`@sample_code`
```{r}
data(heights)
# define ggplot object called p like in the previous exercise but using a pipe 
```

`@solution`
```{r}
data(heights)
p <- heights %>% ggplot()
```

`@sct`
```{r}
test_error()
test_function("ggplot", incorrect_msg = "Make sure you are calling `ggplot` and using the `heights` data.")
test_pipe(absent_msg = "We want you to use the pipe `%>%` here.")

ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
}
success_msg("Nice job!")
```

---

## Exercise 4. Layers

```yaml
type: MultipleChoiceExercise
key: 772decbbf9
lang: r
xp: 50
skills:
  - 1
```

Now we are going to add layers and the corresponding aesthetic mappings. For the murders data, we plotted total murders versus population sizes in the videos.

Explore the `murders` data frame to remind yourself of the names for the two variables (total murders and population size) we want to plot and select the correct answer.

`@possible_answers`
- `state` and `abb`
- `total_murders` and `population_size`
- `total` and `population`
- `murders` and `size`

`@hint`
You can type `names(murders)` or read the help file by typing `?murders`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sct`
```{r}
msg3 = "Correct!  Good Job!"
msg1 = msg2 = msg4 = "Incorrect. Try again."
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 5. geom_point 1

```yaml
type: NormalExercise
key: fdcac65e14
lang: r
xp: 100
skills:
  - 1
```

To create a scatter plot, we add a layer with the function `geom_point`. The aesthetic mappings require us to define the x-axis and y-axis variables respectively. So the code looks like this:

```{r, eval=FALSE}
murders %>% ggplot(aes(x = , y = )) +
  geom_point()
```
except we have to fill in the blanks to define the two variables `x` and `y`.

`@instructions`
Fill out the sample code with the correct variable names to plot total murders versus population size.

`@hint`
In the previous exercise we determined that the variable names we want here are `population` and `total`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
## Fill in the blanks
murders %>% ggplot(aes(x = , y = )) +
  geom_point()
```

`@solution`
```{r}
murders %>% ggplot(aes(x = population, y = total)) +
  geom_point()
```

`@sct`
```{r}
test_error()
test_function("ggplot", incorrect_msg = "Make sure you are calling `ggplot` and using the `murders` data")
test_pipe(absent_msg = "We want you to use the pipe `%>%` here.")

ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_point", not_called_msg="Did you add the `geom_point()` layer?")
}
success_msg("Nice job!!")
```

---

## Exercise 6. geom_point 2

```yaml
type: NormalExercise
key: 7a9a873231
lang: r
xp: 100
skills:
  - 1
```

Note that if we don't use argument names, we can obtain the same plot by making sure we enter the variable names in the desired order:

```{r}
murders %>% ggplot(aes(population, total)) +
  geom_point()
```

`@instructions`
Remake the plot but flip the axes so that `total` is on the x-axis and `population` is on the y-axis.

`@hint`
Remember to flip the order of `total` and `population` in your code.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}

```

`@solution`
```{r}
murders %>% ggplot(aes(total, population)) +
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
   }
   check_function(., "geom_point", not_called_msg="Did you add the `geom_point()` layer?")
}
success_msg("Nice job!!")
```

---

## Exercise 7. geom_point text

```yaml
type: MultipleChoiceExercise
key: 5a6cbcf56e
lang: r
xp: 50
skills:
  - 1
```

If instead of points we want to add text, we can use the `geom_text()` or `geom_label()` geometries. However, note that the following code 

```{r, eval=FALSE}
murders %>% ggplot(aes(population, total)) +
  geom_label()
```

will give us the error message:
`Error: geom_label requires the following missing aesthetics: label`

Why is this?

`@possible_answers`
- We need to map a character to each point through the label argument in aes
- We need to let `geom_label` know what character to use in the plot
- The `geom_label` geometry does not require  x-axis and y-axis values.
- `geom_label` is not a ggplot2 command

`@hint`
Read the help file for `geom_label` carefully and look at the required arguments.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sct`
```{r}
msg1 = "Correct!  Good Job!"
msg3 = msg2 = msg4 = msg5 = "Incorrect. Try again"
test_mc(1, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 8. geom_point text

```yaml
type: NormalExercise
key: a46d573cd9
lang: r
xp: 100
skills:
  - 1
```

You can also add labels to the points on a plot.

`@instructions`
Rewrite the code from the previous exercise to:
- add a `label` aesthetic to `aes` equal to the state abbreviation
- use `geom_label` instead of `geom_point`

`@hint`
- The column name for abbreviation in the `murders` dataset is `abb`. You need to map it to the points using `aes` like this `aes(population, total, label = abb)`.
- You will also need to change `geom_point` in the code to `geom_label`- see Exercise 7 for an example.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
## edit the next line to add the label
murders %>% ggplot(aes(population, total)) +
  geom_point()
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
murders %>% ggplot(aes(population, total, label = abb)) +
  geom_label()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(.,"label") %>% check_equal(eval=FALSE)
   }
   check_function(., "geom_label", not_called_msg="Did you add the `geom_label()` layer?")
}
success_msg("Great job!!")
```

---

## Exercise 9. geom_point colors

```yaml
type: MultipleChoiceExercise
key: d7f3eb3027
lang: r
xp: 50
skills:
  - 1
```

Now let's change the color of the labels to blue. How can we do this?

`@possible_answers`
- By adding a column called `blue` to `murders`
- By mapping the colors through `aes` because each label needs a different color
- By using the `color` argument in `ggplot`
- By using the `color` argument in `geom_label` because we want all colors to be blue so we do not need to map colors

`@hint`
Note that because all points will be blue this is not a mapping. We therefore assign the color outside of `aes`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
data(murders)
```

`@sct`
```{r}
msg4 = "Correct!  Good Job!"
msg3 = msg2 = msg1 = "Incorrect. Try again."
test_mc(4, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 10. geom_point colors 2

```yaml
type: NormalExercise
key: 76adde45cd
lang: r
xp: 100
skills:
  - 1
```

Now let's go ahead and make the labels blue. We previously wrote this code to add labels to our plot:

```{r, eval=FALSE}
murders %>% ggplot(aes(population, total, label= abb)) +
  geom_label()
```
Now we will edit this code.

`@instructions`
- Rewrite the code above to make the labels blue by adding an argument to `geom_label`.
- You do not need to put the `color` argument inside of an `aes` col.
- Note that the grader expects you to use the argument `color` instead of `col`; these are equivalent.

`@hint`
You can tell ggplot to make blue point via the `color` argument in `geom_label`. You can use the character `"blue"`. There is no need to use `aes` inside of `geom_label`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
murders %>% ggplot(aes(population, total,label= abb)) +
  geom_label()
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
murders %>% ggplot(aes(population, total, label = abb)) +
  geom_label(color = "blue")
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(.,"label") %>% check_equal(eval=FALSE)
   }
   check_function(., "geom_label", not_called_msg="Did you add the `geom_label()` layer?") %>% {
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
}
success_msg("Great job!!")
```

---

## Exercise 11. geom_labels by region

```yaml
type: MultipleChoiceExercise
key: ef630d59d6
lang: r
xp: 50
skills:
  - 1
```

Now suppose we want to use color to represent the different regions. So the states from the West will be one color, states from the Northeast another, and so on. In this case, which of the following is most appropriate:

`@possible_answers`
- Adding a column called `color` to `murders` with the color we want to use
- Mapping the colors through the color argument of `aes` because each label needs a different color
- Using the `color` argument in `ggplot`
- Using the `color` argument in `geom_label` because we want all colors to be blue so we do not need to map colors

`@hint`
Now we are assigning a different color to each state and this color is determined by one of the variables in the dataset. So we do need to assign the color through the `aes` mapping.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sct`
```{r}
msg2 = "Correct!  Good Job!"
msg3 = msg4 = msg1 = "Incorrect. Try again."
test_mc(2, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 12. geom_label colors

```yaml
type: NormalExercise
key: e9ff3ae827
lang: r
xp: 100
skills:
  - 1
```

We previously used this code to make a plot using the state abbreviations as labels:
```{r}
murders %>% ggplot(aes(population, total, label = abb)) +
  geom_label()
```
We are now going to add color to represent the region.

`@instructions`
Rewrite the code above to make the label color correspond to the state's region. Because this is a mapping, you will have to do this through the `aes` function. Use the existing `aes` function inside of the `ggplot` function.

`@hint`
The variable that contains the information determining color is called `region`. We can assign `color = region` through `aes` and ggplot will automatically do what we want.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
## edit this code
murders %>% ggplot(aes(population, total, label = abb)) +
  geom_label()
```

`@solution`
```{r}
murders %>% ggplot(aes(population, total, label = abb, color = region)) +
  geom_label()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(.,"label") %>% check_equal(eval=FALSE)
       check_arg(.,"color") %>% check_equal(eval=FALSE)
   }
   check_function(., "geom_label", not_called_msg="Did you add the `geom_label()` layer?")
}
success_msg("Nice plot!")
```

---

## Exercise 13. Log-scale

```yaml
type: NormalExercise
key: 00f2deb781
lang: r
xp: 100
skills:
  - 1
```

Now we are going to change the axes to log scales to account for the fact that the population distribution is skewed. Let's start by defining an object `p` that holds the plot we have made up to now:

```{r}
p <- murders %>% ggplot(aes(population, total, label = abb, color = region)) +
  geom_label() 
```

To change the x-axis to a log scale we learned about the `scale_x_log10()` function. We can change the axis by adding this layer to the object `p` to change the scale and render the plot using the following code:

```{r}
p + scale_x_log10()
```

`@instructions`
Change **both** axes to be in the log scale on a single graph. Make sure you do not redefine `p` - just add the appropriate layers.

`@hint`
You will be adding two layers now. After defining `p` the resulting code will look something like this `p + layer_1 + layer_2`. Make sure you do not redefine `p` - just add the layers to it.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
p <- murders %>% ggplot(aes(population, total, label = abb, color = region)) + geom_label()
## add layers to p here
```

`@solution`
```{r}
p<- murders %>% ggplot(aes(population, total, label = abb, color = region)) + geom_label()
p + scale_x_log10() + scale_y_log10()
```

`@sct`
```{r}
test_error()
test_object("p",incorrect_msg = "Make sure to define `p`")
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(.,"label") %>% check_equal(eval=FALSE)
       check_arg(.,"color") %>% check_equal(eval=FALSE)
   }
   check_function(., "scale_x_log10", not_called_msg="Did you add the `scale_x_log10()` layer?")
   check_function(., "scale_y_log10", not_called_msg="Did you add the `scale_y_log10()` layer?")
   check_function(., "geom_label", not_called_msg="Did you add the `geom_label()` layer?")
}
success_msg("Nice plot!")
```

---

## Exercise 14. Titles

```yaml
type: NormalExercise
key: f013c3250d
lang: r
xp: 100
skills:
  - 1
```

In the previous exercises we created a plot using the following code:

```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
p<- murders %>% ggplot(aes(population, total, label = abb, color = region)) +
  geom_label()
p + scale_x_log10() + scale_y_log10()
```

We are now going to add a title to this plot. We will do this by adding yet another layer, this time with the function `ggtitle`.

`@instructions`
Edit the code above to add the title "Gun murder data" to the plot.

`@hint`
Use the function like this `p + ggtitle("Put title here")`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(murders)
```

`@sample_code`
```{r}
p <- murders %>% ggplot(aes(population, total, label = abb, color = region)) +
  geom_label()
# add a layer to add title to the next line
p + scale_x_log10() + 
    scale_y_log10()
```

`@solution`
```{r}
p<- murders %>% ggplot(aes(population, total, label = abb, color = region)) +
  geom_label()
p + scale_x_log10() +
  scale_y_log10() + 
  ggtitle("Gun murder data")
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "y") %>% check_equal(eval = FALSE)
       check_arg(.,"label") %>% check_equal(eval=FALSE)
       check_arg(.,"color") %>% check_equal(eval=FALSE)
   }
   check_function(., "scale_x_log10", not_called_msg="Did you add the `scale_x_log10()` layer?")
   check_function(., "scale_y_log10", not_called_msg="Did you add the `scale_y_log10()` layer?")
   check_function(., "geom_label", not_called_msg="Did you add the `geom_label()` layer?")
   check_function(., "ggtitle", not_called_msg="Did you add the `ggtitle()` layer?") %>% check_arg(.,"label") %>% check_equal()
}
success_msg("Nice plot!")
```

---

## Exercise 15. Histograms

```yaml
type: MultipleChoiceExercise
key: 524fb260ba
lang: r
xp: 50
skills:
  - 1
```

We are going to shift our focus from the `murders` dataset to explore the `heights` dataset.

We use the `geom_histogram` function to make a histogram of the heights in the `heights` data frame. When reading the documentation for this function we see that it requires just one mapping, the values to be used for the histogram. 

What is the variable containing the heights in inches in the `heights` data frame?

`@possible_answers`
- `sex`
- `heights`
- `height`
- `heights$height`

`@hint`
Look at `names(heights)` to see the variable names.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sct`
```{r}
msg3 = "Correct!  Good Job!"
msg1 = msg2 = msg4 = "Incorrect. Try again"
test_mc(3, c(msg1, msg2, msg3, msg4))
```

---

## Exercise 16. A second example

```yaml
type: NormalExercise
key: 94d29619a2
lang: r
xp: 100
skills:
  - 1
```

We are now going to make a histogram of the heights so we will load the `heights` dataset. The following code has been pre-run for you to load the heights dataset:

```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@instructions`
- Create a ggplot object called `p` using the pipe to assign the heights data to a ggplot object.
- Assign `height` to the x values through the `aes` function.

`@hint`
Just as before, we will use the pipe `heights %>% ggplot( AES MAPPING HERE)`. But the `aes` mapping only has one variable now.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
# define p here
p <- 
```

`@solution`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
p <- heights %>% 
  ggplot(aes(height))
```

`@sct`
```{r}
test_error()
test_pipe(absent_msg = "We want you to use the pipe `%>%` here.")
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
}
success_msg("Good job!")
```

---

## Exercise 17. Histograms 2

```yaml
type: NormalExercise
key: 744cb87b5b
lang: r
xp: 100
skills:
  - 1
```

Now we are ready to add a layer to actually make the histogram.

`@instructions`
Add a layer to the object `p` (created in the previous exercise) using the `geom_histogram` function to make the histogram.

`@hint`
We are simply adding a layer `+ geom_histogram`. Make sure you do not redefine `p`!

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
p <- heights %>% 
  ggplot(aes(height))
## add a layer to p
```

`@solution`
```{r}
p <- heights %>% 
  ggplot(aes(height))
p + geom_histogram()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_histogram", not_called_msg="Did you add the `geom_histogram()` layer?")
}
success_msg("Great job!")
```

---

## Exercise 18. Histogram binwidth

```yaml
type: NormalExercise
key: 9723af5161
lang: r
xp: 100
skills:
  - 1
```

Note that when we run the code from the previous exercise we get the following warning:

>> `stat_bin() using bins = 30. Pick better value with binwidth.`

`@instructions`
Use the `binwidth` argument to change the histogram made in the previous exercise to use bins of size 1 inch.

`@hint`
The `binwidth` argument goes inside the `geom_histogram` function.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
p <- heights %>% 
  ggplot(aes(height))
## add the geom_histogram layer but with the requested argument
```

`@solution`
```{r}
p <- heights %>% 
  ggplot(aes(height))
p + geom_histogram(binwidth = 1)
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_histogram", not_called_msg="Did you add the `geom_point()` layer?") %>%
        check_arg(.,"binwidth") %>% check_equal(eval=FALSE)
}
success_msg("Great job!")
```

---

## Exercise 19. Smooth density plot

```yaml
type: NormalExercise
key: bd3cb2d728
lang: r
xp: 100
skills:
  - 1
```

Now instead of a histogram we are going to make a smooth density plot. In this case, we will not make an object `p`. Instead we will render the plot using a single line of code. In the previous exercise, we could have created a histogram using one line of code like this:

```{r, eval=FALSE}
heights %>% 
  ggplot(aes(height)) +
  geom_histogram()
```

Now instead of `geom_histogram` we will use `geom_density` to create a smooth density plot.

`@instructions`
Add the appropriate layer to create a smooth density plot of heights.

`@hint`
Instead of using `geom_histogram`, use `geom_density`.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
## add the correct layer using +
heights %>% 
  ggplot(aes(height))
```

`@solution`
```{r}
heights %>% 
  ggplot(aes(height)) + 
  geom_density()
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
}
success_msg("Great job!")
```

---

## Exercise 20. Two smooth density plots

```yaml
type: NormalExercise
key: b2bb7f2d81
lang: r
xp: 100
skills:
  - 1
```

Now we are going to make density plots for males and females separately. We can do this using the `group` argument within the `aes` mapping. Because each point will be assigned to a different density depending on a variable from the dataset, we need to map within `aes`.

`@instructions`
Create separate smooth density plots for males and females by defining `group` by sex. Use the existing `aes` function inside of the `ggplot` function.

`@hint`
We just need to change the `aes` by adding the argument `group = sex`. Then you add the `geom_density` layer as before.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
## add the group argument then a layer with +
heights %>% 
  ggplot(aes(height))
```

`@solution`
```{r}
heights %>% 
  ggplot(aes(height, group = sex)) + 
  geom_density()
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "group") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density", not_called_msg="Did you add the `geom_density()` layer?")
}
success_msg("Great job!")
```

---

## Exercise 21. Two smooth density plots 2

```yaml
type: NormalExercise
key: 5d73d44fd1
lang: r
xp: 100
skills:
  - 1
```

In the previous exercise we made the two density plots, one for each sex, using:

```{r}
heights %>% 
  ggplot(aes(height, group = sex)) + 
  geom_density()
```
We can also assign groups through the `color` or `fill` argument. For example, if you type `color = sex` ggplot knows you want a different color for each sex. So two densities must be drawn. You can therefore skip the `group = sex` mapping.
Using `color` has the added benefit that it uses color to distinguish the groups.

`@instructions`
Change the density plots from the previous exercise to add color.

`@hint`
Instead of using `group = sex`, we can use `color = sex` within `aes` to do the mapping. And remember to add the smooth density layer!

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}
## edit the next line to use color instead of group then add a density layer
heights %>% 
  ggplot(aes(height, group = sex))
```

`@solution`
```{r}
heights %>% 
  ggplot(aes(height, color = sex)) + 
  geom_density() 
```

`@sct`
```{r}
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "color") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density", not_called_msg="Did you add the `geom_density()` layer?")
}
success_msg("Great job!")
```

---

## Exercise 22. Two smooth density plots 3

```yaml
type: NormalExercise
key: af8c96629b
lang: r
xp: 100
skills:
  - 1
```

We can also assign groups using the `fill` argument. When using the `geom_density` geometry, `color` creates a colored line for the smooth density plot while `fill` colors in the area under the curve.

We can see what this looks like by running the following code:

```{r}
heights %>% 
  ggplot(aes(height, fill = sex)) + 
  geom_density() 
```
However, here the second density is drawn over the other. We can change this by using something called _alpha blending_.

`@instructions`
Set the alpha parameter to 0.2 in the `geom_density` function to make this change.

`@hint`
Make sure you set `alpha = 0.2` in the correct part of your code.

`@pre_exercise_code`
```{r}
library(dplyr)
library(ggplot2)
library(dslabs)
data(heights)
```

`@sample_code`
```{r}

```

`@solution`
```{r}
heights %>% 
  ggplot(aes(height, fill = sex)) + 
  geom_density(alpha = 0.2)
```

`@sct`
```{r}
test_error()
test_error()
ex() %>% {
   check_function(., "ggplot") %>% check_arg(., "data") %>% check_equal()
   check_function(., "aes") %>% {
       check_arg(., "x") %>% check_equal(eval = FALSE)
       check_arg(., "fill") %>% check_equal(eval = FALSE)
   }
   check_function(., "geom_density", not_called_msg="Did you add the `geom_density()` layer?") %>% check_arg(.,"alpha") %>% check_equal(eval=TRUE)
}
success_msg("Great job!")
```

---

## End of Assessment: Introduction to ggplot2

```yaml
type: PureMultipleChoiceExercise
key: eb426fb216
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
