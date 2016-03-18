---
layout: default
title: MBBC2 L4,5,6 Two Sample Binomial Tests
comments: true
author: Chen Hao
categories: [Notes]
tags: [MBBC2, stastics, R]
---


## MBBC2 Lecture 4,5,6 - Two Sample Binomial Tests
---


>This is my course notes for [Mathematical Biostatistics Boot Camp 2](https://www.coursera.org/learn/biostatistics-2/home/welcome), course materials are free on [github](https://github.com/bcaffo/MathematicsBiostatisticsBootCamp2).


### 1. Hypothesis tests for binomial proportions

#### 1.1 An Example:

![](/images/MBBC2_L456/1.png)
![](/images/MBBC2_L456/2.png)

#### 1.2 Calculate Confidence Interval

![](/images/MBBC2_L456/3.png)

In the one sample case, the Wald interval and test performs poorly relative to the score interval and test. For testing, always use the score test.For intervals, inverting the score test is hard and not offered in standard software. the Agresti/Caffo interval does not approximate the score interval, but does perform better than the Wald interval.

### 2. Comparing two binomials 

![](/images/MBBC2_L456/4.png)

#### 2.1 Absolute change

![](/images/MBBC2_L456/5.png)

#### 2.2 Relative change

![](/images/MBBC2_L456/6.png)

#### 2.3 Odds ratio

![](/images/MBBC2_L456/7.png)

#### 2.4 Summary and Comments

![](/images/MBBC2_L456/8.png)
![](/images/MBBC2_L456/9.png)


### 3. Comparison of Two Population Proportions in R

#### 3.1 Chi-squared test
{% highlight r linenos %}
prop.test(c(17,8),c(25,20),correct=FALSE)
# 
#     2-sample test for equality of proportions without continuity correction
# 
# data:  c(17, 8) out of c(25, 20)
# X-squared = 3.528, df = 1, p-value = 0.06034
# alternative hypothesis: two.sided
# 95 percent confidence interval:
#  -0.002016956  0.562016956
# sample estimates:
# prop 1 prop 2 
#   0.68   0.40 
{% endhighlight %}

In the case of small samples (low value of n), you must specify `correct = TRUE`, so as to change the computation of chi-square based on the continuity of Yates

#### 3.2 Fisher's Exact Test
{% highlight r linenos %}
fisher.test(matrix(c(17, 25-17, 8, 20-8), ncol=2))
    Fisher's Exact Test for Count Data
# data:  matrix(c(17, 25 - 17, 8, 20 - 8), ncol = 2)
# p-value = 0.07671
# alternative hypothesis: true odds ratio is not equal to 1
# 95 percent confidence interval:
#   0.7990888 13.0020065
# sample estimates:
# odds ratio 
#   3.101466 
{% endhighlight %}

