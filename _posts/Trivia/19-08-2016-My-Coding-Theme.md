---
layout: post
title: 给自己一个赏心悦目的命令行工具
comments: true
categories: [Trivia]
tags: [github, blog, jekyll]
---

> 持续的关注某些大牛，时间久了就会不断的有意外惊喜（serendipity）发生。大牛们散发出来的光辉，和它们看到的世界会不断的激励我们去探索，并且绕开许多坑。所以，我要说，**持续的关注大牛是一个优秀的习惯**，数量不要多，一边关注一边思索，学习...最后不一定成为大牛，但是你肯定会更优秀，并且更开心。

2013年，脱离了学生的身份，开始工作的我犹豫是否要买一台MacBook。那时搜索了很多相关的内容，偶然也是必然，我认识到[池建强](http://macshuo.com)老师。读了他几篇文章后，顿觉神清气爽，毫不犹豫甚至迫不及待地买了MacBook Pro 13'。至今依然觉得那是一个无比正确的决定，因为我得到的不仅仅是一台电脑，更是其持续激发的学习和工作的热情。当每天打开MacBook，那训疾如风的开机速度，视网膜级别的高清画面，清脆干净的键盘，操纵自如的触控板，没有一寸多余，整个人瞬感心旷神怡，心里默吼一句perfect，感叹一声「Life is short, use MacBook」, 然后自信满满地开始一天的任务和挑战。

迟老师是当之无愧的计算机领域的大牛，大牛们的特质让它们彼此惺惺相惜，相互吸引。在关注迟老师的过程中，我陆续地认识到其他大牛，比如罗永浩，[冯大辉](http://dbanotes.net)，霍矩，朱赟，还有引起我写这篇文章的[李笑来](http://xiaolai.li/about/)。笑来老师的书[《把时间当朋友》](http://zhibimo.com/books/xiaolai/ba-shi-jian-dang-zuo-peng-you/)读来真是醍醐灌顶，爱不释手。并且笑来老师是一个终身学习的实践者，不断地在不同的领域李挑战自己的学习能力，升级自己的大脑。最近，笑来老师发出了对全栈工程师的挑战，一篇一篇的学习笔记接踵而至。读了[『基本开发环境设置』](http://xiaolai.li/2016/06/16/makecs-basic-dev-env-settup/)后，我花了好几个小时开始折腾自己的开发环境，时间竟然都要花在了字体和配色上，不过想想也是挺有意义，天天用的东西，值得选一个赏心悦目的外表。

MacBook自带的命令行工具其实已经很不错了，只是这个世界有一群默默的开发者，它们对美有一种极致的理解，对懒惰有着某种疯狂的追求，更重要的是还天赋异禀，在无数个寂寞的白天和黑夜中，为这个世界贡献了无数的神兵利器。是他们创造了比Terminal更优秀的[iTerm](https://www.iterm2.com/)，比Finder更好用的[TotalFinder](http://totalfinder.binaryage.com/)，比Spotlight更强大的[Alfred](https://www.alfredapp.com/)...。

对于好评一致的zsh+[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)，我还是依然使用基础的bash+[bash-it](https://github.com/Bash-it/bash-it)，在`.bash_profile`设置主题`export BASH_IT_THEME='nwinkler'`。换上[iTerm](https://www.iterm2.com/), 挨个装[Homebrew](http://brew.sh)，[Git](https://git-scm.com)，[rvm](https://rvm.io)。瞬觉一切美好，可是唯独这个字体和配色让我看着有点别扭。平常用R最多，[Rstudio](https://www.rstudio.com)是我的主力开发工具，并且我一直使用其自带的`Cobalt`主题，字体我选`Monaco`。如下：

![](/images/codingTheme/Rstudio_theme.png)

笑来老师推荐的`Courier New`字体看起来纤细明了，可是我还是喜欢用了很久的`Monaco`(这单词是我一意大利同事的姓，也是世界倒数第二小的国家摩纳哥的英文名，印象深刻)，所以我把iTerm改成了与Rstudio一样的主题，如下：

![](/images/codingTheme/iterm_font.png)   
![](/images/codingTheme/iterm_color.png)   

配置完之后重启iTerm，一切都好了，全身舒畅，然后开心地开始学习...

![](/images/codingTheme/iterm_screenshot.png)  





