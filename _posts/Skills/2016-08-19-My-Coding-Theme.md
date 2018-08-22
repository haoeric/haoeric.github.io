---
layout: post
title: 给自己一个赏心悦目的命令行终端
comments: true
categories: [Skills]
tags: [commander, shell, theme]
---

> 持续地关注大牛，时间久了就会不断地有意外惊喜（serendipity）发生。大牛们散发出来的光辉，和他们所思考的世界会不断的激励我们去探索，并且引导我们绕开许多坑。所以，我想说，**持续地关注大牛是一个优秀的习惯**，数量不要多，一边关注一边思考，持续地学习...最后不一定成为大牛，但是肯定会变优秀，伴随的成长总是令人开心。

2013年，脱离了学生的身份，开始工作的我犹豫是否要买一台MacBook。那时搜索了很多相关的内容，是偶然也是必然，我认识到[池建强](http://macshuo.com)老师，迟老师通过自己的[「MacTalk」](http://macshuo.com)品牌和[《MacTalk·人生元编程》](https://www.amazon.cn/dp/B00ID5UV30)一书被冠以大中华区苹果总代理。读了他几篇文章后，顿觉神清气爽，毫不犹豫甚至迫不及待地入手了现在的13' MacBook Pro。至今依然觉得那是一个无比正确的决定，因为我得到的不仅仅是一台优质的电脑，更是其持续激发的学习和工作的热情。每天当你打开MacBook，带来的是训疾如风的开机速度，视网膜级别的高清画面，清脆干净的键盘以及操控自如的触控板。如此浑然天成，没有一寸多余，整个人瞬感心旷神怡。心里不禁默吼一句perfect，感叹一声「Life is short, use Mac」, 然后自信满满地开始一天的任务和挑战。

迟老师是计算机领域当之无愧的大牛，大牛们的特质让它们彼此惺惺相惜，相互吸引。在关注迟老师的过程中，陆续地认识到其他几个大牛，比如罗永浩，[冯大辉](http://dbanotes.net)，霍矩，朱赟等，还有引起我写这篇文章的[李笑来](http://xiaolai.li/about/)。笑来老师的书[《把时间当朋友》](http://zhibimo.com/books/xiaolai/ba-shi-jian-dang-zuo-peng-you/)读来真是醍醐灌顶，相见恨晚。并且笑来老师是一个终身学习的实践者，不断地在不同的领域挑战着自己的学习能力，升级自己的大脑系统。最近，笑来老师发起了对全栈工程师的挑战，一篇一篇的学习笔记接踵而至。读了[『基本开发环境设置』](http://xiaolai.li/2016/06/16/makecs-basic-dev-env-settup/)一文后，我花了好几个小时开始折腾自己的开发环境，时间竟然大部分都花在了字体和配色上，不过想想也是挺有意义，天天用的东西，值得选一个赏心悦目的外表。

MacBook自带的命令行工具其实已经很不错了，只是这个世界上有那么一群默默的开发者，它们对美有一种极致的理解，对懒惰有着某种疯狂的追求，更重要的是他们还天赋异禀。在无数个寂寞的白天和黑夜中，为这个世界打造出各种神兵利器。是他们创造了比Terminal更优秀的[iTerm](https://www.iterm2.com/)，比Finder更好用的[TotalFinder](http://totalfinder.binaryage.com/)，比Spotlight更强大的[Alfred](https://www.alfredapp.com/)...。

好东西要用起来。相比好评如潮的zsh+[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)，我还是依然喜欢朴素的bash+[bash-it](https://github.com/Bash-it/bash-it)。装完bash-it，在`.bash_profile`里设置主题`export BASH_IT_THEME='nwinkler'`。换上[iTerm](https://www.iterm2.com/), 然后挨个装[Homebrew](http://brew.sh)，[Git](https://git-scm.com)，[rvm](https://rvm.io)。一气呵成，瞬间觉得一切美好，可是唯独这个字体和配色让我看着有点别扭。平常用R最多，[Rstudio](https://www.rstudio.com)是我的主力开发工具，并且我一直使用其自带的`Cobalt`主题，字体我选`Monaco`。如下：

![](/images/codingTheme/Rstudio_theme.png)

笑来老师推荐的`Courier New`字体看起来纤细明了，可是我还是喜欢用了很久的`Monaco`(这单词是我一意大利同事的姓，也是世界倒数第二小的国家摩纳哥的英文名，印象深刻)，所以我把iTerm改成了与Rstudio一样的主题，如下：

ASCII编码和non-ASCII编码我都使用相同的`Monaco`字体，这个字体中英文看起来都很舒适。

![](/images/codingTheme/iterm_font.png)  

颜色使用Mac自带的取色器（或者[sip](http://sipapp.io)），在Rstudio中获取对应的颜色，非常方便。
![](/images/codingTheme/iterm_color.png)   

配置完之后保存profile, 然后重启iTerm。一切都好了，全身舒畅，终于可以踏实地工作了...

![](/images/codingTheme/iterm_screenshot.png)  





