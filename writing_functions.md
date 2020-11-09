Iteration
================

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.4     v dplyr   1.0.2
    ## v tidyr   1.1.2     v stringr 1.4.0
    ## v readr   1.4.0     v forcats 0.5.0

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(rvest)
```

    ## Loading required package: xml2

    ## 
    ## Attaching package: 'rvest'

    ## The following object is masked from 'package:purrr':
    ## 
    ##     pluck

    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

## Setting options

``` r
library(tidyverse)

knitr::opts_chunk$set(
  fig.width = 6,
  fig.asp = 0.6,
  out.width= "90%"
)


theme_set(theme_minimal() + theme(legend.position = "bottom")
          

          options(
            ggplot2.continuous.colour= "viridis"
            ggplot2.continuous.fill = "viridis"
          )        


scale_colour_discrete = scale_color_viridis_d
scale_fill_discrete = scale_fill_viridis_d
```

## Do something simple

``` r
x_vec= rnorm(30, mean = 5, sd=3)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1] -0.478875244  1.312339337  1.230718250 -0.210760446 -0.218341463
    ##  [6]  1.749505809  0.338558347 -0.837029932 -0.550534571  0.016192111
    ## [11] -0.682258732  1.690594572 -0.384554852 -1.162522025  0.102788651
    ## [16]  1.107145732 -0.897359125  2.144877413 -1.078204936 -0.335000222
    ## [21]  0.182846462  0.034648331  1.303610994 -0.005960336  0.193258426
    ## [26] -0.857609708 -1.791821236  0.309721342 -1.453289211 -0.772683736

I want a function to compute z-scores

``` r
z_scores = function(x) {
  
  if (!is.numeric(x)) {
    stop("Input must be numeric")
  }
  
  if (length(x) < 3) {
    stop("Input must have at least three numbers")
  }
  
  z = (x - mean(x))/ sd(x)
  
  return(z)
  
}

z_scores(x_vec)
```

    ##  [1] -0.478875244  1.312339337  1.230718250 -0.210760446 -0.218341463
    ##  [6]  1.749505809  0.338558347 -0.837029932 -0.550534571  0.016192111
    ## [11] -0.682258732  1.690594572 -0.384554852 -1.162522025  0.102788651
    ## [16]  1.107145732 -0.897359125  2.144877413 -1.078204936 -0.335000222
    ## [21]  0.182846462  0.034648331  1.303610994 -0.005960336  0.193258426
    ## [26] -0.857609708 -1.791821236  0.309721342 -1.453289211 -0.772683736

Try my function on some other things. These should give errors

``` r
z_scores(3)
```

    ## Error in z_scores(3): Input must have at least three numbers

``` r
z_scores("my name is jeff")
```

    ## Error in z_scores("my name is jeff"): Input must be numeric

``` r
z_scores(mtcars)
```

    ## Error in z_scores(mtcars): Input must be numeric

``` r
z_scores(c(TRUE, TRUE, FALSE, TRUE))
```

    ## Error in z_scores(c(TRUE, TRUE, FALSE, TRUE)): Input must be numeric
