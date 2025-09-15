# 2025-09-09  Frederic Bertrand <frederic.bertrand@lecnam.net>
    * version 1.2-0
    * maintainer email update
    * fixes to Rd files
    * added unit tests
    * added package doi

# 2023-03-29  Frederic Bertrand <frederic.bertrand@lecnam.net>
    * version 1.1-0
    * fixed to come back on the CRAN

# 2013-05-29  Ying-Ying Zhang (Robert) <robertzhangyying@qq.com>
    * version 1.0-3
    * add the package vignettes

# 2013-05-13  Ying-Ying Zhang (Robert) <robertzhangyying@qq.com>
    * version 1.0-2
    * in folder "R"
      1) revise function one_two_sample(): 
	in the place "Interval estimation and test of hypothesis of mu1-mu2"; 
	add graphics.off(); 
	add attr(x, "DNAME") = deparse(substitute(x))
      2) revise function one_sample(): 
	add dev.new();
	revise hist paragraph; 
	revise DNAME = if (!is.null(attr(x, "DNAME"))) attr(x, "DNAME") else deparse(substitute(x))
    * add a "tests" folder: add a file "tests_OneTwoSamples.R"
    * in folder "man"
      1) revise one_sample.Rd: in the places \item{mu} and \item{sigma}

# 2013-04-27  Ying-Ying Zhang (Robert) <robertzhangyying@qq.com>
    * version 1.0-1
    * Create the package OneTwoSamples
