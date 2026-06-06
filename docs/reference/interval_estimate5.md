# Two sided or one sided interval estimation of `mu1-mu2` of two normal samples

Compute the two sided or one sided interval estimation of `mu1-mu2` of
two normal samples when the population variances are known, unknown
equal, or unknown unequal.

## Usage

``` r
interval_estimate5(x, y, sigma = c(-1, -1), var.equal = FALSE, side = 0, alpha = 0.05)
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

  The difference of sample means xb-yb.

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
#>  [1] 0.8441429 1.3078899 1.1400111 1.0235185 0.9432755 1.0995818 1.3219886
#>  [8] 1.3722272 1.0772498 0.7062713
y=rnorm(20, mean = 2, sd = 0.3); y
#>  [1] 2.215257 2.039573 1.440223 1.723801 2.361209 2.080180 1.459922 1.605099
#>  [9] 1.928436 1.657061 1.764657 1.751669 2.283301 1.808092 1.347131 1.934857
#> [17] 2.173974 2.587151 1.714219 1.439784

interval_estimate5(x, y, sigma = c(0.2, 0.3), side = -1)
#>         mean df    a          b
#> 1 -0.7821642 30 -Inf -0.6305162
interval_estimate5(x, y, var.equal = TRUE)
#>         mean df         a          b
#> 1 -0.7821642 28 -1.025611 -0.5387177
interval_estimate5(x, y)
#>         mean       df         a          b
#> 1 -0.7821642 26.24205 -0.992436 -0.5718925
```
