<!-- .slide: data-background="#acf2dc" data-transition="linear" -->

# SESSION 6: <br> DESCRIPTIVE INFERENCE&nbsp;1
## Data Analysis using Stata
Summer 2020 | MA Sociology | FU Berlin
    


---

## Learning Goals Session 6

- 6.1 Research Questions and Hypotheses
- 6.2 What is "Descriptive Inference"
- 6.3 Compare group means using t-test

---

## Learning Module 6.1: Research Questions

- In most cases, we are interested in the relationship between two or more variables.
- Basic question "What is the relationship between X and Y?"
- As we already know, there might be third variables involved. We are going to ignore these for now.

---

<!-- .slide: data-background="#F3E2A9" data-transition="linear" -->

### Conceptual Models

#### Simple effect

![diagram_simple_effect.svg](./img/diagram_simple_effect.svg)


#### Moderation / Mediation

![diagram_moderation.svg](img/diagram_moderation.svg)

---

## Task:

- For your own analysis, please look through the Allbus variables and find a relationship that you want to analyze. 
- This entails both a dependent variable and one or more explanatory variables.
- Upload a brief draft of your proposal to blackboard.
    - This entails a research question, names of the respective variables, and preferably a simple diagram of the hypothesized relationship.


---

## Caution! Variable types

- With the methods we learn in this course, we can only analyze **continuous dependent variables**.
- However, you may analyze categorical variables on 7-point scales or above, as they can be argued to be quasi-continuous.


![likert_scale.jpeg](img/likert_scale.jpeg)


- Explanatory variables may be both categorial and continuous.

---

## Hypotheses

- After we have formulated a research question, we derive testable hypotheses.
- Usually, there are two contrasting hypotheses:
    - H0: "X and Y are not related" (null-hypothesis)
    - H1: "X has an influence on Y" (alternative hypothesis)

---

## Example:

- H0: Gender does not have an influence on Income.
- H1: Gender has an influence on income. (undirected hypothesis)

OR:

- H1: Being male increases income on average (directed hypothesis)

---

## Errors types


[](https://www.youtube.com/watch?v=7mE-K_w1v90)

| Test \ Reality         | H0 is false      | H0 is true       |
|------------------------|:----------------:|:----------------:|
| **We reject H0**       | Correct Decision | *Type I error*   |
| **We don't reject H0** | _Type II Error_  | Correct Decision |

$\alpha = $ probability of Type I error

$\beta =$ probability of Type II error

- when testing hypotheses, we aim to minimize $\alpha$.


---

## Hypothesis testing

- To find out whether variables are related **in our sample**, we could compare means across groups. (e.g. mean income men vs. mean income women)

---

## Compare 2 Sample Means

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

---

## What about the population

- <!-- .element class="fragment" --> An effect in our __sample__ might be caused by chance.

- The *true* relationship in the **population** might look completely different.
- In order to test hypotheses **for our population**, we need statistical tests / inferential statistics.

Note:

But why should we worry about error types, if we can in fact look at the numbers in our sample and see whether there are relationships? Example: Boxplot Income across gender.
Errors occur when we generalize an effect / relationship from our sample to the populaiton.
(this can be 3 slides.)


---