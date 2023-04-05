---
layout: post
title: 使用github搭建个人的博客记录
date: 2023-04-05
author: ego
tags: [Blog, GitHub, Note]
comments: true
toc: false
pinned: false
---

一直以来就想搭建自己的博客网站，将自己平时的一些笔记系统化，整理为博客内容，形成自己的知识输出。

偶然看到一个博客讲述了自己利用github搭建博客的过程，有别人写好的模板可以直接用，而且我觉得他的博客形式蛮好的，我就按照他博客进行搭建。

<!-- more -->

## 搭建步骤

### 选择博客模板

对我来说，博客的外观页面只要看起来简单素雅，具有一定的美观性（作为一个工程师，对网站的要求就是文字美观，黑白搭配就蛮好了），重要的是博客本身的内容。因此，选择一个github上已经有的模板就可以了。

本博客使用[FromEndWorld/LOFFER](https://github.com/FromEndWorld/LOFFER)模板进行搭建，在此向原作者表示感谢，具体使用方式在下一节详细介绍。

1. [zxl19/zxl19.github.io](https://github.com/zxl19/zxl19.github.io)
2. [FromEndWorld/LOFFER](https://github.com/FromEndWorld/LOFFER)

博客模板涉及到两个知识点**Jekyll**和**Github Pages**，下面简单介绍一下两者的含义。

#### Jekyll

```
引用自官网：
Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过一个转换器（如 Markdown）和我们的 Liquid 渲染器转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的。
```

具体来讲，Jekyll就是将纯文本转化为静态博客网站。对于我们来说只需要写好markdown文本的博客，放置到相应的目录下就可以在github上显示自己的博客内容。

#### **Github Pages**

```
GitHub Pages 是一个静态网站托管服务，直接从github仓库托管你个人、公司或者项目页面 ，并且不需要你写任何后端语言来支持。
```

Github Pages的服务是免费的，但是也有一些限制：

- 仓库空间不大于**1G**
- 每个月的流量不超过**100G**
- 每小时更新不超过 10 次

### 搭建自己的博客内容

具体参考模板提供的教程，请[点击这里](https://fromendworld.github.io/LOFFER/document/)

#### 第一步：进入博客模板的仓库

选择使用这个模板，并创建自己的仓库

![img](https://cdn.nlark.com/yuque/0/2023/png/22895350/1680616419517-7bec8d6c-8a4a-4b61-81d1-1a2888507b60.png)

#### 第二步：填写自己仓库的信息

填写仓库名，创建仓库

![img](https://cdn.nlark.com/yuque/0/2023/png/22895350/1680616950475-9bf13d49-0a51-475b-b0b7-0e036315506b.png)

#### 第三步：进入仓库的settings进行相关设置



![img](https://cdn.nlark.com/yuque/0/2023/png/22895350/1680617680425-28caf54d-d55f-4cd6-aed5-c13f690ca919.png)

#### 第四步：设置站点信息

主要就是修改仓库中的_config.yml文件。

进入_config.yml之后，里面有具体的提示信息关于如何修改。

其实重要的几项，给自己的博客起名字，选择首页的图标。这些设置好以后，将修改提交到github的仓库。过一两分钟，刷新自己的首页，就可以看到更新的内容。

#### 第五步：发布博文

终于来到了核心的环节，发布博文。

**_posts**目录就是专门存放博客文件的，你可以使用**markdown**、**Textile**（这个没听过）或者**html**格式的文件来写博客，我是用**markdown**格式写的。但是不管是哪种格式的文件都需要包含 [YAML](https://link.jianshu.com?t=http%3A%2F%2Fyaml.org%2F) 头信息， Jekyll 才会把它当做一个特殊的文件来处理。

在**_posts**目录下新建一个**markdown**文件，头信息必须在文件的开始部分，并且需要按照 YAML 的格式写在两行三虚线之间。如下所示：

```
layout: post
title: 标题信息
date: 2023-04-05
author: 作者
tags: [Blog, GitHub, Note]
comments: true
toc: true
pinned: false

...
这里就可以使用markdown格式或其他格式写博客内容啦

```



| date | 这里的日期会覆盖文章名字中的日期。这样就可以用来保障文章排序的正确。日期的具体格式为`YYYY-MM-DD HH:MM:SS +/-TTTT`；时，分，秒和时区都是可选的。 |
| ---- | ------------------------------------------------------------ |
| tags | 类似分类 `categories`，一篇文章也可以给它增加一个或者多个标签。同样，`tags` 可以通过 YAML 列表或者以逗号隔开的字符串指定。 |

## 常见问题及解决方法

### 博客模板更新同步

由于博客仓库通过博客模板构建，在博客模板更新后无法通过Pull Request的方式进行同步。为实现对于博客模板更新的同步，可以保留`_posts`文件夹下的文件，将其他文件直接替换为更新后博客模板中的文件，在进行简单配置后即可完成同步更新。

## 参考

1. [如何在GitHub上写博客？-少数派的回答-知乎](https://www.zhihu.com/question/20962496/answer/677815713)
2. [Gitee码云pages+Jekyll主题搭建个人博客-bilibili](https://www.bilibili.com/video/BV1cJ411h7q3)
3. [各种开源协议介绍-菜鸟教程](https://www.runoob.com/w3cnote/open-source-license.html)
4. [Open Source Guides](https://opensource.guide)
5. [github/choosealicense.com](https://github.com/github/choosealicense.com)
6. [【最新】解决Github网页上图片显示失败的问题-CSDN博客](https://blog.csdn.net/qq_38232598/article/details/91346392)
7. [几条经验美化你的GitHub开源项目-简书](https://www.jianshu.com/p/d587b91bacb3)
8. [simple-icons/simple-icons](https://github.com/simple-icons/simple-icons)
9. [Maddoc42/Android-Material-Icon-Generator](https://github.com/Maddoc42/Android-Material-Icon-Generator)
10. [Online Tools-RedKetchup](https://redketchup.io)
11. [如何制作个人学术主页？-知乎](https://www.zhihu.com/question/281476526)