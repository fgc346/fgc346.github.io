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

## 2 使用鼠标
具体方式：  
按完前缀ctrl+B后，再按冒号：进入命令行模式。  
输入以下命令：

```
set -g mouse on
```
## 3 分屏下使用鼠标复制的方法
通常使用tmux时会用shift+鼠标选中内容,然后右键复制。但正如图中的情况，存在分屏也会将左边的内容一并拷贝。  
**解决方法：  **  
一个比较方便的解决办法是ctrl+b+z，将需要的复制内容所在的面板最大化，再用上述通用的复制方法复制，复制完成后再ctrl+b+z，恢复之前的视图。  

## 4 tmux如何自定义配置文件
电脑的tmux的版本是 tmux 2.6。发现网上说的自定义配置文件不对。  
~~网上给的配置文件项  ~~
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
## 参考

1. [https://www.cnblogs.com/yangjianfengzj/p/16919610.html](https://www.cnblogs.com/yangjianfengzj/p/16919610.html)  
2. [https://blog.csdn.net/ddydavie/article/details/79031564](https://blog.csdn.net/ddydavie/article/details/79031564)  
3. [https://www.ruanyifeng.com/blog/2019/10/tmux.html](https://www.ruanyifeng.com/blog/2019/10/tmux.html)  
4. [https://apple.stackexchange.com/questions/217166/unknown-option-mode-mouse-with-iterm-tmux](https://apple.stackexchange.com/questions/217166/unknown-option-mode-mouse-with-iterm-tmux)
4. https://cenalulu.github.io/linux/tmux/
