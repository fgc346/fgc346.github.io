---
layout: post
title: 安装autoware遇到的问题汇总
date: 2023-04-21
author: ego
tags: [autoware]
categories: [自动驾驶]
toc: true
pinned: false
---
# 安装autoware中间遇到的坑
## 1 本机基本环境

```
版本：ubuntu 18.04
QT版本：4.8.7 （qmake -v）
OpenCV：3.2.0 （pkg-config --modversion opencv）
PCL: 1.8.1+dfsg1-2ubuntu2.18.04.1  (dpkg -s libpcl-dev | grep Version)
备注：括号后为ubuntu查询软件的版本的命令
```

## 2 安装教程的地址

可参考autoware的[**官方教程**](https://gitlab.com/autowarefoundation/autoware.ai/autoware/-/wikis/Source-Build),

官方教程中觉得有误导人的地方，下面那个版本适应图，打x的是指适配于哪个版本的ubuntu，而不是**不适配**的版本。这一点一定要注意。

我最开始选了v1.11.1这个版本，源码编译一大堆错误，解决问题心累，后面看一个博客的介绍，才知道这个坑。

又选了v1.14.0这个版本，按照官方教程的步骤安装成功。

![image-20230421164357514](https://raw.githubusercontent.com/fgc346/image/main/img/image-20230421164357514.png)

具体安装步骤如下：

```
sudo apt update
sudo apt install -y python-catkin-pkg python-rosdep ros-$ROS_DISTRO-catkin
sudo apt install -y python3-pip python3-colcon-common-extensions python3-setuptools python3-vcstool
pip3 install -U setuptools

我安装的是v1.14.0，支持CUDA版本。
cd ~/Projects/autoware
mkdir -p autoware.ai/src
cd autoware.ai
wget -O autoware.ai.repos "https://gitlab.com/autowarefoundation/autoware.ai/autoware/raw/1.14.0/autoware.ai.repos?inline=false"
vcs import src < autoware.ai.repos
 rosdep update
rosdep install -y --from-paths src --ignore-src --rosdistro $ROS_DISTRO
 AUTOWARE_COMPILE_WITH_CUDA=1 colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release

```

# Autoware 官方demo演示

具体步骤可参考[博客](https://blog.csdn.net/zhao5269/article/details/106864985).

按照博客中的步骤，最后demo演示的效果。

![image-20230421221959982](https://raw.githubusercontent.com/fgc346/image/main/img/image-20230421221959982.png)

# 参考

1. [autoware 安装时踩过的坑](https://blog.csdn.net/Summeryyyy/article/details/119532438)
2. [Autoware入门学习](https://blog.csdn.net/zhao5269/article/details/106827618)