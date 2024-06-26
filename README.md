# additivityTests

additivityTests is R package for additivity tests in the two way ANOVA with just one observation per cell.

## Introduction

In many applications of statistical methods, it is assumed that the response
variable is a sum of several factors and a random noise. In a real world this may
not be an appropriate model. For example, some patients may react differently
to the same drug treatment or the effect of fertilizer may be influenced
by the type of a soil. There might exist an interaction between factors. 

If there is more than one observation per cell then standard ANOVA techniques
may be applied. Unfortunately, in many cases it is infeasible to get
more than one observation taken under the same conditions. For instance, it
is not logical to ask the same student the same question twice.

Six tests of additivity hypothesis (under various alternatives) have been included in this package: 
Tukey test, modified Tukey test, Johnson-Graybill test, LBI test, Mandel test and Tusell test.

## Example

Let us generate 10 random subjects, 10 random treatmeants and combine them into a dataset (with no interaction):

```S
    set.seed(123)
    subjects = rnorm(10)
    treatments = rnorm(10)
    noise = rnorm(100)/100
    Y = matrix(rep(subjects,10), 10, 10) + matrix(rep(treatments, each=10), 10, 10) + noise
```

The tests should **not** reject the additive hypothesis: 

```S
    tukey.test(Y)
    mandel.test(Y)
    lbi.test(Y)
    tusell.test(Y)
    johnson.graybill.test(Y)
    mandel.test(Y)
    mtukey.test(Y, correction=2, Nboot=1000)
```

Now, the extra effect will be added to the last 5 subjects. The tests **should** reject the additive hypothesis:   

```S
    Y[1:5,] = Y[1:5,] + 10*rep(treatments, each=5)
    
    tukey.test(Y)
    mandel.test(Y)
    lbi.test(Y)
    tusell.test(Y)
    johnson.graybill.test(Y)
    mandel.test(Y)
    mtukey.test(Y, correction=2, Nboot=1000)
```

## Installation

To install the additivityTests from Github, it's easiest to use the `devtools` package:

```S
    # install.packages("devtools")
    library(devtools)
    install_github("simecek/additivityTests")
```    

Or you can access the stable package version available on [[CRAN]](https://cran.r-project.org/package=additivityTests)

## References

Simecek, Petr and Simeckova, Marie. "Modification of Tukey's additivity test." Journal of Statistical Planning and Inference (2012). [[ScienceDirect]](https://www.sciencedirect.com/science/article/pii/S037837581200239X) [[arXiv]](http://arxiv.org/abs/1207.2883)

Rasch, Dieter, et al. "Tests of additivity in mixed and fixed effect two-way ANOVA models with single sub-class numbers." Statistical Papers 50.4 (2009): 905-916. [[Springer]](https://rd.springer.com/article/10.1007/s00362-009-0254-4#page-1)
