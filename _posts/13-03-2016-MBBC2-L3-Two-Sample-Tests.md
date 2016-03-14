---
layout: default
title: MBBC2 L3 Two Sample Tests
comments: true
categories: [Notes]
tags: [MBBC2, stastics, R]
---

## Lecture 3 - Two Sample Tests
---

>This is my course notes for [Mathematical Biostatistics Boot Camp 2](https://www.coursera.org/learn/biostatistics-2/home/welcome), course materials are free on [github](https://github.com/bcaffo/MathematicsBiostatisticsBootCamp2).


### 1. Matched data

![](/images/MBBC2_L3/1.png)

#### Example 

![](/images/MBBC2_L3/2.png)

![](/images/MBBC2_L3/3.png)

![](/images/MBBC2_L3/4.png)


#### R Code

{% highlight r linenos %}

diff <- test2 - test1
n <- sum(!is.na(diff)) #49
mean(diff) #2.88
sd(diff) #7.61
testStat <- sqrt(n) * mean(diff) / sd(diff) #2.65
# below works out to be 0.01
2 * pt(abs(testStat), n -1, lower.tail = FALSE)
##uses the R function
t.test(diff)

{% endhighlight %}

#### Discussion of matched data

![](/images/MBBC2_L3/5.png)


#### Regression to mediocrity

![](/images/MBBC2_L3/6.png)

![](/images/MBBC2_L3/7.png)

![](/images/MBBC2_L3/8.png)

![](/images/MBBC2_L3/9.png)

![](/images/MBBC2_L3/10.png)

#### Comments

![](/images/MBBC2_L3/11.png)


### 2. Two independent groups

![](/images/MBBC2_L3/12.png)

![](/images/MBBC2_L3/13.png)

![](/images/MBBC2_L3/14.png)

#### Example

![](/images/MBBC2_L3/15.png)

 * 1 note this is not obtained by averaging the two standard deviations, it’s obtained by averaging the variances then square rooting
 
![](/images/MBBC2_L3/16.png)

#### Comments

![](/images/MBBC2_L3/17.png)
