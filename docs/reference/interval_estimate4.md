# Two sided or one sided interval estimation of `mu` of one normal sample

Compute the two sided or one sided interval estimation of `mu` of one
normal sample when the population variance is known or unknown.

## Usage

``` r
interval_estimate4(x, sigma = -1, side = 0, alpha = 0.05)
```

## Arguments

- x:

  A numeric vector.

- sigma:

  The standard deviation of the population. `sigma>=0` indicates it is
  known, `sigma<0` indicates it is unknown. Default to unknown standard
  deviation.

- side:

  A parameter used to control whether to compute two sided or one sided
  interval estimation. When computing the one sided upper limit, input
  `side = -1`; when computing the one sided lower limit, input
  `side = 1`; when computing the two sided limits, input `side = 0`
  (default).

- alpha:

  The significance level, a real number in \[0, 1\]. Default to 0.05.
  1-alpha is the degree of confidence.

## Value

A data.frame with variables:

- mean :

  The sample mean.

- df :

  The degree of freedom.

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
x=rnorm(10, mean = 1, sd = 0.2); x
#>  [1] 0.9528708 1.0088669 0.5760600 0.9343016 1.0924105 1.1387249 0.8582811
#>  [8] 0.9582206 1.0704558 1.3489427
interval_estimate4(x, sigma = 0.2, side = -1)
#>        mean df    a        b
#> 1 0.9939135 10 -Inf 1.097943
interval_estimate4(x, side = 1)
#>        mean df         a   b
#> 1 0.9939135  9 0.8776059 Inf
```
