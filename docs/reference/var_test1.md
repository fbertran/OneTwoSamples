# Two sided or one sided test of hypothesis of `sigma^2` of one normal sample

Compute the two sided or one sided test of hypothesis of `sigma^2` of
one normal sample when the population mean is known or unknown.

## Usage

``` r
var_test1(x, sigma2 = 1, mu = Inf, side = 0)
```

## Arguments

- x:

  A numeric vector.

- sigma2:

  `sigma2` is `sigma0^2` in the null hypothesis. Default is 1, i.e.,
  `H0: sigma^2 = 1`.

- mu:

  The population mean. `mu < Inf` indicates it is known, `mu == Inf`
  indicates it is unknown. Default to unknown population mean.

- side:

  A parameter used to control two sided or one sided test of hypothesis.
  When inputting `side = 0` (default), the function computes two sided
  test of hypothesis, and `H1: sigma^2 != sigma0^2`; when inputting
  `side = -1` (or a number \< 0), the function computes one sided test
  of hypothesis, and `H1: sigma^2 < sigma0^2`; when inputting `side = 1`
  (or a number \> 0), the function computes one sided test of
  hypothesis, and `H1: sigma^2 > sigma0^2`.

## Value

A data.frame with variables:

- var :

  The estimate of the population variance. When the population mean `mu`
  is known, `var = mean((x-mu)^2)`. When `mu` is unknown,
  `var = var(x)`.

- df :

  The degree of freedom.

- chisq2 :

  The chisquare statistic.

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
#>  [1] 1.0682239 0.7741274 1.2866047 1.3960800 0.9265557 0.7911731 1.1139439
#>  [8] 0.9729891 1.4803236 0.9921520
var_test1(x, sigma2 = 0.2^2, mu = 1, side = 1)
#>          var df   chisq2 P_value
#> 1 0.05881824 10 14.70456 0.14321
var_test1(x, sigma2 = 0.2^2, side = 1)
#>         var df   chisq2   P_value
#> 1 0.0582038  9 13.09586 0.1583167
```
