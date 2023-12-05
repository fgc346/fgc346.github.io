---
layout: post
title: Tmux使用汇总
date: 2023-12-01
author: ego
tags: [工具]
categories: [工具]
toc: true
pinned: false
---

# Tmux基础知识
## 1 tmux 介绍
tmux是一个终端多路复用工具，它允许你在一个终端中轻松切换多个程序，使任务在后台运行并且能够在不同的终端中恢复之前的任务。  
官方定位为：  
```
tmux is a terminal multiplexer. It lets you switch easily between several programs in one terminal, detach them (they keep running in the background) and reattach them to a different terminal.
```
## 2 tmux安装
```
在ubuntu系统中
apt-get install tmux
```
## 3 基本概念
需要理解tmux的几个术语，tmux主要分为三层:    

- Session 一组窗口的集合，通常用来汇总同一个任务。session可以用名字标识，便于任务切换。
- Window 单个可见的窗口，windows可以按0，1,2,...编号
- Pane 窗格，将一个屏幕分割为多个小窗口，可以实现分屏的功能。

下图是一个形象的三层的展示：  

![image-20231201131236345](https://raw.githubusercontent.com/fgc346/image/main/img/image-20231201131236345.png)解释：
session总是显示在tmux的左下角，通常有一个名字，windows类似于tab形式，pane就是不同的窗口细分小窗口。  

# 使用记录
## 1 常用的快捷键
tmux输入快捷键有个前缀操作，默认是Ctrl + B，操作快捷键时，先按前缀键，然后再按相应的快捷键。  

| 功能 | 快捷键 | 解释 |
| --- | --- | --- |
| 上下分屏 | Ctrl + B，” | 先按前缀键Ctrl + B，然后再按" |
| 左右分屏 | Ctrl + B，% |  |
| 窗格切换 | Ctrl  + B, o |  |
| 窗格上下左右拉伸 | Ctrl + B + 方向键 | 同时按 Ctrl + B + ←，表示窗格向左拉伸 |
| 对当前面板进行缩放（全屏） | Ctrl + B ,z |  |
| 窗格上下左右拉伸 | Ctrl + B + 方向键 | 同时按 Ctrl + B + ←，表示窗格向左拉伸 |
| 重新命名窗口名称 | Ctrl + B， ， | 注意按完前缀键，接下来需要按**逗号**键 |
| 查看所有的会话 | Ctrl + B，s | |

## 2 使用鼠标
具体方式：  
按完前缀ctrl+B后，再按冒号：进入命令行模式。  
输入以下命令：

```
set -g mouse on
```
## 3 分屏下使用鼠标复制的方法
通常使用tmux时会用shift+鼠标选中内容,然后右键复制。但正如图中的情况，存在分屏也会将左边的内容一并拷贝。  
**解决方法：**  
一个比较方便的解决办法是ctrl+b+z，将需要的复制内容所在的面板最大化，再用上述通用的复制方法复制，复制完成后再ctrl+b+z，恢复之前的视图。  

## 4 tmux如何自定义配置文件
电脑的tmux的版本是 tmux 2.6。发现网上a找的自定义配置文件本机使用不生效。  
网上给的配置文件项  
```
#Mouse mode
# tmux 2.6版本不生效
#setw -g mode-mouse on
#set -g mouse-resize-pane on
#set -g mouse-select-pane on
#set -g mouse-select-window on

```
**报错**：  
```
运行命令：
tmux source-file .tmux.conf 
报错：
invalid option: mode-mouse
invalid option: mouse-resize-pane
invalid option: mouse-select-pane
invalid option: mouse-select-windo
```
问题解决：  
```
#Mouse mode
set-option -g mouse on
```
如何使配置文件生效？  
```
1 在终端运行命令：
tmux source-file .tmux.conf 
```
**关于配置文件的说明**  
网上有很多tmux的配置文件，但是都没有标明适用的tmux的版本。  
在本机电脑使用tmux时，发现tmux自定义配置的命令一直在迭代升级，有些命令是不兼容的。从网上直接粘贴过来的相关配置不一定能在自己的tmux中生效，因此，需要找到tmux相关版本的对应命令。  

## 5 常用的tmux操作
### 5.1 关于session的操作
```
在终端创建一个新的 session
tmux new -s  demo-one
如果需要tmux在后台运行：
运行快捷键 Ctrl + B，d，然后就恢复原来的终端界面
要想重新恢复 tmux 会话，可以运行快捷键 Ctrl + B，a

```
### 5.2 关于窗口的操作
#### 5.2.1 如何重命名一个窗口
```
前缀键 + ，（先按前缀键 Ctrl和B，然后再按“，”键）
```
#### 5.2.2 如何关闭一个窗口
```
tmux kill-window -t 
```

# 参考资料汇总

下面是学习tmux的过程中，参考的比较好的学习教程。  

| 标题                                                         | 链接                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| tmux: Productive Mouse-Free Development 中文版（一本小书，比较容易看） | [https://www.kancloud.cn/kancloud/tmux/62462](https://www.kancloud.cn/kancloud/tmux/62462) |
| Tmux使用手册（内容丰富，写的很清晰）                         | [https://louiszhai.github.io/2017/09/30/tmux/](https://louiszhai.github.io/2017/09/30/tmux/) |
| tmux简洁教程                                                 | [https://notes.maxwi.com/2017/11/10/tmux/](https://notes.maxwi.com/2017/11/10/tmux/) |
| tmux简洁教程及config关键配置                                 | [https://www.jianshu.com/p/fd3bbdba9dc9](https://www.jianshu.com/p/fd3bbdba9dc9) |
| Tmux 配置：打造最适合自己的终端复用工具                      | [https://www.cnblogs.com/zuoruining/p/11074367.html](https://www.cnblogs.com/zuoruining/p/11074367.html) |

# 参考

1. [https://www.cnblogs.com/yangjianfengzj/p/16919610.html](https://www.cnblogs.com/yangjianfengzj/p/16919610.html)  
2. [https://blog.csdn.net/ddydavie/article/details/79031564](https://blog.csdn.net/ddydavie/article/details/79031564)  
3. [https://www.ruanyifeng.com/blog/2019/10/tmux.html](https://www.ruanyifeng.com/blog/2019/10/tmux.html)  
4. [https://apple.stackexchange.com/questions/217166/unknown-option-mode-mouse-with-iterm-tmux](https://apple.stackexchange.com/questions/217166/unknown-option-mode-mouse-with-iterm-tmux)
5. [https://cenalulu.github.io/linux/tmux/](https://cenalulu.github.io/linux/tmux/)
