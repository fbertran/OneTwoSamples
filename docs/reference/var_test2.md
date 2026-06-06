# Two sided or one sided test of hypothesis of `sigma1^2` and `sigma2^2` of two normal samples

Compute the two sided or one sided test of hypothesis of `sigma1^2` and
`sigma2^2` of two normal samples when the population means are known or
unknown.

## Usage

``` r
var_test2(x, y, mu = c(Inf, Inf), side = 0)
```

## Arguments

- x:

  A numeric vector.

- y:

  A numeric vector.

- mu:

  The population means. When it is known, input it, and the function
  computes the F value using an F distribution with degree of freedom
  `(n1, n2)`. When it is unknown, ignore it, and the function computes
  the F value using an F distribution with degree of freedom
  `(n1-1, n2-1)`.

- side:

  A parameter used to control two sided or one sided test of hypothesis.
  When inputting `side = 0` (default), the function computes two sided
  test of hypothesis, and `H1: sigma1^2 != sigma2^2`; when inputting
  `side = -1` (or a number \< 0), the function computes one sided test
  of hypothesis, and `H1: sigma1^2 < sigma2^2`; when inputting
  `side = 1` (or a number \> 0), the function computes one sided test of
  hypothesis, and `H1: sigma1^2 > sigma2^2`.

## Value

A data.frame with variables:

- rate :

  The estimate of the ratio of population variances, `rate = Sx2/Sy2`.
  When the population means `mu` is known, `Sx2 = 1/n1*sum((x-mu[1])^2)`
  and `Sy2 = 1/n2*sum((y-mu[2])^2`. When `mu` is unknown, `Sx2 = var(x)`
  and `Sy2 = var(y)`.

- df1 :

  The first degree of freedom.

- df2 :

  The second degree of freedom.

- F :

  The F statistic.

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
#>  [1] 1.0056004 0.8513454 1.0377585 0.6390083 1.2931110 1.0306507 1.4345223
#>  [8] 1.0951019 0.8580107 1.1221453
y=rnorm(20, mean = 2, sd = 0.3); y
#>  [1] 1.719771 1.623910 2.087434 1.867012 2.000332 2.022302 1.823144 1.829399
#>  [9] 1.959446 2.353426 1.542930 2.178184 2.099885 2.318930 1.908745 2.111006
#> [17] 2.080130 1.837244 2.362360 2.348121
var_test2(x, y, mu = c(1, 2), side = 1)
#>        rate df1 df2         F  P_value
#> 1 0.8681847  10  20 0.8681847 0.575379
var_test2(x, y, side = 1)
#>        rate df1 df2         F   P_value
#> 1 0.8905436   9  19 0.8905436 0.5511375
```
