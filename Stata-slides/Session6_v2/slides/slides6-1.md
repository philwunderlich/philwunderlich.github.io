<!-- .slide: data-background="var(--blue-bell)" data-transition="linear" -->

# SESSION 6: <br> DESCRIPTIVE INFERENCE&nbsp;1
## Data Analysis using Stata
Summer 2020 | MA Sociology | FU Berlin


Note:

- Welcome to Session 6 on discrete Inference.

----

<!-- .slide: data-background="var(--blue-bell)" data-transition="linear" -->

## Learning Goals Session 6

- <!-- .element class="fragment" -->6.1 Research Questions and Hypotheses
- <!-- .element class="fragment" -->6.2 What is "Descriptive Inference"
- <!-- .element class="fragment" -->6.3 Compare group means using t-test

Note:

- Learning Goals.
- Using the logic of statistical tests, you can
- Next Session further tests.

----

<!-- .slide: data-background="var(--blue-bell)" data-transition="linear" -->

## Learning Module 6.1: Research Questions

How to formutlate a research question?

- <!-- .element class="fragment" -->In most cases, we are interested in the relationship between two or more variables.
- <!-- .element class="fragment" -->Basic question "What is the relationship between X and Y?"
- <!-- .element class="fragment" -->As we already know, there might be third variables involved.



---

## Task 1

- <!-- .element class="fragment" -->For your own analysis / term paper, please look through the Allbus variables and find a relationship that you want to analyze.
- <!-- .element class="fragment" -->This entails both a dependent variable (DV) and one or more explanatory or independent variables (IV).
- <!-- .element class="fragment" -->Upload a brief draft of your proposal to blackboard.
    - <!-- .element class="fragment" -->This entails a research question, names and types of the respective variables, and preferably a simple conceptual diagram of the hypothesized relationship.


----

### Caution! Variable types

- With the methods we learn in this course, we can only analyze **continuous dependent variables**.
- However, you may analyze categorical variables on 7-point scales or above, as they can be argued to be quasi-continuous. <!-- .element class="fragment" -->


![likert_scale.jpeg](img/likert_scale.jpeg)  <!-- .element class="fragment" -->


- Explanatory variables may be both categorial and continuous.  <!-- .element class="fragment" -->

----

### Example: Research Question

"What is the relationship between gender and income?"

Variables:

- IV: Gender (dichotomous, V81)
- DV: Income (continuous, V417)
- Mediator / Moderatore: e.g University Degree (dichotomous, V96)

----


### Conceptual Models

#### Simple effect <!-- .element class="fragment" -->

![diagram_simple_effect.svg](./img/diagram_simple_effect.png)<!-- .element class="fragment" width="600"-->


#### Moderation / Mediation  <!-- .element class="fragment" -->

![diagram_moderation.svg](img/diagram_moderation.png) <!-- .element class="fragment" width="600"-->

---

<!-- .slide: data-background="var(--blue-bell)" data-transition="linear" -->
## Hypotheses

- After we have formulated a research question, we can derive testable hypotheses.
- Usually, there are two contrasting hypotheses:
    - H0: "X and Y are not related" (null-hypothesis)
    - H1: "X has an influence on Y" (alternative hypothesis)

----

### Example: Hypotheses

- H0: Gender does not have an influence on Income.
- H1: Gender has an influence on income. (undirected hypothesis)

OR:

- H1: Being male increases income on average (directed hypothesis)

----

### Causality

- Some of these hypotheses above imply causality.
- With descriptive inference we can only describe relationships but we cannot determine whether they are causal relationships.


Note:
- We cannot answer questions pertaining to causality. A difference in income across gender does not mean that this difference is *caused* by gender.
- We can, however, ask questions pertaining to certain statistics, differences between groups or even associations of variables in the population.

---

### Hypothesis testing: Error types


[](https://www.youtube.com/watch?v=7mE-K_w1v90)

| Test \ Reality         | H0 is false      | H0 is true       |
|------------------------|:----------------:|:----------------:|
| **We reject H0**       | Correct Decision | *Type I error*   |
| **We don't reject H0** | _Type II Error_  | Correct Decision |

---
- $\alpha :$ Type I error rate (significance level)
- $\beta :$ Type II error rate (significance level)
- when testing hypotheses, we aim to minimize $\alpha$.


----

## Hypothesis testing

- To find out whether variables are related **in our sample**, we could compare means across groups. (e.g. mean income men vs. mean income women)


Note:
But why should we worry about error types, if we can in fact look at the numbers in our sample and see whether there are relationships? Example: Boxplot Income across gender.


----

### Compare Sample Means

```stata
. summarize income if gender==1 // Male
```
<!-- .element class="fragment" -->
```
    Variable |        Obs        Mean    Std. Dev.       Min        Max
-------------+---------------------------------------------------------
      income |      1,468    1833.628      1936.6          0      60000
```
<!-- .element class="fragment" -->

```stata
. summarize income if gender==2 // Female
```
<!-- .element class="fragment" -->
```
    Variable |        Obs        Mean    Std. Dev.       Min        Max
-------------+---------------------------------------------------------
      income |      1,446    1050.256    876.6623          0      17500

```
<!-- .element class="fragment" -->

----

### Compare Sample Means

![income-gender.svg](img/income-gender.svg)




----

<!-- .slide: data-background="var(--middle-blue-green)" data-transition="linear" -->
### But What about the population?

- <!-- .element class="fragment" --> An effect in our sample might be caused by chance.
- <!-- .element class="fragment" -->The true relationship in the population might look completely different.
- <!-- .element class="fragment" -->In order to test hypotheses for our population, we need statistical tests / inferential statistics

[→ Learning Module 6.2](./LM-6-2.html) <!-- .element class="fragment" -->

Note:
Errors occur when we generalize an effect / relationship from our sample to the populaiton.
(this can be 3 slides.)
