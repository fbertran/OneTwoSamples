# Deal with one and two (normal) samples

Deal with one and two (normal) samples. For one normal sample x, the
function reports descriptive statistics, plot, interval estimation and
test of hypothesis of x. For two normal samples x and y, the function
reports descriptive statistics, plot, interval estimation and test of
hypothesis of x and y, respectively. It also reports interval estimation
and test of hypothesis of mu1-mu2 (the difference of the means of x and
y) and sigma1^2/sigma2^2 (the ratio of the variances of x and y), tests
whether x and y are from the same population, finds the correlation
coefficient of x and y if x and y have the same length.

## Usage

``` r
one_two_sample(x, y = NULL, mu = c(Inf, Inf), sigma = c(-1, -1), 
               var.equal = FALSE, ratio = 1, side = 0, alpha = 0.05)
```

## Arguments

- x:

  A numeric vector.

- y:

  A numeric vector.

- mu:

  If `y = NULL`, i.e., there is only one sample. See the argument `mu`
  in
  [`one_sample`](https://fbertran.github.io/OneTwoSamples/reference/one_sample.md).
  For two normal samples `x` and `y`, `mu` plays one role: the
  population means. However, `mu` is used in two places: one is the two
  sided or one sided interval estimation of `sigma1^2 / sigma2^2` of two
  normal samples, another is the two sided or one sided test of
  hypothesis of `sigma1^2` and `sigma2^2` of two normal samples. When
  `mu` is known, input it, and the function computes the interval
  endpoints (or the F value) using an F distribution with degree of
  freedom `(n1, n2)`. When it is unknown, ignore it, and the function
  computes the interval endpoints (or the F value) using an F
  distribution with degree of freedom `(n1-1, n2-1)`.

- sigma:

  If `y = NULL`, i.e., there is only one sample. See the argument
  `sigma` in
  [`one_sample`](https://fbertran.github.io/OneTwoSamples/reference/one_sample.md).
  For two normal samples `x` and `y`, `sigma` plays one role: the
  population standard deviations. However, `sigma` is used in two
  places: one is the two sided or one sided interval estimation of
  `mu1-mu2` of two normal samples, another is the two sided or one sided
  test of hypothesis of `mu1` and `mu2` of two normal samples. When the
  standard deviations are known, input it, then the function computes
  the interval endpoints using normal population; when the standard
  deviations are unknown, ignore it, now we need to consider whether the
  two populations have equal variances. See `var.equal` below.

- var.equal:

  A logical variable indicating whether to treat the two variances as
  being equal. If `TRUE` then the pooled variance is used to estimate
  the variance otherwise the Welch (or Satterthwaite) approximation to
  the degrees of freedom is used.

- ratio:

  The hypothesized ratio of the population variances of `x` and `y`. It
  is used in `var.test(x, y, ratio = ratio, ...)`, i.e., when computing
  the interval estimation and test of hypothesis of
  `sigma1^2 / sigma2^2` when `mu1` or `mu2` is unknown.

- side:

  If `y = NULL`, i.e., there is only one sample. See the argument `side`
  in
  [`one_sample`](https://fbertran.github.io/OneTwoSamples/reference/one_sample.md).
  For two normal samples `x` and `y`, `sigma` is used in four places:
  interval estimation of `mu1-mu2`, test of hypothesis of `mu1` and
  `mu2`, interval estimation of `sigma1^2 / sigma2^2`, test of
  hypothesis of `sigma1^2` and `sigma2^2`. In interval estimation of
  `mu1-mu2` or `sigma1^2 / sigma2^2`, `side` is a parameter used to
  control whether to compute two sided or one sided interval estimation.
  When computing the one sided upper limit, input `side = -1` (or a
  number \< 0); when computing the one sided lower limit, input
  `side = 1` (or a number \> 0); when computing the two sided limits,
  input `side = 0` (default). In test of hypothesis of `mu1` and `mu2`
  or `sigma1^2` and `sigma2^2`, `side` is a parameter used to control
  two sided or one sided test of hypothesis. When inputting `side = 0`
  (default), the function computes two sided test of hypothesis, and
  `H1: mu1 != mu2` or `H1: sigma1^2 != sigma2^2`; when inputting
  `side = -1` (or a number \< 0), the function computes one sided test
  of hypothesis, and `H1: mu1 < mu2` or `H1: sigma1^2 < sigma2^2`; when
  inputting `side = 1` (or a number \> 0), the function computes one
  sided test of hypothesis, and `H1: mu1 > mu2` or
  `H1: sigma1^2 > sigma2^2`.

- alpha:

  The significance level, a real number in \[0, 1\]. Default to 0.05.
  1-alpha is the degree of confidence.

## Value

A list with the following components:

- one_sample_x :

  It contains the results by `one_sample(x, ...)`.

- one_sample_y :

  It contains the results by `one_sample(y, ...)`.

- mu1_mu2_interval :

  It contains the results of interval estimation of `mu1-mu2`.

- mu1_mu2_hypothesis :

  It contains the results of test of hypothesis of `mu1-mu2`.

- sigma_ratio_interval :

  It contains the results of interval estimation of
  `sigma1^2 / sigma2^2`.

- sigma_ratio_hypothesis :

  It contains the results of test of hypothesis of
  `sigma1^2 / sigma2^2`.

- res.ks :

  It contains the results of `ks.test(x,y)`.

- res.binom :

  It contains the results of `binom.test(sum(x<y), length(x))`.

- res.wilcox :

  It contains the results of `wilcox.test(x, y, ...)`.

- cor.pearson :

  It contains the results of `cor.test(x, y, method = "pearson", ...)`.

- cor.kendall :

  It contains the results of `cor.test(x, y, method = "kendall", ...)`.

- cor.spearman :

  It contains the results of `cor.test(x, y, method = "spearman", ...)`.

## References

Zhang, Y. Y., Wei, Y. (2013), One and two samples using only an R
funtion,
[doi:10.2991/asshm-13.2013.29](https://doi.org/10.2991/asshm-13.2013.29)
.

## Author

Ying-Ying Zhang (Robert) <robertzhangyying@qq.com>

## Examples

``` r
## One sample
x=rnorm(10, mean = 1, sd = 0.2); x
#>  [1] 1.0298811 0.9227715 0.9539012 1.0784212 1.0939866 1.1977686 0.8572544
#>  [8] 1.2539380 1.1418132 1.2093845

## one_sample(x, ...) == one_two_sample(x, ...)
one_sample(x, mu = 1, sigma = 0.2, side = 1)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8572544 0.9728962 1.0862039 1.1837797 1.2539380 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.073912 0.01747354 0.1321875 1.086204 0.04180136 12.30897 0.1572618
#>        USS         R        R1   Skewness  Kurtosis
#> 1 11.69013 0.3966836 0.2108836 -0.2943003 -1.065115
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.95981, p-value = 0.7837
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation: interval_estimate4()
#>       mean df         a   b
#> 1 1.073912 10 0.9698824 Inf
#> Test of hypothesis: mean_test1()
#> H0: mu <= 1     H1: mu > 1 
#>       mean df        Z  p_value
#> 1 1.073912 10 1.168652 0.121272
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a   b
#> 1 0.02118917 10 0.01157433 Inf
#> Test of hypothesis: var_test1()
#> H0: sigma2 <= 0.04     H1: sigma2 > 0.04 
#>          var df   chisq2   P_value
#> 1 0.02118917 10 5.297293 0.8704546
one_two_sample(x, mu = 1, sigma = 0.2, side = 1)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8572544 0.9728962 1.0862039 1.1837797 1.2539380 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.073912 0.01747354 0.1321875 1.086204 0.04180136 12.30897 0.1572618
#>        USS         R        R1   Skewness  Kurtosis
#> 1 11.69013 0.3966836 0.2108836 -0.2943003 -1.065115
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.95981, p-value = 0.7837
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation: interval_estimate4()
#>       mean df         a   b
#> 1 1.073912 10 0.9698824 Inf
#> Test of hypothesis: mean_test1()
#> H0: mu <= 1     H1: mu > 1 
#>       mean df        Z  p_value
#> 1 1.073912 10 1.168652 0.121272
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a   b
#> 1 0.02118917 10 0.01157433 Inf
#> Test of hypothesis: var_test1()
#> H0: sigma2 <= 0.04     H1: sigma2 > 0.04 
#>          var df   chisq2   P_value
#> 1 0.02118917 10 5.297293 0.8704546

one_sample(x, sigma = 0.2, side = 1)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8572544 0.9728962 1.0862039 1.1837797 1.2539380 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.073912 0.01747354 0.1321875 1.086204 0.04180136 12.30897 0.1572618
#>        USS         R        R1   Skewness  Kurtosis
#> 1 11.69013 0.3966836 0.2108836 -0.2943003 -1.065115
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.95981, p-value = 0.7837
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation: interval_estimate4()
#>       mean df         a   b
#> 1 1.073912 10 0.9698824 Inf
#> Test of hypothesis: mean_test1()
#> H0: mu <= 0     H1: mu > 0 
#>       mean df        Z p_value
#> 1 1.073912 10 16.98004       0
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df           a   b
#> 1 0.01747354  9 0.009294995 Inf
#> Test of hypothesis: var_test1()
#> H0: sigma2 <= 0.04     H1: sigma2 > 0.04 
#>          var df   chisq2   P_value
#> 1 0.01747354  9 3.931546 0.9158599
one_two_sample(x, sigma = 0.2, side = 1)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8572544 0.9728962 1.0862039 1.1837797 1.2539380 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.073912 0.01747354 0.1321875 1.086204 0.04180136 12.30897 0.1572618
#>        USS         R        R1   Skewness  Kurtosis
#> 1 11.69013 0.3966836 0.2108836 -0.2943003 -1.065115
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.95981, p-value = 0.7837
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation: interval_estimate4()
#>       mean df         a   b
#> 1 1.073912 10 0.9698824 Inf
#> Test of hypothesis: mean_test1()
#> H0: mu <= 0     H1: mu > 0 
#>       mean df        Z p_value
#> 1 1.073912 10 16.98004       0
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df           a   b
#> 1 0.01747354  9 0.009294995 Inf
#> Test of hypothesis: var_test1()
#> H0: sigma2 <= 0.04     H1: sigma2 > 0.04 
#>          var df   chisq2   P_value
#> 1 0.01747354  9 3.931546 0.9158599

one_sample(x, mu = 1, side = 1)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8572544 0.9728962 1.0862039 1.1837797 1.2539380 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.073912 0.01747354 0.1321875 1.086204 0.04180136 12.30897 0.1572618
#>        USS         R        R1   Skewness  Kurtosis
#> 1 11.69013 0.3966836 0.2108836 -0.2943003 -1.065115
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.95981, p-value = 0.7837
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
#> t = 1.7682, df = 9, p-value = 0.05541
#> alternative hypothesis: true mean is greater than 1
#> 95 percent confidence interval:
#>  0.9972854       Inf
#> sample estimates:
#> mean of x 
#>  1.073912 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a   b
#> 1 0.02118917 10 0.01157433 Inf
#> Test of hypothesis: var_test1()
#> H0: sigma2 <= 1     H1: sigma2 > 1 
#>          var df    chisq2   P_value
#> 1 0.02118917 10 0.2118917 0.9999999
one_two_sample(x, mu = 1, side = 1)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8572544 0.9728962 1.0862039 1.1837797 1.2539380 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.073912 0.01747354 0.1321875 1.086204 0.04180136 12.30897 0.1572618
#>        USS         R        R1   Skewness  Kurtosis
#> 1 11.69013 0.3966836 0.2108836 -0.2943003 -1.065115
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.95981, p-value = 0.7837
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
#> t = 1.7682, df = 9, p-value = 0.05541
#> alternative hypothesis: true mean is greater than 1
#> 95 percent confidence interval:
#>  0.9972854       Inf
#> sample estimates:
#> mean of x 
#>  1.073912 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a   b
#> 1 0.02118917 10 0.01157433 Inf
#> Test of hypothesis: var_test1()
#> H0: sigma2 <= 1     H1: sigma2 > 1 
#>          var df    chisq2   P_value
#> 1 0.02118917 10 0.2118917 0.9999999

one_sample(x)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8572544 0.9728962 1.0862039 1.1837797 1.2539380 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.073912 0.01747354 0.1321875 1.086204 0.04180136 12.30897 0.1572618
#>        USS         R        R1   Skewness  Kurtosis
#> 1 11.69013 0.3966836 0.2108836 -0.2943003 -1.065115
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.95981, p-value = 0.7837
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
#> t = 25.691, df = 9, p-value = 9.881e-10
#> alternative hypothesis: true mean is not equal to 0
#> 95 percent confidence interval:
#>  0.9793508 1.1684733
#> sample estimates:
#> mean of x 
#>  1.073912 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df           a          b
#> 1 0.01747354  9 0.008267031 0.05823672
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>          var df    chisq2      P_value
#> 1 0.01747354  9 0.1572618 3.840908e-07
one_two_sample(x)
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8572544 0.9728962 1.0862039 1.1837797 1.2539380 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.073912 0.01747354 0.1321875 1.086204 0.04180136 12.30897 0.1572618
#>        USS         R        R1   Skewness  Kurtosis
#> 1 11.69013 0.3966836 0.2108836 -0.2943003 -1.065115
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.95981, p-value = 0.7837
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
#> t = 25.691, df = 9, p-value = 9.881e-10
#> alternative hypothesis: true mean is not equal to 0
#> 95 percent confidence interval:
#>  0.9793508 1.1684733
#> sample estimates:
#> mean of x 
#>  1.073912 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df           a          b
#> 1 0.01747354  9 0.008267031 0.05823672
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>          var df    chisq2      P_value
#> 1 0.01747354  9 0.1572618 3.840908e-07

## Two samples
set.seed(1)
x=rnorm(10, mean = 1, sd = 0.2); x
#>  [1] 0.8747092 1.0367287 0.8328743 1.3190562 1.0659016 0.8359063 1.0974858
#>  [8] 1.1476649 1.1151563 0.9389223
y=rnorm(20, mean = 2, sd = 0.3); y
#>  [1] 2.453534 2.116953 1.813628 1.335590 2.337479 1.986520 1.995143 2.283151
#>  [9] 2.246366 2.178170 2.275693 2.234641 2.022369 1.403194 2.185948 1.983161
#> [17] 1.953261 1.558774 1.856555 2.125382
y2=rnorm(20, mean = 2, sd = 0.2); y2
#>  [1] 2.271736 1.979442 2.077534 1.989239 1.724588 1.917001 1.921142 1.988137
#>  [9] 2.220005 2.152635 1.967095 1.949328 2.139393 2.111333 1.862249 1.858501
#> [17] 2.072916 2.153707 1.977531 2.176222

## sigma1, sigma2 known; mu1, mu2 known
one_two_sample(x, y, sigma = c(0.2, 0.3), mu = c(1, 2))
#> Interval estimation and test of hypothesis
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
#> 
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.91028, p-value = 0.06452
#> 
#> 
#> x and y are both from the normal populations.
#> 
#> x: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8328743 0.8907625 1.0513151 1.1107387 1.3190562 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.026441 0.02437258 0.1561172 1.051315 0.04936859 15.20957 0.2193532
#>        USS         R        R1  Skewness   Kurtosis
#> 1 10.75516 0.4861819 0.2199761 0.3512426 -0.3169031
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation: interval_estimate4()
#>       mean df         a      b
#> 1 1.026441 10 0.9024815 1.1504
#> Test of hypothesis: mean_test1()
#> H0: mu = 1     H1: mu != 1 
#>       mean df         Z   p_value
#> 1 1.026441 10 0.4180619 0.6759019
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a          b
#> 1 0.02263442 10 0.01105025 0.06970931
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 0.04     H1: sigma2 != 0.04 
#>          var df   chisq2   P_value
#> 1 0.02263442 10 5.658606 0.3138319
#> 
#> y: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of y
#>       0%      25%      50%      75%     100% 
#> 1.335590 1.929085 2.069661 2.237572 2.453534 
#> data_outline of y
#>    N     Mean        Var   std_dev   Median   std_mean       CV      CSS
#> 1 20 2.017276 0.09116068 0.3019283 2.069661 0.06751321 14.96713 1.732053
#>        USS        R        R1  Skewness  Kurtosis
#> 1 83.12008 1.117944 0.3084875 -1.003374 0.5258495
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.91028, p-value = 0.06452
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation: interval_estimate4()
#>       mean df        a        b
#> 1 2.017276 20 1.885797 2.148754
#> Test of hypothesis: mean_test1()
#> H0: mu = 2     H1: mu != 2 
#>       mean df         Z   p_value
#> 1 2.017276 20 0.2575318 0.7967683
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>         var df          a        b
#> 1 0.0869011 20 0.05086456 0.181218
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 0.09     H1: sigma2 != 0.09 
#>         var df   chisq2   P_value
#> 1 0.0869011 20 19.31135 0.9966434
#> 
#> Interval estimation and test of hypothesis of mu1-mu2
#> 
#> Interval estimation: interval_estimate5()
#>         mean df         a          b
#> 1 -0.9908352 30 -1.171535 -0.8101355
#> 
#> Test of hypothesis: mean_test2()
#>         mean df         Z      p_value
#> 1 -0.9908352 30 -10.74712 6.114309e-27
#> 
#> Interval estimation and test of hypothesis of sigma1^2/sigma2^2
#> Interval estimation: interval_var4()
#>        rate df1 df2         a         b
#> 1 0.2604619  10  20 0.0939051 0.8904003
#> Test of hypothesis: var_test2()
#>        rate df1 df2         F    P_value
#> 1 0.2604619  10  20 0.2604619 0.03318465
#> n1 != n2
#> 
#> Test whether x and y are from the same population
#> H0: x and y are from the same population (without significant difference)
#> ks.test(x,y)
#> 
#>  Exact two-sample Kolmogorov-Smirnov test
#> 
#> data:  x and y
#> D = 1, p-value = 6.657e-08
#> alternative hypothesis: two-sided
#> 
#> wilcox.test(x, y, alternative = alternative)
#> 
#>  Wilcoxon rank sum exact test
#> 
#> data:  x and y
#> W = 0, p-value = 6.657e-08
#> alternative hypothesis: true location shift is not equal to 0
#> 

## sigma1 = sigma2 unknown; mu1, mu2 known
one_two_sample(x, y2, var.equal = TRUE, mu = c(1, 2))
#> Interval estimation and test of hypothesis
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
#> 
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.975, p-value = 0.8548
#> 
#> 
#> x and y are both from the normal populations.
#> 
#> x: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8328743 0.8907625 1.0513151 1.1107387 1.3190562 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.026441 0.02437258 0.1561172 1.051315 0.04936859 15.20957 0.2193532
#>        USS         R        R1  Skewness   Kurtosis
#> 1 10.75516 0.4861819 0.2199761 0.3512426 -0.3169031
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation and test of hypothesis: t.test()
#> H0: mu = 1     H1: mu != 1 
#> 
#>  One Sample t-test
#> 
#> data:  x
#> t = 0.53557, df = 9, p-value = 0.6052
#> alternative hypothesis: true mean is not equal to 1
#> 95 percent confidence interval:
#>  0.914761 1.138120
#> sample estimates:
#> mean of x 
#>  1.026441 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a          b
#> 1 0.02263442 10 0.01105025 0.06970931
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>          var df    chisq2      P_value
#> 1 0.02263442 10 0.2263442 2.816068e-07
#> 
#> y: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of y
#>       0%      25%      50%      75%     100% 
#> 1.724588 1.942281 1.988688 2.142703 2.271736 
#> data_outline of y
#>    N     Mean        Var   std_dev   Median   std_mean       CV      CSS
#> 1 20 2.025487 0.01911437 0.1382547 1.988688 0.03091469 6.825753 0.363173
#>       USS         R       R1   Skewness  Kurtosis
#> 1 82.4151 0.5471478 0.200422 -0.1631305 -0.298063
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.975, p-value = 0.8548
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation and test of hypothesis: t.test()
#> H0: mu = 2     H1: mu != 2 
#> 
#>  One Sample t-test
#> 
#> data:  y
#> t = 0.82442, df = 19, p-value = 0.4199
#> alternative hypothesis: true mean is not equal to 2
#> 95 percent confidence interval:
#>  1.960781 2.090192
#> sample estimates:
#> mean of x 
#>  2.025487 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a          b
#> 1 0.01880822 20 0.01100874 0.03922147
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>          var df    chisq2      P_value
#> 1 0.01880822 20 0.3761644 2.573594e-14
#> 
#> Interval estimation and test of hypothesis of mu1-mu2
#> 
#> Interval estimation and test of hypothesis: t.test()
#> 
#>  Two Sample t-test
#> 
#> data:  x and y
#> t = -17.884, df = 28, p-value < 2.2e-16
#> alternative hypothesis: true difference in means is not equal to 0
#> 95 percent confidence interval:
#>  -1.1134763 -0.8846159
#> sample estimates:
#> mean of x mean of y 
#>  1.026441  2.025487 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma1^2/sigma2^2
#> Interval estimation: interval_var4()
#>       rate df1 df2         a        b
#> 1 1.203432  10  20 0.4338771 4.113986
#> Test of hypothesis: var_test2()
#>       rate df1 df2        F   P_value
#> 1 1.203432  10  20 1.203432 0.6914616
#> n1 != n2
#> 
#> Test whether x and y are from the same population
#> H0: x and y are from the same population (without significant difference)
#> ks.test(x,y)
#> 
#>  Exact two-sample Kolmogorov-Smirnov test
#> 
#> data:  x and y
#> D = 1, p-value = 6.657e-08
#> alternative hypothesis: two-sided
#> 
#> wilcox.test(x, y, alternative = alternative)
#> 
#>  Wilcoxon rank sum exact test
#> 
#> data:  x and y
#> W = 0, p-value = 6.657e-08
#> alternative hypothesis: true location shift is not equal to 0
#> 

## sigma1 != sigma2 unknown; mu1, mu2 known
one_two_sample(x, y, mu = c(1, 2))
#> Interval estimation and test of hypothesis
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
#> 
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.91028, p-value = 0.06452
#> 
#> 
#> x and y are both from the normal populations.
#> 
#> x: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8328743 0.8907625 1.0513151 1.1107387 1.3190562 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.026441 0.02437258 0.1561172 1.051315 0.04936859 15.20957 0.2193532
#>        USS         R        R1  Skewness   Kurtosis
#> 1 10.75516 0.4861819 0.2199761 0.3512426 -0.3169031
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation and test of hypothesis: t.test()
#> H0: mu = 1     H1: mu != 1 
#> 
#>  One Sample t-test
#> 
#> data:  x
#> t = 0.53557, df = 9, p-value = 0.6052
#> alternative hypothesis: true mean is not equal to 1
#> 95 percent confidence interval:
#>  0.914761 1.138120
#> sample estimates:
#> mean of x 
#>  1.026441 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a          b
#> 1 0.02263442 10 0.01105025 0.06970931
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>          var df    chisq2      P_value
#> 1 0.02263442 10 0.2263442 2.816068e-07
#> 
#> y: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of y
#>       0%      25%      50%      75%     100% 
#> 1.335590 1.929085 2.069661 2.237572 2.453534 
#> data_outline of y
#>    N     Mean        Var   std_dev   Median   std_mean       CV      CSS
#> 1 20 2.017276 0.09116068 0.3019283 2.069661 0.06751321 14.96713 1.732053
#>        USS        R        R1  Skewness  Kurtosis
#> 1 83.12008 1.117944 0.3084875 -1.003374 0.5258495
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.91028, p-value = 0.06452
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation and test of hypothesis: t.test()
#> H0: mu = 2     H1: mu != 2 
#> 
#>  One Sample t-test
#> 
#> data:  y
#> t = 0.25589, df = 19, p-value = 0.8008
#> alternative hypothesis: true mean is not equal to 2
#> 95 percent confidence interval:
#>  1.875969 2.158583
#> sample estimates:
#> mean of x 
#>  2.017276 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>         var df          a        b
#> 1 0.0869011 20 0.05086456 0.181218
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>         var df   chisq2      P_value
#> 1 0.0869011 20 1.738022 6.160195e-08
#> 
#> Interval estimation and test of hypothesis of mu1-mu2
#> 
#> Interval estimation and test of hypothesis: t.test()
#> 
#>  Welch Two Sample t-test
#> 
#> data:  x and y
#> t = -11.847, df = 27.907, p-value = 2.111e-12
#> alternative hypothesis: true difference in means is not equal to 0
#> 95 percent confidence interval:
#>  -1.162185 -0.819485
#> sample estimates:
#> mean of x mean of y 
#>  1.026441  2.017276 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma1^2/sigma2^2
#> Interval estimation: interval_var4()
#>        rate df1 df2         a         b
#> 1 0.2604619  10  20 0.0939051 0.8904003
#> Test of hypothesis: var_test2()
#>        rate df1 df2         F    P_value
#> 1 0.2604619  10  20 0.2604619 0.03318465
#> n1 != n2
#> 
#> Test whether x and y are from the same population
#> H0: x and y are from the same population (without significant difference)
#> ks.test(x,y)
#> 
#>  Exact two-sample Kolmogorov-Smirnov test
#> 
#> data:  x and y
#> D = 1, p-value = 6.657e-08
#> alternative hypothesis: two-sided
#> 
#> wilcox.test(x, y, alternative = alternative)
#> 
#>  Wilcoxon rank sum exact test
#> 
#> data:  x and y
#> W = 0, p-value = 6.657e-08
#> alternative hypothesis: true location shift is not equal to 0
#> 

## sigma1, sigma2 known; mu1, mu2 unknown
one_two_sample(x, y, sigma = c(0.2, 0.3))
#> Interval estimation and test of hypothesis
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
#> 
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.91028, p-value = 0.06452
#> 
#> 
#> x and y are both from the normal populations.
#> 
#> x: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8328743 0.8907625 1.0513151 1.1107387 1.3190562 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.026441 0.02437258 0.1561172 1.051315 0.04936859 15.20957 0.2193532
#>        USS         R        R1  Skewness   Kurtosis
#> 1 10.75516 0.4861819 0.2199761 0.3512426 -0.3169031
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation: interval_estimate4()
#>       mean df         a      b
#> 1 1.026441 10 0.9024815 1.1504
#> Test of hypothesis: mean_test1()
#> H0: mu = 0     H1: mu != 0 
#>       mean df        Z p_value
#> 1 1.026441 10 16.22945       0
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a          b
#> 1 0.02437258  9 0.01153109 0.08123021
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 0.04     H1: sigma2 != 0.04 
#>          var df  chisq2   P_value
#> 1 0.02437258  9 5.48383 0.4194824
#> 
#> y: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of y
#>       0%      25%      50%      75%     100% 
#> 1.335590 1.929085 2.069661 2.237572 2.453534 
#> data_outline of y
#>    N     Mean        Var   std_dev   Median   std_mean       CV      CSS
#> 1 20 2.017276 0.09116068 0.3019283 2.069661 0.06751321 14.96713 1.732053
#>        USS        R        R1  Skewness  Kurtosis
#> 1 83.12008 1.117944 0.3084875 -1.003374 0.5258495
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.91028, p-value = 0.06452
#> 
#> 
#> The data is from the normal population.
#> 
#> The data is from the normal population.
#> 
#> Interval estimation and test of hypothesis of mu
#> Interval estimation: interval_estimate4()
#>       mean df        a        b
#> 1 2.017276 20 1.885797 2.148754
#> Test of hypothesis: mean_test1()
#> H0: mu = 0     H1: mu != 0 
#>       mean df        Z p_value
#> 1 2.017276 20 30.07177       0
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a         b
#> 1 0.09116068 19 0.05272238 0.1944703
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 0.09     H1: sigma2 != 0.09 
#>          var df   chisq2   P_value
#> 1 0.09116068 19 19.24503 0.8824428
#> 
#> Interval estimation and test of hypothesis of mu1-mu2
#> 
#> Interval estimation: interval_estimate5()
#>         mean df         a          b
#> 1 -0.9908352 30 -1.171535 -0.8101355
#> 
#> Test of hypothesis: mean_test2()
#>         mean df         Z      p_value
#> 1 -0.9908352 30 -10.74712 6.114309e-27
#> 
#> Interval estimation and test of hypothesis of sigma1^2/sigma2^2
#> Interval estimation and test of hypothesis: var.test()
#> 
#>  F test to compare two variances
#> 
#> data:  x and y
#> F = 0.26736, num df = 9, denom df = 19, p-value = 0.04757
#> alternative hypothesis: true ratio of variances is not equal to 1
#> 95 percent confidence interval:
#>  0.09283112 0.98477156
#> sample estimates:
#> ratio of variances 
#>          0.2673585 
#> 
#> n1 != n2
#> 
#> Test whether x and y are from the same population
#> H0: x and y are from the same population (without significant difference)
#> ks.test(x,y)
#> 
#>  Exact two-sample Kolmogorov-Smirnov test
#> 
#> data:  x and y
#> D = 1, p-value = 6.657e-08
#> alternative hypothesis: two-sided
#> 
#> wilcox.test(x, y, alternative = alternative)
#> 
#>  Wilcoxon rank sum exact test
#> 
#> data:  x and y
#> W = 0, p-value = 6.657e-08
#> alternative hypothesis: true location shift is not equal to 0
#> 

## sigma1 = sigma2 unknown; mu1, mu2 unknown
one_two_sample(x, y2, var.equal = TRUE)
#> Interval estimation and test of hypothesis
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
#> 
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.975, p-value = 0.8548
#> 
#> 
#> x and y are both from the normal populations.
#> 
#> x: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8328743 0.8907625 1.0513151 1.1107387 1.3190562 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.026441 0.02437258 0.1561172 1.051315 0.04936859 15.20957 0.2193532
#>        USS         R        R1  Skewness   Kurtosis
#> 1 10.75516 0.4861819 0.2199761 0.3512426 -0.3169031
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
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
#> t = 20.791, df = 9, p-value = 6.446e-09
#> alternative hypothesis: true mean is not equal to 0
#> 95 percent confidence interval:
#>  0.914761 1.138120
#> sample estimates:
#> mean of x 
#>  1.026441 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a          b
#> 1 0.02437258  9 0.01153109 0.08123021
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>          var df    chisq2      P_value
#> 1 0.02437258  9 0.2193532 1.674074e-06
#> 
#> y: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of y
#>       0%      25%      50%      75%     100% 
#> 1.724588 1.942281 1.988688 2.142703 2.271736 
#> data_outline of y
#>    N     Mean        Var   std_dev   Median   std_mean       CV      CSS
#> 1 20 2.025487 0.01911437 0.1382547 1.988688 0.03091469 6.825753 0.363173
#>       USS         R       R1   Skewness  Kurtosis
#> 1 82.4151 0.5471478 0.200422 -0.1631305 -0.298063
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.975, p-value = 0.8548
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
#> data:  y
#> t = 65.519, df = 19, p-value < 2.2e-16
#> alternative hypothesis: true mean is not equal to 0
#> 95 percent confidence interval:
#>  1.960781 2.090192
#> sample estimates:
#> mean of x 
#>  2.025487 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a         b
#> 1 0.01911437 19 0.01105471 0.0407761
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>          var df   chisq2      P_value
#> 1 0.01911437 19 0.363173 1.369903e-13
#> 
#> Interval estimation and test of hypothesis of mu1-mu2
#> 
#> Interval estimation and test of hypothesis: t.test()
#> 
#>  Two Sample t-test
#> 
#> data:  x and y
#> t = -17.884, df = 28, p-value < 2.2e-16
#> alternative hypothesis: true difference in means is not equal to 0
#> 95 percent confidence interval:
#>  -1.1134763 -0.8846159
#> sample estimates:
#> mean of x mean of y 
#>  1.026441  2.025487 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma1^2/sigma2^2
#> Interval estimation and test of hypothesis: var.test()
#> 
#>  F test to compare two variances
#> 
#> data:  x and y
#> F = 1.2751, num df = 9, denom df = 19, p-value = 0.6233
#> alternative hypothesis: true ratio of variances is not equal to 1
#> 95 percent confidence interval:
#>  0.4427323 4.6965951
#> sample estimates:
#> ratio of variances 
#>           1.275092 
#> 
#> n1 != n2
#> 
#> Test whether x and y are from the same population
#> H0: x and y are from the same population (without significant difference)
#> ks.test(x,y)
#> 
#>  Exact two-sample Kolmogorov-Smirnov test
#> 
#> data:  x and y
#> D = 1, p-value = 6.657e-08
#> alternative hypothesis: two-sided
#> 
#> wilcox.test(x, y, alternative = alternative)
#> 
#>  Wilcoxon rank sum exact test
#> 
#> data:  x and y
#> W = 0, p-value = 6.657e-08
#> alternative hypothesis: true location shift is not equal to 0
#> 

## sigma1 != sigma2 unknown; mu1, mu2 unknown
one_two_sample(x, y)
#> Interval estimation and test of hypothesis
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
#> 
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.91028, p-value = 0.06452
#> 
#> 
#> x and y are both from the normal populations.
#> 
#> x: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of x
#>        0%       25%       50%       75%      100% 
#> 0.8328743 0.8907625 1.0513151 1.1107387 1.3190562 
#> data_outline of x
#>    N     Mean        Var   std_dev   Median   std_mean       CV       CSS
#> 1 10 1.026441 0.02437258 0.1561172 1.051315 0.04936859 15.20957 0.2193532
#>        USS         R        R1  Skewness   Kurtosis
#> 1 10.75516 0.4861819 0.2199761 0.3512426 -0.3169031
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  x
#> W = 0.93828, p-value = 0.534
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
#> t = 20.791, df = 9, p-value = 6.446e-09
#> alternative hypothesis: true mean is not equal to 0
#> 95 percent confidence interval:
#>  0.914761 1.138120
#> sample estimates:
#> mean of x 
#>  1.026441 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a          b
#> 1 0.02437258  9 0.01153109 0.08123021
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>          var df    chisq2      P_value
#> 1 0.02437258  9 0.2193532 1.674074e-06
#> 
#> y: descriptive statistics, plot, interval estimation and test of hypothesis
#> quantile of y
#>       0%      25%      50%      75%     100% 
#> 1.335590 1.929085 2.069661 2.237572 2.453534 
#> data_outline of y
#>    N     Mean        Var   std_dev   Median   std_mean       CV      CSS
#> 1 20 2.017276 0.09116068 0.3019283 2.069661 0.06751321 14.96713 1.732053
#>        USS        R        R1  Skewness  Kurtosis
#> 1 83.12008 1.117944 0.3084875 -1.003374 0.5258495
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  y
#> W = 0.91028, p-value = 0.06452
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
#> data:  y
#> t = 29.88, df = 19, p-value < 2.2e-16
#> alternative hypothesis: true mean is not equal to 0
#> 95 percent confidence interval:
#>  1.875969 2.158583
#> sample estimates:
#> mean of x 
#>  2.017276 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma
#> Interval estimation: interval_var3()
#>          var df          a         b
#> 1 0.09116068 19 0.05272238 0.1944703
#> Test of hypothesis: var_test1()
#> H0: sigma2 = 1     H1: sigma2 != 1 
#>          var df   chisq2      P_value
#> 1 0.09116068 19 1.732053 2.061657e-07
#> 
#> Interval estimation and test of hypothesis of mu1-mu2
#> 
#> Interval estimation and test of hypothesis: t.test()
#> 
#>  Welch Two Sample t-test
#> 
#> data:  x and y
#> t = -11.847, df = 27.907, p-value = 2.111e-12
#> alternative hypothesis: true difference in means is not equal to 0
#> 95 percent confidence interval:
#>  -1.162185 -0.819485
#> sample estimates:
#> mean of x mean of y 
#>  1.026441  2.017276 
#> 
#> 
#> Interval estimation and test of hypothesis of sigma1^2/sigma2^2
#> Interval estimation and test of hypothesis: var.test()
#> 
#>  F test to compare two variances
#> 
#> data:  x and y
#> F = 0.26736, num df = 9, denom df = 19, p-value = 0.04757
#> alternative hypothesis: true ratio of variances is not equal to 1
#> 95 percent confidence interval:
#>  0.09283112 0.98477156
#> sample estimates:
#> ratio of variances 
#>          0.2673585 
#> 
#> n1 != n2
#> 
#> Test whether x and y are from the same population
#> H0: x and y are from the same population (without significant difference)
#> ks.test(x,y)
#> 
#>  Exact two-sample Kolmogorov-Smirnov test
#> 
#> data:  x and y
#> D = 1, p-value = 6.657e-08
#> alternative hypothesis: two-sided
#> 
#> wilcox.test(x, y, alternative = alternative)
#> 
#>  Wilcoxon rank sum exact test
#> 
#> data:  x and y
#> W = 0, p-value = 6.657e-08
#> alternative hypothesis: true location shift is not equal to 0
#> 
```
