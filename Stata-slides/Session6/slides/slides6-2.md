<!-- .slide: data-background="var(--puce)" data-transition="linear" -->

## Learning Module 6.2: Descriptive Inference

- How can we infer properties of the population from our sample?

Note:
- Don't be afraid of the math in this LM.
- You don't need to memorize formulas. Instead it is about understanding the logic of significance tests and confidence intervals.

---

## Descriptive Inference

- <!-- .element class="fragment"--> The population refers to all individuals (or cases) we are interested in.
- <!-- .element class="fragment"-->In survey research, we do not monitor the whole population. Instead we draw random samples from the population.
    - <!-- .element class="fragment"-->This means, that all units of observation have the same probabilty of ending up in our sample.
- <!-- .element class="fragment"--> Descrictive inference is needed to generalize findings from a sample to the population with confidence.

<!-- KK(211): Nachbauen von Zufallsprozessen -->

---


### Central limit Theorem

- <!-- .element class="fragment"-->How can we know the true mean of our population, if we only know the mean of a random sample?
- <!-- .element class="fragment"-->We need to know how our sample mean relates to the population mean!
- <!-- .element class="fragment"-->This is where the Central Limit Theorem can help us.

----

### Example: Sampling Distribution

- Let's find out what happens if we draw samples from a population!
- We can draw random samples by creating a random variable, sorting the data according to this variable and using an if-condition

```stata
capture drop randomnumber
gen randomnumber = runiform()
sum income if randomnumber <=0.001
```

----

### Example: Sampling Distribution

- For the following Animation, I created a "for loop" to draw 200 random samples of 30 observations each from the Allbus dataset.
    - In this case the whole Allbus is our population.
- Then, the mean of each sample is plotted in a histogram.

```stata 
generate smplmeans = .
sum age
local age_mean=r(mean)
  forvalues i = 1/200 {
  summarize age if runiform() < (30/_N), meanonly
  replace smplmeans = r(mean) in `i'
  hist smplmeans, width(2) start(18) yscale(range(0 0.2)) xscale(range(18 90)) xlab(20(10)90) ylab(0(0.05)0.2) name(smpl, replace) xline(`age_mean')
  }
```

----

### Example: Sampling Distribution

<video controls class="stretch">
    <source src="img/age_smplmeans_distr.mp4" type="video/mp4">
</video>

Note:
Example!
In STATA we can simulate the distinction between population and sample by drawing a sub-sample from our data-set

[animation sampling distribution](http://onlinestatbook.com/stat_sim/sampling_dist/)

----

### Central limit Theorem


- If we draw infinite random samples from a population, the distribution of sample means approaches a normal distribution around the true population mean ($\mu$) and a standard error of $\frac{\sigma}{\sqrt{n}}$ 


The sampling distribution of the mean is defined as a normal distribution with two parameters: <!-- .element class="fragment"-->

$N(\mu,\frac{\sigma}{\sqrt{n}})$<!-- .element class="fragment" style="text-align:center"-->

$\mu$ = population mean<!-- .element class="fragment"-->
$\sigma$ = population standard deviation<!-- .element class="fragment"-->

- There are different sampling distributions for different point estimates, this one refers to sample means.<!-- .element class="fragment"-->

---

### Standard Error

- <!-- .element class="fragment"-->The Standard Error (S.E.) is the Standard Deviation of the Sampling Distribution.
- <!-- .element class="fragment"-->It can indicate the average distance of sample means from the true population mean. (Standard Error of the Mean)
- <!-- .element class="fragment"-->The S.E. is crucial to determine how efficient our estimation of the population mean is.

----

### Standard Error Estimation

As we have seen above, the S.E. is defined as follows:

$S.E.=\frac{\sigma}{\sqrt{n}}$

Since we cannot know $\sigma$, we estimate the S.E. using the standard deviation of our sample.:

$S.E.(\bar{X})=\frac{SD(X)}{\sqrt{n}}$

Note:

- we can only do this for large samples.
- move to STATA!

---

### `mean`-command

Stata helps us and calculates the S.E. of the mean for us using `mean`.

```stata
mean income
```
<!-- .element class="fragment" -->

```
Mean estimation                   Number of obs   =      2,914

--------------------------------------------------------------
             |       Mean   Std. Err.     [95% Conf. Interval]
-------------+------------------------------------------------
      income |   1444.899   28.83832      1388.354    1501.445
--------------------------------------------------------------
```
<!-- .element class="fragment" -->


---

### Hypothetical Sampling Distribution

Using the S.E. and the sample mean $\bar{X}$ as estimates for the true mean of all samples ($\mu$) and the sample distribution standard deviation ($\sigma$), we can draw the hypothetical sampling distribution.<!-- .element class="fragment" -->

The normal density function of is defined as follows:<!-- .element class="fragment" -->

$f(x) = \frac{1}{\sqrt{2\pi\sigma^2}}*e^{-\frac{(x-\mu)^2}{2\sigma^2}}$<!-- .element class="fragment" -->

```stata 
twoway function fx = 1/sqrt(2*_pi* >>S.E.<< ^2)* ///
	exp((-(x->>MEAN<<)^2)/(2*>>S.E.<<^2)), xline(>>MEAN<<)
```
<!-- .element class="fragment" -->

Note:

- Back to Stata


---

### Using the Standard error

- Knowing the sampling distribution and in particular the standard error, we can:<!-- .element class="fragment" -->
    1. Compute Confidence Intervals: In which range of values can we expect our true population mean?<!-- .element class="fragment" -->
    2. Execute Tests of Significance: Is a certain value significantly different from what we would expect in H0?<!-- .element class="fragment" -->

---

### Confidence Intervals

- Confidence Intervals (CI) are intervals that are calculated in such a way that there is a fixed probability that they contain an actual value (e.g. the mean)<!-- .element class="fragment" -->
- For a normaldensity distribution as plotted before, we know the critical values of the CI for a given confidence level:<!-- .element class="fragment" -->

lower bound: $\hat{\mu} - 1.96 * \hat{\sigma}$ <!-- .element class="fragment" style="text-align:center"-->

upper bound: $\hat{\mu} + 1.96 * \hat{\sigma}$ <!-- .element class="fragment" style="text-align:center"-->

- There is a 95% confidence that a CI calculated this way covers our true population mean ($\mu$).<!-- .element class="fragment" -->

----

### Example in STATA

	

---

### Tests of significance

- Tests of significance are hypothesis tests.<!-- .element class="fragment" -->
- We specify a significance level $\alpha = 0.05$ below which we have to reject H0.<!-- .element class="fragment" -->
    - This means, our probability of falsely rejecting H0 (Type I error) should only be 0.05<!-- .element class="fragment" -->
- Next, we calculate a test-statistic for the parameter we are interested in, based on the assumption that the H0 is true.<!-- .element class="fragment" -->
    - The probability with which this test value or a more extreme one could occur is called "p-value".<!-- .element class="fragment" -->
    - If the p-value is smaller than our $\alpha = 0.05$ significance level, we have to reject the H0.<!-- .element class="fragment" -->


----

### Tests of significance

- <!-- .element class="fragment" -->The mean for income in our sample is 1444,9 €.
- <!-- .element class="fragment" -->We know from literature that the true population mean should be 1500€ (H0)
- <!-- .element class="fragment" -->With which probability $p(\bar{X}=1444,9 | H_0)$ could we observe the sample mean 1444,9 if the H0 was actually true?

----

### z-test

- p-values for a standard normal distribution (or z-distribution) with a mean of $\mu=0$ and a standard deviation of $\sigma=1$ are known.
- e.g. $Pr(-1.96=>z>=1.96)=0.05$
    - This is the same critical value we used for the CI!
    - You can use the `display normal()` command to calculate p-valu es for specific z-values.

---

### z-distribution

![z-distribution](img/zdistr.svg) 

---

### z-test

- No we need to transform our sampling mean to a z-value using the z-statistic: <!-- .element class="fragment" -->

$z=\frac{\bar{X}-\hat{\mu}}{\hat{\sigma}}$ <!-- .element class="fragment" style="text-align:center"-->


Note:
using the formula, every normal distribution can be converted to a standard normal distribution.

----

### Example in STATA


----

### z-test vs. t-test

- In the z-test we conducted, we assumed that the true standard deviation in the population and the standard error of the mean could be estimated by using the sample standard deviation. 
- The t-test does not require this assumption and is preferred in many cases. 

---


## Task

- Calculate the standard error of the mean and the 95% Confidence Interval (CI) for the population mean of the dependend variable of your own analysis "by hand" (i.e. without using the `mean`command)
    - How can the CI be interpreted?
    - use the `mean`command to verify your results.
- Repeat the same procedure for the life-satisfaction variable `sat`