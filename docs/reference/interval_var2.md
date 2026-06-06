# Two sided interval estimation of `sigma1^2 / sigma2^2` of two normal samples

Compute the two sided interval estimation of `sigma1^2 / sigma2^2` of
two normal samples when the population means are known or unknown.

## Usage

``` r
interval_var2(x, y, mu = c(Inf, Inf), alpha = 0.05)
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
#>  [1] 1.0337024 1.0478129 1.0472643 0.9481762 1.1298091 0.7564718 1.1683941
#>  [8] 0.6761579 1.0528332 1.0194621
y=rnorm(20, mean = 2, sd = 0.3); y
#>  [1] 2.5366596 1.7033952 2.5672710 2.3602482 1.4560367 2.1111297 1.8551970
#>  [8] 2.0303853 2.0117232 2.3194477 0.8870452 2.4800535 2.3539010 1.2048454
#> [15] 1.7675672 2.1817633 1.9099158 2.3031477 1.4691850 2.2016608
interval_var2(x, y, mu = c(1,2))
#>        rate df1 df2          a         b
#> 1 0.1105592  10  20 0.03986024 0.3779515
interval_var2(x, y)
#>        rate df1 df2          a         b
#> 1 0.1160633   9  19 0.04029904 0.4275005
```
