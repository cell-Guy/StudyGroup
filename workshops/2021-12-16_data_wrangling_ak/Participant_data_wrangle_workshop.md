---
title: "Introduction to data wrangling in R"
output:
  html_document:
    keep_md: true
    toc: true
    toc_depth: 3
    toc_float:
      collapsed: true
      smooth_scroll: true
    number_sections:  true
    theme: paper
    self_contained: yes
editor_options: 
  chunk_output_type: inline
---

Adapted from Tutorial by: Victor Yuan

Who: Almas Khan, [Trainee Omics Group (TOG)](https://bcchr-trainee-omics-group.github.io/)

What: Introduction to data wrangling in R

Where: BC Children's Hospital Research Institute

When: December 16 2021

# Introduction 

## Who is this tutorial for?

- Those interested using R for data analysis
- Beginners in R, and those curious about `dplyr` and **tidyverse**

## Setup

- Please have the latest version of R and Rstudio installed. 
- Download the [r markdown file](https://github.com/BCCHR-trainee-omics-group/StudyGroup/blob/master/workshops/2021-12-16_data_wrangling_ak/Participant_data_wrangle_workshop.Rmd) for this workshop and open it in Rstudio.

- Install the following R packages now, if you haven't already:


```r
install.packages(c('gapminder', 'tidyverse'))
```


## Overall Learning outcomes

- Familiarity with tidyverse syntax
- Understanding how to use dplyr to manipulate data in R
- "Piping"

<!---The following chunk allows errors when knitting--->





To learn data manipulation in R, some understanding of how to use R is required. A comprehensive lesson on R is out of the scope of this tutorial, but here I go over some of the basics that will be helpful to follow along the data wrangling portion of this workshop.


## Resources

- [R Swirl](https://swirlstats.com/) for interactive lesson on programming with R
- *R for data science* [tibbles chapter](http://r4ds.had.co.nz/tibbles.html) to learn more about tibble/data.frames
- [Learnr package](https://rstudio.github.io/learnr/) another interactive lesson within R on programming


I recommend using **r markdown file (recommended)** for all of your analysis scripts. Think of it as a like a notebook for your code that includes comments and I find it's easier to keep track of your analysis. 

In `.rmd` files, code needs to be in code chunks (insert code chunk shortcut is Windows: `ctrl` `+` `alt` `+` `i`, Mac: `cmd` `+` `alt` `+` `i`) in order to run.


## Error messages (4 min)

As you work with R you will encounter error messages along the way, here are some steps I recommend you follow: 

1. Inspect your code for simple mistakes. Examples: are you missing a bracket or quotation mark? Did you mean to use `=` instead of `==`? Did you spell the name of the function or object wrong?
2. Are using the function correctly? Use the `?` command to pull up the help page. 
3. Make sure your input is correct. Does the function expect a `data.frame` but you gave it a `vector`?
4. Copy and paste the error and the name of the function you are using into **Google**.

# Understand the data in base R: Intro to data types and initial exploration

## Topics

- Basic data types
- `data.frame` and `tibble` objects
- Basic functions for exploring dataframes

Before we begin to manipulate data we should understand what type of data we have:

In R there are multiple types of data and I have listed a couple of basic ones below: 


```r
3.14 # This is a numeric 
```

```
## [1] 3.14
```

```r
"This is a character" # A character type 
```

```
## [1] "This is a character"
```

```r
"3.14" # This is also a character 
```

```
## [1] "3.14"
```

```r
TRUE # logical
```

```
## [1] TRUE
```

```r
FALSE # These are logicals
```

```
## [1] FALSE
```

These different types of data can be combined into objects like data frames or tibbles:

## Data frames and tibbles (5 min)

`data.frame` objects are by far the most common and useful way to work with your data in R.

A data.frame is basically just a table, it has a certain number of rows, and a certain number of columns.

"trees" is a built-in dataset in R available as a `data.frame`.


```r
trees
```

```
##    Girth Height Volume
## 1    8.3     70   10.3
## 2    8.6     65   10.3
## 3    8.8     63   10.2
## 4   10.5     72   16.4
## 5   10.7     81   18.8
## 6   10.8     83   19.7
## 7   11.0     66   15.6
## 8   11.0     75   18.2
## 9   11.1     80   22.6
## 10  11.2     75   19.9
## 11  11.3     79   24.2
## 12  11.4     76   21.0
## 13  11.4     76   21.4
## 14  11.7     69   21.3
## 15  12.0     75   19.1
## 16  12.9     74   22.2
## 17  12.9     85   33.8
## 18  13.3     86   27.4
## 19  13.7     71   25.7
## 20  13.8     64   24.9
## 21  14.0     78   34.5
## 22  14.2     80   31.7
## 23  14.5     74   36.3
## 24  16.0     72   38.3
## 25  16.3     77   42.6
## 26  17.3     81   55.4
## 27  17.5     82   55.7
## 28  17.9     80   58.3
## 29  18.0     80   51.5
## 30  18.0     80   51.0
## 31  20.6     87   77.0
```

The columns of the trees `data.frame` object are individual `vector` objects. So trees has 3 columns/vectors that are each 31 elements long. The dbl is just a type of numeric class of data. 

### Some basic functions to help understand your `data.frame` objects are:


```r
# number of rows
FILL_THIS_IN(trees)
```

```
## Error in FILL_THIS_IN(trees): could not find function "FILL_THIS_IN"
```

```r
# number of columns
FILL_THIS_IN(trees)
```

```
## Error in FILL_THIS_IN(trees): could not find function "FILL_THIS_IN"
```

```r
# row x columns
FILL_THIS_IN(trees)
```

```
## Error in FILL_THIS_IN(trees): could not find function "FILL_THIS_IN"
```

```r
# some basic info on the "structure" of the data.frame
FILL_THIS_IN(trees)
```

```
## Error in FILL_THIS_IN(trees): could not find function "FILL_THIS_IN"
```

```r
# calculates some summary statistics on each column
FILL_THIS_IN(trees)
```

```
## Error in FILL_THIS_IN(trees): could not find function "FILL_THIS_IN"
```

```r
# print first 6 rows
FILL_THIS_IN(trees)
```

```
## Error in FILL_THIS_IN(trees): could not find function "FILL_THIS_IN"
```

```r
# print last 6 rows
FILL_THIS_IN(trees)
```

```
## Error in FILL_THIS_IN(trees): could not find function "FILL_THIS_IN"
```

### Tibbles

We are going to use the "gapminder" dataset today, which is stored as a special type of `data.frame`, called a [`tibble`](https://tibble.tidyverse.org/index.html). 

- tibbles have a special printing output
- tibbles never have row names
- any function that works with `data.frame` objects (e.g. `str`, `summary`), will also work with `tibble` objects 
- use functions `as_tibble` and `as.data.frame` to convert between `tibble` and `data.frame`


```r
library(FILL_THIS_IN) #load gapminder
```

```
## Error in library(FILL_THIS_IN): there is no package called 'FILL_THIS_IN'
```


```r
# tibble
gapminder
```

```
## Error in eval(expr, envir, enclos): object 'gapminder' not found
```

```r
# data.frame 
head(FILL_THIS_IN(gapminder), n = 50)
```

```
## Error in FILL_THIS_IN(gapminder): could not find function "FILL_THIS_IN"
```

Note that I printed only the first 50 rows of the `data.frame` version of gapminder. By default, printing `tibble` objects will display the top 10 rows to avoid over-printing.

# Let's wrangle:  Intro to tidyverse

Now that we've learned some basics about data types in R. Let's wrangle some data using the tidyverse package. 

## Topics

* Relational/comparison and logical operators
* "Base R" vs tidyverse
* dplyr basic functions


## Resources

Most of this material is inspired from the [STAT 545 `dplyr` lecture](https://stat545guidebook.netlify.com/intro-to-data-wrangling-part-i.html)

Other resources for `dplyr`:

* [Old STAT 545 `dplyr` tutorial](http://stat545.com/block009_dplyr-intro.html)
* [The `dplyr` vignette](https://cran.r-project.org/web/packages/dplyr/vignettes/dplyr.html)

### R Operators (4 min)

Before diving into the tidyverse, let's take a look at a list of built-in operators in R that can help in wrangling our data and using within tidyverse functions. 

See knitted html for pretty tables.

**Arithmetic** operators allow us to carry out mathematical operations:

| Operator | Description |
|------|:---------|
| + | Add |
| - | Subtract |
| * | Multiply |
| / | Divide |
| ^ | Exponent |
| %% | Modulus (remainder from division) |

**Relational** operators allow us to compare values:

| Operator | Description |
|------|:---------|
| < | Less than |
| > | Greater than |
| <= | Less than or equal to |
| >= | Greater than or equal to |
| == | Equal to |
| != | Not equal to |

* Arithmetic and relational operators work on vectors.

**Logical** operators allow us to carry out boolean operations:

| Operator | Description |
|---|:---|
| ! | Not |
| \| | Or (element_wise) |
| & | And (element-wise) |
| \|\| | Or |
| && | And |

## Base-R vs tidyverse

The [tidyverse](https://www.tidyverse.org/) is a collection of packages that were designed under a specific philosophy of making data analysis in R easy, reproducible, and consistent. The tidyverse packages:

* has an easy-to-read syntax
* can be much quicker (to write)  
* are comprehensive in covering a wide variety of applications (e.g. [`ggplot2`](https://ggplot2.tidyverse.org/) for plotting, [`dplyr`](https://dplyr.tidyverse.org/) for data manipulation, ..., etc.)

Most base-r operations can be replaced with tidyverse code. However, in genomics research, this is less true because many genomics analysis workflows rely on [**Bioconductor**](https://www.bioconductor.org/).

[Bioconductor](https://www.bioconductor.org/) is an online R package repository specifically for analyzing and storing genomic data. If you are in genomics, it is highly likely you will use these packages. Bioconductor is basically all based in base-R code, so learning *some* base-R is going to be a requirement for any genomics analysis.


## Tidyverse syntax (2 min)

- Almost all functions from a **tidyverse** package will accept a `tibble` or `data.frame` as the first argument.

```
function(a_tibble, operations_involving_columns)
```

- **tidyverse** functions tend to be [named](https://principles.tidyverse.org/function-names.html) as verbs. (e.g. `select()`, `pivot_longer()`, `str_extract()`)

- More information on the design principles behind tidyverse packages can be found [here](https://principles.tidyverse.org/index.html).

# Basic `dplyr` functions

We're going to be working with the gapminder dataframe we loaded before. Additionally we need to we need to load in the `dplyr` R package. This is a package within the tidyverse that stands for data frame applyer and contains functions to help wrangle data in data.frames or tibbles. 



```r
# load your package here:
library(FILL_THIS_IN)
```

```
## Error in library(FILL_THIS_IN): there is no package called 'FILL_THIS_IN'
```

We're going to go over these dplyr functions:

1. select 
2. arrange
3. filter 
4. mutate
5. grouped operations in dplyr:
    a. group_by
    b. summarize
6. across
### `select()` (8 min)

`select()` allows you to subset to the columns(or variables) that you specify. 

1. Make a data frame containing the columns `year`, `lifeExp`, `country` from the gapminder data, in that order.


```r
select(gapminder, FILL_THIS_IN)
```

```
## Error in select(gapminder, FILL_THIS_IN): could not find function "select"
```


2. Select all variables, from `country` to `lifeExp`.


```r
# This will work:
select(gapminder, country, continent, year, lifeExp)
```

```
## Error in select(gapminder, country, continent, year, lifeExp): could not find function "select"
```

```r
# Better way:
select(gapminder, FILL_THIS_IN)
```

```
## Error in select(gapminder, FILL_THIS_IN): could not find function "select"
```


3. Select all variables, except `lifeExp`.


```r
select(gapminder, FILL_THIS_IN)
```

```
## Error in select(gapminder, FILL_THIS_IN): could not find function "select"
```

4. Put `continent` first. Hint: use the `everything()` function.


```r
select(gapminder, FILL_THIS_IN, FILL_THIS_IN)
```

```
## Error in select(gapminder, FILL_THIS_IN, FILL_THIS_IN): could not find function "select"
```

### `arrange()` (8 min)

1. Order by year.


```r
arrange(gapminder, FILL_THIS_IN)
```

```
## Error in arrange(gapminder, FILL_THIS_IN): could not find function "arrange"
```

2. Order by year, in descending order.


```r
arrange(gapminder, FILL_THIS_IN)
```

```
## Error in arrange(gapminder, FILL_THIS_IN): could not find function "arrange"
```

3. Order by year, then by life expectancy.


```r
arrange(gapminder, FILL_THIS_IN, FILL_THIS_IN)
```

```
## Error in arrange(gapminder, FILL_THIS_IN, FILL_THIS_IN): could not find function "arrange"
```

## Piping, `%>%` (8 min)

*Piping* refers to using the `%>%` operator to write nested function calls in a more readable manner.

- Takes an output as the input for the first argument of the next function.

- Think of `%>%` as the word "then"!

**Demonstration:** Here I want to combine `select()` Task 1 with `arrange()` Task 3.

This is how I could do it by *nesting* the two function calls, **without piping**:


```r
# Nesting function calls can be hard to read
arrange(select(gapminder, year, lifeExp, country), year, lifeExp)
```

Now using **with piping**:


```r
# alter the function above to include 2 "pipes"
FILL_THIS_IN
```

```
## Error in eval(expr, envir, enclos): object 'FILL_THIS_IN' not found
```


## `filter()` (6 min)

Use `filter()` to subset to rows within your data where the condition you specify is TRUE. 

1. Only take data with population greater than 100 million.


```r
gapminder %>%
  filter(FILL_THIS_IN)
```

```
## Error in gapminder %>% filter(FILL_THIS_IN): could not find function "%>%"
```

2. Your turn: of those rows filtered from step 1., only take data from Asia.


```r
gapminder %>%
  filter(FILL_THIS_IN)
```

```
## Error in gapminder %>% filter(FILL_THIS_IN): could not find function "%>%"
```

3. Only take data from countries Brazil and China. 


```r
gapminder %>%
  filter(FILL_THIS_IN)
```

```
## Error in gapminder %>% filter(FILL_THIS_IN): could not find function "%>%"
```

## `mutate()` (8 min)

The `mutate()` function _creates_ new columns in the tibble by transforming other variables. Like `select()`, `filter()`, and `arrange()`, the `mutate()` function also takes a tibble as its first argument, and returns a tibble. 

The general syntax is:

```
mutate(tibble, NEW_COLUMN_NAME = CALCULATION)
```

1. Make a new column named `GDP` that equals to multiplying GPD per capita with population.


```r
gapminder %>%
  mutate(FILL_THIS_IN)
```

```
## Error in gapminder %>% mutate(FILL_THIS_IN): could not find function "%>%"
```

2. Make a new column named `GDP_bill`, that is GDP in billions.


```r
gapminder %>%
  mutate(FILL_THIS_IN)
```

```
## Error in gapminder %>% mutate(FILL_THIS_IN): could not find function "%>%"
```

Your turn: Make a new column called `cc` that pastes the country name followed by the continent, separated by a comma. (Hint: use the `paste` function with the `sep=", "` argument).




# `dplyr`: grouped operations

*Most of this material was taken/modified from the [STAT545 lecture: Intro to data wrangling, Part II](https://stat545guidebook.netlify.com/intro-to-data-wrangling-part-ii.html)*

## Resources

- [STAT545 lecture: Intro to data wrangling, Part II](https://stat545guidebook.netlify.com/intro-to-data-wrangling-part-ii.html)
- [r4ds: transform](http://r4ds.had.co.nz/transform.html)
- [Intro to `dplyr` vignette](https://cran.r-project.org/web/packages/dplyr/vignettes/dplyr.html)

## `summarize()` (3 min)

Like `mutate()`, the `summarize()` function also creates new columns, but the calculations that make the new columns must reduce down to a single number.

For example, let’s compute the mean and standard deviation of life expectancy in the gapminder data set:


```r
gapminder %>% 
  summarize(mu    = FILL_THIS_IN,
            sigma = FILL_THIS_IN)
```

```
## Error in gapminder %>% summarize(mu = FILL_THIS_IN, sigma = FILL_THIS_IN): could not find function "%>%"
```

Notice that all other columns were dropped. This is necessary, because there’s no obvious way to compress the other columns down to a single row. This is unlike `mutate(`), which keeps all columns.

As it is, this is hardly useful. But that’s outside of the context of *grouping*, coming up next...

## `group_by()` (15 min)

* `group_by()` allows you to apply functions to separate chunks of your data frame, where the chunks are defined by a specified grouping variable.

Let’s group the gapminder dataset by continent and year:


```r
gapminder %>% 
  group_by(continent, year)
```

```
## Error in gapminder %>% group_by(continent, year): could not find function "%>%"
```

The only thing different from a regular tibble is the indication of grouping variables above the tibble. This means that the tibble is recognized as having “chunks” defined by unique combinations of continent and year:

- Asia in 1952 is one chunk.
- Asia in 1957 is another chunk.
- Europe in 1952 is another chunk.
- etc…

Notice that the data frame isn’t rearranged by chunk!

Now that the tibble is grouped, operations that you do on a grouped tibble will be done independently within each chunk, as if no other chunks exist.

1. What is the mean and standard deviation of life expectancy for each year for every continent?


```r
gapminder %>% 
  group_by(continent, year) %>% 
  FILL_THIS_IN(mu    = FILL_THIS_IN,
            sigma = FILL_THIS_IN)
```

```
## Error in gapminder %>% group_by(continent, year) %>% FILL_THIS_IN(mu = FILL_THIS_IN, : could not find function "%>%"
```

2. In the gapminder dataset, how many rows are there for each continent? Hint: use the convenience function `dplyr::n()`


```r
# solution 1
gapminder %>%
  group_by(FILL_THIS_IN) %>%
  FILL_THIS_IN
```

```
## Error in gapminder %>% group_by(FILL_THIS_IN) %>% FILL_THIS_IN: could not find function "%>%"
```

```r
# solution 2: use dplyr::count()
```

2. (a) What's the minimum life expectancy for each continent and each year? (b) Arrange by min life expectancy.


```r
gapminder %>% 
  group_by(FILL_THIS_IN, FILL_THIS_IN) %>% 
  FILL_THIS_IN(min_life = min(FILL_THIS_IN)) %>%
  arrange(FILL_THIS_IN)
```

```
## Error in gapminder %>% group_by(FILL_THIS_IN, FILL_THIS_IN) %>% FILL_THIS_IN(min_life = min(FILL_THIS_IN)) %>% : could not find function "%>%"
```

3. Calculate the growth in population since the first year on record _for each country_. Here's another convenience function for you: `dplyr::first()`. 


# `across()` (10 min.)

* `across()` allows you to easily perform multiple dplyr operations to transform data in multiple columns. 

The general syntax is:

```
tibble %>% DPLYR_FUN(across,COLNAME,FUNCTION_FOR_COLs)
```
### Additional Resources for `across()`
[Hadley Wickham's blogpost on across](https://www.tidyverse.org/blog/2020/04/dplyr-1-0-0-colwise/) : Some of the info in this section is taken from here

### Use cases for across

- Say you would like to summarize the mean and median values for lifeExp, gdpPercap and pop in the gapminder dataset by continent and year.

**Without across:**

Earlier we used the `summarize()` function to achieve this. 


```r
gapminder %>% 
  group_by(FILL_THIS_IN) %>%
  summarize(mean(FILL_THIS_IN),mean(FILL_THIS_IN), mean(FILL_THIS_IN),median(FILL_THIS_IN),median(FILL_THIS_IN), median(FILL_THIS_IN))
```

```
## Error in gapminder %>% group_by(FILL_THIS_IN) %>% summarize(mean(FILL_THIS_IN), : could not find function "%>%"
```
With multiple columns this can get long, tedious, and subject to errors during copy-pasting.

**With across:**


```r
gapminder %>% 
  group_by(continent,year) %>%
  summarize(across(FILL_THIS_IN,FILL_THIS_IN))
```

```
## Error in gapminder %>% group_by(continent, year) %>% summarize(across(FILL_THIS_IN, : could not find function "%>%"
```
Alternatively:


```r
gapminder %>% 
  group_by(continent,year) %>%
  summarize(across(c(FILL_THIS_IN),FILL_THIS_IN)))
```

```
## Error: <text>:3:50: unexpected ')'
## 2:   group_by(continent,year) %>%
## 3:   summarize(across(c(FILL_THIS_IN),FILL_THIS_IN)))
##                                                     ^
```

Or if you were just looking for the mean you could do this:


```r
gapminder %>% 
  group_by(continent,year) %>%
  summarize(across(c(FILL_THIS_IN),FILL_THIS_IN))
```

```
## Error in gapminder %>% group_by(continent, year) %>% summarize(across(c(FILL_THIS_IN), : could not find function "%>%"
```

Your turn: 

1. Use `across()` to round the `lifeExp`, `gdpPercap`, `pop` columns grouped by continent and year in the gapminder. Hint use the `round` function in across. 




