# Session 5: <br> Basic Plots
## Data Analysis Using Stata

Summer 2020 | MA Sociology | FU Berlin


---

## Learning Goals for Session 5

Drawing plots with STATA!<!-- .element: class="fragment" -->

- 5.1. Univariate Plots <!-- .element: class="fragment" -->
- 5.2. Combining and Exporting Plots <!-- .element: class="fragment" -->
- 5.3. Bivariate Plots <!-- .element: class="fragment" -->

---

## Learning Module 5.1

1. When and why to use plots?
   - What to avoid...
2. Univariate Plots:
  - Histograms and density plots
  - Box plots
  - Bar plots for categorical data

---

## 1. Why to use plots?

----

## So why?

- Often, plots are easier to grasp than numbers!
  - Visualize <span class="fragment bold">distributions</span>
  - Visualize  <span class="fragment bold">frequencies</span> and <span class="fragment bold">proportions</span>.
  - Visualize <span class="fragment bold">relationships</span> between two or more variables (We will see this in 5.3).
- Exploration: Take a look at the data!<!-- .element: class="fragment" -->

----

## What to avoid?

- Unclear or distorted scales (axis break, truncation, zooming in etc.)<!-- .element: class="fragment" -->
- 3D effects and the like<!-- .element: class="fragment" -->
- Pie charts!<!-- .element: class="fragment" -->
- Excessive use of graphs<!-- .element: class="fragment" -->


----

### What is wrong here?

![truncated](img/truncated_hhinc_gender.svg)

----

### BETTER!

![truncated](img/untruncated_hhinc_gender.svg)

----

### 3D Graphs

- There are no 3D Graphs in STATA … for a good reason.

----

### Evil 3D Pie Charts


<div class="container" data-markdown>

![3d-pie](img/Misleading_Pie_Chart.png) <!-- .element: class="col" height="300" -->
![pie](img/Sample_Pie_Chart.png)<!-- .element: class="col" height="300" -->

</div>


---

## 2. Univariate Plots

---

### Reminder: Variable Types

- Continuous variables: Can take arbitrary values in a certain range. (interval or ratio scale)<!-- .element: class="fragment" -->
- Categorical variables: Can only take certain values (ordinal or nominal scale)<!-- .element: class="fragment" -->

---

## Histograms

- Histograms give us a very intuitive overview over the<!-- .element: class="fragment" --> <span class="fragment bold">distribution</span> of continuous variables.
- They draw columns representing how often a certain value or range of values is present in the data.<!-- .element: class="fragment" -->

----

<video controls class="stretch">
    <source src="img/output.ogv" type="video/ogg">
    <source src="img/output.webm" type="video/webm">
</video>

----

### Drawing a histogram

<!-- using the `histogram` command, we can create a simple histogram. -->

<div class="fragment fade-in-then-semi-out" data-markdown>

```stata
histogram age
```

</div>

<div class="fragment" data-markdown>

```
(bin=35, start=18, width=2.0857143)
```
![](img/hist_age_den.svg)

</div>

----

### Density vs. Frequency

- by default, STATA plots density histograms, meaning that all columns would add up to a total of 1.0.<!-- .element: class="fragment" -->
- We can also ask STATA to use absolute frequencies (numbers of observations per bin).<!-- .element: class="fragment" -->

----

#### Frequency

```stata
hist age, frequency
```
<!-- .element: class="fragment fade-in-then-semi-out" -->


![](img/hist_age_fre.svg) <!-- .element: width="500" class="fragment" -->

----

### Bins

STATA choses the number of "bins" or columns automatically.

<div class="fragment" data-markdown>

```stata
hist age
```

```
(bin=35, start=18, width=2.0857143)
```
![](img/hist_age_den .svg) <!-- .element: width="400" -->
</div>

Note:
 The property "width=2.2" in the output above means that each bin represents 2.2 years. `start` tells us the value of the first bin.

----

### Changing Bins

- The option <!-- .element: class="fragment" data-fragment-index="1" -->`discrete`<!-- .element: class="fragment" data-fragment-index="1" --> tells STATA to create one bin per category (here: year)
- The option <!-- .element: class="fragment" data-fragment-index="2" -->`bin(#)`<!-- .element: class="fragment" data-fragment-index="2" --> allows us to specify the number of bins ourselves.
- With  <!-- .element: class="fragment" data-fragment-index="3" --> `width(#)`<!-- .element: class="fragment" data-fragment-index="3" --> we may specify the range covered by one bin.

----

#### Discrete

```stata
hist age, discrete
```
<!-- .element: class="fragment fade-in-then-semi-out" -->

![](img/hist_age_discrete.svg) <!-- .element: class="fragment" -->


----

#### Fixed number of bins

```stata
hist age, bin(10)
```
<!-- .element: class="fragment fade-in-then-semi-out" -->

![bins](img/hist_age_bins.svg)<!-- .element: class="fragment" -->

----

#### Fixed width


```stata
hist age, width(5)
```
<!-- .element: class="fragment fade-in-then-semi-out" -->

![widths](img/hist_age_width.svg)<!-- .element: class="fragment" -->

----

### Vertical Lines
- using the `xline()` option, we can add vertical lines at a specific value.
- for example, we can plot the mean of our variable.<!-- .element: class="fragment" -->

<!-- TODO move to STATA for this example! -->

```stata
*** Adding a vertical mean line ***
summarize age // get the mean
```
<!-- .element: class="fragment" -->

```
    Variable |        Obs        Mean    Std. Dev.       Min        Max
-------------+---------------------------------------------------------
         age |      3,468    49.44031    17.50623         18         91
```
<!-- .element: class="fragment" -->

```stata
local age_mean = r(mean) // save the mean to a local macro
hist age, xline(`age_mean') // draw the graph
```
<!-- .element: class="fragment" -->

Note:
- `return list` to display all stored stats.

----

![](img/hist_meanline.svg)<!-- .element: width="650" -->

---

## The normal distribution

- Often we are interested in whether our data is normally distributed.
- Many natural phenomena that are produced by chance follow a normal distribution (e.g. height of people in a group)
- Some statistical tests assume an approximate normal distribution

[Video: Normal distribution](https://www.youtube.com/watch?v=iYiOVISWXS4)

[Video: Normal distribuion in real life](https://www.youtube.com/watch?v=RKdB1d5-OE0)

----

### The normal distribution

![normal distributions](img/normal_distributions.svg)<!-- .element: class="" width="650" -->


<!-- ----

### The normal distribution&nbsp;

- The reason for the prevalence of the normal distribution is in the central limit theorem. -->

----

### Histogram with normal distribution

```stata
hist age, normal
```


---

### Kernel Density Plots

![KDE](img/Comparison_of_1D_histogram_and_KDE.png)

<div style="font-size:1rem">
By <a href="https://en.wikipedia.org/wiki/User:Drleft" class="extiw" title="wikipedia:User:Drleft">Drleft</a> at <a href="https://en.wikipedia.org/wiki/" class="extiw" title="wikipedia:">English Q52</a>, <a href="https://creativecommons.org/licenses/by-sa/3.0" title="Creative Commons Attribution-Share Alike 3.0">CC BY-SA 3.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=57332968">Link</a>
</div>

---

```stata
kdensity age
```
![](img/kdernsity_age.svg)<!-- .element: width="650" -->




## Categorical Variables: <br> Bar plots

- A simple way to plot categorical variables.
- Bar plots display a variables mean by default.
- They can divide bars across categories of a variable.


---

## Drawing Bar Plots

Commands for bar plots.

```stata
graph bar varname
graph bar, over(varname)
```

<!-- example in STATA: Yoga! -->

---


## Task 5.1

<div style="font-size:1.5rem">
Please open a do file and prepare the following variables: Household Income, Gender, Age, Employment Status.

---
1. Create a histogram for household income.
    - Set the bin width, so that one column of the histogram represents 2500€ of income.
    - Plot the actual frequencies of respondents per category on the x axis.
2. Create a second histogram in which you ignore cases with extremely high household incomes of above 40.000 €. Adjust the bin width in a sensible way.
    - does the household income follow an approximate normal distribution? Draw a normal density line to assess!
    - Add a line for the median. How does the median behave as compared to the mean?
3. Create a box plot that illustrates the distribution of the household income.
    - Make an informed decision where to cut off the box plot to keep outliers but exclude extreme outliers that distort the graphical representation.
4. Draw a Bar plot for all categories of the employment status.

(Remark: Excluding outliers from a graphic is a measure that should be used with care, as pointed out before !</div>
