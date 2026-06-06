# Two sided interval estimation of `sigma^2` of one normal sample

Compute the two sided interval estimation of `sigma^2` of one normal
sample when the population mean is known or unknown.

## Usage

``` r
interval_var1(x, mu = Inf, alpha = 0.05)
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
#>  [1] 1.1584902 1.3630062 0.8126055 1.1722601 1.1243280 0.5711336 1.0969443
#>  [8] 0.9105451 1.1092194 1.2888373
interval_var1(x, mu = 1)
#>         var df          a         b
#> 1 0.0533823 10 0.02606153 0.1644064
interval_var1(x)
#>         var df          a         b
#> 1 0.0552148  9 0.02612308 0.1840228
```
