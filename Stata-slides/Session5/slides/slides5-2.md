# Session 5: <br> Basic Plots
## Data Analysis Using Stata

Summer 2020 | MA Sociology | FU Berlin

---

## Learning Module 5.2


1. Twoway Plots
1. Saving and Exporting Graphs
2. Combining Graphs
3. Editing Graphs



---

## Twoway Plots

The `twoway` command allows us to overlay two plots of certain types.

```STATA
twoway (graph1 var, options) (graph2 var, options)
*or:
twoway graph1 var, options || graph2 var, options

```
<!-- .element class="fragment" -->

---

## Saving and Exporting Graphs

- Stata can store graphs in memory or on disk.
- Graphs in memory are lost after each session, graphs on disk not.<!-- .element class="fragment" -->
- For publication, STATA can also export graphs.<!-- .element class="fragment" -->

----

### Commands

<div class="fragment">

You can name graphs to keep them in memory:

```stata
graph (...), name(my_graph)
graph display my_graph
```
</div>

<div class="fragment">

... or save them to store on disk.

```stata
graph (...), saving($out/my_graph)
graph use $out/mygraph
```

</div>

----

### Exporting graphs


It is easiest to export the last graph you created or loaded:

```stata
graph export "mygraph.svg", replace
```
<!-- .element class="fragment" -->

---

## Combining Graphs

- using `graph combine`, you can create graphs containing multiple plots
- use the options `row()`and `col()` to specify the layout.

Note:
Example in Stata

---

## Layout adjustments

- There are a number of ways to change the appearance of plots.
    - Options like `title()`, `xtitle()`, `ylabel()` can adjust specific properties.
    - Color schemes can change the look of a plot.
    - The graph editor can be used to adjust each element.
- Check out the [cheatsheet](https://www.stata.com/bookstore/statacheatsheets.pdf) or use the help command for details.

----

### Color schemes

- There is a set of different color schemes build into Stata.
- Schemes can be applied by using the option `scheme()`
- List of schemes: https://www.stata.com/manuals13/g-4schemesintro.pdf

Note:
Example in Stata

---


### The Graph Editor

https://www.youtube.com/watch?v=17opC4fDeME




---

## Task 5.2

<div style="font-size:1.5rem">
You may continue using your do-file from LM 5.1.

---
1. Create a twoway plot that combines the kernel density plot and the histogram of income.
    - restrict the plot to incomes under 15.000€
2. Save your plot to memory or disk and create an additional box plot of the same distribution. Save this one to memory or disk as well.
3. Combine both plots to one graph with 2 rows.
4. Export the result as a vector graphic (e.g. svg)
5. Change the color scheme of the twoway plot to a blackscale scheme and export the result as a pixel graphic (e.g. png)
</div>
