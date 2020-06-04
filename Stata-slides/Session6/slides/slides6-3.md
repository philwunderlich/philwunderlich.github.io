<!-- .slide: data-background="#E9BBAA" data-transition="linear" -->

## Learning Module 6.3: t-test

- Student's t-distribution
- Conduct a two sample t-test in STATA


---

### Significance of mean differences.

- Now, we want to find out, whether the difference in means across two groups is statistically significant.<!-- .element class="fragment"-->
- Remember, this only means whether we can assume a mean difference in the population based on our sample.<!-- .element class="fragment"-->

![income-gender.svg](img/income-gender.svg)<!-- .element class="fragment" style="width:450" -->


----

### t-test

- <!-- .element class="fragment"-->The sampling distribution of mean differences follows a Student's t-distribution.
- <!-- .element class="fragment"-->Degrees of Freedom affect the shape of the distribution $df=N-1$ 
- <!-- .element class="fragment"-->For $N>30$ the t-distribution converges towards a normal distribution.
    - <!-- .element class="fragment"-->Thus, for large samples, z-test and t-test converge.

----

### t-distribution

![t-distribution](img/t-distr.svg)


Note:
- Before we assessed whether 
- We want to compare the means of Group A and Group B.
    - note: comparing means across two groups means testing the association of a binary, categorical variable and a metric variable.
- Our Null-hypothesis: _The difference between the means of group A and group B is zero_.
- We need to estimate the standard errors of the mean difference.
- The sampling distribution of mean differences is not the normal distribution but the "student-t-distribution".



---


### t-test Example: comparison of income across gender

- H0: There is no mean difference of income across gender.
- H1 (undirected): There is a mean difference of income across gender.

---


### t-test command


```stata
ttest income, by(gender) unequal
```

```[1-9|10-13|14-17]
Two-sample t test with unequal variances
------------------------------------------------------------------------------
   Group |     Obs        Mean    Std. Err.   Std. Dev.   [95% Conf. Interval]
---------+--------------------------------------------------------------------
     Men |   1,468    1833.628    50.54484      1936.6     1734.48    1932.776
   Women |   1,446    1050.256     23.0541    876.6623    1005.033    1095.479
---------+--------------------------------------------------------------------
combined |   2,914    1444.899    28.83832    1556.735    1388.354    1501.445
---------+--------------------------------------------------------------------
    diff |            783.3722    55.55423                674.4236    892.3208
------------------------------------------------------------------------------
    diff = mean(Men) - mean(Women)                                t =  14.1010
Ho: diff = 0                     Satterthwaite's degrees of freedom =  2050.77

    Ha: diff < 0                 Ha: diff != 0                 Ha: diff > 0
 Pr(T < t) = 1.0000         Pr(|T| > |t|) = 0.0000          Pr(T > t) = 0.0000


```
<!-- .element class="fragment"-->

---


## Significance and Effect Size

- As we learnd before, significance means that we can assume an effect we measure in our sample is actually present in the population with e.g $\alpha=0.05$. <!-- .element class="fragment"-->
- here, this means we have to rejext H0, that states, there is no mean difference across groups in the population.
- Using a large sample, we might find a significant difference that is so small, that it is practically meaningless.<!-- .element class="fragment"-->

Note:
It is easy to imagine: If our sample size approaches our population size, we can be sure that every difference in mean income across gender we find is actually present in the population, even if this difference was only 10 cents and thus rather unimportant.

---


## Cohen's d

- <!-- .element class="fragment"--> The mean difference is the effect size in this case. But it is dependent of the scale (e.g. income, life satisfaction...)
- <!-- .element class="fragment"--> The mean difference can be standardized using the standard-deviation "Cohen's d"


$d=\frac{\bar{x_1}-\bar{x_2}}{s}$<!-- .element class="fragment" style="text-align:center; font-size:1.8em" -->

- <!-- .element class="fragment"--> 0.2: small effect, 0.5: medium effect, 0.8 large effect.
    - 	<!-- .element class="fragment"-->Effect sizes are context dependent (sample size, type of effect)!

Note:

- verifying a physical law, we would expect different effect sizes as compared to psyhcological constructs.

----

### Cohen's d

```stata
ssc install cohend // install command
cohend income gender
```
```
(1) Cohen's d and (2) Cohen's d corrected for uneven groups

(1) .52002118
(2) .520036
```
<!-- .element class="fragment"-->

---


### Task

<div data-markdown style="font-size:1.8rem">

- Please conduct a t-test on the variables you selected for your analysis.
    - In case you have a non-dichotomous explanatory variable (i.e. more than two categories), you may need to dichotomize your IV.
    - Example (also in the session do-file):

```stata [1-2|3-4|5-8|9]
capture drop income_d //new variable
gen income_d =.
replace income_d=0 if income <= 1450 // low category (1450 and below)
replace income_d=1 if income > 1450 // high category
capture label drop income_d_lab //labels
lab def income_d_lab 0"low" 1"high"
lab var income_d "Income high"
lab val income_d income_d_lab
bys income_d: sum income // check
```

- In addition, conduct a t-test to test whether life satisfaction differs across genders.
    - interpret the results in terms of significance and effect size.
</div>