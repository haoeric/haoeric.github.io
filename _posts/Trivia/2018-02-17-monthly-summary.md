---
layout: post
title: 2018年2月-Kondratieff Waves, Web 3.0, 套路和铺垫
comments: true
categories: [Trivia]
tags: [Kondratieff Waves, Web 3.0, AWS, 套路, 铺垫]
---


## Kondratieff Waves

https://mp.weixin.qq.com/s/2VaKacBKYqKAhSBzIehS3g


Book Principle

predicting the future is useless, but what and how guidance for daily activity matters. 



## cryptocurrency and Money

https://www.reddit.com/r/CryptoCurrency/comments/7vga1y/i_will_tell_you_exactly_what_is_going_on_here/?st=JDBJOLK7&sh=84ad7c07


https://www.monetary.org/wp-content/uploads/2016/03/money-creation-in-the-modern-economy.pdf


## Web 3.0

https://medium.com/@matteozago/why-the-web-3-0-matters-and-you-should-know-about-it-a5851d63c949?source=linkShare-15f8f2cf5fe-1518593825

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

### DNS records

说到DNS record，就需要了解下集中常见的记录类型：

understand common DNS records, like SOA, NS, A, AAAA, CNAME and MX records

good website for checking DNS [whois](https://who.is)


create subdomain 
https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-do-i-create-a-subdomain-for-my-domain


### Certificate Signing Request (CSR code) 

[What is CSR](https://helpdesk.ssls.com/hc/en-us/articles/203226631-What-is-CSR-)? CSR code contains:

* organization - who applies for an SSL certificate
* domain - what needs to be secured
* public key - CSR code with the public key are generated out of the RSA private key

Public and private keys are related in such a way that only a public key can be used to encrypt messages, and only the corresponding private key can be used to decrypt them. Therefore, after the RSA key and CSR code are generated, you can use the CSR code for the certificate activation through your account with us. In the meanwhile, the private key should remain secret and be stored on the server, it will be needed for the certificate installation on the server and will be used to decrypt the information encrypted with the public key.

[CSR generation instructions](https://helpdesk.ssls.com/hc/en-us/sections/201192032-CSR-generation-instructions)

https://blog.cloudflare.com/announcing-keyless-ssl-all-the-benefits-of-cloudflare-without-having-to-turn-over-your-private-ssl-keys/

https://blog.cloudflare.com/keyless-ssl-the-nitty-gritty-technical-details/


## AWS 

Netflix

https://medium.com/refraction-tech-everything/how-netflix-works-the-hugely-simplified-complex-stuff-that-happens-every-time-you-hit-play-3a40c9be254b?source=linkShare-15f8f2cf5fe-1518925437


https://aws.amazon.com/blogs/startups/launch-your-app-with-the-aws-startup-kit/?sc_channel=sm&sc_campaign=Startups&sc_publisher=TWITTER&sc_country=Startups&sc_geo=GLOBAL&sc_outcome=awareness&trk=_TWITTER&sc_content=Blog_part2_startupKit&linkId=48053056


## 套路和铺垫
