# Two sided or one sided test of hypothesis of `mu` of one normal sample

Compute the two sided or one sided test of hypothesis of `mu` of one
normal sample when the population variance is known or unknown.

## Usage

``` r
mean_test1(x, mu = 0, sigma = -1, side = 0)
```

## Arguments

- x:

  A numeric vector.

- mu:

  `mu` is `mu0` in the null hypothesis. Default is 0, i.e.,
  `H0: mu = 0`.

- sigma:

  The standard deviation of the population. `sigma>=0` indicates it is
  known, `sigma<0` indicates it is unknown. Default to unknown standard
  deviation.

- side:

  A parameter used to control two sided or one sided test of hypothesis.
  When inputting `side = 0` (default), the function computes two sided
  test of hypothesis, and `H1: mu != mu0`; when inputting `side = -1`
  (or a number \< 0), the function computes one sided test of
  hypothesis, and `H1: mu < mu0`; when inputting `side = 1` (or a number
  \> 0), the function computes one sided test of hypothesis, and
  `H1: mu > mu0`.

## Value

A data.frame with variables:

- mean :

  The sample mean.

- df :

  The degree of freedom.

- statistic :

  The statistic, when `sigma>=0`,
  `statistic = Z = (xb-mu)/(sigma/sqrt(n))`; when `sigma<0`,
  `statistic = T = (xb-mu)/(sd(x)/sqrt(n))`.

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
#>  [1] 1.0753290 1.1944273 1.0517805 1.2414938 0.9461027 0.8603386 0.7023488
#>  [8] 1.4926738 1.1138596 0.7778598
mean_test1(x, mu = 1, sigma = 0.2, side = 1)
#>       mean df         Z   p_value
#> 1 1.045621 10 0.7213377 0.2353509
mean_test1(x, mu = 1)
#>       mean df         T   p_value
#> 1 1.045621  9 0.6122542 0.5555203
```
