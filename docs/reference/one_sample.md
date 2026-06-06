# Deal with one (normal) sample

Deal with one sample `x`, especially normal. Report descriptive
statistics, plot, interval estimation and test of hypothesis of `x`.

## Usage

``` r
one_sample(x, mu = Inf, sigma = -1, side = 0, alpha = 0.05)
```

## Arguments

- x:

  A numeric vector.

- mu:

  `mu` plays two roles.

  In two sided or one sided interval estimation (or test of hypothesis)
  of `sigma^2` of one normal sample, `mu` is the population mean. When
  it is known, input it, and the function computes the interval
  endpoints (or chi-square statistic) using a chi-square distribution
  with degree of freedom `n`. When it is unknown, ignore it (the
  default), and the function computes the interval endpoints (or
  chi-square statistic) using a chi-square distribution with degree of
  freedom `n-1`.

  In two sided or one sided test of hypothesis of `mu` of one normal
  sample, `mu` is `mu0` in the null hypothesis, and
  `mu0 = if (mu < Inf) mu else 0`.

- sigma:

  `sigma` plays two roles.

  In two sided or one sided interval estimation (or test of hypothesis)
  of `mu` of one normal sample, `sigma` is the standard deviation of the
  population. `sigma>=0` indicates it is known, and the function
  computes the interval endpoints (or `Z` statistic) using a standard
  normal distribution. `sigma<0` indicates it is unknown, and the
  function computes the interval endpoints (or `T` statistic) using a
  `t` distribution with degree of freedom `n-1`. Default to unknown
  standard deviation.

  In two sided or one sided test of hypothesis of `sigma^2` of one
  normal sample, `sigma` is `sigma0` in the null hypothesis. Default is
  1, i.e., `H0: sigma^2 = 1`.

- side:

  `side` plays two roles and is used in four places.

  In two sided or one sided interval estimation of `mu` of one normal
  sample, `side` is a parameter used to control whether to compute two
  sided or one sided interval estimation. When computing the one sided
  upper limit, input `side = -1`; when computing the one sided lower
  limit, input `side = 1`; when computing the two sided limits, input
  `side = 0` (default).

  In two sided or one sided interval estimation of `sigma^2` of one
  normal sample, `side` is a parameter used to control whether to
  compute two sided or one sided interval estimation. When computing the
  one sided upper limit, input `side = -1`; when computing the one sided
  lower limit, input `side = 1`; when computing the two sided limits,
  input `side = 0` (default).

  In two sided or one sided test of hypothesis of `mu` of one normal
  sample, `side` is a parameter used to control two sided or one sided
  test of hypothesis. When inputting `side = 0` (default), the function
  computes two sided test of hypothesis, and `H1: mu != mu0`; when
  inputting `side = -1` (or a number \< 0), the function computes one
  sided test of hypothesis, and `H1: mu < mu0`; when inputting
  `side = 1` (or a number \> 0), the function computes one sided test of
  hypothesis, and `H1: mu > mu0`.

  In two sided or one sided test of hypothesis of `sigma^2` of one
  normal sample, `side` is a parameter used to control two sided or one
  sided test of hypothesis. When inputting `side = 0` (default), the
  function computes two sided test of hypothesis, and
  `H1: sigma^2 != sigma0^2`; when inputting `side = -1` (or a number \<
  0), the function computes one sided test of hypothesis, and
  `H1: sigma^2 < sigma0^2`; when inputting `side = 1` (or a number \>
  0), the function computes one sided test of hypothesis, and
  `H1: sigma^2 > sigma0^2`.

- alpha:

  The significance level, a real number in \[0, 1\]. Default to 0.05.
  1-alpha is the degree of confidence.

## Value

A list with the following components:

- mu_interval :

  It contains the results of interval estimation of `mu`.

- mu_hypothesis :

  It contains the results of test of hypothesis of `mu`.

- sigma_interval :

  It contains the results of interval estimation of `sigma`.

- sigma_hypothesis :

  It contains the results of test of hypothesis of `sigma`.

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
#>  [1] 0.7543430 1.2079064 1.0911204 0.5240150 1.1195131 1.0255681 0.6566256
#>  [8] 1.0072219 1.2014536 1.1426218
one_sample(x, mu = 1, sigma = 0.2, side = 1)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.5240150 0.8175627 1.0583442 1.1368447 1.2079064 
#> data_outline of x
#>    N      Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 0.9730389 0.05833198 0.2415202 1.058344 0.07637538 24.82122 0.5249879
#>        USS         R        R1   Skewness   Kurtosis
#> 1 9.993035 0.6838915 0.3192819 -0.9656092 -0.4767062
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.85822, p-value = 0.07271
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation: interval_estimate4()
#>        mean df         a   b
#> 1 0.9730389 10 0.8690092 Inf
#> Test of hypothesis: mean_test1()
#> H0: mu <= 1     H1: mu > 1 
#>        mean df          Z   p_value
#> 1 0.9730389 10 -0.4262925 0.6650526
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a   b
#> 1 0.05322569 10 0.02907389 Inf
#> Test of hypothesis: var_test1()
#> H0: sigma2 <= 0.04     H1: sigma2 > 0.04 
#>          var df   chisq2   P_value
#> 1 0.05322569 10 13.30642 0.2070405
one_sample(x, sigma = 0.2, side = 1)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.5240150 0.8175627 1.0583442 1.1368447 1.2079064 
#> data_outline of x
#>    N      Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 0.9730389 0.05833198 0.2415202 1.058344 0.07637538 24.82122 0.5249879
#>        USS         R        R1   Skewness   Kurtosis
#> 1 9.993035 0.6838915 0.3192819 -0.9656092 -0.4767062
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.85822, p-value = 0.07271
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation: interval_estimate4()
#>        mean df         a   b
#> 1 0.9730389 10 0.8690092 Inf
#> Test of hypothesis: mean_test1()
#> H0: mu <= 0     H1: mu > 0 
#>        mean df       Z p_value
#> 1 0.9730389 10 15.3851       0
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a   b
#> 1 0.05833198  9 0.03102953 Inf
#> Test of hypothesis: var_test1()
#> H0: sigma2 <= 0.04     H1: sigma2 > 0.04 
#>          var df  chisq2   P_value
#> 1 0.05833198  9 13.1247 0.1570446
one_sample(x, mu = 1, side = 1)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.5240150 0.8175627 1.0583442 1.1368447 1.2079064 
#> data_outline of x
#>    N      Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 0.9730389 0.05833198 0.2415202 1.058344 0.07637538 24.82122 0.5249879
#>        USS         R        R1   Skewness   Kurtosis
#> 1 9.993035 0.6838915 0.3192819 -0.9656092 -0.4767062
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.85822, p-value = 0.07271
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation and test of hypothesis: t.test()
#> H0: mu <= 1     H1: mu > 1 
#> 
#>  One Sample t-test
#> 
#> data:  x
#> t = -0.35301, df = 9, p-value = 0.6339
#> alternative hypothesis: true mean is greater than 1
#> 95 percent confidence interval:
#>  0.8330342       Inf
#> sample estimates:
#> mean of x 
#> 0.9730389 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a   b
#> 1 0.05322569 10 0.02907389 Inf
#> Test of hypothesis: var_test1()
#> H0: sigma2 <= 1     H1: sigma2 > 1 
#>          var df    chisq2   P_value
#> 1 0.05322569 10 0.5322569 0.9999911
one_sample(x)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.5240150 0.8175627 1.0583442 1.1368447 1.2079064 
#> data_outline of x
#>    N      Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 0.9730389 0.05833198 0.2415202 1.058344 0.07637538 24.82122 0.5249879
#>        USS         R        R1   Skewness   Kurtosis
#> 1 9.993035 0.6838915 0.3192819 -0.9656092 -0.4767062
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.85822, p-value = 0.07271
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation and test of hypothesis: t.test()
#> H0: mu = 0     H1: mu != 0 
#> 
#>  One Sample t-test
#> 
#> data:  x
#> t = 12.74, df = 9, p-value = 4.617e-07
#> alternative hypothesis: true mean is not equal to 0
#> 95 percent confidence interval:
#>  0.8002658 1.1458120
#> sample estimates:
#> mean of x 
#> 0.9730389 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a         b
#> 1 0.05833198  9 0.02759787 0.1944119
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>          var df    chisq2      P_value
#> 1 0.05833198  9 0.5249879 7.503865e-05
```
