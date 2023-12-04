---
layout: post
title: vim编辑器使用记录
date: 2023-07-18
author: ego
tags: [工具]
categories: [工具]
toc: true
pinned: false
---
# Vim编辑器使用
## 1 背景
缘起，对于很多linux机器，除了vim编辑器，一般没有其他编辑器可用，因此熟悉vim的使用能够更高效地工作，通过记录vim的使用方法，来进一步强化对vim的掌握程度。

通过阅读《vim 实用技巧》学习到一个理念：一键移动，一键操作。
## 2 命令记录
### 2.1 复制命令
```
全部复制： 
ESC键进入普通模式，先按gg(光标跳转到文档第一行)，
然后ggyG操作，最后按回车键。已经将全文拷贝到剪切板。
```
### 2.2 去掉vim每行结尾的^M
问题产生的原因：
```
windows的换行符是\n\r
linux的换行符是\n
```
在 vim下， 这个多余的\r就会被显示为^M，虽然显示为两个字符，但其实是一个字符。  
解决方法：
```
1 字符串替换：
:%s/\r//g
2 将文件格式转化为unix格式：
:set ff=unix
```
## 3 学习资料
### 3.1 书籍
1. [Vim 实用技巧(第二版)](https://agou-images.oss-cn-qingdao.aliyuncs.com/pdfs/Vim%E5%AE%9E%E7%94%A8%E6%8A%80%E5%B7%A7%EF%BC%88%E7%AC%AC2%E7%89%88%EF%BC%89.pdf)
2. [Learn Vimscript the Hard Way](https://learnvimscriptthehardway.stevelosh.com/)

## 参考
1. [Vim系列教程](https://www.kawabangga.com/vim%e7%b3%bb%e5%88%97)
2. [去掉 vim 每行结尾的 ^M](https://zhiqiang.org/it/remove-m-from-vim.html)

