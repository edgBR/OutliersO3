<!-- README.md is generated from README.Rmd. Please edit that file -->
OutliersO3
==========

OutliersO3 is for visualising results of outlier analyses. Overview of Outliers (O3) plots show which cases are identified as potential outliers for different combinations of variables from a dataset.

You can compare sets of outliers identified by up to six different methods. You can also compare results for a single method at up to three different tolerance levels.

Install in the usual way
------------------------

install.packages("OutliersO3")

What outliers are there amongst the genuine banknotes in the Swiss banknote dataset?
------------------------------------------------------------------------------------

Flury and Riedwyl introduced the famous banknote dataset in their excellent book on multivariate statistics. There are measurements on 100 genuine banknotes and on 100 counterfeit banknotes. Presumably the genuine notes should all be very similar.

The method mvBACON from *robustX* has been used to identify possible outliers. There are 6 numeric measurements of the notes, so there are 63 possible variable combinations. An O3 plot has one row for each variable combination for which outliers were found and those variables are specified by the relevant columns on the left of the plot. The cases identified as outliers for at least one combination each get a column to the right of the plot.

``` r
library(OutliersO3)
data(banknote, package="mclust")
data <- banknote %>% filter(Status=="genuine") %>% select(-Status)
pB <- O3prep(data, method="BAC", tols=c(0.05, 0.01, 0.001), boxplotLimits=c(6,10,12))
pX <- O3plotT(pB)
pX$gO3
```

![](man/figures/README-unnamed-chunk-3-1.png)

The O3 plot shows outliers found by the mvBACON method for three tolerance levels. Two banknotes, X71 and X5, are only identified for a few combinations at a level of 0.05. Two further banknotes, X40 and X70, are identified more often, sometimes at a level of 0.01. One banknote, X1, was identified an outlier at a level of 0.001 for the combination of attributes Length and Right. When it is identified as an outlier at other levels the attribute Right is always involved. The supporting parallel coordinate plot suggests why:

``` r
pX$gpcp
```

![](man/figures/README-unnamed-chunk-4-1.png) This plot also suggests that all five cases identified as potential outliers are relatively extreme on at least one of the six attributes.

There are more examples in the package vignettes.
