---
title: "Introduction to Data Manipulation"
subtitle: "Getting our data right with `dplyr`"
type: book
weight: 4
output:
  blogdown:html_page:
    theme: journal
    df_print: paged
    toc: yes
    toc_float:
      collapsed: false
---

<script src="/2022-spring-stats2rmarkdown-libs/kePrint/kePrint.js"></script>
<link href="/2022-spring-stats2rmarkdown-libs/lightable/lightable.css" rel="stylesheet" />
<script src="/2022-spring-stats2rmarkdown-libs/kePrint/kePrint.js"></script>
<link href="/2022-spring-stats2rmarkdown-libs/lightable/lightable.css" rel="stylesheet" />
<script src="/2022-spring-stats2rmarkdown-libs/kePrint/kePrint.js"></script>
<link href="/2022-spring-stats2rmarkdown-libs/lightable/lightable.css" rel="stylesheet" />
<script src="/2022-spring-stats2rmarkdown-libs/kePrint/kePrint.js"></script>

<link href="/2022-spring-stats2rmarkdown-libs/lightable/lightable.css" rel="stylesheet" />

# 1. Introduction

## Welcome!

Welcome to our second tutorial for the Statistics II: Statistical Modeling & Causal Inference (with R) course.

The labs are designed to reinforce the material covered during the lectures by introducing you to hands-on applications.

The practical nature of our class means that our labs will be data-centered. Throughout our class, we will get acquinted with multiple packages of the `tidyverse`.

Though we expect that some of you may already know them, the `tidyverse` is a collection of R packages that share an underlying design, syntax, and structure. They will definitely make your life easier!!

Today, we will start with a brief introduction to data manipulation through the `dplyr` package.

In this tutorial, you will learn to:

-   identify the purpose of a set of `dplyr` verbs
-   write statements in **tidy** syntax
-   apply `dplyr` verbs to solve your data manipulation challenges

This tutorial is partly based on [*R for Data Science*](http://r4ds.had.co.nz/), section 5.2, and [*Quantitative Politics with R*](http://qpolr.com/data.html/), chapter 3.

------------------------------------------------------------------------

## What we will need today

We’ll practice some wrangling in `dplyr` using data for penguin sizes recorded by Dr. Kristen Gorman and others at several islands in the Palmer Archipelago, Antarctica. Data are originally published in: Gorman KB, Williams TD, Fraser WR (2014) PLoS ONE 9(3): e90081. doi:10.1371/journal.pone.0090081

You do **not** need to import the data to work through this tutorial - the data are already here waiting behind the scenes.

But if you *do* ever want to use the penguins data outside of this tutorial, they now exist in the [**palmerpenguins**](https://github.com/allisonhorst/palmerpenguins) package in *R*.

Let’s begin!

------------------------------------------------------------------------

# 2. Data Structure

## Tidy data

Generally, we will encounter data in a tidy format. Tidy data refers to a way of mapping the structure of a data set. In a tidy data set:

1.  Each variable forms a column.
2.  Each observation forms a row.
3.  Each type of observational unit forms a table

<img src="https://raw.githubusercontent.com/seramirezruiz/hertiestats2/master/inst/tutorials/basics/images/tidy_data.png" width="70%" style="display: block; margin: auto;" />

## The `penguins` data set

The 3 species of penguins in this data set are Adelie, Chinstrap and Gentoo. The data set contains 8 variables:

-   **species:** a factor denoting the penguin species (Adelie, Chinstrap, or Gentoo)
-   **island:** a factor denoting the island (in Palmer Archipelago, Antarctica) where observed
-   **culmen\_length\_mm:** a number denoting length of the dorsal ridge of penguin bill (millimeters)
-   **culmen\_depth\_mm:** a number denoting the depth of the penguin bill (millimeters)
-   **flipper\_length\_mm:** an integer denoting penguin flipper length (millimeters)
-   **body\_mass\_g:** an integer denoting penguin body mass (grams)
-   **sex:** a factor denoting penguin sex (MALE, FEMALE)
-   **year** an integer denoting the year of the record

<img src="https://raw.githubusercontent.com/seramirezruiz/hertiestats2/master/inst/tutorials/basics/images/penguins.png" width="70%" style="display: block; margin: auto;" />
<p style="text-align:right;">
*Illustration by @allisonhorst*
</p>

## Let’s explore the data set.

`head()` is a function that returns the first couple rows from a data frame. Write the R code required to explore the first observations of the `penguins` data set:

Notice that when you press ‘Run,’ the **output** of the code is returned below it! So by pressing ‘Run,’ you’ve run your first *R* code of the class!

``` r
head(penguins)
```

<table class="table table-striped" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
species
</th>
<th style="text-align:left;">
island
</th>
<th style="text-align:right;">
bill\_length\_mm
</th>
<th style="text-align:right;">
bill\_depth\_mm
</th>
<th style="text-align:right;">
flipper\_length\_mm
</th>
<th style="text-align:right;">
body\_mass\_g
</th>
<th style="text-align:left;">
sex
</th>
<th style="text-align:right;">
year
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Adelie
</td>
<td style="text-align:left;">
Torgersen
</td>
<td style="text-align:right;">
39.1
</td>
<td style="text-align:right;">
18.7
</td>
<td style="text-align:right;">
181
</td>
<td style="text-align:right;">
3750
</td>
<td style="text-align:left;">
male
</td>
<td style="text-align:right;">
2007
</td>
</tr>
<tr>
<td style="text-align:left;">
Adelie
</td>
<td style="text-align:left;">
Torgersen
</td>
<td style="text-align:right;">
39.5
</td>
<td style="text-align:right;">
17.4
</td>
<td style="text-align:right;">
186
</td>
<td style="text-align:right;">
3800
</td>
<td style="text-align:left;">
female
</td>
<td style="text-align:right;">
2007
</td>
</tr>
<tr>
<td style="text-align:left;">
Adelie
</td>
<td style="text-align:left;">
Torgersen
</td>
<td style="text-align:right;">
40.3
</td>
<td style="text-align:right;">
18.0
</td>
<td style="text-align:right;">
195
</td>
<td style="text-align:right;">
3250
</td>
<td style="text-align:left;">
female
</td>
<td style="text-align:right;">
2007
</td>
</tr>
<tr>
<td style="text-align:left;">
Adelie
</td>
<td style="text-align:left;">
Torgersen
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:right;">
2007
</td>
</tr>
<tr>
<td style="text-align:left;">
Adelie
</td>
<td style="text-align:left;">
Torgersen
</td>
<td style="text-align:right;">
36.7
</td>
<td style="text-align:right;">
19.3
</td>
<td style="text-align:right;">
193
</td>
<td style="text-align:right;">
3450
</td>
<td style="text-align:left;">
female
</td>
<td style="text-align:right;">
2007
</td>
</tr>
<tr>
<td style="text-align:left;">
Adelie
</td>
<td style="text-align:left;">
Torgersen
</td>
<td style="text-align:right;">
39.3
</td>
<td style="text-align:right;">
20.6
</td>
<td style="text-align:right;">
190
</td>
<td style="text-align:right;">
3650
</td>
<td style="text-align:left;">
male
</td>
<td style="text-align:right;">
2007
</td>
</tr>
</tbody>
</table>

------------------------------------------------------------------------

# 3. Manipulating data with `dplyr`

## What we will learn today

In this tutorial, you’ll learn and practice examples using some functions in `dplyr` to work with data. Those are:

-   `select()`: keep or exclude some columns
-   `filter()`: keep rows that satisfy your conditions
-   `mutate()`: add columns from existing data or edit existing columns
-   `group_by()`: lets you define groups within your data set
-   `summarize()`: get summary statistics
-   `arrange()`: reorders the rows according to single or multiple variables

Let’s get to work.

------------------------------------------------------------------------

## 3.1. `select()`

The first verb (function) we will utilize is `select()`. We can employ it to manipulate our data based on columns. If you recall from our initial exploration of the data set there were eight variables attached to every observation. Do you recall them? If you do not, there is no problem. You can utilize `names()` to retrieve the names of the variables in a data frame.

``` r
names(penguins)
```

    ## [1] "species"           "island"            "bill_length_mm"   
    ## [4] "bill_depth_mm"     "flipper_length_mm" "body_mass_g"      
    ## [7] "sex"               "year"

Say we are only interested in the species, island, and year variables of these data, we can utilize the following syntax:

<center>
select(data, columns)
</center>

------------------------------------------------------------------------

**Activity**
*The following code chunk would select the species, island, and year variables. What should we do to keep the body\_mass\_g and sex variables as well?*

``` r
dplyr::select(penguins, species, island, year)
```

<iframe src="../wid1.html" width="100%" height="500">
</iframe>

{{% spoiler text="Answer" %}}

``` r
# you just need to type the names of the columns
dplyr::select(penguins, species, island, year, body_mass_g, sex)
```

<iframe src="../wid2.html" width="100%" height="500">
</iframe>

{{% /spoiler %}}

{{% callout note %}}

To drop variables, use - before the variable name.

For example, `select(penguins, -year)` will drop the year column.

{{% /callout %}}

------------------------------------------------------------------------

## 3.2. `filter()`

The second verb (function) we will employ is `filter()`. `filter()` lets you use a logical test to extract specific rows from a data frame. To use `filter()`, pass it the data frame followed by one or more logical tests. `filter()` will return every row that passes each logical test.

The more commonly used logical operators are:

-   `==`: Equal to
-   `!=`: Not equal to
-   `>`, `>=`: Greater than, greater than or equal to
-   `<`, `<=`: Less than, less than or equal to
-   `&`, `|`: And, or

Say we are interested in retrieving the observations from the year 2007. We would do:

``` r
dplyr::filter(penguins, year == 2007)
```

<iframe src="../wid3.html" width="100%" height="500">
</iframe>

**Activity**
*Can you adapt the code to retrieve all the observations of Chinstrap penguins from 2007 (remember that species contains character units)*

{{% spoiler text="Answer" %}}

``` r
# you just need to utilize & and type the logical operator for the species
dplyr::filter(penguins, year == 2007 & species == "Chinstrap")
```

<iframe src="../wid4.html" width="100%" height="500">
</iframe>

{{% /spoiler %}}

------------------------------------------------------------------------

## 3.3. The Pipe Operator: `%>%`

The pipe, `%>%`, comes from the `magrittr` package by Stefan Milton Bache. Packages in the `tidyverse` load `%>%` for you automatically, so you don’t usually load `magrittr` explicitly. This will be one of your best friends in *R*.
&gt;**Pipes are a powerful tool for clearly expressing a sequence of multiple operations. Let’s think about baking for a second.**

<img src="https://user-images.githubusercontent.com/54796579/92409417-d3b0c600-f140-11ea-8596-561a05586988.png" style="display: block; margin: auto;" />

------------------------------------------------------------------------

**Activity**
*We can leverage the pipe operator to sequence our code in a logical manner. Can you adapt the following code chunk with the pipe and conditional logical operators we discussed?*

``` r
only_2009 <- dplyr::filter(penguins, year == 2009)
only_2009_chinstraps <- dplyr::filter(only_2009, species == "Chinstrap")
only_2009_chinstraps_species_sex_year <- dplyr::select(only_2009_chinstraps, species, sex, year)
final_df <- only_2009_chinstraps_species_sex_year
final_df #to print it in our console
```

{{% spoiler text="Answer" %}}

``` r
penguins %>% #we start off with out df
  dplyr::filter(year == 2009 & species == "Chinstrap") %>% #filter
  dplyr::select(species, sex, year) #select
```

<iframe src="../wid5.html" width="100%" height="500">
</iframe>

{{% /spoiler %}}

------------------------------------------------------------------------

## 3.4. `mutate()`

`mutate()` lets us create, modify, and delete columns. The most common use for now will be to create new variables based on existing ones. Say we are working with a U.S. American client and they feel more confortable with assessing the weight of the penguins in pounds. We would utilize `mutate()` as such:

<p>
<center>
mutate(new\_var\_name = conditions)
</center>

<br>

**Activity**
*Can you edit the following code chunk to render a new variable body\_mass\_kg?*

``` r
penguins %>%
  dplyr::mutate(body_mass_lbs = body_mass_g/453.6)
```

<iframe src="../wid6.html" width="100%" height="500">
</iframe>

{{% spoiler text="Answer" %}}

``` r
penguins %>%
  dplyr::mutate(body_mass_kg = body_mass_g/1000) #grams divided by 1000 
```

<iframe src="../wid7.html" width="100%" height="500">
</iframe>

{{% /spoiler %}}

------------------------------------------------------------------------

## 3.5. `group_by()` and `summarize()`

These two verbs `group_by()` and `summarize()` tend to go together. When combined , ’summarize()\` will create a new data frame. It will have one (or more) rows for each combination of grouping variables; if there are no grouping variables, the output will have a single row summarising all observations in the input. For example:

-   `summarize()`:

``` r
penguins %>%
  dplyr::summarize(heaviest_penguin = max(body_mass_g, na.rm = T)) #max() does not know how to deal with NAs very well
```

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:right;">
heaviest\_penguin
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
6300
</td>
</tr>
</tbody>
</table>

-   `group_by()` + `summarize()`:

``` r
penguins %>%
  dplyr::group_by(species) %>%
  dplyr::summarize(heaviest_penguin = max(body_mass_g, na.rm = T))
```

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
species
</th>
<th style="text-align:right;">
heaviest\_penguin
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Adelie
</td>
<td style="text-align:right;">
4775
</td>
</tr>
<tr>
<td style="text-align:left;">
Chinstrap
</td>
<td style="text-align:right;">
4800
</td>
</tr>
<tr>
<td style="text-align:left;">
Gentoo
</td>
<td style="text-align:right;">
6300
</td>
</tr>
</tbody>
</table>

**Activity**
*Can you get the weight of the lightest penguin of each species? You can use `min()`. What happens when in addition to species you also group by year `group_by(species, year)`?*

{{% spoiler text="Answers" %}}

``` r
penguins %>%
  dplyr::group_by(species) %>%
  dplyr::summarize(lightest_penguin = min(body_mass_g, na.rm = T))
```

<table class="table" style="margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
species
</th>
<th style="text-align:right;">
lightest\_penguin
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Adelie
</td>
<td style="text-align:right;">
2850
</td>
</tr>
<tr>
<td style="text-align:left;">
Chinstrap
</td>
<td style="text-align:right;">
2700
</td>
</tr>
<tr>
<td style="text-align:left;">
Gentoo
</td>
<td style="text-align:right;">
3950
</td>
</tr>
</tbody>
</table>

``` r
penguins %>%
  dplyr::group_by(species, year) %>%
  dplyr::summarize(lightest_penguin = max(body_mass_g, na.rm = T)) 
```

    ## `summarise()` has grouped output by 'species'. You can override using the `.groups` argument.

{{% /spoiler %}}

------------------------------------------------------------------------

## 3.6. `arrange()`

The `arrange()` verb is pretty self-explanatory. `arrange()` orders the rows of a data frame by the values of selected columns in ascending order. You can use the `desc()` argument inside to arrange in descending order. The following chunk arranges the data frame based on the length of the penguins’ bill. You hint tab contains the code for the descending order alternative.

<center>
arrange(variable\_of\_interest)
</center>

<br>

``` r
penguins %>%
  dplyr::arrange(bill_length_mm)
```

<iframe src="../wid12.html" width="100%" height="500">
</iframe>

``` r
penguins %>%
  dplyr::arrange(desc(bill_length_mm))
```

<iframe src="../wid13.html" width="100%" height="500">
</iframe>

**Activity**
*Can you create a data frame arranged by body\_mass\_g of the penguins observed in the “Dream” island?*

{{% spoiler text="Answer" %}}

``` r
penguins %>%
  dplyr::filter(island == "Dream") %>%
  dplyr::arrange(desc(body_mass_g)) 
```

<iframe src="../wid14.html" width="100%" height="500">
</iframe>

{{% /spoiler %}}
