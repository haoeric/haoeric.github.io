---
layout: post
title: Markdown知道这些就够用了
comments: true
author: Chen Hao
categories: [Skills]
tags: [markdown, 标记语言]
---


Markdown是在Ruby应用中广泛使用的标记语言，语法简洁并可混用HTML(标准markup语言)。[标准的Markdown语法](http://daringfireball.net/projects/markdown/syntax)缺乏如表格等关键特性的支持，虽然不同的解析器都对其语法进行了扩展，但实现各有不同，造成一定的混乱。

GitHub使用[kramdown](http://kramdown.gettalong.org)作为Markdown的解析工具([Starting May 1st 2016](https://github.com/blog/2100-github-pages-now-faster-and-simpler-with-jekyll-3-0))，并添加了额外的语法扩展。以下归纳github-flavored-markdown的语法表以及一些HTML拓展，让你的markdown使用起来得心应手。



|类别|语法格式|示例|
|----|:------:|-----|
||**内容组**||
|加粗|`**加粗** or --加粗--`|**加粗**|
|斜体|`*斜体* or -斜体-`|*斜体*|
|删除线|`~~删除内容~~`|~~删除内容~~|
|下划线|`<u>下划内容</u>`|<u>下划内容</u>|
|上标|`<sub>上标内容</sub>`|Water: H<sub>2</sub>O|
|下标|`<sup>上标内容</sup>`|E = mc<sup>2</sup>|
|角注|`[^角注]`|[见下文](#1)|
|首行缩进|`&ensp;` 或 `&emsp;`|缩进一个，或两个空格|
|文字链接|`[链接标签](链接网址)`|[github](http://daringfireball.net/projects/markdown/syntax)|
|内部跳转|`<a name="tt" id="tt"></a> 跳转至 [文内链接](#tt)`|<a name="md-anchor" id="md-anchor"></a>跳转至 [文内链接](#md-anchor)|
|引用|`> 引用内容`|[见下文](#1)|
|插入图片|`![GitHub](/images/github.png "Logo")`|[见下文](#2)|
|使用emoji|`:EMOJICODE:`|[见下文](#3)|
|忽略md标记符|`标记符前加\`|[见下文](#4)|
|插入代码|`见下文`|[见下文](#5)|
|插入视频|`见下文`|[见下文](#12)|
||**格式组**||
|一级标题(最大)|`# 一级标题`|[见下文](#6)|
|二级标题|`## 二级标题`|[见下文](#6)|
|三级标题|`### 三级标题`|[见下文](#6)|
|四级标题|`#### 四级标题`|[见下文](#6)|
|五级标题|`##### 五级标题`|[见下文](#6)|
|六级标题(最小)|`###### 六级标题`|[见下文](#6)|
|分割线|`三条或更多短线（或星号、下划线）`|[见下文](#7)|
|分段|`第二段和第一段间有一空行`|略|
|换行|`行尾两空格换行`|略|
|续行|`一个回车不分段，本行续上行`|略|
|无序列表|`星号、减号、加号开始列表`|[见下文](#9)|
|有序列表|`数字和点开始有序列表`|[见下文](#9)|
|任务列表|`[] and [x]`|[见下文](#10)|
|表格|`见下文`|[见下文](#11)|



### 示例
<a name="引用" id="1"></a>

#### 1. 角注与引用  

<u>角注示例：</u>

```
Text prior to footnote reference 1.[^1]

[^1]: 1 Comment to include in footnote.

Text prior to footnote reference 2.[^2]

[^2]: 2 Comment to include in footnote.
```

Text prior to footnote reference 1.[^1]

[^1]: 1 Comment to include in footnote.

Text prior to footnote reference 2.[^2]

[^2]: 2 Comment to include in footnote.

<u>引用示例：</u>

在引用内容前加\>, 比如：

```
>Anything that can be automated, should be automated.    ------Hadley Wickham
```

>Anything that can be automated, should be automated.    ------Hadley Wickham


<a name="插入图片" id="2"></a>

#### 2. 插入图片  

比插入链接多了个`!`, 例如插入markdown logo:  

```
![markdown logo](/images/markdown_grammar/Markdown_mark_log.png)
```

![markdown logo](/images/markdown_grammar/Markdown_mark_log.png)


使用如下命令`<img src="图片地址" width="图片显示宽度" height="显示高度" alt="图片名称"/>`设置图片大小.

```
<img src="/images/markdown_grammar/Markdown_mark_log.png" width="400" height="400" alt="markdown logo"/>
```


<img src="/images/markdown_grammar/Markdown_mark_log.png" width="400" height="400" alt="markdown logo"/>



<a name="使用emoji" id="3"></a>


#### 3. 使用emoji

各种emoji的标识符见[相关资源](#xg), 举个例子：

`笑脸 :smile: 转尖叫 :scream:`

笑脸:smile:转尖叫:scream:


<a name="引用" id="4"></a>

#### 4. 忽略md标记符

在markdown标识符前加`\`就会忽略后面的markdown标记， 比如：`我想保留\*星号\*`  

我想保留\*星号\*


<a name="插入代码" id="5"></a>

#### 5. 插入代码

用单 \` 包住即嵌入代码：

计算`c <- a + b`

用三个连续 \` 包住即插入代码块：

```ruby
require 'redcarpet'  
markdown = Redcarpet.new("Hello World!")  
puts markdown.to_html  
```

<a name="加入视频" id="12"></a>

#### 6. 加入视频

视频不能直接加载，但可以使用照片加链接的形式来模拟，比如

```html
<a href="http://www.youtube.com/watch?feature=player_embedded&v=YOUTUBE_VIDEO_ID_HERE
" target="_blank"><img src="http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>
```

<a href="http://www.youtube.com/watch?feature=player_embedded&v=FyfwLX4HAxM
" target="_blank"><img src="http://img.youtube.com/vi/FyfwLX4HAxM/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>

或者用存markdown,但是不能调整图片大小：

`[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](http://www.youtube.com/watch?v=YOUTUBE_VIDEO_ID_HERE)`

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/FyfwLX4HAxM/0.jpg)](http://www.youtube.com/watch?v=FyfwLX4HAxM)


<a name="标题" id="6"></a>

#### 7. 标题

`# 一级标题`  

# 一级标题

`## 二级标题` 

## 二级标题

`### 三级标题`

### 三级标题

`#### 四级标题`

#### 四级标题

`##### 五级标题`

##### 五级标题

`###### 六级标题`

###### 六级标题



<a name="分割线" id="7"></a>

#### 8. 分割线

使用三条或更多短线（或星号、下划线）画下华丽丽的分割线：
`---`

---


<a name="列表" id="9"></a>

#### 9. 无序列表

可以使用`*`,`+` `-`， 比如：

```
* 星号、减号、加号开始列表。

  - 列表层级和缩进有关。

    + 和具体符号无关。

* 返回一级列表。
```

* 星号、减号、加号开始列表。

  - 列表层级和缩进有关。

    + 和具体符号无关。

* 返回一级列表。

#### 10. 有序列表

用数字加`.`， 比如：

```
1. 数字和点开始有序列表。

   1. 注意子列表的缩进位置。

      1. 三级列表。
      1. 编号会自动更正。

   1. 二级列表，编号自动更正为2。

2. 返回一级列表。
```

1. 数字和点开始有序列表。

   1. 注意子列表的缩进位置。

      1. 三级列表。
      1. 编号会自动更正。

   1. 二级列表，编号自动更正为2。

2. 返回一级列表。


#### 11. 列表续行、段落和代码块

```
1. 列表项可以折行，
   对齐则自动续行。

2. 列表项可包含多个段落。

    空行开始的新段落必须缩进四个空格，
    段落才属于列表项。

3. 列表中的代码块要缩进8个空格。

        $ printf "Hello, world.\n"
```

1. 列表项可以折行，
   对齐则自动续行。

2. 列表项可包含多个段落。

    空行开始的新段落必须缩进四个空格，
    段落才属于列表项。

3. 列表中的代码块要缩进8个空格。

        $ printf "Hello, world.\n"


<a name="任务列表" id="10"></a>


#### 12. 任务列表

```
- [x] 买西红柿
- [x] 买鸡蛋
- [x] 买葱花
- [ ] 做西红柿炒鸡蛋
```

- [x] 买西红柿
- [x] 买鸡蛋
- [x] 买葱花
- [ ] 做西红柿炒鸡蛋


<a name="表格" id="11"></a>

#### 13. 表格

```
| 左对齐 | 中间对齐 | 右对齐 |
| :---  |  :---:   |   ---: |
| 你好   | 你好     | 你好   |
| 你不好 | 你好     | 你好   |
```

| 左对齐 | 中间对齐 | 右对齐 |
| :---   |  :---: |  ---: |
| 你好   | 你好     | 你好   |
| 你不好 | 你不好     | 你不好   |


<a name="xg" id="xg"></a>

### 相关资源

* [github markdown](http://github.github.com/github-flavored-markdown/)
* [Emoji cheatsheet](http://www.emoji-cheat-sheet.com)
* learn HTML [THE WORLD'S LARGEST WEB DEVELOPER SITE](http://www.w3schools.com/default.asp)


### 参考 
[1] [worldhello:轻量级标记语言](http://www.worldhello.net/gotgithub/appendix/markups.html)  
[2] [gitbook markdown](http://github.github.com/github-flavored-markdown/)   
[3] [MarkDown使用小技巧](http://www.jianshu.com/p/9d94660a96f1)