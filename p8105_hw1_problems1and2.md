Data Science 1: Homework 1
================
Caroline Andy
9/18/2020

Here are my solutions to homework 1.

``` r
library(tidyverse)
```

**Problem 1**

Generate a data frame containing the required elements.

``` r
prob1_df = 
  tibble(
    samp = rnorm(10),
    samp_gt_0 = samp > 0,
    char_vec = c("a","b","c","d","e","f","g","h","i","j"),
    factor_vec = factor(c("level_1","level_1","level_1","level_2","level_2","level_2","level_3","level_3","level_3","level_3")))
```

*Calculating mean*

Next I will attempt to take the mean of each variable.

``` r
mean(pull(prob1_df, samp))
```

    ## [1] -0.3275954

``` r
mean(pull(prob1_df, samp_gt_0))
```

    ## [1] 0.4

``` r
mean(pull(prob1_df, char_vec))
```

    ## [1] NA

``` r
mean(pull(prob1_df, factor_vec))
```

    ## [1] NA

I am able to take the mean of my numerical and logical variables, samp
and samp\_gt\_0, but not my character and factor variables, char\_vec
and factor\_vec.

*Converting variable types*

In some cases, I can explicitly convert variables from one type to
another. Here, I will attempt to convert each of my variables to
numeric.

``` r
as.numeric(pull(prob1_df, samp))
as.numeric(pull(prob1_df, samp_gt_0))
as.numeric(pull(prob1_df, char_vec))
as.numeric(pull(prob1_df, factor_vec))
```

The as.numeric function generates numeric variable outputs for the
numeric and logical vectors, samp and samp\_gt\_0. The samp field,
numeric to begin with, remained unchanged. The mean of samp, generated
above, was calculated using its numeric entries.

The samp\_gt\_0 field was a logical vector with 0 and 1 values denoting
whether the samp entries are above or below 0. This binary field was
converted into numeric using the as.numeric function. In the above
example, the mean function generated the mean for samp\_gt\_0 by first
converting its logical entries into numeric values.

The character vector was unable to be converted into a numeric field; we
cannot calculate a mean for this variable.

The factor vector was able to be coerced into a numeric variable;
however, the mean cannot be calculated until the variable is first
manually converted into a numeric variable.

*Multiplying coerced variables*

Now I will multiply the random sample variable by the logical vector.

``` r
as.numeric(pull(prob1_df, samp_gt_0)) * pull(prob1_df, samp) 
```

    ##  [1] 0.0000000 0.0000000 0.0000000 0.1510347 0.0000000 0.1949417 0.0000000
    ##  [8] 0.0000000 0.5836468 0.3199950

Now I will convert the logical vector to a factor, and multiply the
random sample by the result.

``` r
as.factor(pull(prob1_df, samp_gt_0)) * pull(prob1_df, samp) 
```

    ##  [1] NA NA NA NA NA NA NA NA NA NA

Now I will convert the logical vector to a factor and then convert the
result to numeric, and multiply the random sample by the result

``` r
as.numeric(as.factor(pull(prob1_df, samp_gt_0))) * pull(prob1_df, samp) 
```

    ##  [1] -0.03753744 -0.03715824 -2.21060612  0.30206938 -1.50109240  0.38988334
    ##  [7] -0.65574226 -0.08343567  1.16729355  0.63999004

**Problem 2**

*Loading and describing dataset*

For the following problem, I will load the penguins dataset.

``` r
data("penguins", package = "palmerpenguins")
```

The penguin dataset contains 344 rows, where each row corresponds with
an observed penguin. This dataset contains 8 columns, which include the
following variables: penguin species, island, bill length, bill depth,
flipper length, body mass, sex and year.

Data are collected from years 2007 to 2009. There are 3 different
species (Adelie, Chinstrap, Gentoo), and 3 different islands (Biscoe,
Dream, Torgersen) represented in the penguins dataset.

The mean bill length is 43.92 millimeters. Mean body mass is 4201.75
grams. The mean flipper length is 200.92 millimeters.

*Generating a scatterplot*

Next I will generate a scatterplot graphing bill length and flipper
length for each observed penguin, where dot color is determined by
penguin species.

``` r
# generating scatterplot
library(ggplot2)
penguinsggplot <- ggplot(penguins, aes(x = bill_length_mm, y = flipper_length_mm, color = species)) + geom_point()
#viewing scatterplot
penguinsggplot
```

![](p8105_hw1_problems1and2_files/figure-gfm/scatterplot-1.png)<!-- -->

``` r
# exporting scatterplot
ggsave("penguinsggplot.pdf")
```

    ## Saving 7 x 5 in image
