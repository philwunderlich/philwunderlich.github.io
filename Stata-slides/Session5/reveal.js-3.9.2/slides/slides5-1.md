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

- Unclear or distorted scales<!-- .element: class="fragment" -->
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

- Different plots fit different variable types!
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
![](img/hist_age_den.svg) <!-- .element: width="400" -->
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

Note:

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

- `return list` to display all stored stats.

![](img/hist_meanline.svg)<!-- .element: width="650" -->

----

#### Example: Histogram with mean line

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
![Histogram normal distributions](img/hist_normal.svg)<!-- .element: class="" width="650" -->

----

## Kernel Density Plots

![KDE](img/Comparison_of_1D_histogram_and_KDE.png)

<div style="font-size:1rem">
By <a href="https://en.wikipedia.org/wiki/User:Drleft" class="extiw" title="wikipedia:User:Drleft">Drleft</a> at <a href="https://en.wikipedia.org/wiki/" class="extiw" title="wikipedia:">English Q52</a>, <a href="https://creativecommons.org/licenses/by-sa/3.0" title="Creative Commons Attribution-Share Alike 3.0">CC BY-SA 3.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=57332968">Link</a>
</div>

----

```stata
kdensity age
```
![](img/kdensity_age.svg)<!-- .element: width="650" -->

---

## Box Plots

- Another plot to visualize distributions.
- Especially: Measures of central tendency and outliers

---

## Box Plots

<!-- svg example box plot -->
<svg
   xmlns:dc="http://purl.org/dc/elements/1.1/"
   xmlns:cc="http://creativecommons.org/ns#"
   xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
   xmlns:svg="http://www.w3.org/2000/svg"
   xmlns="http://www.w3.org/2000/svg"
   width="800"
   id="svg200"
   viewBox="0 0 712.94143 437.18"
   version="1.1">
  <metadata
     id="metadata2644">
    <rdf:RDF>
      <cc:Work
         rdf:about="">
        <dc:format>image/svg+xml</dc:format>
        <dc:type
           rdf:resource="http://purl.org/dc/dcmitype/StillImage" />
        <dc:title>example_boxplot</dc:title>
      </cc:Work>
    </rdf:RDF>
  </metadata>
  <defs
     id="defs2642" />
  <title
     id="title2418">example_boxplot</title>
  <g
     transform="translate(0,-72.910004)"
     id="g2522">
    <rect
       id="rect10"
       x="0.5"
       y="73.410004"
       width="372.01999"
       height="436.17999"
       style="fill:#eaf2f3;stroke:#eaf2f3" />
    <rect
       id="rect12"
       x="59.639999"
       y="88.660004"
       width="289.62"
       height="401.14999"
       style="fill:#ffffff;stroke:#ffffff" />
    <line
       id="line14"
       x1="59.759998"
       y1="474.45001"
       x2="350.29999"
       y2="474.45001"
       style="fill:none;stroke:#eaf2f3" />
    <line
       id="line16"
       x1="59.759998"
       y1="400.35001"
       x2="350.29999"
       y2="400.35001"
       style="fill:none;stroke:#eaf2f3" />
    <line
       id="line18"
       x1="59.759998"
       y1="326.26999"
       x2="350.29999"
       y2="326.26999"
       style="fill:none;stroke:#eaf2f3" />
    <line
       id="line20"
       x1="59.759998"
       y1="252.19"
       x2="350.29999"
       y2="252.19"
       style="fill:none;stroke:#eaf2f3" />
    <line
       id="line22"
       x1="59.759998"
       y1="178.10001"
       x2="350.29999"
       y2="178.10001"
       style="fill:none;stroke:#eaf2f3" />
    <line
       id="line24"
       x1="59.759998"
       y1="104.02"
       x2="350.29999"
       y2="104.02"
       style="fill:none;stroke:#eaf2f3" />
    <rect
       id="rect26"
       x="107.03"
       y="344.82999"
       width="194.86"
       height="74.120003"
       style="fill:#8da3b7;stroke:#1a476f" />
    <line
       id="line28"
       x1="107.03"
       y1="385.57999"
       x2="301.88"
       y2="385.57999"
       style="fill:none;stroke:#1a476f" />
    <line
       id="line30"
       x1="204.45"
       y1="418.95001"
       x2="204.45"
       y2="474.54999"
       style="fill:none;stroke:#1a476f" />
    <line
       id="line32"
       x1="204.45"
       y1="344.82999"
       x2="204.45"
       y2="233.63"
       style="fill:none;stroke:#1a476f" />
    <line
       id="line34"
       x1="139.17999"
       y1="474.54999"
       x2="269.73001"
       y2="474.54999"
       style="fill:none;stroke:#1a476f" />
    <line
       id="line36"
       x1="139.17999"
       y1="233.63"
       x2="269.73001"
       y2="233.63"
       style="fill:none;stroke:#1a476f" />
    <ellipse
       id="circle38"
       cx="204.45"
       cy="233.63"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle40"
       cx="204.45"
       cy="233.63"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle42"
       cx="204.45"
       cy="233.63"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle44"
       cx="204.45"
       cy="233.63"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle46"
       cx="204.45"
       cy="233.63"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle48"
       cx="204.45"
       cy="233.63"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle50"
       cx="204.45"
       cy="233.63"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle52"
       cx="204.45"
       cy="233.63"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle54"
       cx="204.45"
       cy="233.63"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle56"
       cx="204.45"
       cy="233.63"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle58"
       cx="204.45"
       cy="226.23"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle60"
       cx="204.45"
       cy="226.23"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle62"
       cx="204.45"
       cy="222.52"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle64"
       cx="204.45"
       cy="222.52"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle66"
       cx="204.45"
       cy="222.52"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle68"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle70"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle72"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle74"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle76"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle78"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle80"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle82"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle84"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle86"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle88"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle90"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle92"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle94"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle96"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle98"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle100"
       cx="204.45"
       cy="215.09"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle102"
       cx="204.45"
       cy="211.39999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle104"
       cx="204.45"
       cy="211.39999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle106"
       cx="204.45"
       cy="203.98"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle108"
       cx="204.45"
       cy="200.28999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle110"
       cx="204.45"
       cy="196.57001"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle112"
       cx="204.45"
       cy="196.57001"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle114"
       cx="204.45"
       cy="196.57001"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle116"
       cx="204.45"
       cy="196.57001"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle118"
       cx="204.45"
       cy="196.57001"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle120"
       cx="204.45"
       cy="196.57001"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle122"
       cx="204.45"
       cy="196.57001"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle124"
       cx="204.45"
       cy="196.57001"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle126"
       cx="204.45"
       cy="188.42"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle128"
       cx="204.45"
       cy="181.75"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle130"
       cx="204.45"
       cy="178.03999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle132"
       cx="204.45"
       cy="178.03999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle134"
       cx="204.45"
       cy="178.03999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle136"
       cx="204.45"
       cy="178.03999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle138"
       cx="204.45"
       cy="178.03999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle140"
       cx="204.45"
       cy="178.03999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle142"
       cx="204.45"
       cy="178.03999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle144"
       cx="204.45"
       cy="178.03999"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle146"
       cx="204.45"
       cy="163.21001"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle148"
       cx="204.45"
       cy="140.98"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle150"
       cx="204.45"
       cy="131.71001"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle152"
       cx="204.45"
       cy="122.46"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle154"
       cx="204.45"
       cy="122.46"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle156"
       cx="204.45"
       cy="103.92"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle158"
       cx="204.45"
       cy="103.92"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle160"
       cx="204.45"
       cy="103.92"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle162"
       cx="204.45"
       cy="103.92"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle164"
       cx="204.45"
       cy="103.92"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle166"
       cx="204.45"
       cy="103.92"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <ellipse
       id="circle168"
       cx="204.45"
       cy="103.92"
       rx="1.84"
       ry="3.3399999"
       style="fill:#1a476f;stroke:#1a476f" />
    <line
       id="line170"
       x1="59.759998"
       y1="489.70001"
       x2="59.759998"
       y2="88.769997"
       style="fill:none;stroke:#000000" />
    <line
       id="line172"
       x1="59.759998"
       y1="474.45001"
       x2="53.700001"
       y2="474.45001"
       style="fill:none;stroke:#000000" />
    <text
       transform="rotate(-90,262.39,216.27)"
       style="font-size:15.1374px;font-family:Helvetica, Helvetica;isolation:isolate"
       id="text2502">0</text>
    <line
       id="line176"
       x1="59.759998"
       y1="400.35001"
       x2="53.700001"
       y2="400.35001"
       style="fill:none;stroke:#000000" />
    <text
       transform="rotate(-90,232.705,186.585)"
       style="font-size:15.1374px;font-family:Helvetica, Helvetica;isolation:isolate"
       id="text2505">2,000</text>
    <line
       id="line180"
       x1="59.759998"
       y1="326.26999"
       x2="53.700001"
       y2="326.26999"
       style="fill:none;stroke:#000000" />
    <text
       transform="rotate(-90,195.665,149.545)"
       style="font-size:15.1374px;font-family:Helvetica, Helvetica;isolation:isolate"
       id="text2508">4,000</text>
    <line
       id="line184"
       x1="59.759998"
       y1="252.19"
       x2="53.700001"
       y2="252.19"
       style="fill:none;stroke:#000000" />
    <text
       transform="rotate(-90,158.625,112.505)"
       style="font-size:15.1374px;font-family:Helvetica, Helvetica;isolation:isolate"
       id="text2511">6,000</text>
    <line
       id="line188"
       x1="59.759998"
       y1="178.10001"
       x2="53.700001"
       y2="178.10001"
       style="fill:none;stroke:#000000" />
    <text
       transform="rotate(-90,121.58,75.46)"
       style="font-size:15.1374px;font-family:Helvetica, Helvetica;isolation:isolate"
       id="text2514">8,000</text>
    <line
       id="line192"
       x1="59.759998"
       y1="104.02"
       x2="53.700001"
       y2="104.02"
       style="fill:none;stroke:#000000" />
    <text
       transform="rotate(-90,86.645,40.525)"
       style="font-size:15.1374px;font-family:Helvetica, Helvetica;isolation:isolate"
       id="text2517">10,000</text>
    <text
       transform="rotate(-90,190.69,161.23)"
       style="font-size:15.1374px;font-family:Helvetica, Helvetica;isolation:isolate"
       id="text2519">Household income</text>
    <line
       id="line198"
       x1="59.759998"
       y1="489.70001"
       x2="349.72"
       y2="489.70001"
       style="fill:none;stroke:#000000" />
  </g>
  <path
     d=""
     style="fill:none"
     id="path2524" />
  <path
     id="path214"
     d="M 216.47,104.69"
     style="stroke:#000000" />
  <path
     d=""
     style="fill:none"
     id="path2527" />
  <path
     id="path214-7"
     d="M 301.88,271.92"
     style="stroke:#000000" />
  <path
     d=""
     style="fill:none"
     id="path2530" />
  <path
     id="path1440"
     d="M 269.73,160.72"
     style="stroke:#000000" />
  <g data-fragment-index="6"
     class="fragment"
     transform="translate(0,-72.910004)"
     id="g2547">
    <g
       id="g2539">
      <line
         x1="222.59"
         y1="161.89"
         x2="466.45001"
         y2="135.05"
         style="fill:none;stroke:#e73c16;stroke-width:2px"
         id="line2535" />
      <path
         d="m 210.33,89.71 c 5.88,1.47 13.28,4.27 18,7.58 l -4.46,-9.08 2.38,-9.82 c -3.89,4.26 -10.5,8.61 -15.92,11.32 z"
         transform="translate(0.26,73.5)"
         style="fill:#e73c16"
         id="path2537" />
    </g>
    <text
       transform="translate(475.26,140.98)"
       style="font-size:18.66666667px;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-weight:normal;font-style:normal;font-stretch:normal;font-variant:normal;font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
       id="text2545"><tspan
         style="letter-spacing:0.00297408em;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-family:Helvetica, Helvetica;font-weight:normal;font-style:normal;font-stretch:normal;font-variant:normal;font-size:18.66666667px;font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
         id="tspan2541">Outliers</tspan></text>
  </g>
  <g data-fragment-index="4"
    class="fragment"
     transform="translate(0,-72.910004)"
     id="g2577">
    <g
       id="g2553">
      <line
         x1="288.17001"
         y1="230.39999"
         x2="466.45001"
         y2="188.42"
         style="fill:none;stroke:#e73c16;stroke-width:2px"
         id="line2549" />
      <path
         d="m 276.16,159.66 c 6,0.75 13.7,2.64 18.82,5.35 l -5.53,-8.47 1.17,-10 c -3.38,4.66 -9.41,9.77 -14.46,13.12 z"
         transform="translate(0.26,73.5)"
         style="fill:#e73c16"
         id="path2551" />
    </g>
    <text
       transform="translate(475.26,193.24)"
       style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-size:18.66666667px;line-height:1.2;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;letter-spacing:0px;"
       id="text2575"><tspan
         id="tspan3229"
         style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-size:18.66666667px;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
         x="0"
         y="0">Maximum</tspan><tspan
         id="tspan3231"
         style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-size:18.66666667px;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
         x="0"
         y="22.400042">(highest value within</tspan><tspan
         id="tspan3233"
         style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-size:18.66666667px;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
         x="0"
         y="44.800083">1,5 IQR from 75% quantile)</tspan></text>
  </g>
  <g data-fragment-index="3"
     class="fragment"
     transform="translate(0,-72.910004)"
     id="g2591">
    <g
       id="g2583">
      <line
         x1="320.54001"
         y1="340.28"
         x2="466.45001"
         y2="280.85999"
         style="fill:none;stroke:#e73c16;stroke-width:2px"
         id="line2579" />
      <path
         d="m 309.11,271.33 c 6.05,-0.19 13.93,0.48 19.42,2.36 l -6.78,-7.51 -0.4,-10.1 c -2.61,5.17 -7.78,11.16 -12.24,15.25 z"
         transform="translate(0.26,73.5)"
         style="fill:#e73c16"
         id="path2581" />
    </g>
    <text
       transform="translate(475.26,289.23)"
       style="font-size:18.66666667px;font-family:Helvetica, Helvetica;letter-spacing:0px;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-weight:normal;font-style:normal;font-stretch:normal;font-variant:normal;font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
       id="text2589"><tspan
         id="tspan3239"
         x="0"
         y="0"
         style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;font-size:18.66666667px;">75% quantile</tspan></text>
  </g>
  <g data-fragment-index="1"
     class="fragment"
     transform="translate(0,-72.910004)"
     id="g2605">
    <g
       id="g2597">
      <line
         x1="321.38"
         y1="382.54999"
         x2="466.45001"
         y2="344.82999"
         style="fill:none;stroke:#e73c16;stroke-width:2px"
         id="line2593" />
      <path
         d="m 309.43,312.08 c 6,0.62 13.76,2.32 18.94,4.91 l -5.72,-8.34 0.94,-10.07 c -3.27,4.78 -9.19,10.04 -14.16,13.5 z"
         transform="translate(0.26,73.5)"
         style="fill:#e73c16"
         id="path2595" />
    </g>
    <text
       transform="translate(475.26,352.59)"
       style="font-size:18.66666667px;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-weight:normal;font-style:normal;font-stretch:normal;font-variant:normal;font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
       id="text2603"><tspan
         id="tspan3245"
         style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-size:18.66666667px;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
         x="0"
         y="0">Median (50% quantile)</tspan></text>
  </g>
  <g data-fragment-index="2"
     class="fragment"
     transform="translate(0,-72.910004)"
     id="g2619">
    <g
       id="g2611">
      <line
         x1="325.98001"
         y1="415.13"
         x2="466.45001"
         y2="406.98001"
         style="fill:none;stroke:#e73c16;stroke-width:2px"
         id="line2607" />
      <path
         d="m 313.67,342.33 c 5.79,1.78 13,5 17.61,8.51 l -4,-9.3 2.88,-9.69 c -4.16,4.05 -10.95,8.05 -16.49,10.48 z"
         transform="translate(0.26,73.5)"
         style="fill:#e73c16"
         id="path2609" />
    </g>
    <text
       transform="translate(475.26,415.96)"
       style="font-size:18.66666667px;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-weight:normal;font-style:normal;font-stretch:normal;font-variant:normal;font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
       id="text2617"><tspan
         id="tspan3249"
         style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-size:18.66666667px;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
         x="0"
         y="0">25% quantile</tspan></text>
  </g>
  <g
     class="fragment"
     transform="translate(0,-72.910004)"
     id="g2637">
    <g
       id="g2625">
      <line
         x1="291.03"
         y1="474.45001"
         x2="466.45001"
         y2="474.45001"
         style="fill:none;stroke:#e73c16;stroke-width:2px"
         id="line2621" />
      <path
         d="m 278.7,401 c 5.68,2.1 12.73,5.7 17.1,9.51 l -3.45,-9.51 3.45,-9.51 c -4.37,3.76 -11.42,7.35 -17.1,9.51 z"
         transform="translate(0.26,73.5)"
         style="fill:#e73c16"
         id="path2623" />
    </g>
    <text
       transform="translate(475.26,478.66)"
       style="font-size:18.66666667px;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-weight:normal;font-style:normal;font-stretch:normal;font-variant:normal;font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
       id="text2635"><tspan
         id="tspan3251"
         x="0"
         y="0"><tspan
           style="font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;font-size:18.66666667px;font-family:Helvetica, Helvetica;-inkscape-font-specification:'Helvetica, Helvetica, Normal';font-variant-ligatures:normal;font-variant-caps:normal;font-variant-numeric:normal;font-variant-east-asian:normal;"
           id="tspan3253">Minimum (see Maximum)</tspan></tspan></text>
  </g>
</svg>



Note:
- As mentioned before, the median is a measure of central tendency that is more robust to outliers compared to the mean
-     - 50% of all cases lie within the range of the box.
- A box plot is another way to display a distribution.
- central horizontal line: _median_.
- bottom of the box: *25% quantile*
- top of the box: *75% quantile*.
- The middle 50% are the _Inter Quartile Range_ (IQR)
- The "whiskers" indicate the minimum or maximum (up to 1.5 * IQR)
- extreme outliers are indicated by dots.


----


### Box Plot Command

```stata
graph box age
```
<!-- .element: class="fragment fade-in-then-semi-out" -->

![](img/box_age.svg)<!-- .element: width="650" class="fragment"-->


----

#### Example: Box Plot and Outliers

---


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
    - Set the bin width, so that each column of the histogram represents 2500€ of income.
    - Plot the actual frequencies of respondents per category on the x axis.
2. Create a second histogram in which you ignore cases with extremely high household incomes of above 40.000 €. Adjust the bin width in a sensible way.
    - does the household income follow an approximate normal distribution? Draw a normal density line to assess!
    - Add a line for the median. How does the median behave as compared to the mean?
3. Create a box plot that illustrates the distribution of the household income.
    - Try to make an informed decision where to cut off the box plot to keep outliers but exclude extreme outliers that distort the graphical representation.
4. Draw a bar plot for all categories of the employment status.

(Remark: Excluding outliers from a graphic is a measure that should be used with care, as pointed out before !</div>
