# Session 5: <br> Basic Plots
## Data Analysis Using Stata

Summer 2020 | MA Sociology | FU Berlin


---

## Learning Module 5.3

Relationships between variables:

1. Box Plots across groups
2. Bar Plots across groups
3. Scatter Plots and Smoothers

---

## Box Plots Across Groups

- Using the the `over()` option, we can use box plots to compare distributions of two subsamples.

```stata
graph box continuous_var, over(categorical_var)
```
<!-- .element class="fragment"-->

---

## Bar Plots across groups

- Bar plots can be used to compare means of a continuous variable across groups.
- They can also be used to assess relationships between two categorical variables.

```stata
graph bar continuous_var, over(categorical_var)
graph bar, over(categorical_var1) over(categorical_var2)
```
<!-- .element class="fragment"-->

---

## Scatter Plots and Smoothers

- Scatter plots are useful to assess the relationship between to continuous variables.
- If variables have only few categories, we can use `jitter()` to introduce random noise.
- A lowess smoother draws a locally weighed regression line into the scatterplot that visualizes the shape of a relationship.

```stata
scatter continuous_var1 continuous_var1, jitter(#)
lowess continuous_var1 continuous_var1, jitter(#)
```
<!-- .element class="fragment"-->

---


## Task 5.3

<div style="font-size:1.5rem">
You may continue using your do-file from LM 5.1 and 5.2.

---
1. Use a boxplot to compare the distribution of income across gender
2. Use a bar plot to compare the employment status across gender
3. Draw a scatter plot to assess the relationship between age and income. Eliminate outliers above 10.000€. Add a lowess smoother to describe the shape of the relationship. What is the shape of the relationship?

</div>
