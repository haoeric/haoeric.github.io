---
layout: post
title: Precision and Recall
comments: true
categories: [Statistics]
tags: [Statistics, R]
---


In binary classification, **precision** (also called **positive predictive value**) is the fraction of retrieved instances that are relevant, while **recall** (also known as **sensitivity**) is the fraction of relevant instances that are retrieved. Both precision and recall are therefore based on an understanding and measure of **relevance**. 


### 1. Contingency Table

The outcomes of binary classification can be formulated in a 2×2 **contingency table** or **confusion matrix**, as follows:

![](/images/Precision_and_recall/contingency_table.png)


### 2. F-measure

A measure that combines precision and recall is the harmonic mean of precision and recall, the traditional **F-measure** or **balanced F-score**. There are several reasons that the **F-score** can be criticized in particular circumstances due to its bias as an evaluation metric. This is also known as the *F_1* measure, because recall and precision are evenly weighted.

It is a special case of the general *F_beta* measure (for non-negative real values of *beta*):

![](/images/Precision_and_recall/f_measure.png)

Two other commonly used F measures are the *F_2* measure, which weights recall higher than precision, and the *F_0.5* measure, which puts more emphasis on precision than recall.

### 3. Accuracy

**Accuracy** measures how well a binary classification test correctly identifies or excludes a condition. That is, the accuracy is the proportion of true results (both true positives and true negatives) among the total number of cases examined. 

![](/images/Precision_and_recall/accurancy.png)

Another useful performance measure is the **balanced accuracy** which avoids inflated performance estimates on imbalanced datasets. It is defined as the arithmetic mean of sensitivity and specificity, or the average accuracy obtained on either class:

![](/images/Precision_and_recall/balanced_accuracy.png)


If the classifier performs equally well on either class, this term reduces to the conventional accuracy (i.e., the number of correct predictions divided by the total number of predictions). In contrast, if the conventional accuracy is above chance only because the classifier takes advantage of an imbalanced test set, then the balanced accuracy, as appropriate, will drop to chance.[10] A closely related chance corrected measure is:

![](/images/Precision_and_recall/Informedness.png)


### 4. kappa

A direct approach to debiasing and renormalizing Accuracy is [**Cohen's kappa**](http://www.wikiwand.com/en/Cohen%27s_kappa), whilst **Informedness** has been shown to be a Kappa-family debiased renormalization of Recall. **Informedness** and **Kappa** have the advantage that chance level is defined to be 0, and they have the form of a probability. Informedness has the stronger property that it is the probability that an informed decision is made (rather than a guess), when positive. When negative this is still true for the absolutely value of Informedness, but the information has been used to force an incorrect response.

The formula for Kappa is:

![](/images/Precision_and_recall/kappa_1.png)

#### Example

![](/images/Precision_and_recall/kappa_2.png)



### 5. Reference

 * [Precision and recall](http://www.wikiwand.com/en/Precision_and_recall)
 * [Accuracy and precision](http://www.wikiwand.com/en/Accuracy_and_precision)
 * [Cohen's Kappa](http://www.wikiwand.com/en/Cohen%27s_kappa)