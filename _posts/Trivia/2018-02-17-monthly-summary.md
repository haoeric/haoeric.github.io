---
layout: post
title: 2018年2月-Kondratieff Waves, Web 3.0, 套路和铺垫
comments: true
categories: [Trivia]
tags: [Kondratieff Waves, Web 3.0, AWS, 套路, 铺垫]
---


## Kondratieff Waves

苏联著名经济学家尼古拉·康德拉季耶夫在1952年出版了「大经济周期」一书，提出了著名的[康德拉季耶夫长波](http://www.wikiwand.com/zh/康德拉季耶夫长波)理论。该理论指出资本主义经济发展以50-60年为一个周期，自工业革命以后，世界经济已经历了五个周期(如下图）。

![](/images/2018_Feb/Kondratieff_wave_of_economy.png)

按照这一理论，我们现在处在第六个周期。2018年很有可能是经济大变革的一年，从今年[央行加息，美联储缩表](https://mp.weixin.qq.com/s/5F2xIzc7C4vXNQLTmJaDvQ)，到中美的贸易战争，这个变化正在发生。这几篇文章值得一读：

- [【全球股市大跌，财富大势骤然清晰！你再不懂就晚了！】](https://mp.weixin.qq.com/s/2VaKacBKYqKAhSBzIehS3g) by 周金涛      
- [【未来五年在中国最赚钱的不是股市、房地产，而是......】](https://mp.weixin.qq.com/s/bDyJ6CB26JeEBdtn88Pnuw) by 吴晓波  

Bridgewater创始人Ray Dalio关于经济周期有个很经典的解释动画，推荐一下[How The Economic Machine Works by Ray Dalio](https://www.youtube.com/watch?v=PHe0bXAIuk0&list=FLRCfyU9AfxhfgDmeUqPn-kg&t=0s&index=1)。

![](/images/2018_Feb/The_Economic_Cycle_RayDalio.png)

光知道历史的规律是没用的，关键有没有在变革之时做好了准备去抓住机会。正如最近在「Principle」一书中读到的：

> Predicting the future is useless, but what and how guidance for daily activity matters.   -- Ray Dalio

再来一篇鸡汤文，[【你哀叹错失的十年良机，其实从不属于你】](https://mp.weixin.qq.com/s/2glY_Oqin9pubJ0nYT7r_w)，好好努力吧！


## cryptocurrency and Money

所以行动才是力量，这不，上个月就砸了一笔钱到币圈，为了搭上区块链的末班车。可惜好景不长，这个月来了个大跳水，简直不忍直视，好了，提醒自己patience and discipline，多么难得的实战学习经验。有那闲工夫后悔没能晚点买，还不如好好学习学习，[I will tell you exactly what is going on here, this is critical information to understand if you are going to make money in this space. How prices work, and what moves them - and it's not money invested/withdrawn](https://www.reddit.com/r/CryptoCurrency/comments/7vga1y/i_will_tell_you_exactly_what_is_going_on_here/?st=JDBJOLK7&sh=84ad7c07)，这篇文章你值得好好读上十遍。

也顺便看看老板发来的[Money creation in the modern economy](https://www.monetary.org/wp-content/uploads/2016/03/money-creation-in-the-modern-economy.pdf)。


## Web 3.0

区块链不仅改变了金融业，也撬开了互联网的新时代，传说中的Web 3.0， 你准备好了吗？[Why the Web 3.0 Matters and you should know about it](https://medium.com/@matteozago/why-the-web-3-0-matters-and-you-should-know-about-it-a5851d63c949)

说到互联网，最近由于工作需要，补充了点网络小知识，做点小笔记总结下：

### SSL/TLS

为了保证服务器端和客户端信息交流的安全，就需要对传输的数据进行加密。SSL/TLS协议是为了解决这个通信加密而设计的。使用SSL/TLS的好处是：

1. 所有信息都是加密传播，第三方无法窃听。窃听风险（eavesdropping）
2. 具有校验机制，一旦被篡改，通信双方会立刻发现。篡改风险（tampering）
3. 配备身份证书，防止身份被冒充。冒充风险（pretending）

所以在网站上加上SSL/TLS加密协议是很有必要的，google最近就宣布新版Chrome68会给所有使用http的网站打上标签-“不安全”。

There are [three types of SSL certificates](https://www.symantec.com/connect/blogs/types-ssl-certificates-choose-right-one) that offer 3 levels of user trust for SSL/TLS negotiations: 

* Domain Validated certificates (DV)
* Organization Validated certificate (OV)
* Extended Validation certificates (EV).

Following this post [get free DV SSL certificate from Cloudflare](https://medium.freecodecamp.org/free-https-c051ca570324), I added SSL for my personal website. Actually it is quite easy, Firstly, I changed my website's nameserver from [DNSPod](https://www.dnspod.cn) to [Cloudflare](https://www.cloudflare.com) on my domain registrar [GoDaddy](https://sg.godaddy.com), then I updated my DNS records on Cloudflare.

![](/images/2018_Feb/haoeric_DNS_records.png)

原理方面，就得好好看看这两篇了：

- [All the Benefits of CloudFlare Without Having to Turn Over Your Private SSL Keys](https://blog.cloudflare.com/announcing-keyless-ssl-all-the-benefits-of-cloudflare-without-having-to-turn-over-your-private-ssl-keys/)    
- [Keyless SSL: The Nitty Gritty Technical Details](https://blog.cloudflare.com/keyless-ssl-the-nitty-gritty-technical-details/)  


### DNS Records

说到DNS record，就需要了解下集中常见的记录类型：

- A: 将域名指向一个IPv4地址    
- AAAA: 主机名（或域名）指向一个IPv6地址    
- CNAME: 一个域名指向另外一个域名，实现与被指向域名相同的访问效果     
- MX: 建立电子邮箱服务，将指向邮件服务器地址    
- TXT: 可任意填写，一般做一些验证记录时会使用此项    
- SOA: SOA记录用于在众多NS记录中那一台是主服务器    
- NS: 域名解析服务器记录   

比如，想创建一个subdomian就是简单的添加一个A record or CNAME record。[How do I create a subdomain for my domain](https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-do-i-create-a-subdomain-for-my-domain)

[whois](https://who.is)能够用来快速查看一个域名的DNS信息，更酷一点就看这里[DNS 原理入门](http://www.ruanyifeng.com/blog/2016/06/dns.html)。


### Certificate Signing Request (CSR code) 

如果需要给网站用上EV SSL（就是让你的网站在浏览器中显示为高贵的绿色的SSL），那么就免不了搞个CSR了。[What is CSR](https://helpdesk.ssls.com/hc/en-us/articles/203226631-What-is-CSR-)? 

CSR code contains:

* organization - who applies for an SSL certificate
* domain - what needs to be secured
* public key - CSR code with the public key are generated out of the RSA private key

Public and private keys are related in such a way that only a public key can be used to encrypt messages, and only the corresponding private key can be used to decrypt them. Therefore, after the RSA key and CSR code are generated, you can use the CSR code for the certificate activation through your account with us. In the meanwhile, the private key should remain secret and be stored on the server, it will be needed for the certificate installation on the server and will be used to decrypt the information encrypted with the public key. [CSR generation instructions](https://helpdesk.ssls.com/hc/en-us/sections/201192032-CSR-generation-instructions)

## AWS 

云服务基本上已是现实Startup公司的标配，在众多的云服务提供商中，AWS这个市场当之无愧的先驱和领头羊，也是在我体验中做的最强大，体验最好的云服务。除了创业公司，很多大企业也拥抱了AWS，其中甚至包括亚马逊primer video的竞争对手Netflix - [How Netflix works](https://medium.com/refraction-tech-everything/how-netflix-works-the-hugely-simplified-complex-stuff-that-happens-every-time-you-hit-play-3a40c9be254b?source=linkShare-15f8f2cf5fe-1518925437)。能做到这有点，可见AWS多牛X。所以买点亚马逊股票吧，这个让人惊叹不已的公司会给我们更多惊喜。如果对云计算的部署和技术感兴趣，可以follow AWS blog， 比如这篇[Launch your app with the AWS Startup Kit](
https://aws.amazon.com/blogs/startups/launch-your-app-with-the-aws-startup-kit/?sc_channel=sm&sc_campaign=Startups&sc_publisher=TWITTER&sc_country=Startups&sc_geo=GLOBAL&sc_outcome=awareness&trk=_TWITTER&sc_content=Blog_part2_startupKit&linkId=48053056)。目前除了在AWS上部署了几条production pipeline，也了做一些有意思的小玩具，比如这个Echo Skill - [Daily Digest in Chinese](https://www.amazon.com/dp/B078Q45FZX/ref=sr_1_1?s=digital-skills&ie=UTF8&qid=1514726935&sr=1-1&keywords=daily+digest)。


## 套路和铺垫

一切的看似微不足道的努力都是铺垫，一切痛定思痛后的领悟都能总结成改变行动的套路。加油吧，不用隐藏你是个有梦想有目标的人，对，我们做的就是铺垫，学习的就是套路。

