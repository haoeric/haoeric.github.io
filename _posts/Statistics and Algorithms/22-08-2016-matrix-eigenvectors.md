---
layout: post
title: 特征值和特征向量的几何意义
comments: true
categories: [Statistics and Algorithms]
tags: [Matrix, eigenvalues, eigenvectors]
---


## 1. 向量的基本运算

一个长度为$N$的向量可以看成是在$N$维空间中的由原点$(0,0,\dots,0)$引出的一条由$N$个维度上的单位向量按某种线性组合构成的一个向量，向量可以表示成列向量和行向量，感受一下：

$$
\overrightarrow{a} = \begin{bmatrix}
                       a_1 \\
                       a_2 \\
                       \dots \\
                       a_n
                     \end{bmatrix}   
$$

$$
\overrightarrow{a} = \begin{bmatrix} 
                       a_1\ 
                       a_2\ 
                       \dots \ 
                       a_n
                     \end{bmatrix}
$$

首先回顾一下向量的几个基本数学操作[1]，毕竟温故而知新。给定两个向量$\overrightarrow{u}=(u_1, u_2, u_3)$和$\overrightarrow{v}=(v_1, v_2, v_3)$，其基本运算包括：

1. 加法：满足[三角形法则](http://www.wikiwand.com/zh/向量#.E5.8A.A0.E6.B3.95.E4.B8.8E.E5.87.8F.E6.B3.95)  

    $$\overrightarrow{u}+\overrightarrow{v}=(u_1+v_1, u_2+v_2, u_3+v_3)$$
    
2. 减法：满足[三角形法则](http://www.wikiwand.com/zh/向量#.E5.8A.A0.E6.B3.95.E4.B8.8E.E5.87.8F.E6.B3.95)  

    $$\overrightarrow{u}-\overrightarrow{v}=(u_1-v_1, u_2-v_2, u_3-v_3)$$
    
3. 伸缩：方向不变，只是长度发生变化    

    $$\alpha\overrightarrow{u}=(\alpha u_1,\ \alpha u_2,\ \alpha u_3)$$
    
4. 范数：即向量的长度   

    $$ || \overrightarrow{u} || = \sqrt{u_1^2 + u_2^2 + u_3^2}$$
    
5. 点乘（内积）：即$\overrightarrow{u}$向量在$\overrightarrow{v}$向量上的投影长度与$\overrightarrow{v}$向量长度的积，结果是一个纯量（数值）    

    $$
    \overrightarrow{u} \cdot \overrightarrow{v} 
    = 
    u_1 v_1 + u_2 v_2 + u_3 v_3    
    = 
    ||\overrightarrow{u}|| \ ||\overrightarrow{v}||\cos \theta
    $$
    
6. 叉乘（向量积）：结果是个向量，它的几何意义是所得的向量与被乘向量所在平面垂直，方向由[右手定则](http://www.wikiwand.com/zh/向量积)规定，大小是两个被乘向量构成的平行四边形的面积  

    $$
    \overrightarrow{u} \times \overrightarrow{v} 
    = 
    (u_2 v_3 - u_3 v_2,\ u_3 v_1 - u_1 v_3,\ u_1 v_2 - u_2 v_1)
    $$

## 2. 两个向量点乘的的几何意义

两个向量点乘的几何意义非同小可。上面我们讲到$\overrightarrow{u} \cdot \overrightarrow{v}$可以理解为$\overrightarrow{u}$向量在$\overrightarrow{v}$向量上的投影再乘以$\overrightarrow{v}$向量的长度。画个图来直观体会下：

![](/images/matrix_eigenvectors/dotproduct.png)

从两个向量点乘的公式中我们可以知道点积的运算是可交换的。接下来，我们看几个向量点乘运算的特殊例子：

1. 如果向量$\overrightarrow{u}$与自身做点乘，则结果为向量$\overrightarrow{u}$长度的平方  

    $$ \overrightarrow{u} \cdot \overrightarrow{u} 
    = u_1^2 + u_2^2 + u_3^2 = || \overrightarrow{u} ||^2
    $$
    
2. 如果向量$\overrightarrow{v}$的长度为1，即为单位向量，那么向量$\overrightarrow{u}$与向量$\overrightarrow{v}$的点乘为向量$\overrightarrow{u}$在向量$\overrightarrow{v}$上的投影长度   

    $$
    \overrightarrow{u} \cdot \overrightarrow{v} 
    = 
    ||\overrightarrow{u}|| \ ||\overrightarrow{v}||\cos \theta 
    = 
    ||\overrightarrow{u}|| \cos \theta
    $$
    
3. 如果$\overrightarrow{u}$与$\overrightarrow{v}$的夹角为90度，即两个向量垂直，则向量$\overrightarrow{u}$与向量$\overrightarrow{v}$的点乘为0  

    $$
    \overrightarrow{u} \cdot \overrightarrow{v} 
    = 
    ||\overrightarrow{u}|| \ ||\overrightarrow{v}||\cos \theta 
    = 
    ||\overrightarrow{u}|| \ ||\overrightarrow{v}|| \cdot 0 = 0
    $$


## 3. 两个矩阵点乘的几何意义

矩阵可以看成是多个维度相同的向量按行或列组合构成的一种结构体。一个$m$行$n$列的矩阵$A$可以表示如下：

$$
A_{m,n} = 
  \begin{bmatrix}
    a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\
    a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\
    \vdots  & \vdots  & \ddots & \vdots  \\
    a_{m,1} & a_{m,2} & \cdots & a_{m,n} 
 \end{bmatrix}
$$

首先上维基百科自行复习下[矩阵的基本运算](http://www.wikiwand.com/zh/矩阵#.E7.9F.A9.E9.99.A3.E7.9A.84.E5.9F.BA.E6.9C.AC.E9.81.8B.E7.AE.97)。既然矩阵是向量的组合，所以矩阵的基本运算也基本可以通过向量的基本运算来引申理解。这里我们重点来看看矩阵乘法，两个矩阵相乘的运算定义如下：

$$
C\ =\ AB\ \Leftrightarrow\ c_{ij} = \sum_{k=1}^{n}  a_{ik} b_{kj}
$$

用个例子展开来看如下：

$$
\begin{bmatrix}
    a_{1,1} & a_{1,2} \\
    a_{2,1} & a_{2,2} \\
    a_{3,1} & a_{3,2} 
\end{bmatrix}

\begin{bmatrix}
    b_{1,1} & b_{1,2} \\
    b_{2,1} & b_{2,2} 
\end{bmatrix}

=

\begin{bmatrix}
    a_{1,1}b_{1,1} +a_{1,2} b_{2,1} & a_{1,1}b_{1,2} +a_{1,2} b_{2,2} \\
    a_{2,1}b_{1,1} +a_{2,2} b_{2,1} & a_{2,1}b_{1,2} +a_{2,2} b_{2,2} \\
    a_{3,1}b_{1,1} +a_{3,2} b_{2,1} & a_{3,1}b_{1,2} +a_{3,2} b_{2,2} 
\end{bmatrix}
$$

既然矩阵可以看成是向量按行或者列的组合，那么对于矩阵相乘的几个意义，我们也可以从行或列两个角度来理解：

- **行向量视角**：将左边矩阵看成由行向量按行组合的矩阵

    $$
    \begin{bmatrix}
        a_{1,1} & a_{1,2} \\
        a_{2,1} & a_{2,2} \\
        a_{3,1} & a_{3,2} 
    \end{bmatrix}

   \begin{bmatrix}
        b_{1,1} & b_{1,2} \\
        b_{2,1} & b_{2,2} 
    \end{bmatrix}

    =

    \begin{bmatrix}
        \begin{bmatrix} a_{1,1} & a_{1,2} \end{bmatrix} \begin{bmatrix} b_{1,1} \\ b_{2,1} \end{bmatrix} &
        \begin{bmatrix} a_{1,1} & a_{1,2} \end{bmatrix} \begin{bmatrix} b_{1,2} \\ b_{2,2} \end{bmatrix}  \\  
        \begin{bmatrix} a_{2,1} & a_{2,2} \end{bmatrix} \begin{bmatrix} b_{1,1} \\ b_{2,1} \end{bmatrix} &
        \begin{bmatrix} a_{2,1} & a_{2,2} \end{bmatrix} \begin{bmatrix} b_{1,2} \\ b_{2,2} \end{bmatrix}  \\  
        \begin{bmatrix} a_{3,1} & a_{3,2} \end{bmatrix} \begin{bmatrix} b_{1,1} \\ b_{2,1} \end{bmatrix} &
        \begin{bmatrix} a_{3,1} & a_{3,2} \end{bmatrix} \begin{bmatrix} b_{1,2} \\ b_{2,2} \end{bmatrix}
    \end{bmatrix}    
    $$

    从行向量视角来看，两个矩阵相乘，可以看成是将右边矩阵的每一列投影到以左边矩阵每一行为基的空间中去；或者看成是将左边矩阵的每一行投影到以右边矩阵的每一列为基的空间中去。这里的变化称为**投影变化**（旋转和伸缩）。

- **列向量视角**：将左边矩阵看成由列向量按列组合的矩阵

    $$
    \begin{bmatrix}
        a_{1,1} & a_{1,2} \\
        a_{2,1} & a_{2,2} \\
        a_{3,1} & a_{3,2} 
    \end{bmatrix}

   \begin{bmatrix}
        b_{1,1} & b_{1,2} \\
        b_{2,1} & b_{2,2} 
    \end{bmatrix}

    =

    \begin{bmatrix}
        \begin{bmatrix} a_{1,1} \\ a_{2,1} \\ a_{3,1} \end{bmatrix}  b_{1,1} 
        + 
        \begin{bmatrix} a_{1,2} \\ a_{2,2} \\ a_{3,2} \end{bmatrix}  b_{2,1} &
        \begin{bmatrix} a_{1,1} \\ a_{2,1} \\ a_{3,1} \end{bmatrix}  b_{1,2} 
        + 
        \begin{bmatrix} a_{1,2} \\ a_{2,2} \\ a_{3,2} \end{bmatrix}  b_{2,2}
    \end{bmatrix}    
    $$  

    从列向量视角来看，两个矩阵相乘后的列向量是左边矩阵中的每一个列向量按照右边矩阵对应的列向量的元素做某种线性组合后生成的新向量。这里的变化称为**线性组合**（[解方程组](http://www.wikiwand.com/zh/矩阵#/.E7.BA.BF.E6.80.A7.E6.96.B9.E7.A8.8B.E7.BB.84)）。

矩阵的乘法**不满足交换律**，但是满足结合律，对矩阵加法的分配律，转置之间则满足倒置的分配律：

* 结合律：$(AB)C = A(BC)$
* 左分配律：$(A + B)C = AC + BC$
* 右分配律：$C(A + B) = CA + CB$
* 倒置的分配律：$(AB)^\top = B^\top A^\top$


## 4. 特征值和特征向量的几何意义

在引入特征值和特征向量前，我们先来看一种特殊的矩阵：方块矩阵（**方阵**）。方阵拥有相同的行数和列数。下面我们先来看看关于方阵的两个很重要的运算：**逆矩阵**和**行列式**。

**<u>逆矩阵</u>**：如果存在另一个方阵$B$，使得

$$
AB = I_n，\ 可以证明 BA = I_n 也成立
$$

那么方阵$A$称为<u>可逆或非奇异的</u>。这里，$I_n$为单位矩阵，也就是主对角线上的元素为1，其它元素为0的矩阵。在上述条件成立下，矩阵$B$称为矩阵$A$的**逆矩阵**（逆矩阵如果存在就是唯一的），也可以记为：

$$
B = A^{-1}
$$

在矩阵相乘的行向量视角中，我们看到矩阵相乘对应了一种投影变换。在这个变换的过程中，原向量主要发生旋转、伸缩的变化。如果一个矩阵$A$是可逆的，那么矩阵$A$对另外一个矩阵$B$点乘后的投影变换可以通过该矩阵的逆矩阵$A^{-1}$来逆转：

$$
AB = C   \\
A^{-1}C = A^{-1}AB = B
$$

**<u>行列式</u>**：方块矩阵$A$的行列式是一个将其映射到标量的函数，记作$det(A)$或$\|A\|$，反映了矩阵自身的一定特性。一个$2\times2$矩阵的行列式计算公式如下：

$$
det
\begin{bmatrix}
        a & b \\
        c & d 
\end{bmatrix}
= ad - bc
$$

对于更高纬方阵的行列式计算可以参考[这里](http://www.wikiwand.com/zh/行列式)。这里我们记住两个行列式的特性：两个矩阵相乘，乘积的行列式等于它们的行列式的乘积：$$det(AB) = det(A)·det(B)$$；并且一个方阵如果不可逆那么它的行列式等于0。


好了，基本准备工作已经做好了，我们回到我们的重点： 

**<u>特征值和特征向量</u>**：如果一个$n \times n$方阵$A$与一个非零向量$x$点乘满足如下条件：

$$
Ax\ = \ \lambda x
$$

那么向量$x$为矩阵$A$的一个特征向量，$\lambda$（非零）即特征向量$x$对应的特征值。

等式左边我们可以看成是将非零向量$x$投影到以方阵$A$每一行为基的坐标系中，等式右边可以看成是对向量$x$进行伸缩变换，伸缩的比例为$\lambda$。所以，如果一个向量投影到一个方阵定义的空间中只发生伸缩变化，而不发生旋转变化，那么该向量就是这个方阵的一个特征向量，伸缩的比例就是特征值。

一般来说，一个向量在经过映射之后可以变为任何可能的向量，而特征向量在这里就很特殊，特征向量其实反应了投影方阵的内部特性。关于特征向量的[应用](http://www.wikiwand.com/zh/特征向量#.E5.BA.94.E7.94.A8)，以后再整理。这里我们了解几个特征值与特征向量的性质：

1. 一个特征值对应的特征向量其实不止一个向量，而是在同一方向上的一个向量族。
2. 一个$n \times n$方阵$A$会对应有$n$个特征值，并且其所有特征值的和与方正$A$对角线上的元素之和相等。
3. 如果一个$n \times n$方阵$A$的所有特征值都不相等，那么该方阵就对应有$n$个相互独立的特征向量。

## 5. 特征值和特征向量的求解

由以上特征值和特征向量满足的等式做以下变换可以得到：

$$
Ax - \lambda x = 0 \\
(A - \lambda I)x = 0
$$

这里$x$是非零向量，那么也就说明$(A - \lambda I)$不可逆，等价于：

$$
det(A - \lambda I) = 0
$$

这样特征值就可以通过行列式来求解，得到的特征值再带入原等式即可算出对应的特征向量。下面我们看几个简单的$2 \times 2$方正特征值与特征向量的求解实例：

<u>实例1</u>：普通情况

$$
A = 
\begin{bmatrix}
        3 & 1 \\
        1 & 3 
\end{bmatrix}  \\

det(A - \lambda I) = 
\begin{bmatrix}
        3 - \lambda & 1 \\
        1 & 3 - \lambda 
\end{bmatrix} = 
(3  - \lambda)^2 - 1 = 0  \\

so \ \ 
\lambda = 
\begin{cases}
    2,\ A - 2I = \begin{bmatrix} 1 & 1 \\ 1 & 1 \end{bmatrix} \Rightarrow x = \begin{bmatrix} -1 \\ 1 \end{bmatrix}  \\
    4,\ A - 4I = \begin{bmatrix} -1 & 1 \\ 1 & -1 \end{bmatrix} \Rightarrow x = \begin{bmatrix} 1 \\ 1 \end{bmatrix}  \\
\end{cases}
$$


<u>实例2</u>：非实数特征值

$$
A = 
\begin{bmatrix}
        0 & -1 \\
        1 & 0 
\end{bmatrix}\ \ 是一个旋转90度的变化矩阵\\

det(A - \lambda I) = 
\begin{bmatrix}
        - \lambda & 1 \\
        1 & - \lambda 
\end{bmatrix} = 
(\lambda)^2 + 1 = 0  \\

so \ \ 
\lambda = 
\begin{cases}
    i\ (非实数解)\\
    -i\ (非实数解)\\
\end{cases}
$$


<u>实例3</u>：相同特征值

$$
A = 
\begin{bmatrix}
        3 & 1 \\
        0 & 3 
\end{bmatrix}  \\

det(A - \lambda I) = 
\begin{bmatrix}
        3 - \lambda & 1 \\
        0 & 3 - \lambda 
\end{bmatrix} = 
(3  - \lambda)^2  = 0  \\

so \ \ 
\lambda = 
\begin{cases}
    3,\ A - 2I = \begin{bmatrix} 1 & 1 \\ 1 & 1 \end{bmatrix} \Rightarrow x = \begin{bmatrix} -1 \\ 1 \end{bmatrix}  \\
    3,\ 没有第二个特征向量  \\
\end{cases}
$$



## 参考

1. [Linear algebra explained in four pages](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwj5vqq9sdTOAhWKPo8KHX09B1EQFggeMAA&url=http%3A%2F%2Fcnd.mcgill.ca%2F~ivan%2Fminiref%2Flinear_algebra_in_4_pages.pdf&usg=AFQjCNHc4rkXXH43cd1KF1qwPkXDfbJciw&sig2=ibyyLJHpsfTXIsMlXBhUnA)

2. [Linear Algebra course by Professor Gilbert Strang](http://ocw.mit.edu/courses/mathematics/18-06-linear-algebra-spring-2010/video-lectures/)