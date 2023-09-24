---
title: "关于 RSS Feeds"
date: 2023-09-17T02:55:22+08:00
toc: true
tocNum: false
share: true
tags: ['news','阅读','工具','技术','rss','rsshub','工作流','互联网精神']
---



## 什么是RSS feeds？

RSS（英文全称：RDF Site Summary 或 Really Simple Syndication），中文译作简易信息聚合，也称聚合内容，是一种消息来源格式规范，用以聚合多个网站更新的内容并自动通知网站订阅者。使用 RSS 后，网站订阅者便无需再手动查看网站是否有新的内容，同时 RSS 可将多个网站更新的内容进行整合，以摘要的形式呈现，有助于订阅者快速获取重要信息，并选择性地点阅查看。——&nbsp;&nbsp;摘至中文维基百科

## RSS相较其它信息源的优势

### 反商业化

RSS能够过滤商业广告，并且摆脱各平台针对性的算法推荐内容，仅获取自愿订阅的内容。

#### 比较抽象的案例 * 1

微博是国内最大的社交媒体。但其上的某些内容，以及过分娱乐、低龄化的遣词造句，实在让人不想成为它的用户。

但有时候又不得不用。体量最大的娱乐信息集散地使很多需要传播的商业内容别无选择。 

但：喂！我只是想嗑我家甜甜的艾七诶 

![i7.jpg](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/i7.jpg)

而Weibo察觉到我关注了CP类的超话之后 居然开始给我推送蔡徐坤的CP了...... <span style="white-space: nowrap;">ಠ_ಠ</span>（听我说，谢谢你）

由于其反商业化的特质，RSS solves it.

### 聚合化

#### 工作用例 - 资讯

我们知道，想要获得一个事件相对客观的解读，往往需要比对多家媒体的报道，再自己判断。尤其是一些重要的政治经济事件，中外不同媒体可能完全是两个画风。

在此基础上，如果除关心国内新闻外，还想拥有一些国际视野的话，那么在联合早报中国/世界版，BBC中/英文版，国内资讯平台，新闻联播文稿，纽约时报，经济学人之间反复穿梭似乎会相当麻烦。

况且我们可能会想同时关注多个不同领域的媒体，比如区块链和传统金融。并不总有100%符合需求的Newsletter。

由于其聚合资讯的特质，RSS solves it.

![blog-rss-001.png](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-rss-001.png)


#### 私人用例 - 追星

<del>你家的CP今天发糖了么？</del>在各个平台发碎糖，不关注的话很容易就漏掉了。想要追踪她们的日常，及时收到关注的信息，却并不想要成为抖音、微博、小红书的日常用户，如何解决呢？

由于其聚合资讯的特质，RSS solves it.

### 高度定制化

通过对RSS源的配置（如通过自建RSSHub生成的源，后面会介绍），或者对在线服务/客户端的设置，可以做到自定义的关键词筛选，重要性排序，时间权重调整等等。

想要接收什么信息，怎样的信息，应该由我们自己来决定，而不是让推荐算法替我们决定。

由于其高度可定制化，RSS solves it.

## RSSHub

### RSSHub是什么？

<a href="https://docs.rsshub.app/zh/" target="_blank">RSSHub</a> 是一个开源、简单易用、易于扩展的 RSS 生成器，可以给任何奇奇怪怪的内容生成 RSS 订阅源。RSSHub 借助于开源社区的力量快速发展中，目前已适配数百家网站的上千项内容。

例如，你可以使用RSSHub为自己关注的微博用户、抖音用户、字幕组、GitHub仓库等等制作RSS订阅源。

![blog-rss-002.png](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-rss-002.png)


### 互联网精神

由于RSS具有的反商业化特质，越来越多的网站不再提供RSS源。

RSSHub是技术对商业化的回击， 消除传播壁垒 ，信息互联互通。

Everything is RSSible. 这符合我心中的互联网精神。


## 我的RSS工作流

### 网页端 or 客户端？

#### 网页端
要订阅各个网站的RSS Feed，需要使用相关的网页服务来获取feeds或使用客户端进行本地请求。

常见的RSS服务商（如<a href="https://feedly.com/" target="_blank">feedly</a>）的域名都已被大陆屏蔽。（<del>信息的自由传播是不被允许的！</del>）所以想要使用这种方式，需要自建服务，可以采取的方案有<a href="https://tt-rss.org/" target="_blank">Tiny Tiny RSS</a>等（支持高度定制化）

#### 客户端

通过自己的设备发送请求，更新feeds。我使用的是<a href="https://reederapp.com/" target="_blank">Reeder</a>（Mac & IOS）,支持iCloud多设备同步，简洁好用。

>Tip：在Reeder中将某些默认只有内容摘要的订阅源设置为默认在阅读模式打开，可以达到全文阅读的体验。

![blog-rss-003.png](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-rss-003.png)


### 自建RSSHub

公共的RSS源容易被墙，可能不提供全文阅读；而公共的RSShub使用人数过多，受到刷新时间过长等多种限制，且可靠性较低，可能会意外失效。

实测在vercel等免费托管服务上部署的RSSHub几乎不可用，很多路由都报`503 Timeout`。

故直接在自有的服务器上编译源码部署即可，最低配的服务器也OK。如果配置较高可以考虑用docker部署，更方便。

部署完成后配置一下nginx 反向代理，将域名（子域名）解析到主机即可。

没有强迫症也可以直接通过`http`协议用`ip+端口号`使用。

更多关于部署RSSHub的细节见<a href="https://docs.rsshub.app/zh/install" target="_blank">这里</a>

## 结语

### 从资讯获取谈信息输入

摆脱了商业平台的算法推荐，由自己定义要接收哪些资讯，我们究竟是摆脱了信息茧房，还是自建了一个更加封闭的信息茧房呢？

Anyway，想要变成自己认同的人，我们需要接受自己认同的信息。

![blog-rss-004.png](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-rss-004.png)

