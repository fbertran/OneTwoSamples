# Two sided or one sided interval estimation of `sigma1^2 / sigma2^2` of two normal samples

Compute the two sided or one sided interval estimation of
`sigma1^2 / sigma2^2` of two normal samples when the population means
are known or unknown.

## Usage

``` r
interval_var4(x, y, mu = c(Inf, Inf), side = 0, alpha = 0.05)
```

## Arguments

- x:

  A numeric vector.

- y:

  A numeric vector.

- mu:

  The population means. When it is known, input it, and the function
  computes the interval endpoints using an F distribution with degree of
  freedom `(n1, n2)`. When it is unknown, ignore it, and the function
  computes the interval endpoints using an F distribution with degree of
  freedom `(n1-1, n2-1)`.

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

- rate :

  The estimate of the ratio of population variances, `rate = Sx2/Sy2`.
  When the population means `mu` is known, `Sx2 = 1/n1*sum((x-mu[1])^2)`
  and `Sy2 = 1/n2*sum((y-mu[2])^2`. When `mu` is unknown, `Sx2 = var(x)`
  and `Sy2 = var(y)`.

- df1 :

  The first degree of freedom.

- df2 :

  The second degree of freedom.

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
#>  [1] 1.3168995 1.0011351 0.8703591 1.3717326 1.1656606 1.2398071 1.1200102
#>  [8] 1.0117520 0.7420473 0.9747332
y=rnorm(20, mean = 2, sd = 0.3); y
#>  [1] 2.115196 1.837262 2.066782 1.806542 1.875650 1.311562 1.810536 1.840571
#>  [9] 2.213104 1.925540 2.202581 1.821395 2.033027 2.111601 1.817043 2.313182
#> [17] 1.909188 2.425184 1.739870 1.334558
interval_var4(x, y, mu = c(1,2), side = -1)
#>        rate df1 df2 a        b
#> 1 0.5273226  10  20 0 1.462802
interval_var4(x, y)
#>        rate df1 df2         a        b
#> 1 0.5041512   9  19 0.1750493 1.856959
```
