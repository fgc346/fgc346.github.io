---
layout: post
title: Caps映射为Esc和Ctrl
date: 2023-09-18
author: ego
tags: [工具]
categories: [工具]
toc: true
pinned: false
---
## 1 问题背景
平时主要在ubuntu下开发，经常会使用到vim和Tmux。vim操作会用到Esc键，Tmux快捷键为Ctrl +b。而大写键Caps这个位置很好的键基本上不使用。所以考虑将这个键映射为Esc和Ctrl键。
最后想要实现的效果为：
单击Caps键，等于按Esc；
长按Caps键，等于按Ctrl。
## 2 解决方案
借助于Interception这个项目[[https://gitlab.com/interception/linux/tools](https://gitlab.com/interception/linux/tools)],既可以实现在windows上效果，也可以实现linux效果。
### 2.1 windows解决方案
具体参考博客
```
https://www.notion.so/Caps-Esc-Ctrl-c13a0a99a33048fdb776c2f58b7a3583
```
### 2.2 Linux解决方案
注：本机电脑为ubuntu 18.04，以下操作均为在ubuntu18.04下的操作步骤，其他linux机器安装步骤类似。
使用源码编译的方式安装Inerception，借助于Cmake进行编译&&安装。
#### 2.2.1 安装依赖包
```
~ $ sudo apt install cmake libevdev-dev libudev-dev libyaml-cpp-dev\
	libboost-dev
```
#### 2.2.2 安装Inerception Tools
```
$ git clone https://gitlab.com/interception/linux/tools.git
$ cd tools
$ mkdir build
$ cd build
$ cmake ..
$ make
$ sudo make install
```
#### 2.2.3  安装插件caps2esc
```
$ git clone https://gitlab.com/interception/linux/plugins/caps2esc.git
$ cd caps2esc
$ mkdir build
$ cd build
$ cmake ..
$ make
$ sudo make install
```
#### 2.2.4 启动caps2sec并实现开机自启动
1 编辑配置文件 /etc/udevmon.yaml，若没有这个文件，需要新建一个。
```
sudo touch /etc/udevmon.yaml

编译配置文件
sudo vim /etc/udevmon.yaml

```
/etc/udevmon.yaml 内容为
```
- JOB: "intercept -g $DEVNODE | caps2esc | uinput -d $DEVNODE"
  DEVICE:
    EVENTS:
      EV_KEY: [KEY_CAPSLOCK, KEY_ESC]
```
2 添加为开机自启动服务。
新建配置文件  /etc/systemd/system/udevmon.service，并编译该文件
```
sudo vim /etc/systemd/system/udevmon.service
```
/etc/systemd/system/udevmon.service内容如下：
需要注意的是，2.2.2节中执行完sudo make install，要注意查看udevmon这个程序的安装位置
```
使用which查看udevmon安装位置
~$ which udevmon
/usr/local/bin/udevmon
```
```
[Unit]
Description=udevmon
Wants=systemd-udev-settle.service
After=systemd-udev-settle.service

[Service]
ExecStart=/usr/bin/nice -n -20 /usr/local/bin/udevmon -c /etc/udevmon.yaml

# "/usr/local/bin/udevmon" 需要修改为你的电脑上的安装路径
# 可以通过 which udevmon 来查询

[Install]
WantedBy=multi-user.target
```
3 最后启用该启动项
```
sudo systemctl enable --now udevmon
```
完成以上步骤后，就可以实现Caps映射为Esc和Ctrl的效果。
## 参考
1 [https://www.notion.so/Caps-Esc-Ctrl-c13a0a99a33048fdb776c2f58b7a3583](https://www.notion.so/Caps-Esc-Ctrl-c13a0a99a33048fdb776c2f58b7a3583)
2 [https://blog.csdn.net/Nielson_19/article/details/130325553](https://blog.csdn.net/Nielson_19/article/details/130325553)
