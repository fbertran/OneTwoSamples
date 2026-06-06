# Compute various descriptive statistics

Compute various descriptive statistics of x, such as mean, median,
skewness, and kurtosis, etc.

## Usage

``` r
data_outline(x)
```

## Arguments

- x:

  A numeric vector.

## Value

A data.frame with variables:

- N :

  The length.

- Mean :

  The mean.

- Var :

  The variance.

- std_dev :

  Standard deviation.

- Median :

  The median.

- std_mean :

  The standard error of the sample mean.

- CV :

  The coefficient of variation.

- CSS :

  The corrected sum of squares.

- USS :

  The uncorrected sum of squares.

- R :

  The extreme difference.

- R1 :

  The half extreme difference, or the difference of upper quartile and
  lower quartile.

- Skewness :

  The coefficient of skewness.

- Kurtosis :

  The coefficient of kurtosis.

- row.names :

  1\.

## References

Zhang, Y. Y., Wei, Y. (2013), One and two samples using only an R
funtion,
[doi:10.2991/asshm-13.2013.29](https://doi.org/10.2991/asshm-13.2013.29)
.

## Author

Ying-Ying Zhang (Robert) <robertzhangyying@qq.com>

## Examples

``` r
x=rnorm(10, mean = 1, sd = 0.2); x
#>  [1] 0.5125473 0.9988857 1.1243105 1.2296823 0.6356365 0.9505349 0.9511601
#>  [8] 0.9434589 0.8892601 1.1257964
data_outline(x)
#>    N      Mean        Var   std_dev    Median   std_mean       CV       CSS
#> 1 10 0.9361273 0.04821101 0.2195701 0.9508475 0.06943415 23.45515 0.4338991
#>        USS        R        R1   Skewness  Kurtosis
#> 1 9.197242 0.717135 0.1901445 -0.8422809 0.3876286
```
