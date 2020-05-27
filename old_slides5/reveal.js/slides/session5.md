

# Session 5: </br> Basic Plots

## Data Analysis using Stata

7.5.19



---

# Learning Goals

1. visualizing distributions of one variable
    2. histograms
    3. box plots
4. visualizing relationships between two variables
    5. box plots by group
    6. scatter plots

---


## Module 5.1
- Univariate Plots
    - Histograms
        - density, frequency, bin width
        - Drawing vertical lines for mean, median etc.
    - twoway plots: histogram || kdensity
    - Exporting to files
    - Box Plots <!-- .element: class="fragment fade-left" data-fragment-index="1" -->
        - What do the boxes tell us? (Median vs. mean)
        - Illustration of outliers in the case of income <!-- .element: class="fragment highlight-blue" data-fragment-index="2" -->
<!-- .slide: data-background="" -->

---

## Module 5.2
- Bivariate Plots
    - Box Plots over groups
    - Bar plots over groups
    - Scatter Plots
        - Jitter to prevent overplotting
    - Twoway Plots
        - kdensity.
        - Lowess Smoother
    - skew and Kurtosis

---

# Module 5.1: <br> Univariate Graphs

---

## Histograms

- Histograms give us a very intuitive overview over the distribution of values.

---

<video controls height="600">
    <source src="slides/output.ogv" type="video/ogg">
    <source src="slides/output.webm" type="video/webm">
</video>

---


- In STATA, histograms plot the density (y-axis) of a specific value or range of values (x-axis). This tells us which proportion of all observations lie within this range of values.

---

### Example

using the `histogram` command, we can create a simple histogram. (short: ` hist`)

```stata
histogram age
```
```
    Variable |        Obs        Mean    Std. Dev.       Min        Max
-------------+---------------------------------------------------------
       hhinc |      2,608    2732.761    2527.943          0      80400
```

---

### Density vs. Frequency
- by default, STATA plots density histograms, meaning that all columns would add up to a total of 1.0.
- We can also ask STATA to use absolute frequencies (numbers of observations per bin).

---

```stata
hist age, frequency
```

![](img/hist_age.svg) <!-- .element: width="500" -->
![](slides/output_2_16.svg) <!-- .element: width="500" -->

---

### bin-width
- STATA choses the number of "bins" or columns automatically. The property "width=2.2" in the output above means that each bin represents 2.2 years. `start` tells us the value of the first bin.
If needed, we can change this behavior.

---

- the option `discrete` tells STATA to create one bin per category (here: year)
- the option `bin()` allows us to specify the number of bins ourselves.
- In the same way, we may change width or start
- with `width()` we may specify the range covered by one bin

---

```stata
hist age, discrete
```
![](img/hist_age_discrete.svg)

---

```stata
hist age, bin(10)
```
![bins](img/hist_age_bins.svg)

---

```stata
hist age, width(5)
```
![widths](img/hist_age_width.svg)

---

### Vertical Lines
- using xline, we can add vertical lines to our plots.
- for example, we can use `summarize` to plot the mean of our variable.


```stata
*** Adding a vertical mean line ***
summarize r_age // get the mean
local r_age_mean = r(mean) // save the mean to a local macro
hist r_age, xline(`r_age_mean') // draw the graph
```

---

## Skew and Kurtosis

---

## Twoway Plots

- Stata offers the possibility to add multiple plots to one coordinate system.
- After the command `graph twoway` two plots can be specified in parentheses

```stata
*** plotting a twoway plot (histogram and kernel density) ***
graph twoway (histogram r_age, discrete) (kdensity r_age)
```

---

## Exporting Graphs

We can export graphs for further usage (saved in the working directory):

```stata
graph export "graph_name.png", replace
```

---

## Box Plots

- A box plot is another way to display a distribution.
- the central horizontal line in the center of the box marks the _median_.
  - As mentioned before, the median is a measure of central tendency that is more robust to outliers compared to the mean
- the bottom of the box represents the 25quantile and the top of the box the 75quantile.
    - 50of all cases lie within the range of the box.
    - These middle 50are the _Inter Quartile Range_ (IQR)
- The "whiskers" indicate the minimum or maximum (up to 1.5 * IQR)
- extreme outliers are indicated by dots.

### Example: Box Plot for the Age of Respondents

```stata
graph box income if income<10000, aspectratio(2) scheme(s2mono)
```

---

# Task 5.1

## histograms

## twoway

## box plot

## export graph

---

# Learning Module 5.2 Bivariate Plots

## the `by` and `over` options

- using the `by` option, we can compare histograms or box plots across groups.

```stata
*** drawing a histogram by sex ***
hist r_age, by(female)
```

---

```stata
*** drawing a box plot over sex ***
graph box r_age, over(female)
```

---

```stata
*** generating a dummy varible for respondents older than 25 ***
capture drop old
gen old=.
replace old=1 if r_age > 25
replace old=0 if r_age <= 25
* creating labels
lab var old "respondents older than 25"
lab def old_lab 1"yes" 0"no"
lab val old old_lab
```


---

```stata
*** drawing the bar graph over sex and over "old" ***
graph bar (mean) income, over(female) over(old)
```

---

## graph editor

https://www.youtube.com/watch?v=17opC4fDeME
