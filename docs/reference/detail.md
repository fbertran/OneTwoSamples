# Show details of an object

Show details of an object.

## Usage

``` r
detail(x)
```

## Arguments

- x:

  Any `R` object to be tested.

## Value

A list with components:

- x :

  The argument `x`.

- isS4 :

  Logical, indicates whether `x` is an S4 object.

- isObject :

  Logical, indicates whether `x` is an object, i.e., with a class
  attribute.

- class :

  The class of `x`.

- attributes :

  The attributes of `x`. Usually `result$attributes` is also a list.

## References

Zhang, Y. Y., Wei, Y. (2013), One and two samples using only an R
funtion,
[doi:10.2991/asshm-13.2013.29](https://doi.org/10.2991/asshm-13.2013.29)
.

## Author

Ying-Ying Zhang (Robert) <robertzhangyying@qq.com>

## See also

[`isS4`](https://rdrr.io/r/base/isS4.html),
[`is.object`](https://rdrr.io/r/base/is.object.html),
[`class`](https://rdrr.io/r/base/class.html),
[`attributes`](https://rdrr.io/r/base/attributes.html)

## Examples

``` r
x=rnorm(10, mean = 1, sd = 0.2); x
#>  [1] 0.6738021 1.1024854 0.6273977 0.8955975 0.9894796 1.1085993 0.8171850
#>  [8] 1.0936309 1.0725903 0.7390913
t = t.test(x); t
#> 
#>  One Sample t-test
#> 
#> data:  x
#> t = 15.376, df = 9, p-value = 9.096e-08
#> alternative hypothesis: true mean is not equal to 0
#> 95 percent confidence interval:
#>  0.7778131 1.0461587
#> sample estimates:
#> mean of x 
#> 0.9119859 
#> 
detail(t)
#> $x
#> 
#>  One Sample t-test
#> 
#> data:  x
#> t = 15.376, df = 9, p-value = 9.096e-08
#> alternative hypothesis: true mean is not equal to 0
#> 95 percent confidence interval:
#>  0.7778131 1.0461587
#> sample estimates:
#> mean of x 
#> 0.9119859 
#> 
#> 
#> $isS4
#> [1] FALSE
#> 
#> $is.object
#> [1] TRUE
#> 
#> $class
#> [1] "htest"
#> 
#> $attributes
#> $attributes$names
#>  [1] "statistic"   "parameter"   "p.value"     "conf.int"    "estimate"   
#>  [6] "null.value"  "stderr"      "alternative" "method"      "data.name"  
#> 
#> $attributes$class
#> [1] "htest"
#> 
#> 
```
