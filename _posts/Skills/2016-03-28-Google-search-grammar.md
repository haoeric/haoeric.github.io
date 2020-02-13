---
layout: post
title: Practical Google Search Tips
comments: true
author: Chen Hao
categories: [Skills]
tags: [google, 语法]
---


### 1. Common-use Google Search Grammar

|符号|表达意思|解释|  
|:---:|:------|:---|
|双引号|完全匹配|内容和顺序完全匹配|  
|减号|不包含减号后面的词|减号前面必须是空格，减号后面没有空格，紧跟着需要排除的词|  
|星号|通配符|代表任何文字|  
|波浪号|近义词|搜索与关键词相关的词汇|
|`@`|查找社交网络帐户|示例：`@haoeric`|
|`$`|查找价格|示例：`macbook $1900`|
|`#`| 查找话题| 示例：`#throwbackthursday`|
|`..`| 两个点号（不加空格）隔开两个数字，即可搜索包含相应范围内数字的搜索结果|示例：`手机 $2000..$3000`|
|filetype|搜索特定文件格式|e.g. filetype:pdf 关键词|  
|inurl|搜索查询词出现在url中的页面|结果都是网址url中包含关键词的页面|   
|site|搜索某个域名下的所有文件|e.g. site:haoeric.com google|  


### 2. Example Study

![](/images/google_grammar/1.png)
![](/images/google_grammar/2.png)
![](/images/google_grammar/3.png)

### 3. Use Cases

- Search all the sub domains of a comany website, eg. amazon.com

```txt
site:amazon.com -inurl:www
```

- Search all the domains with amazon but not end with .com

```txt
site:amazon.* -site:amazon.com
```

- Search all PDF documents from amazon.com

```txt
site:amazon.com filetype:pdf
```

- Search news before certain date or year

```txt
wuhan virus before:2020-01-01
```

- Search news after certain date or year

```txt
wuhan virus wuhan after:2019
```

### References

- https://www.zhihu.com/question/20161362