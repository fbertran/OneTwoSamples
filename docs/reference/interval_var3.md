# Two sided or one sided interval estimation of `sigma^2` of one normal sample

Compute the two sided or one sided interval estimation of `sigma^2` of
one normal sample when the population mean is known or unknown.

## Usage

``` r
interval_var3(x, mu = Inf, side = 0, alpha = 0.05)
```

## Arguments

- x:

  A numeric vector.

- mu:

  The population mean. When it is known, input it, and the function
  computes the interval endpoints using a chi-square distribution with
  degree of freedom `n`. When it is unknown, ignore it, and the function
  computes the interval endpoints using a chi-square distribution with
  degree of freedom `n-1`.

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

- var :

  The estimate of the population variance. When the population mean `mu`
  is known, `var = mean((x-mu)^2)`. When `mu` is unknown,
  `var = var(x)`.

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
#>  [1] 0.9416208 0.8444366 0.9302892 1.2023435 0.9370456 0.9989236 0.7283394
#>  [8] 1.3145855 0.7601232 0.9854689
interval_var3(x, mu = 1, side = -1)
#>          var df a          b
#> 1 0.03078906 10 0 0.07813888
interval_var3(x)
#>          var df          a         b
#> 1 0.03279536  9 0.01551605 0.1093021
```
