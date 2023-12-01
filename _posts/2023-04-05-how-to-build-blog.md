---
layout: post
title: 使用github搭建个人的博客记录
date: 2023-04-05
author: ego
tags: [Blog, GitHub, Note]
categories: [C++]
toc: false
pinned: false
---

一直以来就想搭建自己的博客网站，将自己平时的一些笔记系统化，整理为博客内容，形成自己的知识输出。

偶然看到一个博客讲述了自己利用**github**搭建博客的过程，有别人写好的模板可以直接用，而且我觉得他的博客形式蛮好的，我就按照他博客进行搭建。

<!-- more -->

## 搭建步骤

### 选择博客模板

对我来说，博客的外观页面只要看起来简单素雅，具有一定的美观性（作为一个工程师，对网站的要求就是文字美观，黑白搭配就蛮好了），重要的是博客本身的内容。因此，选择一个github上已经有的模板就可以了。

本博客最开始使用[FromEndWorld/LOFFER](https://github.com/FromEndWorld/LOFFER)模板进行搭建，在此向原作者表示感谢，具体使用方式在下一节详细介绍。

1. [zxl19/zxl19.github.io](https://github.com/zxl19/zxl19.github.io), 受到启发的博客，该博客也是使用该模板搭建。

2. [FromEndWorld/LOFFER](https://github.com/FromEndWorld/LOFFER)， 使用的模板仓库。

这个博客最开始就是根据[zxl19的博客](https://github.com/zxl19/zxl19.github.io)创建的第一版个人博客。不过，这个模板我不太喜欢的一点就是网站的侧边栏是固定的，占据了很大的空间，后面通过在知乎查询，并且对比了很多模板，最后选定了[oukohou.github.io](https://github.com/oukohou/oukohou.github.io)使用的模板，并在此基础上进行了若干修改。

我去除了评论功能和一些个人不需要的配置。

还根据oukohou博主的一篇博客[使用我的jekyll博客主题的注意事项](https://www.oukohou.wang/2018/12/18/notices-for-jekyll-themes-fork/)，对自己的博客内容进行了修改。


博客模板涉及到两个知识点**Jekyll**和**Github Pages**，下面简单介绍一下两者的含义。

#### Jekyll

```text
引用自官网：
Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，
通过一个转换器（如 Markdown）和我们的 Liquid 渲染器转化成一个完整的可发布的静态网站，
你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，
你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的。
```

具体来讲，Jekyll就是将纯文本转化为静态博客网站。对于我们来说只需要写好markdown文本的博客，放置到相应的目录下就可以在github上显示自己的博客内容。

#### **Github Pages**

```
GitHub Pages 是一个静态网站托管服务，直接从github仓库托管你个人、公司或者项目页面 ，并且不需要你写任何后端语言来支持。
```

Github Pages的服务是免费的，但是也有一些限制：

- 仓库空间不大于**1G**
- 每个月的流量不超过**100G**
- 每小时更新不超过 **10** 次

### 搭建自己的博客内容

以下，皆为首次创建博客的步骤，具体参考模板提供的教程，请[点击这里](https://fromendworld.github.io/LOFFER/document/)

#### 第一步：进入博客模板的仓库

选择使用这个模板，并创建自己的仓库

![img](https://raw.githubusercontent.com/fgc346/image/main/img/1680616419517-7bec8d6c-8a4a-4b61-81d1-1a2888507b60.png)

#### 第二步：填写自己仓库的信息

填写仓库名，创建仓库

![img](https://raw.githubusercontent.com/fgc346/image/main/img/1680616950475-9bf13d49-0a51-475b-b0b7-0e036315506b.png)

#### 第三步：进入仓库的settings进行相关设置

![img](https://raw.githubusercontent.com/fgc346/image/main/img/1680617680425-28caf54d-d55f-4cd6-aed5-c13f690ca919.png)

#### 第四步：设置站点信息

主要就是修改仓库中的_config.yml文件。

进入_config.yml之后，里面有具体的提示信息关于如何修改。

其实重要的几项，给自己的博客起名字，选择首页的图标。这些设置好以后，将修改提交到github的仓库。过一两分钟，刷新自己的首页，就可以看到更新的内容。

#### 第五步：发布博文

终于来到了核心的环节，发布博文。

**_posts**目录就是专门存放博客文件的，你可以使用**markdown**, **html**格式的文件来写博客，我是用**markdown**格式写的。但是不管是哪种格式的文件都需要包含 [YAML](https://link.jianshu.com?t=http%3A%2F%2Fyaml.org%2F) 头信息， Jekyll 才会把它当做一个特殊的文件来处理。

在**_posts**目录下新建一个**markdown**文件，头信息必须在文件的开始部分，并且需要按照 YAML 的格式写在两行三虚线之间。如下所示：

```
---
layout: post
title: 标题信息
date: 2023-04-05
author: 作者
tags: [Blog, GitHub, Note]
comments: true
categories: [教程]
pinned: false
---
...
这里就可以使用markdown格式或其他格式写博客内容啦

```



| date | 这里的日期会覆盖文章名字中的日期。这样就可以用来保障文章排序的正确。日期的具体格式为`YYYY-MM-DD HH:MM:SS +/-TTTT`；时，分，秒和时区都是可选的。 |
| ---- | ------------------------------------------------------------ |
| tags | 类似分类 `categories`，一篇文章也可以给它增加一个或者多个标签。同样，`tags` 可以通过 YAML 列表或者以逗号隔开的字符串指定。 |

## 常见问题及解决方法

### 博客模板更新同步

由于博客仓库通过博客模板构建，在博客模板更新后无法通过Pull Request的方式进行同步。为实现对于博客模板更新的同步，可以保留`_posts`文件夹下的文件(模板中的文件最前面添加.,作为隐藏文件)，将其他文件直接替换为更新后博客模板中的文件，在进行简单配置后即可完成同步更新。

### 博客中的表格不能正常显示，不能显示边框
如果觉得表格显示的比较丑，可以修改相应的css样式。
```
修改的路径为 assets/css/styles.css
解决方案：
1 首先把原来的带table的css样式注释
2 然后添加新的css样式
```
新的css样式代码如下：  
```
table {
    border-left: 1px solid #000000;
    border-top: 1px solid #000000;
    width: 100%;
    word-wrap: break-word;
    word-break: break-all;
}

table th {
    text-align: center;
}

table th,
td {
    border-right: 1px solid #000000;
    border-bottom: 1px solid #000000;
}
```

## 参考

1.  [Jekyll + Github Pages 博客搭建入门](https://www.jianshu.com/p/9f198d5779e6)
2.  [有哪些简洁明快的 Jekyll 模板？](https://www.zhihu.com/question/20223939/answers/updated)
3.  [几条经验美化你的GitHub开源项目-简书](https://www.jianshu.com/p/d587b91bacb3)
4.  [simple-icons/simple-icons](https://github.com/simple-icons/simple-icons)
5.  [Maddoc42/Android-Material-Icon-Generator](https://github.com/Maddoc42/Android-Material-Icon-Generator)
6.  [Online Tools-RedKetchup](https://redketchup.io)
7. [如何制作个人学术主页？-知乎](https://www.zhihu.com/question/281476526)  
8. [MarkDown中的表格在jekyll的pages博客中不能正常显示](https://blog.csdn.net/sdujava2011/article/details/83692576)
