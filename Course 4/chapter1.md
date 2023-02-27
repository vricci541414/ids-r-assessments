---
title: Parameters and Estimates
title_meta: Chapter 1
description: >-
  In this chapter, you will learn about parameters and estimates using the
  example of election polling.
free_preview: true
---

## Exercise 1. Polling - expected value of S

```yaml
type: MultipleChoiceExercise
key: 7de52dae58
lang: r
xp: 50
skills:
  - 1
```

Suppose you poll a population in which a proportion $p$ of voters are Democrats and $1-p$ are Republicans. Your sample size is $N = 25$. Consider the random variable $S$, which is the **total** number of Democrats in your sample. 

What is the expected value of this random variable $S$?

`@possible_answers`
- $$\mbox{E}(S) = 25(1-p)$$
- $$\mbox{E}(S) = 25p$$
- $$\mbox{E}(S) = \sqrt{25 p (1-p)}$$
- $$\mbox{E}(S) = p$$

`@hint`
- The expected value $\mbox{E}(S)$ is a function of a function of $p$ and the sample size.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. This selection tells you the expected value of a random variable for the number of Republicans in your sample."
msg2 = "Nice work!"
msg3 = "Try again. The expected value of `S` is related to the sample size and the proportion of Democrats in your sample."
msg4 = "Try again. You also need to consider the sample size."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 2. Polling - standard error of S

```yaml
type: MultipleChoiceExercise
key: 33f4f606dd
lang: r
xp: 50
skills:
  - 1
```

Again, consider the random variable $S$, which is the **total** number of Democrats in your sample of 25 voters. The variable $p$ describes the proportion of Democrats in the sample, whereas $1-p$ describes the proportion of Republicans.

What is the standard error of $S$?

`@possible_answers`
- $$\mbox{SE}(S) = 25 p (1-p)$$
- $$\mbox{SE}(S) = \sqrt{25p}$$
- $$\mbox{SE}(S) = 25(1-p)$$
- $$\mbox{SE}(S) = \sqrt{25 p (1-p)}$$

`@hint`
- The standard error is a function of `p` and the sample size.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. The units of variance are squared."
msg2 = "Try  again. The standard error is affected by the proportions of both Republicans and Democrats."
msg3 = "Try again. The standard error is affected by the proportions of Democrats and Republicans."
msg4 = "Nice work!"
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 3. Polling - expected value of X-bar

```yaml
type: MultipleChoiceExercise
key: ae53ad7aa8
lang: r
xp: 50
skills:
  - 1
```

Consider the random variable $S/N$, which is equivalent to the sample average that we have been denoting as $\bar{X}$. The variable $N$ represents the sample size and $p$ is the proportion of Democrats in the population.

What is the expected value of $\bar{X}$?

`@possible_answers`
- $$ \mbox{E}(\bar{X}) = p $$
- $$ \mbox{E}(\bar{X}) = Np $$
- $$ \mbox{E}(\bar{X}) = N(1-p)$$
- $$ \mbox{E}(\bar{X}) = 1-p $$

`@hint`
- The expected value of the sum $S$ is $N \times p$. Dividing by the non-random constant $N$ gives us the expected value of the average.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Nice work!"
msg2 = "Try  again. The expected value of the sum `S` must be divided by the sample size."
msg3 = "Try again. The expected value is a function of `p`."
msg4 = "Try again. The expected value is a function of `p`."
test_mc(correct = 1, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 4. Polling - standard error of X-bar

```yaml
type: MultipleChoiceExercise
key: 7dab8954ff
lang: r
xp: 50
skills:
  - 1
```

What is the standard error of the sample average, $\bar{X}$?

The variable $N$ represents the sample size and $p$ is the proportion of Democrats in the population.

`@possible_answers`
- $$\mbox{SE}(\bar{X}) = \sqrt{Np (1-p)}$$
- $$\mbox{SE}(\bar{X}) = \sqrt{p (1-p) / N}$$
- $$\mbox{SE}(\bar{X}) = \sqrt{p (1-p)}$$
- $$\mbox{SE}(\bar{X}) = \sqrt{N}$$

`@hint`
- The standard error decreases as the sample size increases.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. The standard error of the average gets smaller as you increase the sample size."
msg2 = "Nice work!"
msg3 = "Try again. Remember that you divide by the sample size when calculating the average."
msg4 = "Try again. The expected value is a function of `p`."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 5. se versus p

```yaml
type: NormalExercise
key: 7bbf8b3928
lang: r
xp: 100
skills:
  - 1
```

Write a line of code that calculates the standard error `se` of a sample average when you poll 25 people in the population. Generate a sequence of 100 proportions of Democrats `p` that vary from 0 (no Democrats) to 1 (all Democrats).   

Plot `se` versus `p` for the 100 different proportions.

`@instructions`
- Use the `seq` function to generate a vector of 100 values of `p` that range from 0 to 1.
- Use the `sqrt` function to generate a vector of standard errors for all values of `p`.
- Use the `plot` function to generate a plot with `p` on the x-axis and `se` on the y-axis.

`@hint`
- The standard error of the sample average is $\mbox{SE}(\bar{X}) = \sqrt{p (1-p) / N}$.

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# `N` represents the number of people polled
N <- 25

# Create a variable `p` that contains 100 proportions ranging from 0 to 1 using the `seq` function


# Create a variable `se` that contains the standard error of each sample average


# Plot `p` on the x-axis and `se` on the y-axis

```

`@solution`
```{r}
# `N` represents the number of people polled
N <- 25

# Create a variable `p` that contains 100 proportions ranging from 0 to 1 using the `seq` function
p <- seq(0, 1, length = 100)

# Create a variable `se` that contains the standard error of each sample average
se <- sqrt(p*(1-p)/N)

# Plot `p` on the x-axis and `se` on the y-axis
plot(p, se)
```

`@sct`
```{r}
test_error()
test_function("seq", args = c("from","to","length.out"), eval=c(NA,NA,NA),
              not_called_msg = "Have you used `seq` function to generate a vector of proportions?",
              incorrect_msg = "Make sure to specify the beginning value (0), end value (1), and length of the vector you want (100) when using the `seq` function.")
              
test_object("p",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = NULL,
            incorrect_msg = "Remember to create an object called `p` that has 100 values ranging from 0 to 1. Specify `length = 100` in the `seq` function to generate this vector.")

test_object("se",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = NULL,
            incorrect_msg = "Use `sqrt` to calculate the standard error and save it as `se`. Make sure to specify the correct formula for standard error.")
    
test_function("plot", args = c("x","y"),
              not_called_msg = "Have you used `plot` to generate a plot `p` and `se`?",
              args_not_specified = "Remember to specify the vectors that contain the values to be plotted on the x- and y-axes when using the `plot` function.",
              incorrect_msg = "Make sure to plot `p` on the x-axis and `se` on the y-axis.")

success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 6. Multiple plots of se versus p

```yaml
type: NormalExercise
key: 010569b05a
lang: r
xp: 100
skills:
  - 1
```

Using the same code as in the previous exercise, create a for-loop that generates three plots of `p` versus `se` when the sample sizes equal $N = 25$, $N = 100$, and $N = 1000$.

`@instructions`
- Your for-loop should contain two lines of code to be repeated for three different values of N.
- The first line within the for-loop should use the `sqrt` function to generate a vector of standard errors `se` for all values of `p`.
- The second line within the for-loop should use the `plot` function to generate a plot with `p` on the x-axis and `se` on the y-axis.
- Use the `ylim` argument to keep the y-axis limits constant across all three plots. The lower limit should be equal to 0 and the upper limit should equal 0.1 (it can be shown that this value is the highest calculated standard error across all values of `p` and `N`).

`@hint`
- The standard error of the sample average is $$\mbox{SE}(\bar{X}) = \sqrt{p (1-p) / N}$$.
- The standard error of the sample average is highest when p = 0.5 and N is small.
- Use the command `for` to define your loop within parentheses. Write the lines of code to be repeated within curly brackets. For example, the example for-loop executes two lines of code for each element `N` in the vector `sample_sizes`.

```{r}
for(N in sample_sizes){
  example_line1
  example_line2
}
```

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# The vector `p` contains 100 proportions of Democrats ranging from 0 to 1 using the `seq` function
p <- seq(0, 1, length = 100)

# The vector `sample_sizes` contains the three sample sizes
sample_sizes <- c(25, 100, 1000)

# Write a for-loop that calculates the standard error `se` for every value of `p` for each of the three samples sizes `N` in the vector `sample_sizes`. Plot the three graphs, using the `ylim` argument to standardize the y-axis across all three plots.






```

`@solution`
```{r}
# The vector `p` contains 100 proportions of Democrats ranging from 0 to 1 using the `seq` function
p <- seq(0, 1, length = 100)

# The vector `sample_sizes` contains the three sample sizes
sample_sizes <- c(25, 100, 1000)

# Write a for-loop that calculates the standard error `se` for every value of `p` for each of the three samples sizes `N` in the vector `sample_sizes`. Plot the three graphs, using the `ylim` argument to standardize the y-axis across all three plots.
for(N in sample_sizes){
  se <- sqrt(p*(1-p)/N)
  plot(p, se, ylim = c(0,0.5/sqrt(25)))
}
```

`@sct`
```{r}
test_error()
test_function("seq", args = c("from","to","length.out"), eval=c(NA,NA,NA),
              not_called_msg = "Have you used `seq` function to generate a vector of proportions?",
              incorrect_msg = "Make sure to specify the beginning value (0), end value (1), and length of the vector you want (100) when using the `seq` function.")
test_object("p",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = NULL,
            incorrect_msg = "Remember to create an object called `p` that has 100 values ranging from 0 to 1. Specify `length = 100` in the `seq` function to generate this vector.")
test_for_loop(cond_test = "cond",
              expr_test = test_function(c("sqrt","plot"), not_called_msg="Make sure to begin your for loop with `for(N in sample_sizes)` and put the code to run inside the loop in curly brackets `{}`. Make sure to call the `sqrt` function to generate the standard errors and the `plot` function to make the plot."),
              not_found_msg = "Make sure to write a for-loop using `for`.")
success_msg("Great work! Let's move on to the next exercise.")
```

---

## Exercise 7. Expected value of d

```yaml
type: MultipleChoiceExercise
key: cd6a755085
lang: r
xp: 50
skills:
  - 1
```

Our estimate for the difference in proportions of Democrats and Republicans is $d = \bar{X} - (1-\bar{X})$.

Which derivation correctly uses the rules we learned about sums of random variables and scaled random variables to derive the expected value of $d$?

`@possible_answers`
- $$\begin{eqnarray}
\mbox{E}[\bar{X} - (1-\bar{X})] &=& \mbox{E}[2\bar{X} - 1] \\
&=& 2\mbox{E}[\bar{X}] - 1  \\
&=& N(2p - 1)\\
&=& Np - N(1-p)
\end{eqnarray}
$$

- $$
\begin{eqnarray}
\mbox{E}[\bar{X} - (1-\bar{X})] &=& \mbox{E}[\bar{X} - 1] \\
&=& \mbox{E}[\bar{X}] - 1  \\
&=& p - 1\\
\end{eqnarray}
$$

- $$
\begin{eqnarray}
\mbox{E}[\bar{X} - (1-\bar{X})] &=& \mbox{E}[2\bar{X} - 1] \\
&=& 2\mbox{E}[\bar{X}] - 1  \\
&=& 2\sqrt{p(1-p)} -1 \\
&=& p - (1-p)
\end{eqnarray}
$$

- $$
\begin{eqnarray}
\mbox{E}[\bar{X} - (1-\bar{X})] &=& \mbox{E}[2\bar{X} - 1] \\
&=& 2\mbox{E}[\bar{X}] - 1  \\
&=& 2p - 1\\
&=& p - (1-p)
\end{eqnarray}
$$

`@hint`
- The expected value of $\bar{X}$ is equal to `p`.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. The sample size is not included in this equation."
msg2 = "Try again. Pay attention to the algebra in the first step."
msg3 = "Try again. The expected value is equal to `p`."
msg4 = "Nice work!"
test_mc(correct = 4, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 8. Standard error of d

```yaml
type: MultipleChoiceExercise
key: 41575febb7
lang: r
xp: 50
skills:
  - 1
```

Our estimate for the difference in proportions of Democrats and Republicans is $d = \bar{X} - (1-\bar{X})$.

Which derivation correctly uses the rules we learned about sums of random variables and scaled random variables to derive the standard error of $d$?

`@possible_answers`
- $$
\begin{eqnarray}
\mbox{SE}[\bar{X} - (1-\bar{X})] &=& \mbox{SE}[2\bar{X} - 1] \\
&=& 2\mbox{SE}[\bar{X}]   \\
&=& 2\sqrt{p/N}
\end{eqnarray}
$$

- $$
\begin{eqnarray}
\mbox{SE}[\bar{X} - (1-\bar{X})] &=& \mbox{SE}[2\bar{X} - 1] \\
&=& 2\mbox{SE}[\bar{X} - 1]   \\
&=& 2\sqrt{p(1-p)/N} - 1
\end{eqnarray}
$$

- $$
\begin{eqnarray}
\mbox{SE}[\bar{X} - (1-\bar{X})] &=& \mbox{SE}[2\bar{X} - 1] \\
&=& 2\mbox{SE}[\bar{X}]   \\
&=& 2\sqrt{p(1-p)/N}
\end{eqnarray}
$$

- $$
\begin{eqnarray}
\mbox{SE}[\bar{X} - (1-\bar{X})] &=& \mbox{SE}[\bar{X} - 1] \\
&=& \mbox{SE}[\bar{X}]   \\
&=& \sqrt{p(1-p)/N}
\end{eqnarray}
$$

`@hint`
- The standard error of $\bar{X}$ is equal to $\sqrt{p(1-p)/N}$
- Subtracting a constant does not add any variability, so it does not affect the standard error.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. The standard error of is equal to the square root of the spread divided by the sample size."
msg2 = "Try again. Subtracting 1 does not affect the standard error."
msg3 = "Nice work!"
msg4 = "Try again. Pay attention to the algebra on the first line."
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## Exercise 9. Standard error of the spread

```yaml
type: NormalExercise
key: 647d48fd7c
lang: r
xp: 100
skills:
  - 1
```

Say the actual proportion of Democratic voters is $p=0.45$. In this case, the Republican party is winning by a relatively large margin of $d= -0.1$, or a 10% margin of victory. What is the standard error of the spread $2\bar{X}-1$ in this case?

`@instructions`
- Use the `sqrt` function to calculate the standard error of the spread $2\bar{X}-1$.

`@hint`
- In this case, $\bar{X}$ is equal to $p$.
- Derive the standard error of the spread, $2\bar{X}-1$, knowing that $SE[\bar{X]} = \sqrt{p(1-p)/N}$.
- Subtracting a constant does not add any variability, so it does not affect the standard error.

`@pre_exercise_code`
```{r}
#no pec
```

`@sample_code`
```{r}
# `N` represents the number of people polled
N <- 25

# `p` represents the proportion of Democratic voters
p <- 0.45

# Calculate the standard error of the spread. Print this value to the console.



```

`@solution`
```{r}
# `N` represents the number of people polled
N <- 25

# `p` represents the proportion of Democratic voters
p <- 0.45

# Calculate the standard error of the spread. Print this value to the console.
2*sqrt(p*(1-p)/N)


```

`@sct`
```{r}
test_error()
test_function("sqrt", args = "x", eval=NA,
              not_called_msg = "Make sure you are using the `sqrt` function to calculate the standard error.")
test_output_contains("0.1989975", incorrect_msg = "You are not providing a calculation that gives the correct answer. Make sure you are using the formula we derived to calculate the standard error of the spread.")
success_msg("Great work! Let's work on a similar problem.")
```

---

## Exercise 10. Sample size

```yaml
type: MultipleChoiceExercise
key: 80865a3b9e
lang: r
xp: 50
skills:
  - 1
```

So far we have said that the difference between the proportion of Democratic voters and Republican voters is about 10% and that the standard error of this spread is about 0.2 when $N=25$. Select the statement that explains why this sample size is sufficient or not.

`@possible_answers`
- This sample size is sufficient because the expected value of our estimate $2\bar{X}-1$ is $d$ so our prediction will be right on.
- This sample size is too small because the standard error is larger than the spread.
- This sample size is sufficient because the standard error of about 0.2 is much smaller than the spread of 10%.
- Without knowing `p`, we have no way of knowing that increasing our sample size would actually improve our standard error.

`@hint`
- A standard error of 0.2 means the proportion of Democratic voters may vary from the estimated value by plus or minus 0.2.

`@pre_exercise_code`
```{r}

```

`@sct`
```{r}
msg1 = "Try again. Consider the formula used to calculate standard error. How can standard error be reduced?"
msg2 = "Great work!"
msg3 = "Try again. The spread of 10% means that the proportions differ by 0.1."
msg4 = "Try again. Standard error becomes smaller as you increase the sample size."
test_mc(correct = 2, feedback_msgs = c(msg1,msg2,msg3,msg4))
```

---

## End of Assessment

```yaml
type: PureMultipleChoiceExercise
key: df5bff3f64
xp: 50
```

This is the end of the programming assignment for this section. Please DO NOT click through to additional assessments from this page. If you do click through, your scores may NOT be recorded.

Click "Got it!" and submit to get the "points" for this question.

You can close this window and return to <a href="https://www.edx.org/course/data-science-inference-and-modeling">Data Science: Inference</a>.

`@hint`
Continue on with the course within the edX platform.

`@possible_answers`
- [Got it!]

`@feedback`
- Great!
