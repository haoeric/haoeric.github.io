---
layout: post
title: 一文捋清PCA（No Bullshit PCA）
comments: true
categories: [Statistics and Algorithms]
tags: [PCA, eigenvalues, eigenvectors, 降维]
---

PCA可谓降维界的鼻祖，说到降维就必定面对的是高纬数据。我们平时接触的大部分数据都可以用一个矩阵来存储。例如这样一个带有$m$条记录和$n$个变量的数据，就可以表示成如下矩阵：

$$
A_{m,n} = 
 \begin{pmatrix}
  a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\
  a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\
  \vdots  & \vdots  & \ddots & \vdots  \\
  a_{m,1} & a_{m,2} & \cdots & a_{m,n} 
 \end{pmatrix}
$$


这就是一个$n$维的数据，每一个维度表示了一个变量。为了分析或者用图形来展示各条记录之间的关系，通常我们希望把这$n$个变量通过某种信息压缩的形式转换到一个低维的空间中，其中一个办法就找到这$n$个变量的线性相关性，然后通过线性变化来去除和重组相关的的变量，从而来找到其中最重要的变化关系。

下面我们一点一点来完成这个目标：

### 1. 线性组合
怎么样对矩阵$A$的列进行线性组合呢，在[特征值和特征向量的几何意义](http://haoeric.com/statistics%20and%20algorithms/2016/08/22/matrix-eigenvectors/)一文中我们在矩阵点乘的**列向量视角**中看到，**两个矩阵相乘后的列向量是左边矩阵中的每一个列向量按照右边矩阵对应的列向量的元素做某种线性组合后生成的新向量**。举个例子：

$$
AB =
\begin{bmatrix}
  a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\
  a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\
  \vdots  & \vdots  & \ddots & \vdots  \\
  a_{m,1} & a_{m,2} & \cdots & a_{m,n} 
\end{bmatrix}

\begin{bmatrix}
        b_{1,1} \\
        b_{2,1} \\
        \vdots  \\
        b_{n,1} \\
\end{bmatrix}   \\

=

\begin{bmatrix}
    \begin{bmatrix} a_{1,1} \\ a_{2,1} \\ \vdots \\ a_{m,1} \end{bmatrix}  b_{1,1} 
    + 
    \begin{bmatrix} a_{1,2} \\ a_{2,2} \\ \vdots \\ a_{m,2} \end{bmatrix}  b_{2,1} 
    + 
    \cdots 
    + 
    \begin{bmatrix} a_{1,n} \\ a_{2,n} \\ \vdots \\ a_{m,n} \end{bmatrix}  b_{n,1}
\end{bmatrix}       
$$  

就是这么奇妙，看似繁琐的线性组合，用矩阵相乘就轻松解决了。为了展示方便，上面例子中的矩阵$B$只有一列，如果$B$有$n$列，就对矩阵$A$的列进行$n$种线性组合，生成$n$个新的列向量。


### 2. 相关性

再来看怎么计算两个变量间的相关性，没错，就是统计里学过的协方差（$cov$）。我们先来看看协方差的定义：

$$
cov(a,b) = \frac{1}{m} \displaystyle\sum_{i=1}^{m} (a_i - \mu_a)(b_i - \mu_b)
$$

来个实际的例子，我们计算上面矩阵$A$中第一列和第二列的相关性：

$$
cov(a_{\_,1}, a_{\_,2}) = 
\frac{1}{m} 
\displaystyle \sum_{i=1}^{m} (a_{i,1} - \mu_{a_{\_,1}})(a_{i,2} - \mu_{a_{\_,2}})
$$

想想，如果我们事先将矩阵$A$的每一列的平均值都变成零（即每一列的元素都先减去它的平均值），那么上面的计算就可以简化成：

$$
cov(a_{\_,1}, a_{\_,2}) = 
\frac{1}{m} 
\displaystyle \sum_{i=1}^{m} a_{i,1} a_{i,2} 
$$

这不就是两个向量点乘的结果再除以$m$吗。奇妙再次发生，所以我们只要事先将矩阵的每一列的平均值转化为0，那么矩阵$A$的列与列之间的协方差就可以通过如下方式计算：

$$
C = 
\frac{1}{m} A^{T}A 
= 
\frac{1}{m} 
\begin{bmatrix}
  a_{1,1} & a_{2,1} & \cdots & a_{m,1} \\
  a_{1,2} & a_{2,2} & \cdots & a_{m,2} \\
  \vdots  & \vdots  & \ddots & \vdots  \\
  a_{1,n} & a_{2,n} & \cdots & a_{m,n} 
\end{bmatrix}

\begin{bmatrix}
  a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\
  a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\
  \vdots  & \vdots  & \ddots & \vdots  \\
  a_{m,1} & a_{m,2} & \cdots & a_{m,n} 
\end{bmatrix}                          \\
=
\begin{bmatrix}
  \frac{1}{m} \displaystyle \sum_{i=1}^{m} a_{i,1}a_{i,1} & 
  \frac{1}{m} \displaystyle \sum_{i=1}^{m} a_{i,1}a_{i,2} & 
  \cdots                                                  & 
  \frac{1}{m} \displaystyle \sum_{i=1}^{m} a_{i,1}a_{i,n}   \\
  \frac{1}{m} \displaystyle \sum_{i=1}^{m} a_{i,2}a_{i,1} & 
  \frac{1}{m} \displaystyle \sum_{i=1}^{m} a_{i,2}a_{i,2} & 
  \cdots                                                  & 
  \frac{1}{m} \displaystyle \sum_{i=1}^{m} a_{i,2}a_{i,n}   \\
  \vdots  & \vdots  & \ddots & \vdots  \\
  \frac{1}{m} \displaystyle \sum_{i=1}^{m} a_{i,n}a_{i,1} & 
  \frac{1}{m} \displaystyle \sum_{i=1}^{m} a_{i,n}a_{i,2} & 
  \cdots                                                  & 
  \frac{1}{m} \displaystyle \sum_{i=1}^{m} a_{i,n}a_{i,n}   \\
\end{bmatrix}                         
$$

这里计算的其实就是非常有意思的[协方差矩阵](http://www.wikiwand.com/zh/协方差矩阵)，其每一个元素$C_{i,j}$就对应了矩阵$A$中第$i$列与第$j$列变量之间的协方差。

### 3. 方差

另外我们注意一下上面协方差矩阵对角线上的元素，想一想，当平均值为0的列向量与自身求协方差，实际上计算的是什么？对，其实就是方差，就是这么奇妙：

$$
var(a_{\_,k}, a_{\_,k}) 
= 
\frac{1}{m} \displaystyle \sum_{i=1}^{m} (a_{i,k} - \mu_{a_{\_,k}})^2
=
\frac{1}{m} \displaystyle \sum_{i=1}^{m} a_{i,k}a_{i,k}
$$


### 4. PCA

好的，目前我们的储备知识已经基本充足了，回到我们的主题PCA。这里我们对PCA的目的进行一种更数学性的描述：**对一个矩阵中的列进行某种线性组合后，使得新生成的矩阵中的每一列(主成分)之间无线性相关性（即协方差为0），并且使每一个主成分尽可能多地承载原数据中各条记录间的离散关系（方差尽可能的大）。**

有没有一种眼前一亮的感觉，是否感受到这里有奇妙发生。如果没有，慢慢来，我们将上面的表述再清楚的展示一下：

------

$$
矩阵A + 某种线性组合 \ \Rightarrow \ 新矩阵的列与列（非自身）之间线性不相关，列自身的方差尽可能大
$$

$$
\Downarrow                                                                                       
$$

$$
矩阵A\ 乘以\ 矩阵B \ \Rightarrow \ 新矩阵的协方差矩阵为对角矩阵（除对角线元素外，其他元素均为0） 
$$

$$
\Downarrow                                                                              
$$

$$
P = AB \ \Rightarrow \ \frac{1}{m}P^TP = \Lambda
$$

$$
\Downarrow                                                                              
$$  

$$
\frac{1}{m}(AB)^T(AB) = \Lambda
\ \Rightarrow \ 
\frac{1}{m}B^TA^TAB = \Lambda
\ \Rightarrow \ 
B^T(\frac{1}{m}A^TA)B = \Lambda
$$

------

哈哈，推导到这里，此时有没有一种醍醐灌顶的感觉。如果没有，那你一定是没有好好看[特征值和特征向量的几何意义](http://haoeric.com/statistics%20and%20algorithms/2016/08/22/matrix-eigenvectors/)。是的，这里我们已经找到了PCA计算的本质：

**即将矩阵$A$的列均值变换为0后，求协方差矩阵$\frac{1}{m}A^TA$的特征值和特征向量。**

这里的每一个特征向量对应了原矩阵的一个主成分，而特征值就是该主成分所占有的权重。如果选取k（k大于0，小于n）个最大的特征值对应的特征向量，将原矩按照这k个特征向量进行线性组合就把原矩阵转换成了k维的数据，到达了降维的目的。

**PS**：*有些地方喜欢用投影变换来解释PCA，但是我个人更喜欢用线性组合来解释，起码我觉得这样理解起来更清晰。但是本质上都一样，只是对矩阵点乘的两种理解：行向量视角和列向量视角。同时也提醒下，两个<u>向量正交</u>（点乘为0）与由这两个向量的元素构成的变量之间的<u>线性不相关</u>（协方差为0）是完全两码事。*














