```
---
title: 免费域名+Github/Coding搭建静态网站
description: 这篇文章介绍如何通过免费域名搭建静态网站
tags:
  - 网站
categories: 
  - Web教程
  - 网站
keywords: 
  -	网站
  - 域名
  - Github
  - Coding
comments: false
cover: 'https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/github+coding-cover.png'
top_img: 'https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/github+coding-cover.png'
toc: true
toc_number: true
copyright: true
---
```

# 前置说明

{% note info %}

这篇文章主要是介绍如何白嫖免费域名并且与静态页面绑定，目的是为了之后忘记了还能看教程。。。

{% endnote %}

# 获取免费域名

{% note info %}

免费域名有很多、这里介绍一个比较满意的网站  [Freenom](https://www.freenom.com/) 这个网站提供了 `.tk` `.ml` `.ga`  `.cf` `.gf` 为后缀的免费域名。当然也有付费域名。我们这里白嫖免费域名

{% endnote %}



{% note info %}

注意：网站是外网、访问速度有点慢、建议使用 `Chrome浏览器开启谷歌访问助手`可以有更快的速度，至于为什么速度会这么快。我也不知道

{% endnote %}



1. 进入 [Freenom](https://www.freenom.com/) 官网、搜索一个免费域名、检查可用性

   `注意: 如果背景图片没有加载出来、就说明网络不好,多刷新几次`

   ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200528232412.png)

2. 输入 `xxxxx.后缀` 可以选中一个域名、如: zykjofficial.tk 

   ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200528232645.png)

3. `Period` 将日期修改为 `12 Months @ FREE ` 点击继续

   过了12月可以继续续费

4. 没有登录会提示登录账号或者注册账号、注册的步骤就跳过了、当初注册过程没有截图。。。

   ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529152627.png)

5. 注册成功后、登录用户、在底部Services处找到 `Register a New Domain` 重复2、3步骤

   为什么要这样、因为我在主页里找不到注册页面、只能通过这样的方法来注册。。。

   ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529153207.png)

   ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529153527.png)

   如果不成功、请重复上面的步骤、可能的原因：1.没有人机检查、2.注册账户的地址与当前访问IP的地址不一致，因此建议使用 `Chrome浏览器开启谷歌访问助手`解决

# 域名解析

我们使用第三方的来解析：我这里使用阿里云,当然也可以使用其他的、都类似。

1. 进入 [阿里云控制台](https://homenew.console.aliyun.com/) 找到 云解析 DNS

   ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529154724.png)

2. 点击 `添加域名`,将刚才购买的域名添加进去

3. 回到 Freenom，在底部Services处找到 `My Domains` 进入，通过 `Manage Domain` 配置解析服务器

4. 进入之后、点击`Management Tools`选择 `Nameservers` 

   ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529155609.png)

5.  将阿里云的 DNS 服务器 添加，保存

   ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529155807.png)

   等待 阿里云->云解析 DNS->DNS服务器状态 显示正常就可以了、如果不显示正常、请等待它显示正常、可能很快也可能很慢

6. 解析正常之后进入解析设置配置

   

# 博客配置

如果还没有搭建博客的话可以看 [Hexo搭建个人博客](https://zykjofficial.tk/posts/e55bad60/) 这篇文章

以Hexo博客为例：

1. 在`source` 下创建 `CNAME` 文件、不需要加后缀！！！

   内容写

   ```
   xxx.tk
   ```
    xxx为你的域名
   
2. `hexo g && d` 将本地文件推送到Github、Coding

3. 进入你推送在Github中的仓库 `xxx.github.io` 找到Settings Github Pages

   ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529161421.png)

   记住你的 https://xxx.github.io 网址

4. Coding 一样进入仓库 `持续部署`中找到`静态博客`

   ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529161916.png)

   记住那个网址

   

   ### 配置域名解析

   1. 回到阿里云 -> 云解析 DNS 添加记录

      这样添加
   
      ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529162218.png)
   
      因为Github的国外的、所以要将 xxx.github.解析到境外 Coding `默认` 可以加快访问速度
   
   2. Coding配置域名 点击设置
   
      ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529162505.png)
   
      这样添加域名就可以了
   
      ![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200529162553.png)
   
      如果有问题可以看看这篇博客 [加速自己的hexo，使用GitHub+Coding实现国内外网站加速](https://www.cnblogs.com/sunhang32/p/11969964.html)
   
   3. 直接访问你的域名就可以了

