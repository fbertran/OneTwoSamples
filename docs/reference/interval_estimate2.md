# Two sided interval estimation of `mu1-mu2` of two normal samples

Compute the two sided interval estimation of `mu1-mu2` of two normal
samples when the population variances are known, unknown equal, or
unknown unequal.

## Usage

``` r
interval_estimate2(x, y, sigma = c(-1, -1), var.equal = FALSE, alpha = 0.05)
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
#>  [1] 0.9732006 0.6179825 0.9441526 0.9373108 1.2134616 1.0140070 0.8721753
#>  [8] 0.9900070 0.9497033 1.0889594
y=rnorm(20, mean = 2, sd = 0.3); y
#>  [1] 2.826625 2.013959 2.173313 2.035458 1.426484 2.258626 1.927029 1.938174
#>  [9] 2.005753 2.008868 2.164948 1.317766 2.804767 1.891634 2.064007 2.322304
#> [17] 1.800474 2.334186 1.926231 1.646731

interval_estimate2(x, y, sigma = c(0.2, 0.3))
#>        mean df         a          b
#> 1 -1.084271 30 -1.264971 -0.9035711
interval_estimate2(x, y, var.equal = TRUE)
#>        mean df         a          b
#> 1 -1.084271 28 -1.336608 -0.8319335
interval_estimate2(x, y)
#>        mean       df        a          b
#> 1 -1.084271 27.41274 -1.28135 -0.8871912
```
