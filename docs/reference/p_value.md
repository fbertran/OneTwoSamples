# Compute the P value

Compute the P value of a cumulative distribution function (cdf).

## Usage

``` r
p_value(cdf, x, paramet = numeric(0), side = 0)
```

## Arguments

- cdf:

  The cumulative distribution function. For normal distribution,
  `cdf = pnorm`.

- x:

  A given value to compute the P value.

- paramet:

  The parameter of the corresponding distribution. For normal
  distribution, `paramet = c(mu, sigma)`.

- side:

  A parameter indicating whether to compute one sided or two sided P
  value. When inputting `side = -1` (or a number \< 0), the function
  computes a left side P value; when inputting `side = 1` (or a number
  \> 0), the function computes a right side P value; when inputting
  `side = 0` (default), the function computes a two sided P value.

## Value

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
p_value(pnorm, x = 0, side = 1)
#> [1] 0.5
p_value(pt, x = 0, paramet = 5, side = 1)
#> [1] 0.5
```
