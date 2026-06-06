# Two sided interval estimation of `mu` of one normal sample

Compute the two sided interval estimation of `mu` of one normal sample
when the population variance is known or unknown.

## Usage

``` r
interval_estimate1(x, sigma = -1, alpha = 0.05)
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
#>  [1] 1.3777010 0.9805110 0.8128305 0.9968099 0.8346422 0.6975201 1.1870726
#>  [8] 1.0352977 1.0487371 1.3247098
interval_estimate1(x, sigma = 0.2)
#>       mean df         a        b
#> 1 1.029583 10 0.9056242 1.153542
interval_estimate1(x)
#>       mean df         a       b
#> 1 1.029583  9 0.8728165 1.18635
```
