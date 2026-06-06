# Two sided interval estimation of `mu` of one non-normal sample with large sample size

Compute the two sided interval estimation of `mu` of one non-normal
sample with large sample size when the population variance is known or
unknown.

## Usage

``` r
interval_estimate3(x, sigma = -1, alpha = 0.05)
```

## Arguments

- x:

  A numeric vector.

- sigma:

  The standard deviation of the population. `sigma>=0` indicates it is
  known, `sigma<0` indicates it is unknown. Default to unknown standard
  deviation.

- alpha:

  The significance level, a real number in \[0, 1\]. Default to 0.05.
  1-alpha is the degree of confidence.

## Value

A data.frame with variables:

- mean :

  The sample mean.

- a :

  The confidence lower limit.

- b :

  The confidence upper limit.

## References

Zhang, Y. Y., Wei, Y. (2013), One and two samples using only an R
funtion,
[doi:10.2991/asshm-13.2013.29](https://doi.org/10.2991/asshm-13.2013.29)
.

## Author

Ying-Ying Zhang (Robert) <robertzhangyying@qq.com>

## Examples

``` r
x = rexp(50, 1/2); x
#>  [1] 0.765757945 0.308262778 0.749790982 2.834441237 0.051918341 0.374215161
#>  [7] 3.907787722 0.799317429 3.073531688 1.847652789 1.403940160 2.658441947
#> [13] 1.276329787 0.805944469 0.297973708 0.006233206 0.607387130 0.671263058
#> [19] 2.650079973 2.196284881 0.952366246 0.657141971 4.886073488 0.106721545
#> [25] 4.501601542 0.746276842 3.390559893 0.446185149 0.139539480 0.531464599
#> [31] 0.044489941 0.291552590 6.074501604 0.339542288 1.692191707 0.409996688
#> [37] 0.359350226 1.036633519 1.344301224 1.051277879 2.724453771 2.981786176
#> [43] 4.745921854 0.623930505 0.408015436 0.627983319 2.020831671 0.991458505
#> [49] 3.312639151 6.493250340
interval_estimate3(x)
#>       mean        a        b
#> 1 1.624372 1.171827 2.076917
```
