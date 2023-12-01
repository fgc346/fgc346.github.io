---
layout: post
title: conda使用记录
date: 2023-09-08
author: ego
tags: [工具]
categories: [工具]
toc: true
pinned: false
---
## conda命令汇总
1 创建新环境
```
conda create -n test python=3.6
```

2 删除环境
```
conda remove -n test --all
```

3 重命名环境
分两步，首先复制一份环境，然后删除旧有的环境

- 先 clone 一份 new name 的环境
- 删除 old name 的环境

```
conda create -n test-new --clone test
conda remove -n test --all
```

4 查看有多少环境

```
conda env list
```

## conda 升级 jupyter notebook
1 使用jupyter --version查看当前jupyter notebook版本  
2 升级jupyter notebook  
3 升级jupyter-lab到3.0  