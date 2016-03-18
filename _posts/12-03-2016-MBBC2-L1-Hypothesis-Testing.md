---
layout: default
title: MBBC2 L1 Hypothesis Test (Z-test)
comments: true
categories: [Notes]
tags: [MBBC2, stastics, R]
---

## MBBC2 Lecture 1 - Hypothesis Test (Z-test)
---

>This is my course notes for [Mathematical Biostatistics Boot Camp 2](https://www.coursera.org/learn/biostatistics-2/home/welcome), course materials are free on [github](https://github.com/bcaffo/MathematicsBiostatisticsBootCamp2).


### 1. Hypothesis Testing

Hypothesis testing is concerned with making decisions using data
 * A null hypothesis is specified that represents the status quo, usually labeled H0
 * The null hypothesis is assumed true and statistical evidence is required to reject it in favor of a research or alternative hypothesis
 
For example:
![](/images/MBBC2_L1/1_example.png)

![](/images/MBBC2_L1/2_four_outcome.png)

![](/images/MBBC2_L1/3.png)

![](/images/MBBC2_L1/4.png)

![](/images/MBBC2_L1/5.png)

### 2. General rule

![](/images/MBBC2_L1/6.png)

![](/images/MBBC2_L1/7.png)

![](/images/MBBC2_L1/8.png)

![](/images/MBBC2_L1/9.png)


### 3. Two sided tests

![](/images/MBBC2_L1/10.png)

### 4. Confidence intervals

![](/images/MBBC2_L1/11.png)

![](/images/MBBC2_L1/12.png)


### 5. P-values

![](/images/MBBC2_L1/13.png)

![](/images/MBBC2_L1/14.png)

![](/images/MBBC2_L1/15.png)

#### Criticisms of the P-value

![](/images/MBBC2_L1/16.png)


### 6. R test codes

{% highlight r linenos %}

qnorm(.95)


xval <- seq(-3.2, 3.2, length = 1000)
yval<- dnorm(xval)

plot(xval, yval, type = "l", axes = TRUE, frame = FALSE, lwd = 3, xlab = "", ylab = "")
x <- seq(qnorm(.95), 3.2, length = 100)
polygon(c(x, rev(x)),c(dnorm(x), rep(0, length(x))), col = "salmon")
text(mean(x), mean(dnorm(x))+.02, "5%", cex = 2)
text(qnorm(.95), .01, "1.645", cex = 2)


plot(xval, yval, type = "l", axes = TRUE, frame = FALSE, lwd = 3, xlab = "", ylab = "")
x <- seq(qnorm(.975), 3.2, length = 100)
polygon(c(x, rev(x)),c(dnorm(x), rep(0, length(x))), col = "salmon")
text(mean(x), mean(dnorm(x))+.02, "2.5%", cex = 2)
text(qnorm(.975), .01, "1.96", cex = 2)
x <- seq(-3.2, qnorm(.025),length = 100)
polygon(c(x, rev(x)),c(dnorm(x), rep(0, length(x))), col = "salmon")
text(mean(x), mean(dnorm(x))+.02, "2.5%", cex = 2)
text(qnorm(.025), .01, "-1.96", cex = 2)
text(0, dnorm(0) / 5, "95%", cex = 2)

xval <- seq(-4, 4, length = 1000)
yval<- dt(xval, 15)
plot(xval, yval, type = "l", axes = TRUE, frame = FALSE, lwd = 3, xlab = "", ylab = "")
x <- seq(qt(.975, 15), 4, length = 100)
polygon(c(x, rev(x)),c(dt(x, 15), rep(0, length(x))), col = "salmon")
text(mean(x), mean(dt(x, 15))+.02, "2.5%", cex = 2)
text(qt(.975, 15), .01, "2.13", cex = 2)
x <- seq(-4, qt(.025, 15),length = 100)
polygon(c(x, rev(x)),c(dt(x, 15), rep(0, length(x))), col = "salmon")
text(mean(x), mean(dt(x, 15))+.02, "2.5%", cex = 2)
text(qt(.025, 15), .01, "-2.13", cex = 2)
text(0, dt(0, 15) / 5, "95%", cex = 2)

pt(.8, 15, lower.tail=FALSE)
xval <- seq(-4, 4, length = 1000)
yval<- dt(xval, 15)
plot(xval, yval, type = "l", axes = TRUE, frame = FALSE, lwd = 3, xlab = "", ylab = "")
x <- seq(.8, 4, length = 100)
polygon(c(x, rev(x)),c(dt(x, 15), rep(0, length(x))), col = "salmon")
text(mean(x), mean(dt(x, 15))+.02, "22%", cex = 2)
text(0.8, .01, "0.8", cex = 2)

{% endhighlight %}

