---
layout: postDataAnalysis
title: "爬虫分析利器网，找到最热门的利器"
comments: true
categories: [Data Analysis]
tags: [liqi, data mining]
---

关注[利器](http://liqi.io)这个网站有些时间了，某天突然想把里面推荐的利器写个爬虫程序爬下来然后做个分析。找个周末，就把这个事给做了，然后有了这个MVP (minimum variable product)。爬虫用python强大的scrapy包完成，代码放在[github](https://github.com/haoeric/liqiSpider)。这里只是初步的分析，有很多地方需要改善，同时也有很多有意思的事情可以做，会在这里陆续更新。


{% highlight r %}
## loading data, file "liqi_data_tidy.csv" can be found in above github link
library(dplyr)
library(wordcloud)
library(ggplot2)

liqi_data <- read.csv(file="liqi_data_tidy.csv", header = TRUE, row.names = 1, stringsAsFactors = FALSE)
{% endhighlight %}

截至到2017年2月18号，爬虫出来总共180 位利器分享者，分享工具总计3450个。

## 1. 分享达人榜单


{% highlight r %}
fxdr <- liqi_data %>% 
    group_by(author) %>%
    summarise(toolCounts = n(), source = unique(source)) %>%
    arrange(desc(toolCounts)) 
{% endhighlight %}

#### 分享达人前二十名

> 排名标准：推荐的利器数量越多，排名越靠前


{% highlight r %}
kable(fxdr[1:20, ])
{% endhighlight %}



|author    | toolCounts|source                      |
|:---------|----------:|:---------------------------|
|刘斌      |        116|http://liqi.io/liubin/      |
|有才      |         81|http://liqi.io/youcai/      |
|柳东原    |         81|http://liqi.io/liudongyuan/ |
|李大锤    |         74|http://liqi.io/lidachui/    |
|Shrugged  |         73|http://liqi.io/shrugged/    |
|韩金乌    |         72|http://liqi.io/hanjinwu/    |
|w         |         66|http://liqi.io/w-wanqu/     |
|Allen     |         63|http://liqi.io/allen/       |
|曹舒旻    |         62|http://liqi.io/caoshumin/   |
|Chris Xia |         58|http://liqi.io/chris-xia/   |
|可可苏玛  |         58|http://liqi.io/cocosuma/    |
|Odding    |         57|http://liqi.io/odding/      |
|擎天      |         57|http://liqi.io/qingtian/    |
|月野耕    |         56|http://liqi.io/yueyegeng/   |
|濛子      |         55|http://liqi.io/mengzi/      |
|吴涛      |         54|http://liqi.io/wutao/       |
|零力      |         52|http://liqi.io/lingli/      |
|任宁      |         49|http://liqi.io/renning/     |
|大狗熊    |         49|http://liqi.io/bearbig/     |
|江宏      |         49|http://liqi.io/jianghong/   |

#### 分享达人云图


{% highlight r %}
par(family = "STHeiti")
wordcloud(fxdr$author, fxdr$toolCounts, random.order = FALSE, colors=brewer.pal(8, "Dark2"))
{% endhighlight %}

<img src="/figures/18-02-2017-liqi-data-mining/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" width="504" />


## 2. 利器排行


{% highlight r %}
lqph <- liqi_data %>% 
    group_by(tools) %>%
    summarise(toolCounts = n(), link = links[1], source = source[1]) %>%
    arrange(desc(toolCounts)) 
{% endhighlight %}

#### 利器推荐榜前20名

> 排名标准：被推荐的次数越多，排名越靠前

用柱状图来看看：


{% highlight r %}
ggplot(lqph[1:20, ], aes(x = factor(tools, levels = lqph$tools[1:20]), y = toolCounts)) + geom_bar(stat = "identity", fill="lightgreen") + theme_bw() + theme(axis.text.x = element_text(angle = 90, hjust = 1, face = "bold")) + geom_text(stat='identity',aes(label=toolCounts), vjust=-0.1) + xlab("") + ylab("sharetimes")
{% endhighlight %}

![plot of chunk unnamed-chunk-6](/figures/18-02-2017-liqi-data-mining/unnamed-chunk-6-1.svg)

详情：


{% highlight r %}
kable(lqph[1:20, ])
{% endhighlight %}



|tools       | toolCounts|link                                                            |source                       |
|:-----------|----------:|:---------------------------------------------------------------|:----------------------------|
|MacBook Pro |         51|http://www.apple.com/macbook-pro/                               |http://liqi.io/zhangmiao/    |
|Evernote    |         41|https://evernote.com/                                           |http://liqi.io/yueyegeng/    |
|iPhone 6    |         28|http://www.apple.com/shop/buy-iphone/iphone6                    |http://liqi.io/ivanzhao/     |
|Sketch      |         27|https://www.sketchapp.com/                                      |http://liqi.io/xingmei/      |
|Apple Watch |         24|http://www.apple.com/watch/                                     |http://liqi.io/zhangmiao/    |
|Dropbox     |         24|https://www.dropbox.com/                                        |http://liqi.io/liguoyu/      |
|Chrome      |         23|https://www.google.com/chrome/browser/desktop/index.html        |http://liqi.io/wutao/        |
|MacBook Air |         23|http://www.apple.com/cn/macbook-air/                            |http://liqi.io/liumengxi/    |
|Slack       |         23|https://slack.com/                                              |http://liqi.io/ivanzhao/     |
|Photoshop   |         22|http://www.adobe.com/cn/products/cs6/photoshop.html             |http://liqi.io/haoxiaohao/   |
|Trello      |         22|https://trello.com/                                             |http://liqi.io/yueyegeng/    |
|Kindle      |         21|https://www.amazon.cn/Kindle%E5%95%86%E5%BA%97/b?node=116087071 |http://liqi.io/yueyegeng/    |
|iPhone 6s   |         19|http://www.apple.com/shop/buy-iphone/iphone6s                   |http://liqi.io/zhangmiao/    |
|Ulysses     |         18|https://itunes.apple.com/cn/app/ulysses/id623795237?mt=12       |http://liqi.io/zhangmiao/    |
|1Password   |         17|https://1password.com/                                          |http://liqi.io/liguoyu/      |
|Alfred      |         17|https://www.alfredapp.com/                                      |http://liqi.io/liguoyu/      |
|iPhone      |         17|http://www.apple.com/iphone/                                    |http://liqi.io/xingmei/      |
|Keynote     |         17|http://www.apple.com/keynote/                                   |http://liqi.io/liguoyu/      |
|Xcode       |         17|https://developer.apple.com/xcode/cn/                           |http://liqi.io/ouluhai/      |
|iPad        |         16|http://www.apple.com/ipad/                                      |http://liqi.io/songshaopeng/ |


#### 利器云图

被推荐两次以上的利器总共有229个，放在云图里如下
    

{% highlight r %}
par(family = "STHeiti")
wordcloud(lqph$tools, lqph$toolCounts, min.freq=3, random.order = FALSE, colors=brewer.pal(8, "Dark2"))
{% endhighlight %}

<img src="/figures/18-02-2017-liqi-data-mining/unnamed-chunk-8-1.png" title="plot of chunk unnamed-chunk-8" alt="plot of chunk unnamed-chunk-8" width="504" />


#### 看看那些冷门的推荐利器

那些只被推荐一次的利器总共有2996个, 随机挑选20个来看看：


{% highlight r %}
set.seed(20)
lmlq <- lqph[lqph$toolCounts == 1, ]
lmlq_count <- nrow(lmlq)
kable(lmlq[sample(1:lmlq_count, 20), c(1,2,4)])
{% endhighlight %}



|tools                                                       | toolCounts|source                        |
|:-----------------------------------------------------------|----------:|:-----------------------------|
|樱木A4 透写台                                               |          1|http://liqi.io/shine/         |
|单行道                                                      |          1|http://liqi.io/miyu/          |
|GoPro Hero 4 Silver                                         |          1|http://liqi.io/bearbig/       |
|PowerBook G4 667                                            |          1|http://liqi.io/gongchen/      |
|论中国                                                      |          1|http://liqi.io/wangtao/       |
|钟颖                                                        |          1|http://liqi.io/zhongying/     |
|Aquamacs                                                    |          1|http://liqi.io/yedingding/    |
|AirPort Time Capsule                                        |          1|http://liqi.io/guling/        |
|Hue                                                         |          1|http://liqi.io/liuchengyin/   |
|JPEGmini                                                    |          1|http://liqi.io/tangshenggang/ |
|X500                                                        |          1|http://liqi.io/lvyesu/        |
|养猫                                                        |          1|http://liqi.io/sunqi/         |
|《Bakuman》                                                 |          1|http://liqi.io/lvmunan/       |
|三星 WD80J7260GX/SC 洗烘一体机                              |          1|http://liqi.io/guotingting/   |
|Dell UltraSharp U2414H 23.8 inch Widescreen IPS LCD Monitor |          1|http://liqi.io/maobojue/      |
|Moto X                                                      |          1|http://liqi.io/cuiqiwen/      |
|http://www.mobile-patterns.com/                             |          1|http://liqi.io/duanxianzhou/  |
|Ballpark                                                    |          1|http://liqi.io/duxiao/        |
|G胖                                                         |          1|http://liqi.io/haimaoluohewu/ |
|小米智能家居套装                                            |          1|http://liqi.io/cuiqiwen/      |


