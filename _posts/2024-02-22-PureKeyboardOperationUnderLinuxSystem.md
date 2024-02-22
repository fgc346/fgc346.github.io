---
layout: post
title: Linux系统纯键盘操作 
date: 2024-02-22
author: ego
tags: [工具]
categories: [工具]
toc: true
pinned: false
---

## 环境配置

```
电脑环境配置：
ubuntu 18.04
chrome 安装 vimium C 扩展程序，为了让chrome有类似于vim的效果。

```
## 打开侧边栏的方式
首先可以使用Super + 数字 打开桌面的侧边栏。  
![image.png](https://raw.githubusercontent.com/fgc346/image/main/img/1702285987019-69d2a118-0f16-450b-b77e-053cf8152151.png)   
因此，下面就是键盘打开这些应用的方式  

| 应用 | 快捷键 |
| --- | --- |
| 文件管理器 | Super + 1 |
| Chrome浏览器 | Super + 2 |
| firefox浏览器 | Super + 3 |
| VSCode | Super + 4 |
| 资源监视器 | Super + 5 |
|  |  |

## bash定义的快捷键
来自于书籍 Advanced Bash-Scripting Guide。  
### Ctrl和字母组合
|          快捷键            | 含义 | 英文原意 |
| ---| --- | --- |
| CTRL-A | 命令行跳到行首 | Moves cursor to beginning of line of text |
| CTRL-B | 左移光标 | Backspace(nondestructive) |
| CTRL-C | 中断正在当前正在执行的程序 | Break.Terminate a foreground job |
| CTRL-D | 删除当前光标所在字符 | log out from a shell(similar to exit)|
| CTRL-E | 命令行跳转到行尾 |  aaa|
| CTRL-F | 右移光标 | aaa |
| CTRL-G | 发出响铃的声音 | BEL |
| CTRL-H | 删除光标的前一个字符 | Rubout(destructive backspace).Erases characters the cursor backs over while backspacing. |
| CTRL-I | 相当于tab键功能 | Horizontal tab |
| CTRL-J | aaa |aaa  |
| CTRL-K | 删除光标之后所有字符 | vertical tab，erases from the character under the cursor to end of line |
| CTRL-L | 清屏 | Formfeed(clear the terminal screen) |
|CTRL-M| 相当于回车键，在windows的文本在linux中显示时，可能会有^M这样 | Carriage return                                              |
| CTRL-N | 下一条命令 | Erases a line of text recalled from history |
| CTRL-O |  插入空行 | Issues a newline |
| CTRL-P | 上一条命令 | recalls last command from history buffer |
| CTRL-Q | 恢复终端的正常输出，软件流控制的恢复 | Resume |
| CTRL-R | 在字符串反向搜索 | Backwards search for text in history buffer |
|CTRL-S| 暂停输出，软件流控制，终端会停止向屏幕输出内容，这可以暂时组织屏幕上的任何新文本显示 | Suspend |
| CTRL-T | 交换光标处当前字符和前一个字符的位置 | Reverses the position of the character the cursor is on with the previous character |
| CTRL-U | 清空当前键入的命令 | earse a line of input, from the cursor backward to beginning of line. |
| CTRL-V | 粘贴 | aaa |
| CTRL-W | 从当前光标，往左删除至第一个空白符的位置 | erases from the character under the cursor backwards to the first instance of whitespace |
| CTRL-X | 剪切 | cuts highlighted text and copies to clipboard |
| CTRL-Y | 粘贴或者恢复上次删除的命令 | pastes back text previously erased |
| CTRL-Z | 当前进程后台挂起 | pauses a foreground job |

### Alt 和字母组合
| Alt + B | 左移一个单词 |  |
| --- | --- | --- |
| Alt+ F | 右移一个单词 |  |
| Alt + . | 粘贴上一条命令的最后一个参数 |  |

## chrome快捷键操作
| 快捷键 | 含义 |
| --- | --- |
| Alt + `  快捷键 | 一个程序的多个窗口之间的切换
比如使用chrome打开了两个窗口，就可以使用Alt + `
切换两个不同的窗口 |
| Ctrl + J | 打开下载页面 |
|  |  |


## 多屏幕下的窗口移动
目前使用的电脑是双屏的，想把窗口从一个屏幕拖到另一个屏幕，要使用鼠标很不方便。有快捷键  

| Shrift + Win + ← | 右边屏幕移动到左边屏幕 |
| --- | --- |
| Shrift + Win + → | 左边屏幕窗口移动到右边屏幕 |
|  |  |
|  |  |
|  |  |


## 一些注意事项
### CTRL-S 和CTRL-Q 作用示例
给定一段定时输出到屏幕的python代码
```python
import time

while True:
    print("hello world")
    time.sleep(1)

```
在终端执行执行该python程序
```python
python3 hello-world.py
```
展示效果为每隔1s 屏幕打印一次hello world  
此时，键入 **CTRL-S**，屏幕暂停输出；  
如果恢复程序执行，键入**CTRL-Q**，程序恢复执行  

