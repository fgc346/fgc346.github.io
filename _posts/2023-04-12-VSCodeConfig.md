---
layout: post
title: VScode配置C++环境
date: 2023-04-12
author: ego
tags: [C++]
categories: [C++]
toc: true
pinned: false
---

记录Ubuntu下配置VSCode的C/C++开发环境。

Ubuntu系统为18.04。

VScode中进行C/C++环境时，需要配置launch.json和tasks.json，这两个json文件中，经常需要用到一些全局变量，为了可以自定义配置文件，更方便地修改以适应自己需求。

对VScode的预定义全局变量进行总结。

## 预定义全局变量

| 全局变量                   | 含义                                       |
| -------------------------- | ------------------------------------------ |
| ${workspaceFolder}         | 表示当前`workspace`文件夹路径              |
| ${workspaceRoot}           | 同上表示当前`workspace`文件夹路径          |
| ${cwd}                     | 切换`workspace`文件夹路径                  |
| ${workspaceRootFolderName} | 表示`workspace`的文件夹名                  |
| ${workspaceFolderBasename} | 同上表示`workspace`的文件夹名              |
| ${lineNumber}              | 当前活动文件的光标行号                     |
| ${selectedText}            | 当前活动文件的选中文本                     |
| ${file}                    | 当前活动文件的绝对路径                     |
| ${fileWorkspaceFolder}     | 当前活动文件工作空间绝对路径               |
| ${relativeFile}            | 当前活动文件的相对`workpace`的相对路径     |
| ${relativeFileDirname}     | 当前活动文件的目录相对`workpace`的相对路径 |
| ${fileDirname}             | 当前活动文件的目录绝对路径                 |
| ${fileExtname}             | 当前活动文件的后缀名                       |
| ${fileBasename}            | 当前活动文件的文件名                       |
| ${fileBasenameNoExtension} | 当前活动文件的文件名，不带后缀             |
| ${fileDirnameBasename}     | 当前活动文件目录名                         |
| ${execPath}                | `vscode`的执行文件路径                     |
| ${execInstallFolder}       | 当前工作空间的目录                         |
| ${pathSeparator}           | 系统文件分割符                             |
| ${env:PATH}                | 系统中的环境变量                           |

### 一个具体的预定义变量的例子

![image-20230412182921270](https://raw.githubusercontent.com/fgc346/image/main/img/image-20230412182921270.png)

## 配置VScodeC/C++环境
具体步骤如下（使用chatGPT指导的步骤）：
1. 打开一个新的或现有的C++项目文件夹（文件>打开文件夹）。
2. 在VS Code的左侧边栏中，单击“资源管理器”图标（或使用快捷键“Ctrl+Shift+E”）来打开资源管理器。
3. 在资源管理器中，单击右键并选择“新建文件夹”来创建一个名为“build”的文件夹，该文件夹将用于保存编译生成的二进制文件。
4. 在资源管理器中，单击右键并选择“新建文件”来创建一个名为main.cpp的文件，并在其中编写您的C++代码。
5. 确保您的计算机上已安装C++编译器，例如GCC或Clang。
6. 在VS Code中，打开命令面板（使用快捷键“Ctrl+Shift+P”或在菜单中选择“查看>命令面板”）。
7. 在命令面板中，输入“C++”并选择“配置默认的构建任务”选项，然后选择“g++ build active file”作为默认构建任务。
8. 在命令面板中，再次输入“C++”并选择“创建启动配置”选项，然后选择“g++ Launch”作为调试器类型。

一个具体的C++工程实例
```C++
vs_cpulsplus_demo/
├── build
│   └── vs_cpulsplus_demo
├── main.cpp
└── .vscode
    ├── launch.json
    └── tasks.json
```

## main函数
```C++
#include <iostream>

int main()
{
  std::cout << "Hello World" << std::endl;
  return 0;
}
```


## tasks.json配置
```Json
{
  //
  "version": "2.0.0",
  "tasks": [
    {
      "label": "C++ Build",
      "type": "shell",
      "command": "g++",
      "args": [
        "-g",
        "-o",
        "${workspaceFolder}/build/${workspaceFolderBasename}",
        "${workspaceFolder}/*.cpp"
      ],
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "problemMatcher": {
        "owner": "cpp",
        "fileLocation": [
          "relative",
          "${workspaceFolder}"
        ],
        "pattern": {
          "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
          "file": 1,
          "line": 2,
          "column": 3,
          "severity": 4,
          "message": 5
        }
      }
    }
  ]
}
```
上述的tasks.json配置了一个编译c++的程序
```

g++ -g -o "${workspaceFolder}/build/${workspaceFolderBasename}" "${workspaceFolder}/*.cpp"

如上所述的全局变量
${workspaceFolder} : vs_cpulsplus_demo
{workspaceFolderBasename} : vs_cpulsplus_demo

替换后为 g++ -g -o vs_cpulsplus_demo/build/vs_cpulsplus_demo vs_cpulsplus_demo/main.cpp
```

![image-20230412184415419](https://raw.githubusercontent.com/fgc346/image/main/img/image-20230412184415419.png)

## launch.json配置
```Json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "C++ Launch", 
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}/build/${workspaceFolderBasename}", //调试时候的可执行程序与工作目录的名称保持相同
      "args": [],
      "stopAtEntry": true,
      "cwd": "${workspaceFolder}", // 设置工作目录
      "environment": [],
      "externalConsole": false,
      "MIMode": "gdb",
      "preLaunchTask": "C++ Build" //// 调试会话开始前执行的任务，一般为编译程序, 因此，需要与tasks.json中的label标签保持一致
    }
  ]
}
```
![image-20230412184519912](https://raw.githubusercontent.com/fgc346/image/main/img/image-20230412184519912.png)

## 参考

1.  [VSCode官方关于变量的定义](hhttps://code.visualstudio.com/docs/editor/variables-reference)
2.  [chat GPT](https://chat.openai.com/chat)