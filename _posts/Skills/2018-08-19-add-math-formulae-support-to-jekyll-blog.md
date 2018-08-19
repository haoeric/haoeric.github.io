---
layout: post
title:  简单两步让Jekyll支持Latex公式插入
comments: true
author: Chen Hao
categories: [Skills]
tags: [Jekyll, MathJax, Latex, 公式]
---

MathJax是一个开源JavaScript引擎，能够将LaTeX语法书写的公式在网页上显示出来，而且效果杠杠的。在你的 Jekyll 博客系统中，做如下简单两部配置，就可以愉快的博客中插入Latex公式了。

### 1. 加载和配置MathJax

创建文件`_includes/mathJax_support.html`，里面包括如下代码：

```html
<!-- MathJax Section -->
<!-- copied from http://docs.mathjax.org/en/latest/configuration.html -->
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      extensions: ["tex2jax.js"],
      jax: ["input/TeX", "output/HTML-CSS"],
      tex2jax: {
        inlineMath: [ ['$','$'], ["\\(","\\)"] ],
        displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
        processEscapes: true
      },
      "HTML-CSS": { fonts: ["TeX"] }
    });
</script>
<script type="text/javascript"
   src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-AMS-MML_CHTML">
</script>
```

然后在`_layouts/default.html`文件中添加如下一行代码：

```html
{% include mathJax_support.html %}
```

简单来讲，上面的操作就是博客页面中包含MathJax脚本（注意MathJax原来的DNS地址[已经失效](https://liam0205.me/2015/09/09/fix-conflict-between-mathjax-and-markdown/)，这里是更新过的），同时做一些配置让JavaScript能识别我们定义的公式标签，将Latex编译成我们想要的公式。

通过上面的配置，我们在markdown文本中添加特定的标识符`$`或者`\(`，就可以在文本中插入公式或者单独以段落显示公式，具体效果如下：

来个文中显示，比如$x - \mu$，不错吧。再来个高斯分布方程：

$$
P(x) = \frac{1} {{\sigma \sqrt {2\pi } }} e^ {{{ - \left( {x - \mu } \right)^2 } \mathord{\left/ {\vphantom {{ - \left( {x - \mu } \right)^2 } {2\sigma ^2 }}} \right. \kern-\nulldelimiterspace} {2\sigma ^2 }}}
$$

关于Latex公式的语法，参考[Wiki LaTeX Mathematics](https://en.wikibooks.org/wiki/LaTeX/Mathematics)

### 2. 定制公式显示的CSS Styles

MathJax使用网络字体，支持CSS配置产生高质量的排版。另外，使用MathJax显示数学公式是基于文本的，而非图片，在所有分辨率中都可缩放和显示也可以被搜索引擎直接搜索。


在`styles.scss`文件中添加如下代码：

```css
body div.content {}
    body div.content code.has-jax {
        font: inherit;
        font-size: 100%;
        background: inherit;
        border: inherit;
        color: #000000;
    }
```




### 参考

 [1] [用Markdown写blog的常用操作](http://www.cnblogs.com/mo-wang/p/5117819.html)     
 [2] [Loading and Configuring MathJax](http://docs.mathjax.org/en/latest/configuration.html#loading-and-configuring-mathjax)    
 [3] [CSS Style Objects](http://docs.mathjax.org/en/latest/reference/CSS-styles.html)    