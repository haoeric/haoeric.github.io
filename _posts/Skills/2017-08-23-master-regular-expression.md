---
layout: post
title: 学习《正则表达式》笔记
comments: true
author: Chen Hao
categories: [Skills]
tags: [regular expression, 正则表达式]
---

### 1. Chearsheet

![](/images/regular_expression/regular_expression_cheatsheet.png)



### 2. Notes

* metacharacter 元字符，特殊含义，保留字符。`.^$*+?|(){}[]\-`这15个元字符在正则表达式中有特殊含义，用来编写匹配模式。（连字符在字符组的方括号中用来表示范围。但在其他情况下，则无特殊含义。）   
* 点号可以匹配除行结束符之外的所有字符。dotall选项表示点号除了匹配其他字符之外，还会匹配换行符。   
* `[]` character class, character set    
* `\d` character shorthand, character escape. 
* `()` capturing group    
* `\1` backreference 和capturing group配合使用。还有一种分组是非捕获分组（Non-Capturing Group）。非捕获分组不会将其内容存储在内存中。在你并不想引用分组的时候，可以使用它。由于不存储内容，非捕获分组就会带来较高的性能。比如`(the|The|THE)`，当你不需要任何后向引用，因此可以这样写一个非捕获分组：`(?:the|The|THE)`    
* `{3}` quantifier。
* `^`和`$`，分别表示匹配“行起始”和“行结束”位置，`^`不在最前面时可以表示“取反”。    
* `\w`匹配“单词字符”，包括匹配字母、数字和下划线，等价于`[_a-zA-Z0-9]`   
* `\s`匹配空格，制表符（`\t`），换行符（`\n`），回车符（`\r`）。等同于`[ \t\n\r]`   
* 断言也被称做零宽度断言（zero-width assertion）。零宽度断言不匹配字符，而是匹配字符串中的位置。其中的一些，比如`^`和`$`，也叫做锚位符（anchor）。`\b`匹配单词边界，也是个零宽度断言，表面上它会匹配空格或者是行起始，而实际上它匹配的是个零宽度的不存在的东西。`\B`则匹配非单词边界，匹配除单词边界之外的位置，比如单词或者字符串中的字母或数字。(指定单词边界的另一种方法是使用：`\<`来指定单词的开头，而使用`\>`来指定单词结尾。这是比较旧的语法，在很多最新的正则表达式应用程序中无法使用。但在有些情况下，这种语法就很有用，因为它不会像`\b`那样匹配任意单词边界，而是允许你分别匹配单词的开头或结尾。) 在Perl和PCRE中使用，`\A`匹配主题词的起始，`\Z`匹配主题词的结尾。    
* `(?i)`让你的模式不再区分大小写。
* 假设要匹配单词ancyent，且要求紧随其后的单词是marinere。要达到这个目的，我们可以使用正前瞻：`(?i)ancyent (?=marinere)`。匹配某个模式时，需要在它后面找不到含有给定前瞻模式的内容。反前瞻的形式是：`(?i)ancyent (?!marinere)`。正后顾会查看左边的内容，这与正前瞻方向相反。其语法是：`(?i)(?<=ancyent) marinere`。反后顾会查看某个模式在从左至右的文本流的后面没有出现。同样，它有一个小于号（<）：`(?i)(?<!ancyent) marinere`      
* 电话号码的正则表达式`：^\(?(?:\d{3})\)?[-.]?(?:\d{3})[-.]?(?:\d{4})$`。匹配电子邮件地址的正则表达式：`^([\w-.!#$%&'*+-/=?^_`{|}~]+)@((?:\w+\.)+)(?:[a-zA-Z]{2,4})$`    
* sed中的插入命令（`i`）允许你在文件或字符串中的某个位置之前插入文本。而与`i`命令相反的是命令`a`，它在某个位置之后添加文本。
* `grep -Ec "(the|The|THE)" rime.txt`  `-E`选项表示使用扩展的正则表达式（ERE），而不用基本正则表达式（BRE）。本例省去了将括号和竖线符转义的步骤，如果使用BRE则必须进行转义，像这样`\(THE\|The\|the\)`。`-c`选项返回匹配的行数（不是匹配的单词）。`grep -Eo "(the|The|THE)" rime.txt | wc -l`，命令中`-o`选项将单词的每一次出现都作为一行内容返回。`wc -l`即返回单词the的匹配个数。


- `(?d)`	Unix中的行	Java   
- `(?i)`	不区分大小写	PCRE、Perl、Java   
- `(?J)`	允许重复的名字	PCRE  
- `(?m)`	多行	PCRE、Perl、Java   
- `(?s)`	单行（dotall）	PCRE、Perl、Java   
- `(?u)`	Unicode	Java  
- `(?U)`	默认最短匹配	PCRE   
- `(?x)`	忽略空格和注释	PCRE、Perl、Java   
- `(?-…)`	复原或关闭选项   


### 3. Practices


- [RegexOne](https://regexone.com)   
- [regexr](http://regexr.com)   
- [sketchengine](https://regex.sketchengine.co.uk)  




