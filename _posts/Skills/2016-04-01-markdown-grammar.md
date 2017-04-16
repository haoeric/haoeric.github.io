---
layout: post
title: 让你的Markdown用起来得心应手
comments: true
author: Chen Hao
categories: [Skills]
tags: [markdown, 标记语言]
---

> 文字的发明和使用使得信息的保存和传递有了革命性的飞跃。随着信息的丰富和传递方式的革新，人们对文本提出了新的格式化的要求，以此来方便人们更舒适地获取信息。如此，HTML(HyperText Markup Language)作为一种超文本标记语言(markup language)应运而生，无数的网页从此有了主次分明，层次清晰的格式。如果将HTML比作一架重机枪，那么Markdown就是一把手枪，满足了主要的文本格式标记的需求，可是操作性却大大简化。秉承「易读易写」的宗旨，Markdown作为一种轻量级标记语言(lightweight markup language)，让无数的程序猿和文字工作者爱不释手。学习Markdown，投资短，见效快，提高生活品质立竿见影，那么还有什么阻止你不去学习。

有那么一小撮人，为了满足自己某个特定的需要，它们不甘妥协，走进小黑屋，点亮屏幕，一段指尖与智慧的狂舞后，皱紧的眉头终于舒展开来，随后露出满意的笑容。[Linus Torvalds](http://mp.weixin.qq.com/s?__biz=MjM5ODQ2MDIyMA==&mid=200486872&idx=1&sn=36d0b252a62847df9aad9f83ef7b9a62)如此打造了Linux, [Rasmus Lerdorf](http://www.wikiwand.com/en/Rasmus_Lerdorf)如此贡献出了PHP, [John Gruber和Aaron Swartz](https://www.fooads.com/post/577cd693ab9db6ff28411263)如此开创了Markdown。Markdown的诞生就是因为这哥俩想要『使用一种易读易写的纯文本格式来编写文档，并且可以被转换成XHTML(或者HTML)文档』。2004年，Markdown横空出世，从此红遍大江南北。如今 Markdown深受程序猿所爱，并且已成了[众多优秀工具的标配](http://www.wikiwand.com/zh/Markdown#Markdown.E7.9A.84.E7.94.A8.E6.88.B7)，比如Github, Stack Overflow，简书，为知笔记，etc。

原生的Markdown文本转换是使用Perl实现的，其语法吸收了众家之长，包括Setext，atx，Textile，reStructuredText，Grutatext，EtText以及最原始的邮件格式。[原生的Markdown语法](http://daringfireball.net/projects/markdown/syntax)简洁明了(使用特殊标点符号来标记格式)并且同时支持HTML标签。之后[不同编程语言实现的Markdown版本](http://www.wikiwand.com/zh/Markdown#.E5.AE.9E.E7.8E.B0.E7.89.88.E6.9C.AC)(Markdown解析器)也相继而生。不同的解析器对原生的Markdown语法进行了少许的扩展。其中较为流行的是用Ruby实现的版本[kramdown](http://kramdown.gettalong.org)。大名鼎鼎的GitHub就采用kramdown作为其Markdown的解析器([Starting May 1st 2016](https://github.com/blog/2100-github-pages-now-faster-and-simpler-with-jekyll-3-0))。这里我们从[原生的markdown语法](#original_markdown)介绍起，然后再来学习[kramdown](#kramdown_markdown)和[github-flavored-markdown](#GFM_markdown)对原生语法进行的一些拓展。花上十分钟读读本文，没准你会爱上Markdown。再花点时间练一练，让你的markdown使用起来得心应手，从此写起文章来一气呵成。


<a name="original_markdown" id="original_markdown"></a>

## 1. 原生态Markdown标记语法

### 1.1 标题

Markdown通过在行首添加1-6个`#`符号来定义不同级别的标题，最多到六级标题。注意`#`后需要加一个空格。

<u>书写格式如下：</u>

```
#<空格>一级标题
##<空格>二级标题
###<空格>三级标题
######<空格>六级标题
```

<u>解析效果如下：</u>  

# 一级标题
## 二级标题
### 三级标题
###### 六级标题

另外一级标题和二级标题也可以使用双下划线和单下划线来实现。

<u>书写格式如下：</u>

```
一级标题
======

二级标题
------
```

<u>解析效果如下：</u>  

一级标题
======

二级标题
------

### 1.2 加粗和斜体

markdown使用`*`和`_`来强调文本，使用一个`*`和`_`包围的文本会被转化为斜体，而用两个`*`和`_`包围的文本则会被转化成加粗。

<u>书写格式如下：</u>

```
*斜体文字*

_斜体文字_

**加粗文字**

__加粗文字__
```

<u>解析效果如下：</u> 

*斜体文字*

_斜体文字_

**加粗文字**

__加粗文字__


### 1.3 段落和换行

Markdown中一个普通的段落不需要在首行缩进，直接开始写就是一个段落。当你需要换到另外一个段落时，那么需要在上一段的段尾添加一个或多个空白行。

<u>书写格式如下：</u>

```
开始第一段。。。写完第一段。
<空行>
开始第二段。。。写完第二段。
```

<u>解析效果如下：</u> 

开始第一段。。。写完第一段。

开始第二段。。。写完第二段。

Markdown里回车后的文字默认是紧接上文的，如果你需要换行，那么需要在行尾添加两个以上的空格。

<u>书写格式如下：</u>

```
开始第一段。。。准备换行。<空格><空格>
另起一行。。。
```

<u>解析效果如下（注意换行和换段落的效果区别）：</u>

开始第一段。。。准备换行。  
另起一行。。。


### 1.4 列表

Markdown支持无序列表和有序列表。无序列表可以使用`*`，`+`，`-`三者中任意符号来标记；有序列表则使用数字加`.`来标记。注意标记后面需要加上一个空格，有序列表的数字会被按顺序自动更正。

<u>书写格式如下：</u>

```
*<空格>红红红红红
*<空格>绿绿绿绿绿
*<空格>蓝蓝蓝蓝蓝

+<空格>红红红红红
+<空格>绿绿绿绿绿
+<空格>蓝蓝蓝蓝蓝

-<空格>红红红红红
-<空格>绿绿绿绿绿
-<空格>蓝蓝蓝蓝蓝

1.<空格>红红红红红
2.<空格>绿绿绿绿绿
3.<空格>蓝蓝蓝蓝蓝

2.<空格>红红红红红
3.<空格>绿绿绿绿绿
1.<空格>蓝蓝蓝蓝蓝
```

<u>解析效果如下：</u>  

* 红红红红红
* 绿绿绿绿绿
* 蓝蓝蓝蓝蓝

+ 红红红红红
+ 绿绿绿绿绿
+ 蓝蓝蓝蓝蓝

- 红红红红红
- 绿绿绿绿绿
- 蓝蓝蓝蓝蓝

1. 红红红红红
2. 绿绿绿绿绿
3. 蓝蓝蓝蓝蓝

2. 红红红红红
3. 绿绿绿绿绿
1. 蓝蓝蓝蓝蓝

注意，如果列表中的一项有多个段落，新的段落需要缩进4个空格或1个tab。

<u>书写格式如下：</u>

```
* 项目一，段落一
<空行>
<空格><空格><空格><空格>项目一，段落二  
    
* 项目二，段落一
<空行>
<空格><空格><空格><空格>项目二，段落二
```

<u>解析效果如下：</u>  

* 项目一，段落一

    项目一，段落二
    
* 项目二，段落一

    项目二，段落二
    

### 1.5 引用

在段落前添加一个`>`符号即可将该段落标记为引用，注意`>`后需要添加一个空格。

<u>书写格式如下：</u>

```
><空格>某某大牛曾经说。。。<空格><空格>
某某大牛又说。。。
```

<u>解析效果如下：</u>  

> 某某大牛曾经说。。。  
某某大牛又说。。。


繁琐一点，你也可以在引用段落的每一行都加上`>`符号。并且`>`可以迭代使用，表示引用中的引用效果。

<u>书写格式如下：</u>

```
> 某A大牛曾经说。。。
>
> > 某B大牛曾经说。。。
>
> 某A大牛接着说。。。
```

<u>解析效果如下：</u>  

> 某A大牛曾经说。。。
>
> > 某B大牛曾经说。。。
>
> 某A大牛接着说。。。

### 1.6 分割线

直接上例子吧，如下几种方式都可以画出漂亮的分割线。

<u>书写格式如下：</u>

```
* * *

***

*****

- - -

---------------------------------------
```
   
<u>解析效果如下：</u>   
 
* * *

***

*****

- - -

---------------------------------------   


### 1.7 插入链接

markdown文本中插入链接非常方便，有文内链接和引用链接两种方式。注意如果链接的是本地资源，则链接地址为当地资源的路径。

<u>书写格式如下：</u>

```
## 文内链接
这是一个文内链接的[例子](http://example.com/ "鼠标悬浮此处显示的标题")。

[这个](http://example.net/)链接在鼠标悬浮时没有标题。

[这个](/about/)链接是本地资源。

## 引用链接

这是一个引用链接的[例子][id]。

[id]: http://example.com/  "鼠标悬浮标题（可选）"

## 注意，这里的id没有大小写区分，如果省略id，则前面方括号的内容会被用作id。

我常用的网站包括[Google][1]，[Yahoo][2]和[MSN][3]。

[1]: http://google.com/        "Google"
[2]: http://search.yahoo.com/  "Yahoo Search"
[3]: http://search.msn.com/    "MSN Search"
  
## 也可以写成

我常用的网站包括[Google][]，[Yahoo][]和[MSN][]。

[google]: http://google.com/        "Google"
[yahoo]:  http://search.yahoo.com/  "Yahoo Search"
[msn]:    http://search.msn.com/    "MSN Search"

```

<u>解析效果如下：</u>   

这是一个文内链接的[例子](http://example.com/ "鼠标悬浮此处现实的标题")。

[这个](http://example.net/) 链接在鼠标悬浮时没有标题。

这是一个引用链接的[例子][id]。

[id]: http://example.com/  "鼠标悬浮标题（可选）"

我常用的网站包括[Google][1]，[Yahoo][2]和[MSN][3]。

[1]: http://google.com/        "Google"
[2]: http://search.yahoo.com/  "Yahoo Search"
[3]: http://search.msn.com/    "MSN Search"

我常用的网站包括[Google][]，[Yahoo][]和[MSN][]。

[google]: http://google.com/        "Google"
[yahoo]:  http://search.yahoo.com/  "Yahoo Search"
[msn]:    http://search.msn.com/    "MSN Search"


### 1.8 插入图片

插入图片和插入链接非常类似，只是在方括号前多一个`!`。

<u>书写格式如下：</u>

```
## 方法一

![markdown logo](/images/markdown_grammar/Markdown_mark_log.png "markdown 图标1")

## 方法二

![markdown logo][id]

[id]: /images/markdown_grammar/Markdown_mark_log.png  "markdown 图标2"
```

<u>解析效果如下：</u>  

![markdown logo](/images/markdown_grammar/Markdown_mark_log.png "markdown 图标1")

![markdown logo][id]

[id]: /images/markdown_grammar/Markdown_mark_log.png  "markdown 图标2"


### 1.9 插入代码

在文本中嵌入代码也非常简洁，只需要用反引号`` ` ``将代码包围起来即可。

<u>书写格式如下：</u>

```

可以使用函数`print()`打印输出。

## 如果代码中需要加入反引号`号，则使用两个``加空格来包裹

这里就是一个反引号`` ` ``。

在代码里也可以保留反引号`` `print()` ``。

```

<u>解析效果如下：</u>   

可以使用函数`print()`打印输出。

这里就是一个反引号`` ` ``。

在代码里也可以保留反引号`` `print()` ``。


markdown中插入一整段代码快也非常方便，只需要将代码块的每一行缩进4个空格或一个tab。

<u>书写格式如下：</u>

```
代码如下:

<空格><空格><空格><空格>cat("hello world")
<空格><空格><空格><空格>cat("welcome to learn markdown")
```

<u>解析效果如下：</u>  

代码如下:

    cat("hello world")
    cat("welcome to learn markdown")
    

### 1.10 其他

在markdown中将链接地址或邮箱地址用`<>`包围，则会被自动转换成可点击的链接。

<u>书写格式如下：</u>

```
<http://haoeric.com>

<haoeric0520@gmail.com>
```

<u>解析效果如下：</u>   

<http://haoeric.com>

<haoeric0520@gmail.com>

如果需要避免文本中的符号被当做markdown标识符而发生不必要的格式转化，可以在符号前加`\`来避免。

<u>书写格式如下：</u>

```
\*不是斜体\*
```

<u>解析效果如下：</u>   

\*不是斜体\*

markdown使用的特殊标识符总结如下：

```
\   backslash
`   backtick
*   asterisk
_   underscore
{}  curly braces
[]  square brackets
()  parentheses
#   hash mark
+   plus sign
-   minus sign (hyphen)
.   dot
!   exclamation mark
```

<a name="kramdown_markdown" id="kramdown_markdown"></a>

## 2 kramdown拓展

kramdown对原生的markdown加入了一些拓展，其中最重要的就是对表格的支持，其他主要的还包括定义，缩写和角标。


### 2.1 表格

表格的书写格式一目了然，还是很方便简洁的。

<u>书写格式如下：</u>

```
| 左对齐 | 中间对齐 | 右对齐 |
| :---   |  :---:   |   ---: |
| 左1    |  中1     |  右1   |
| 左2    |  中2     |  右3   |
```

<u>解析效果如下：</u>  

| 左对齐 | 中间对齐 | 右对齐 |
| :---   |  :---:   |   ---: |
| 左1    |  中1     |  右1   |
| 左2    |  中2     |  右3   |

### 2.2 定义

对专有词汇进行定义。

<u>书写格式如下：</u>

```
专有词汇1
: 解释1
: 解释2

专有词汇1
: 解释
```
 
<u>解析效果如下：</u>  

专有词汇1
: 解释1
: 解释2

专有词汇2
: 解释


### 2.3 角标

不同于链接，这里的角标内容会被放在文末，点击可以实现跳转。

<u>书写格式如下：</u>

```
请参阅脚注1. [^1]

[^1]: 脚注1内容。

请参阅脚注2. [^2]

[^2]: 脚注2内容。
```

<u>解析效果如下：</u> 

请参阅脚注1. [^1]

[^1]: 脚注1内容。

请参阅脚注2. [^2]

[^2]: 脚注2内容。


### 2.4 缩写

可以全局定义缩写，当鼠标悬浮缩写词时会显示缩写的全称。

<u>书写格式如下：</u>

```
下面我们一起来学习GFM。

*[GFM]: GitHub Flavored Markdown
```

<u>解析效果如下：</u> 

下面我们一起来学习GFM。

*[GFM]: GitHub Flavored Markdown
*[HTML]: HyperText Markup Language

<a name="GFM_markdown" id="GFM_markdown"></a>

## 3. GitHub Flavored Markdown拓展

GFM取消了下划线作为强调字体的标识符，这样方便在文中自由使用`_`。同时，GFM会对文本中的链接进行自动识别，不需要使用`<>`来标记。另外GFM的几个重要拓展列举如下：


### 3.1 栅栏标记代码快

在GFM中，用户可以使用\`\`\`包围代码来标记代码块。其实这也是kramdown的一个拓展，放在这里讲，避免重复。

<u>书写格式如下：</u>

\`\`\`   
function test() {   
  console.log("notice the blank line before this function?");   
}    
\`\`\`

<u>解析效果如下：</u> 

```
function test() {
  console.log("notice the blank line before this function?");
}
```


### 3.2 代码高亮

使用栅栏标记代码块的一个好处是可以标明代码的语种，然后实现代码的高亮。

<u>书写格式如下：</u>

\`\`\`ruby    
require 'redcarpet'   
markdown = Redcarpet.new("Hello World!")   
puts markdown.to_html    
\`\`\` 

<u>解析效果如下：</u> 

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```


### 3.3 删除线

<u>书写格式如下：</u>

```
~~删除内容~~
```

<u>解析效果如下：</u> 

~~删除内容~~


有关GFM的其他拓展，请查阅[github-flavored-markdown](https://help.github.com/enterprise/11.10.340/user/articles/github-flavored-markdown/)。


## 4. HTML拓展

以上的语法基本可以满足我们大部分写作的需求。如果你还需要其他格式，那么不要忘了markdown本身是支持HTML标签的，这也就说明了markdown的强拓展性。以下列举一些常用的HTML标签用法：


### 4.1 下划线

<u>书写格式如下：</u>

```
<u>下划内容</u>
```

<u>解析效果如下：</u> 

<u>下划内容</u>

### 4.2 上标

<u>书写格式如下：</u>

```
E = mc<sup>2</sup>
```

<u>解析效果如下：</u> 

E = mc<sup>2</sup>


### 4.3 下标

<u>书写格式如下：</u>

```
Water: H<sub>2</sub>O
```

<u>解析效果如下：</u> 

Water: H<sub>2</sub>O


### 4.4 首行缩进  

markdown的段落默认都是顶格写，如果硬要缩进可以通过如下方式实现。

<u>书写格式如下：</u>

```
## 缩进一个空格
&ensp;开始输入

## 缩进两个空格
&emsp;开始输入
```

<u>解析效果如下：</u> 

&ensp;开始输入

&emsp;开始输入


### 4.5 内部跳转

使用如下HTML标签，可以实现在文本内的跳转。在长篇的文章中这个功能非常有用。

<u>书写格式如下：</u>

```
## 设置跳转标签
点此[标签](#锚点)跳转。

## 点击以上标签则跳转至有如下代码的所在行
## 我将下行代码放在了行文的"参考资料"行上面，点击试一下
<a name="锚点" id="锚点"></a>
```

<u>解析效果如下：</u> 

点此[标签](#锚点)跳转


### 4.6 改变插入图片大小

markdown自身插入图片时不会改变图片大小，但是通过THML插入图片可以修改图片大小。

<u>书写格式如下：</u>

```
<img src="/images/markdown_grammar/Markdown_mark_log.png" width="400" height="400" alt="markdown logo"/>
```

<u>解析效果如下：</u> 

<img src="/images/markdown_grammar/Markdown_mark_log.png" width="400" height="300" alt="markdown logo"/>

### 4.7 插入视频

视频不能直接加载，但可以使用照片加链接的形式来模拟，比如：

<u>书写格式如下：</u>

```html
<a href="http://www.youtube.com/watch?feature=player_embedded&v=YOUTUBE_VIDEO_ID_HERE
" target="_blank"><img src="http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>
```

<u>解析效果如下：</u> 

<a href="http://www.youtube.com/watch?feature=player_embedded&v=FyfwLX4HAxM
" target="_blank"><img src="http://img.youtube.com/vi/FyfwLX4HAxM/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>

或者用存markdown,但是不能调整图片大小：

<u>书写格式如下：</u>

```
[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](http://www.youtube.com/watch?v=YOUTUBE_VIDEO_ID_HERE)
```

<u>解析效果如下：</u> 

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/FyfwLX4HAxM/0.jpg)](http://www.youtube.com/watch?v=FyfwLX4HAxM)


<a name="锚点" id="锚点"></a>

### 4. 参考资料

[1] [markdown](http://daringfireball.net/projects/markdown/syntax)    
[2] [kramdown](http://kramdown.gettalong.org/syntax.html)    
[2] [github markdown](http://github.github.com/github-flavored-markdown/)    
[4] [MarkDown使用小技巧](http://www.jianshu.com/p/9d94660a96f1)     
[5] [用Markdown写blog的常用操作](http://www.cnblogs.com/mo-wang/p/5117819.html)     
[6] [worldhello:轻量级标记语言](http://www.worldhello.net/gotgithub/appendix/markups.html)     
[7] [THE WORLD'S LARGEST WEB DEVELOPER SITE](http://www.w3schools.com/default.asp)       

