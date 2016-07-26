---
layout: postDataAnalysis
title: "Transformation Methods for FCM data"
comments: true
categories: [Data Analysis]
tags: [Transformation, cytometry]
---


## Introduction 





### Loading the raw data of a FCS file


{% highlight r %}
library(flowCore)
library(ggplot2)
file <- "~/Ranalysis/Sanofi Day 0 Myeloid panel_SNF002 D0.fcs"
fcs <- read.FCS(file, transformation = FALSE)
{% endhighlight %}


### Summary Information of the data


{% highlight r %}
fs <- pData(fcs@parameters)
fs$minExprs <- apply(fcs@exprs, 2, min)
fs$maxExprs <- apply(fcs@exprs, 2, max)
fs$range <- NULL
fs
{% endhighlight %}



{% highlight text %}
##                   name    desc minRange maxRange    minExprs maxExprs
## $P1              FSC-A    <NA>     -111   262143 -5924094.00 262143.0
## $P2              FSC-H    <NA>        0   262143     5008.00 257470.0
## $P3              FSC-W    <NA>        0   262143        0.00 262143.0
## $P4              SSC-A    <NA>     -111   262143 -7113396.00 262143.0
## $P5              SSC-H    <NA>        0   262143        0.00 257323.0
## $P6              SSC-W    <NA>        0   262143        0.00 262143.0
## $P7             FITC-A   CD11c     -111   262143    -2169.20 262143.0
## $P8            PerCP-A    CD45     -111   262143    -8718.45 262143.0
## $P9     Pacific Blue-A    CD33     -111   262143   -16108.26 262143.0
## $P10  Pacific Orange-A   CD123     -111   262143   -21321.86 262143.0
## $P11        Qdot 605-A  HLA-DR     -111   262143   -18640.58 262143.0
## $P12        Qdot 655-A    CD80     -111   262143   -27556.62 262143.0
## $P13        Qdot 705-A   CD11b     -111   262143   -12407.78 262143.0
## $P14         BUV 395-A    CD15     -111   262143    -7255.44 262143.0
## $P15            DAPI-A     L/D     -111   262143    -7697.16 262143.0
## $P16         BUV 737-A    CD16     -111   262143    -8698.32 262143.0
## $P17             APC-A   CD141     -111   262143    -6508.96 187828.2
## $P18 Alexa Fluor 700-A Lineage     -111   262143   -16094.92 262143.0
## $P19         APC-Cy7-A     CD2     -111   262143    -6440.28 262143.0
## $P20              PE-A    SLAN     -111   262143    -5306.55 262143.0
## $P21    PE-Texas Red-A    CD14     -111   262143   -12159.25 262143.0
## $P22          PE-Cy7-A    CD1c     -111   262143    -7868.45 262143.0
## $P23              Time    <NA>        0   262143        0.00  14422.9
{% endhighlight %}


### Linear Transformation

The formula for linear transformation is `x <- a*x+b`, and the crrosponding funciton is `linearTransform(transformationId="defaultLinearTransform", a = 1, b = 0)`.

#### Transformation function 


{% highlight r %}
ggplot(data.frame(x=c(-5,5)), aes(x)) +
  stat_function(fun=function(x) 1*x+0, geom="line", aes(colour="a=1,b=0")) +
  stat_function(fun=function(x) 2*x+0, geom="line", aes(colour="a=2,b=0")) +
  stat_function(fun=function(x) 2*x+5, geom="line", aes(colour="a=2,b=5")) +
  scale_colour_manual(name="a*x+b", values=c("a=1,b=0"="blue","a=2,b=0"="red", "a=2,b=5"="green")) +
    theme_bw() + geom_hline(yintercept = 0, colour = "gray20") + geom_vline(xintercept = 0, colour = "gray20") + coord_fixed()
{% endhighlight %}

![plot of chunk unnamed-chunk-3](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-3-1.svg)


#### Example


{% highlight r %}
linearTrans <- linearTransform(transformationId="Linear-transformation", a=0.00001, b=1)
lt_fcs <- transform(fcs, transformList('FSC-H' ,linearTrans))

par(mfrow=c(1,2))
plot(density(fcs@exprs[ ,'FSC-H']), main = "Before Transformation")
plot(density(lt_fcs@exprs[ ,'FSC-H']), main = "After Transformation")
{% endhighlight %}

![plot of chunk unnamed-chunk-4](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-4-1.svg)


### Natural Logarithm Transformation (ln transformation)

The formula for ln transformation if `x<-log(x)*(r/d)`, and the crrosponding function is `lnTransform(transformationId="defaultLnTransform", r=1, d=1)`.

#### Transformation function 


{% highlight r %}
ggplot(data.frame(x=c(1e-20,10)), aes(x)) +
  stat_function(fun=function(x) log(x)*(1/1), geom="line", aes(colour="r=1,d=1")) +
  stat_function(fun=function(x) log(x)*(2/1), geom="line", aes(colour="r=2,d=1")) +
  stat_function(fun=function(x) log(x)*(1/2), geom="line", aes(colour="r=1,d=2")) +
  scale_colour_manual(name="log(x)*(r/d)", values=c("r=1,d=1"="blue","r=2,d=1"="red", "r=1,d=2"="green")) + 
    theme_bw() + geom_hline(yintercept = 0, colour = "gray20") + geom_vline(xintercept = 0, colour = "gray20")
{% endhighlight %}

![plot of chunk unnamed-chunk-5](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-5-1.svg)

#### Example


{% highlight r %}
lnTrans <- lnTransform(transformationId="ln-transformation", r=1, d=1)
ln_fcs <- transform(fcs, transformList('FSC-H', lnTrans))

par(mfrow=c(1,2))
plot(density(fcs@exprs[ ,'FSC-H']), main = "Before Transformation")
plot(density(ln_fcs@exprs[ ,'FSC-H']), main = "After Transformation")
{% endhighlight %}

![plot of chunk unnamed-chunk-6](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-6-1.svg)


### Logarithmic Transformation

The formula for logarithmic transformation if `x<-log(x,logbase)*(r/d)`, and the crrosponding function is `logTransform(transformationId="defaultLogTransform", logbase=10, r=1, d=1)`. Compared with ln transformation, you can specify the base with `logbase`.

#### Transformation function 


{% highlight r %}
ggplot(data.frame(x=c(1e-20,1000)), aes(x)) +
  stat_function(fun=function(x) log(x,exp(1))*(1/1), geom="line", aes(colour="logbase=e")) +
  stat_function(fun=function(x) log(x,10)*(1/1), geom="line", aes(colour="logbase=10")) +
  stat_function(fun=function(x) log(x,20)*(1/1), geom="line", aes(colour="logbase=20")) +
  scale_colour_manual(name="log(x,logbase)", values=c("logbase=e"="blue","logbase=10"="red", "logbase=20"="green")) + 
    theme_bw() + geom_hline(yintercept = 0, colour = "gray20") + geom_vline(xintercept = 0, colour = "gray20")
{% endhighlight %}

![plot of chunk unnamed-chunk-7](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-7-1.svg)

#### Example


{% highlight r %}
logTrans <- logTransform(transformationId="log10-transformation", logbase=10, r=1, d=1)
log_fcs <- transform(fcs, transformList('FSC-H', logTrans))

par(mfrow=c(1,2))
plot(density(fcs@exprs[ ,'FSC-H']), main = "Before Transformation")
plot(density(log_fcs@exprs[ ,'FSC-H']), main = "After Transformation")
{% endhighlight %}

![plot of chunk unnamed-chunk-8](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-8-1.svg)


### Quadratic Transformation

The formula for quadratic transformation if `x <- a*x^2 + b*x + c`, and the crrosponding function is `quadraticTransform(transformationId="defaultQuadraticTransform", a = 1, b = 1, c = 0)`.

#### Transformation function 


{% highlight r %}
ggplot(data.frame(x=c(-10,10)), aes(x)) +
  stat_function(fun=function(x) 1*x^2 + 0*x + 0, geom="line", aes(colour="a=1,b=0,c=0")) +
  stat_function(fun=function(x) -1*x^2 + 0*x + 0, geom="line", aes(colour="a=-1,b=0,c=0")) +
  stat_function(fun=function(x) 1*x^2 + -10*x + 25, geom="line", aes(colour="a=1,b=-10,c=25")) +
  stat_function(fun=function(x) 4*x^2 + 0*x + 100, geom="line", aes(colour="a=4,b=0,c=100")) +
  scale_colour_manual(name="a*x^2 + b*x + c", values=c("a=1,b=0,c=0"="blue", "a=-1,b=0,c=0"="purple", "a=1,b=-10,c=25"="red", "a=4,b=0,c=100"="green")) + 
    theme_bw() + geom_hline(yintercept = 0, colour = "gray20") + geom_vline(xintercept = 0, colour = "gray20")
{% endhighlight %}

![plot of chunk unnamed-chunk-9](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-9-1.svg)

#### Example


{% highlight r %}
quadTrans <- quadraticTransform(transformationId="Quadratic-transformation", a=1, b=1, c=0)
qd_fcs <- transform(fcs, transformList('FSC-H', quadTrans))

par(mfrow=c(1,2))
plot(density(fcs@exprs[ ,'FSC-H']), main = "Before Transformation")
plot(density(qd_fcs@exprs[ ,'FSC-H']), main = "After Transformation")
{% endhighlight %}

![plot of chunk unnamed-chunk-10](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-10-1.svg)


### Hyperbolic arc-sine Transformation

The formula for arcsinh transformation if `x<-asinh(a+b*x)+c where asinh <- function(x) {log(x + sqrt(x^2 + 1))}`, and the crrosponding function is `arcsinhTransform(transformationId="defaultArcsinhTransform", a=1, b=1, c=0)`.

#### Transformation function 


{% highlight r %}
ggplot(data.frame(x=c(-10,10)), aes(x)) +
  stat_function(fun=function(x) asinh(0+1*x)+0 , geom="line", aes(colour="a=0,b=1,c=0")) +
  stat_function(fun=function(x) asinh(0+4*x)+0, geom="line", aes(colour="a=0,b=4,c=0")) +
  stat_function(fun=function(x) asinh(5+1*x)+5, geom="line", aes(colour="a=5,b=1,c=5")) +
  stat_function(fun=function(x) asinh(0+-1*x)+0, geom="line", aes(colour="a=0,b=-1,c=0")) +
  scale_colour_manual(name="asinh(a+b*x)+c", values=c("a=0,b=1,c=0"="blue", "a=0,b=4,c=0"="purple", "a=5,b=1,c=5"="red", "a=0,b=-1,c=0"="green")) + 
    theme_bw() + geom_hline(yintercept = 0, colour = "gray20") + geom_vline(xintercept = 0, colour = "gray20")
{% endhighlight %}

![plot of chunk unnamed-chunk-11](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-11-1.svg)

#### Example


{% highlight r %}
asinhTrans <- arcsinhTransform(transformationId="ln-transformation", a=1, b=1, c=1)
as_fcs <- transform(fcs, transformList('FSC-H', asinhTrans))

par(mfrow=c(1,2))
plot(density(fcs@exprs[ ,'FSC-H']), main = "Before Transformation")
plot(density(as_fcs@exprs[ ,'FSC-H']), main = "After Transformation")
{% endhighlight %}

![plot of chunk unnamed-chunk-12](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-12-1.svg)


### Biexponential Transformation

Biexponential Transformation is an over-parameterized inverse of the hyperbolic sine, the formula to be inverted takes the form `f(x) = a*exp(b*(x-w))-c*exp(-d*(x-w))+f `, and the crrosponding function is `biexponentialTransform(transformationId="defaultBiexponentialTransform", a = 0.5, b = 1, c = 0.5, d = 1, f = 0, w = 0, tol = .Machine$double.eps^0.25, maxit = as.integer(5000))`

#### Transformation function 


{% highlight r %}
biexp <- function(x, a = 0.5, b = 1, c = 0.5, d = 1, f = 0, w = 0, 
                  tol = .Machine$double.eps^0.25, 
                  maxit = as.integer(5000)){
    
    flowCore:::biexponential_transform(input = x, 
                                       A = a, 
                                       B = b, 
                                       C = c, 
                                       D = d, 
                                       F = f, 
                                       W = w, 
                                       Tol = tol, 
                                       MaxIt = maxit)
}

ggplot(data.frame(x=c(-5000,5000)), aes(x)) +
  stat_function(fun=function(x) biexp(x, a = 0.5, b = 1, c = 1, d = 1, f = 0, w = 0), geom="line", aes(colour="a=0.5,b=1,c=1,d=1,f=0,w=0")) +
  stat_function(fun=function(x) biexp(x, a = 0.5, b = 2, c = 10, d = 1, f = 0, w = 0), geom="line", aes(colour="a=0.5,b=2,c=10,d=1,f=0,w=0")) +
  stat_function(fun=function(x) biexp(x, a = 1, b = 1, c = 0.5, d = 1, f = 0, w = 0), geom="line", aes(colour="a=1,b=1,c=0.5,d=1,f=0,w=0")) +
  stat_function(fun=function(x) biexp(x, a = 0.5, b = 1, c = 1000, d = 1, f = 0, w = 0), geom="line", aes(colour="a=0.5,b=1,c=1000,d=1,f=0,w=0")) +
  scale_colour_manual(name="biexponential", 
                      values=c("a=0.5,b=1,c=1,d=1,f=0,w=0"="blue", 
                               "a=0.5,b=2,c=10,d=1,f=0,w=0"="purple", 
                               "a=1,b=1,c=0.5,d=1,f=0,w=0"="red", 
                               "a=0.5,b=1,c=1000,d=1,f=0,w=0"="green")) + 
    theme_bw() + geom_hline(yintercept = 0, colour = "gray20") + geom_vline(xintercept = 0, colour = "gray20")
{% endhighlight %}

![plot of chunk unnamed-chunk-13](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-13-1.svg)

#### Example


{% highlight r %}
biexp <- biexponentialTransform("myTransform")
biexp_fcs <- transform(fcs, transformList('FSC-H', biexp))

par(mfrow=c(1,2))
plot(density(fcs@exprs[ ,'FSC-H']), main = "Before Transformation")
plot(density(biexp_fcs@exprs[ ,'FSC-H']), main = "After Transformation")
{% endhighlight %}

![plot of chunk unnamed-chunk-14](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-14-1.svg)


### Logicle Transformation

Logicle transformation creates a subset of hyperbolic sine transformation functions that provides several advantages over linear/log transformations for display of flow cytometry data.

and the crrosponding function is `logicleTransform(transformationId="defaultLogicleTransform", w = 0.5, t = 262144, m = 4.5, a = 0)`

#### Transformation function 


{% highlight r %}
lgcl <- function(x, w = 0.5, t = 262144, m = 4.5, a = 0){
    
    flowCore:::logicle_transform(input = x, 
                                 T = t, 
                                 W = w, 
                                 M = m, 
                                 A = a, 
                                 isInverse = FALSE)
}

ggplot(data.frame(x=c(-5000,5000)), aes(x)) +
  stat_function(fun=function(x) lgcl(x, w = 0.5, t = 5000, m = 4.5, a = 1), geom="line", aes(colour="w=0.5,t=5000,m=4.5,a=1")) +
  stat_function(fun=function(x) lgcl(x, w = 0.5, t = 2500, m = 4.5, a = 0), geom="line", aes(colour="w=0.5,t=2500,m=4.5,a=0")) +
  stat_function(fun=function(x) lgcl(x, w = 0.5, t = 5000, m = 3, a = 0), geom="line", aes(colour="w=0.5,t=5000,m=3,a=0")) +
  stat_function(fun=function(x) lgcl(x, w = 1, t = 5000, m = 4.5, a = 0), geom="line", aes(colour="w=1,t=5000,m=4.5,a=0")) +
  scale_colour_manual(name="logicle", 
                      values=c("w=0.5,t=5000,m=4.5,a=1"="blue", 
                               "w=0.5,t=2500,m=4.5,a=0"="purple", 
                               "w=0.5,t=5000,m=3,a=0"="red", 
                               "w=1,t=5000,m=4.5,a=0"="green")) + 
    theme_bw() + geom_hline(yintercept = 0, colour = "gray20") + geom_vline(xintercept = 0, colour = "gray20")
{% endhighlight %}

![plot of chunk unnamed-chunk-15](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-15-1.svg)


We can see that `m` controls the range of positive values, `w` controls the range of negative values,
 `a` changes the slope, `t` is the maximal `x` value corresponds to `m`. A nice explanation is included in paper[]
 
 ![](/figures/25-07-2016-cytometry-transformation/logicle_trans.png)


#### Example


{% highlight r %}
lgcl <- logicleTransform("myTransform", w = 0.5, t= 262144, m = 4.5)
lgcl_fcs <- transform(fcs, transformList("PE-A", lgcl))

par(mfrow=c(1,2))
plot(density(fcs@exprs[ ,'PE-A']), main = "Before Transformation")
plot(density(lgcl_fcs@exprs[ ,'PE-A']), main = "After Transformation")
{% endhighlight %}

![plot of chunk unnamed-chunk-16](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-16-1.svg)

And in `flowCore`, there is a funciton `estimateLogicle` which can help automatic determine the parameters for `logicleTransform`.

And it works as below:


{% highlight r %}
# flowCore:::.lgclTrans
function (dat, p, t, m, a = 0, q = 0.05, type = "instrument") 
{
    type <- match.arg(type, c("instrument", "data"))
    transId <- paste(p, "logicleTransform", sep = "_")
    rng <- range(dat)
    dat <- exprs(dat)[, p]
    if (missing(t)) {
        if (type == "instrument") 
            t <- rng[, p][2]
        else t <- max(dat)
    }
    if (missing(m)) {
        if (type == "instrument") 
            m <- 4.5
        else m <- log10(t) + 1
    }
    dat <- dat[dat < 0]
    w <- 0
    if (length(dat)) {
        r <- .Machine$double.eps + quantile(dat, q)
        w = (m - log10(t/abs(r)))/2
        if (w < 0) 
            stop("w is negative!Try to increase 'm'")
    }
    logicleTransform(transformationId = transId, w = w, t = t, 
        m = m, a = a)
}
{% endhighlight %}



{% highlight r %}
algcl <- estimateLogicle(fcs, channels = c('PE-A'))
algcl_fcs <- transform(fcs, algcl)

par(mfrow=c(1,2))
plot(density(fcs@exprs[ ,'PE-A']), main = "Before Transformation")
plot(density(algcl_fcs@exprs[ ,'PE-A']), main = "After Transformation")
{% endhighlight %}

![plot of chunk unnamed-chunk-18](/figures/25-07-2016-cytometry-transformation/unnamed-chunk-18-1.svg)


## Reference

## Session Information


{% highlight r %}
sessionInfo()
{% endhighlight %}



{% highlight text %}
## R version 3.3.0 (2016-05-03)
## Platform: x86_64-apple-darwin13.4.0 (64-bit)
## Running under: OS X 10.11.6 (El Capitan)
## 
## locale:
## [1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## other attached packages:
## [1] ggplot2_2.1.0   flowCore_1.38.2 knitr_1.13     
## 
## loaded via a namespace (and not attached):
##  [1] graph_1.50.0        Rcpp_0.12.5         cluster_2.0.4      
##  [4] magrittr_1.5        BiocGenerics_0.18.0 munsell_0.4.3      
##  [7] colorspace_1.2-6    lattice_0.20-33     rrcov_1.3-11       
## [10] pcaPP_1.9-60        highr_0.6           plyr_1.8.4         
## [13] stringr_1.0.0       tools_3.3.0         parallel_3.3.0     
## [16] grid_3.3.0          gtable_0.2.0        Biobase_2.32.0     
## [19] corpcor_1.6.8       htmltools_0.3.5     matrixStats_0.50.2 
## [22] yaml_2.1.13         digest_0.6.9        formatR_1.4        
## [25] codetools_0.2-14    rsconnect_0.4.3     robustbase_0.92-6  
## [28] evaluate_0.9        rmarkdown_1.0       labeling_0.3       
## [31] stringi_1.1.1       DEoptimR_1.0-6      scales_0.4.0       
## [34] stats4_3.3.0        mvtnorm_1.0-5
{% endhighlight %}

