---
layout: post
title: nohup命令使用
date: 2023-07-06
author: ego
tags: [Linux]
categories: [Linux]
toc: true
pinned: false
---



## Linux nohup命令

缘起，看到一些程序在运行时，会用到nohup命令，对这个命令不熟悉，自己写了程序，对此加深印象。

### 基本知识

nohup no hang up（不挂起），主要用于在系统后台不挂断地运行命令，退出终端不会影响程序的运行。

语法格式

```
nohup Command [Arg ...] [ &]
```

参数说明：

Command：要执行的命令。

Arg：一些参数，可以指定输出文件。

&：让命令在后台执行，终端退出后命令仍旧执行。

### 具体例子演示

```
#include <chrono>
#include <csignal>
#include <iostream>
#include <thread>

void signal_handler(int signum) {
  std::cout << "get single: " << signum << std::endl;
  std::this_thread::sleep_for(std::chrono::milliseconds(2000));  // 休眠2秒
  system(
      "ps -ef | grep back_job_demo | awk \'{print \" kill -9 \" $2}\' | sh ");
  exit(0);
}

int main() {
  signal(SIGINT, signal_handler);
  int64_t count = 0;
  while (1) {
    ++count;
    std::cout << "count = " << count << std::endl;
    std::this_thread::sleep_for(std::chrono::milliseconds(1000));  // 休眠1秒
  }
  return 0;
}
```

编译这段代码生成可执行程序 back_job_demo。假设路径为~/test。
```
cd ~/test/
nohup ./back_job_demo &
和./back_job_demo &
```
**两者的区别**

&符号表示，该进程在后台运行。

但是只使用“&”虽然比较简单，但是有个致命的缺陷，**back_job_demo**这个进程在一个shell中运行，该进程的父进程仍然是当前的shell。如果shell退出，则使用“&”运行的所有进程均会被强制退出，因此**back_job_demo**这个进程会被强制杀掉。

为什么退出shell时，所有进程都会退出？这涉及到Linux的信号机制。

shell在退出时，会发送HUP信号给其所有子进程，接到HUP信号的进程会中止运行。如果忽略HUP信号，进程不响应该信号，既可以使进程在shell退出时，仍然保持运行。这是nohup的工作原理。

nohup并不是一个让进程后台运行的命令，**nohup只是让该进程忽略来自shell的HUP信号**，因此命令为nohup。

为了让进程在后台运行，可以在进程后面加上“&”符号。

因此 **nohup ./back_job_demo &** 这样执行，就可以让**back_job_demo**在后台运行，又不让其因为shell退出而关闭。

因此 **nohup ./back_job_demo &** 是后台运行进程的最佳方法。

## 参考
1. [菜鸟教程nohup使用](https://www.runoob.com/linux/linux-comm-nohup.html)
2. 书籍《Linux管理与开发实用指南》

