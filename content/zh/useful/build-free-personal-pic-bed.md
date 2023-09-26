---
title: "搭建个人图床"
date: 2022-08-08T21:00:00+08:00
share: true
tags: ["免费","工具","工作流","github","cdn","图床"]
toc: true
tocNum: false
---

## 需求分析

- 使用场景

我们的文章（笔记、论文、博客等）中常需要添加图片。以使用常见的**Markdown**编辑器 **Typora** 记笔记的场景为例，如果我们直接将图片复制粘贴至其中，会得到如下的效果：

![](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-001-changed.jpeg)



可以看到代表着图片的链接是其在**本地的相对路径**，这导致了以下的缺点

- 文章难以迁移，若以博客等形式发布在网络上图片**无法正确加载**
- 若**仅**本地存储无法保证数据安全
- 图片资源存储在本地，由于**Git**特性，难以用其对存在大量图片的重要文章进行版本控制

使用图床，图片地址将如下，以存储在互联网上的**绝对路径**的形式存在

```url
https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-001-changed.jpeg
```

这样文章中只存储图片在服务器上的链接**文本** 内容迁移、版本管理变得容易

## 方案对比

构建图床有多种方案 这里分析两种常见方式的利弊以佐证我们技术选型的优越

| 方案                          | 优点                   | 缺点                                                           |
| ----------------------------- | ---------------------- | -------------------------------------------------------------- |
| 图床提供商 如七牛云\ SM.MS 等 | 操作简便、速度通常较快 | 付费、有倒闭风险、数据不自主、免费版速度容量受限、迁移困难 |
| 服务器自建图床            | 数据安全自主           | 操作相对繁琐 个人服务器成本                                                               |

## 技术选型

- 使用 **<a href="https://github.com/" target="_blank">GitHub</a>** 仓库作为免费图床（请合理利用资源，不要浪费）
- 使用 **<a href="https://www.jsdelivr.com/" target="_blank">jsDelivr</a>** 的免费CDN加速服务（保证对仓库资源的访问速度)
- 使用 **<a href="https://picgo.github.io/PicGo-Doc/zh/" target="_blank">PicGo</a>** 提供的自动上传服务简化操作

这一套方案的优势是：**完全免费**、速度快、操作简便、图片可同时存放在本地和云端 数据自主安全

## 具体实现

### 前置知识

1. **<a href="https://git-scm.com/" target="_blank">Git</a>** 和 **GitHub** 的基本使用

### 分步演示

1. 在GitHub上创建一个**public**仓库用作免费图床

    **注意** 必须是公开仓库 否则无法利用 **PicGo** 提供的自动上传服务

2. 生成`token`： 
    - 在 **GitHub** 个人账号页面：`Settings` --> `Developer settings` 
    - --> `Personal access tokens` --> `Generate new token` 
    - --> `Expiration`选`no expiration` --> `Select scopes` 勾选 `repo` 
    - --> `Generate token` --> 记下生成的`token`

>相关操作对应的github界面
![](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-002.png)


3. 下载 **<a href="https://picgo.github.io/PicGo-Doc/zh/" target="_blank">PicGo</a>** 打开 **图床设置** 页面：
    1. 打开GitHub图床页面 设为**默认图床**
    2. 设定仓库名 为`username/repo_name`(**替换为你自己的**GitHub用户名/你在步骤1创建的仓库名)
    3. 设定分支名为 `main`(或`master`)
    4. 设置token为上一步生成的token
    5. 指定存储路径 如`img/`
    6. 设定自定义域名 `https://cdn.jsdelivr.net/gh/username/repo_name`

>图床设置页面
![](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-003.png)


4. 启用自动上传服务

    在自己使用的编辑器中配置自动上传服务 如 **Typora** 在设置项 image --> Image Upload Setting中, 设置Image Uploader 为 **PicGo**, 此外强烈推荐使用<a href="https://obsidian.md/" target="_blank">Obsidian</a>编辑器，可配合插件使用以获得最佳体验，其他编辑器配置请自行<a href="https://google.com" target="_blank">搜索</a>
    
>obsidiain Image auto upload Plugin界面
![](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-004.png)


5. 完成 测试效果 尽情使用自己的图床吧～

>在Typora配置好了图床后再粘贴图片出现Upload Image选项，点击即可
![](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-005.png)


我们既能在自己的GitHub仓库中找到这些图片，

>被上传到GitHub仓库的图片（注意！<mark>直接加载GitHub中的图片需要科学上网</mark>，这也是我们选择自定义链接CDN的原因）
![](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-006.png)

还能通过命令`git pull`将它们拉取到本地存储，确保自己的数据安全。

>终端中输入命令拉取图片到本地
![](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-007.png)

>存储在本地的图片文件
![](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/blog-pic-bed-example-008.png)

下图是示例中上传到图床的图片:

![](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/Ophelia.JPG)

它在博客中的源代码是
```
![](https://cdn.jsdelivr.net/gh/AlexLiu2022/resources/img/Ophelia.JPG)
```
