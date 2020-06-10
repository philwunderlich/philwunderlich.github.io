<!-- .slide: data-background="#3cdbd3ff" -->

## Learning Module 7.2: Correlation coefficient


---

### Linear relationships beween two variables

- <!-- .element class="fragment" -->When describing relationships between two continuous / metric variables, we are often interested in their linear relationship. 
- <!-- .element class="fragment" -->Linear relationship / association means, that with each increase on one variable, the other variable changes proportionally.

---

### Perfect linear relationship

```stata
twoway (lfit income school) if income < 10000
```
<!-- .element class="fragment" -->
![perfect linear relationship](img/line_income_school.svg)<!-- .element class="fragment" -->

---

### Strength of association

```stata
twoway (scatter income school) (lfit income school) if income < 10000

```
<!-- .element class="fragment" -->

![scatter with regression](img/income_school.svg)<!-- .element class="fragment" -->

Note:

- most relationships between two vars are not perfect. One variable may only have a partial effect on another.
    - Variation on other variables causes further *variance*.
- Additionally, there might be measurement error causing further variation.
- Point out differences between reg line and values.
- we need a measure to 


---

### Joint Variability

- How can we quantify linear relationships? <!-- .element class="fragment" -->
- The variance of one variable is defined as the squared deviation of values from the mean: <!-- .element class="fragment" -->

$Var(X)=\frac{\sum{(x-\bar{x})^2}}{n-1}$  <!-- .element class="fragment" style="text-align:center" -->


- the covariance on the other hand tells us to which degree both variables vary jointly. <!-- .element class="fragment" -->

$Cov(X,Y)=\frac{1}{n}\sum\limits_{i=1}^n(x_i-\bar{x})(y_i-\bar{y})$  <!-- .element class="fragment" style="text-align:center" -->

---

### Correlation as a standardized measure

- <!-- .element class="fragment" -->just as we use the sqaure root of the variance to get the standard deviation, we can standardize the covariance to get the correlation coefficient $r$.

$r=\frac{Cov(X,Y)}{s_xs_y}$ <!-- .element class="fragment" style="text-align:center" -->


---

### Interpreting the Correlation coefficient

- <!-- .element class="fragment" -->$r$ tells us the <em>strength</em> and <em>direction</em> of linear relationships    
- range: $-1 \leq r \leq 1$ <!-- .element class="fragment" -->
 
Interpretation:<!-- .element class="fragment" -->

- $r>0$ signifies a positive linear relationship.<!-- .element class="fragment" -->
- $r<0$ signifies a negative linear relationship<!-- .element class="fragment" -->
- $r=0$ : no linear relationship<!-- .element class="fragment" -->

strength "rule of thumb": weak: 0.2 - 0.4 | moderate: 0.4 - 0.6 | strong: 0.6 - 0.8 <!-- .element class="fragment" -->

---

### Visualizing Correlation


![](https://upload.wikimedia.org/wikipedia/commons/8/83/Pearson_Correlation_Coefficient_and_associated_scatterplots.png)

<span style="font-size: 0.5em">source: <a href="https://statistics.laerd.com/statistical-guides/pearson-correlation-coefficient-statistical-guide.php">https://statistics.laerd.com/statistical-guides/pearson-correlation-coefficient-statistical-guide.php</a></span>


---


### Significance test of the correlation

- <!-- .element class="fragment" -->We can use a t-statistic to test the H0 that the correlation actually is 0. (Alternative Hypothesis: $r\neq0$)

$t = r \sqrt{\frac{n-2}{1-r^2}}$ <!-- .element class="fragment" -->

- <!-- .element class="fragment" -->Assumption: Both variables need to be approximately normally distributed.

Note:
- STATA will do this for you!

---

### `pwcorr` - Command

```stata
pwcorr income school
```
<!-- .element class="fragment" -->
```
             |   income   school
-------------+------------------
      income |   1.0000 
      school |   0.2810   1.0000 
```
<!-- .element class="fragment" -->

---

### Correlation matrix & Observations


```stata
pwcorr income school age, obs
```
<!-- .element class="fragment" -->
```
             |   income   school      age
-------------+---------------------------
      income |   1.0000 
             |     2914
             |
      school |   0.2810   1.0000 
             |     1427     1699
             |
         age |   0.0773  -0.2108   1.0000 
             |     2913     1698     3468
             |
```
<!-- .element class="fragment" -->

---

### Significance test

```stata
pwcorr income school, sig
```
<!-- .element class="fragment" -->
```
             |   income   school
-------------+------------------
      income |   1.0000 
             |
             |
      school |   0.2810   1.0000 
             |   0.0000
             |
```
<!-- .element class="fragment" -->

---

### Example in Stata

---

## Task 7.2

- Calculate and interpret the correlation coefficient for all pairs of metric/continuous variables in your analysis. 
    - If you only have one metric/continuous variable in your analysis so far, find another on, that might be related to your dependent variable, or use one of the example variables.
- Is there a linear association between respondent's age and the age of their partner? (1) Identify and recode the relevant variables. (2) Plot the relationship between both variables. (3) Calculate and interpret the correlation coefficient. (4) Interpret the number of observations the correlation coefficient is based on. 
