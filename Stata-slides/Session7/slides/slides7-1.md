<!-- .slide: data-background="#7dce82ff" -->

#7dce82ff
# SESSION 7: <br> DESCRIPTIVE INFERENCE&nbsp;2
## Data Analysis using Stata
Summer 2020 | MA Sociology | FU Berlin

----

## Learning Goals Session 7

- <!-- .element class="fragment" -->7.1 Testing relationship between two categorical variables
- <!-- .element class="fragment" -->7.2 Testing relationship between two continuous variables

---

### Recap: Significance tests

1. <!-- .element class="fragment" -->Formulate Hypotheses. (e.g. H0: There is no difference in means in the population)
2. <!-- .element class="fragment" -->Calculating a test statistic for the observed values under the assumption of H0. (e.g. t-value for difference in means)
3. <!-- .element class="fragment" -->Calculating p-values for the test statistic. → significance?
4. <!-- .element class="fragment" -->Calculate effect size (e.g. Cohen's d)

---

## Learning Module 7.1: $\chi^2$-test for categorical variables

- <!-- .element class="fragment" -->Are to categorical variables independent?

---

### Independent? Parental education and yoga

We can ask stata to show us the *observed frequencies* of each combination of both variables.

```stata
tab pedu_d yoga_d
```
<!-- .element class="fragment" -->
```
Parent has |
  tertiary |    Practices yoga
    degree |        no        yes |     Total
-----------+----------------------+----------
        no |     1,511        630 |     2,141 
       yes |       548        469 |     1,017 
-----------+----------------------+----------
     Total |     2,059      1,099 |     3,158 
```
<!-- .element class="fragment" -->

----

#### row percentages

Are the observed frequencies distributed the same way as the marginal distributions? <!-- .element class="fragment" -->

```stata
tab pedu_d yoga_d, row
```
<!-- .element class="fragment" -->
```
Parent has |
  tertiary |    Practices yoga
    degree |        no        yes |     Total
-----------+----------------------+----------
        no |     1,511        630 |     2,141 
           |     70.57      29.43 |    100.00 
-----------+----------------------+----------
       yes |       548        469 |     1,017 
           |     53.88      46.12 |    100.00 
-----------+----------------------+----------
     Total |     2,059      1,099 |     3,158 
           |     65.20      34.80 |    100.00 
```
<!-- .element class="fragment" -->

---

### Expected frequencies

But which frequencies would we expect if variables were independent?<!-- .element class="fragment" -->

```
Parent has |
  tertiary |    Practices yoga
    degree |        no        yes |     Total
-----------+----------------------+----------
        no |         ?          ? |     2,141 
       yes |         ?          ? |     1,017 
-----------+----------------------+----------
     Total |     2,059      1,099 |     3,158 
```
<!-- .element class="fragment" -->

<br>

$\text{Expected frequency} = \frac{\text{row total} * \text{column total}}{\text{total}}$ <!-- .element style="text-align:center" class="fragment" -->

---

#### Example in Stata

---

### $\chi^2$ test-statistic

Based on the cross table, we can calculate the test-statistic under the assumption of independence (H0) <!-- .element class="fragment" -->

$\chi^2=\sum\limits_{\text{Kategorie}}\frac{(\text{observed frequency}_i - \text{expected frequency}_i)^2}{\text{expected frequency}_i}$ <!-- .element style="text-align:center" class="fragment" -->

---

#### Example in Stata

---


### $\chi^2$-distribution

The $\chi^2$-distribution and critical p-values are known <!-- .element class="fragment" -->


![chi2.png](img/chi2.png)<!-- .element class="fragment" -->

The distribution depends on degrees of freedom: 
$df=(rows -1)*(columns -1)$<!-- .element class="fragment" --> 

Note:

- in our example we have df=(2-1)(2-1)=1

---

### Critical Values


![chi2_table.png](img/chi2_table.png)



---

### $\chi^2$-test in Stata

Stata allows us to calculate exact p-values for our $\chi^2$ and df without the use of a table.
<!-- .element class="fragment" -->

```stata
tab pedu_d yoga_d, chi2
```
<!-- .element class="fragment" -->
```
Parent has |
  tertiary |    Practices yoga
    degree |        no        yes |     Total
-----------+----------------------+----------
        no |     1,511        630 |     2,141 
       yes |       548        469 |     1,017 
-----------+----------------------+----------
     Total |     2,059      1,099 |     3,158 

          Pearson chi2(1) =  84.6517   Pr = 0.000
```
<!-- .element class="fragment" -->

---

### non-binary variables

$\chi^2$-test works the same way for variables with more than two categories:<!-- .element class="fragment" -->

```stata
tab pedu yoga, chi2
```
<!-- .element class="fragment" -->

```
                      | Respondent does Yoga in leisure
                      |               time
   Parental education | Every day  Once a mo      Never |     Total
----------------------+---------------------------------+----------
No parent has a terti |       313        317      1,511 |     2,141 
One parent has a tert |       139        185        392 |       716 
Both parents have a t |        60         85        156 |       301 
----------------------+---------------------------------+----------
                Total |       512        587      2,059 |     3,158 

          Pearson chi2(4) =  91.9883   Pr = 0.000
```
<!-- .element class="fragment" -->

---

### Effect size: Cramer's V

- <!-- .element class="fragment" -->Represents the effect size between two categorical variables based on Chi2-statistics.
- <!-- .element class="fragment" -->$0\leq V \leq 1$

$V= \frac{\chi^2}{n(min(rows-1,columns-1))}$ <!-- .element style="text-align:center" class="fragment" -->

- <!-- .element class="fragment" -->Remember: $\chi^2$-tests only test the significane of a dependence, while Cramer's V is a measure of effect size: Neither tell us anything about the "shape" or "direction" of a relationship. 

---

### Cramer's V in STATA

```stata
tab yoga_d pedu_d, chi2 V
```
<!-- .element class="fragment" -->
```
           |  Parent has tertiary
 Practices |        degree
      yoga |        no        yes |     Total
-----------+----------------------+----------
        no |     1,511        548 |     2,059 
       yes |       630        469 |     1,099 
-----------+----------------------+----------
     Total |     2,141      1,017 |     3,158 
     
          Pearson chi2(1) =  84.6517   Pr = 0.000
               Cramér's V =   0.1637
```
<!-- .element class="fragment" -->

Note:

Effect sizes are difficult to assess. 0.1 small 0.3 moderate 0.5 large (depends on nr. of categories.)

---

## Task 7.1

- Assess whether Employment status and gender are independent.
    - Interpret the results of the $\chi^2$-test both in terms of significance, effect size.
    - If you find a relationship between both variables, try to interpret it.