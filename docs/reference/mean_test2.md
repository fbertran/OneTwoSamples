# Two sided or one sided test of hypothesis of `mu1` and `mu2` of two normal samples

Compute the two sided or one sided test of hypothesis of `mu1` and `mu2`
of two normal samples when the population variances are known, unknown
equal, or unknown unequal.

## Usage

``` r
mean_test2(x, y, sigma = c(-1, -1), var.equal = FALSE, side = 0)
```

## Arguments

- x:

  A numeric vector.

- y:

  A numeric vector.

- sigma:

  A numeric vector of length 2, which contains the standard deviations
  of two populations. When the standard deviations are known, input it,
  then the function computes the interval endpoints using normal
  population; when the standard deviations are unknown, ignore it, now
  we need to consider whether the two populations have equal variances.
  See `var.equal` below.

- var.equal:

  A logical variable indicating whether to treat the two variances as
  being equal. If `TRUE` then the pooled variance is used to estimate
  the variance otherwise the Welch (or Satterthwaite) approximation to
  the degrees of freedom is used.

- side:

  A parameter used to control two sided or one sided test of hypothesis.
  When inputting `side = 0` (default), the function computes two sided
  test of hypothesis, and `H1: mu1 != mu2`; when inputting `side = -1`
  (or a number \< 0), the function computes one sided test of
  hypothesis, and `H1: mu1 < mu2`; when inputting `side = 1` (or a
  number \> 0), the function computes one sided test of hypothesis, and
  `H1: mu1 > mu2`.

## Value

A data.frame with variables:

- mean :

  The difference of sample means xb-yb.

- df :

  The degree of freedom.

- statistic :

  The statistic, when `all(sigma>=0)`, `statistic = Z`; otherwise,
  `statistic = T`.

- p_value :

  The P value.

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
#>  [1] 0.8694650 0.9705661 0.7451797 1.0790655 0.6134213 1.2109006 0.8358040
#>  [8] 0.8724738 0.9693751 0.7167187
y=rnorm(20, mean = 2, sd = 0.3); y
#>  [1] 2.182195 2.026518 1.528918 2.093852 2.195804 1.997613 2.518110 2.625940
#>  [9] 1.892496 1.567363 2.114383 2.027209 2.048629 2.106785 1.892086 1.967412
#> [17] 2.548336 1.411425 2.283795 2.164689
mean_test2(x, y, sigma = c(0.2, 0.3), side = 1)
#>        mean df         Z p_value
#> 1 -1.171381 30 -12.70541       1
mean_test2(x, y, var.equal = TRUE, side = 1)
#>        mean df         T p_value
#> 1 -1.171381 28 -10.86827       1
mean_test2(x, y, side = 1)
#>        mean       df         T p_value
#> 1 -1.171381 27.44942 -13.01289       1
```
