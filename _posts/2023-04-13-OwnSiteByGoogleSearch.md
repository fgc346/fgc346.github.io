---
layout: post
title: 谷歌搜索到自己在github的个人博客
date: 2023-04-13
author: ego
tags: [C++]
categories: [博客]
toc: true
pinned: false
---



缘起：

发现通过自己的博客名字，不能在搜索引擎找到自己的博客。

## 1 验证网站是否被Google收录

![image-20230414094959511](https://raw.githubusercontent.com/fgc346/image/main/img/image-20230414094959511.png)

## 2 搜索资源提交

进入Google Web Master，点击： [Google Search Console](https://search.google.com/search-console?hl=zh-CN&utm_source=wmx&utm_medium=deprecation-pane&utm_content=home&resource_id=https://saowu.github.io/)（若未登录谷歌账号，需要先登录谷歌账号）

## 3 添加站点地图

站点地图(Site Map)是用来注明网站结构的文件，我们希望搜索引擎的爬虫了解我们的网站结构,以便于高效爬取内容，快速建立索引。

点击进入 [XML-Sitemaps.com](https://www.xml-sitemaps.com/) 页面，输入博客地址，点击 start。

![image-20230414103837207](https://raw.githubusercontent.com/fgc346/image/main/img/image-20230414103837207.png)



## 参考

1 [Github Pages + Jekyll搭建博客之SEO](http://zyzhang.github.io/blog/2012/09/03/blog-with-github-pages-and-jekyll-seo/)

2 [让Google搜索到GitHub Pages](https://saowu.top/blog/4tCVcic30/)

