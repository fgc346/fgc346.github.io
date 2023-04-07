---
layout: post
title: C++从文件中读取数据
date: 2023-04-06
author: ego
tags: [C++]
comments: true
toc: true
pinned: false
---

## C++文件读取操作

[toc]
缘起：

在写图的过程中，《算法》这本书中图结构需要的数据是以读取文件中的文本的方式，读取数据。

因此，c++中对文件的操作需要十分熟悉。

还有如何对一行数据进行分割，string中并没有提供字符串的分割函数，需要自己去手动封装一个函数。

例如一个文件 file_1.txt,内容如下

```
JFK MCO
ORD DEN
ORD HOU
DFW PHX
JFK ATL
ORD DFW
ORD PHX
ATL HOU
DEN PHX
PHX LAX
JFK ORD
DEN LAS
DFW HOU
ORD ATL
LAS LAX
ATL MCO
HOU MCO
LAS PHX
```

如何将文件读入，并将每一行按“ ”分割

### 1 字符串分割函数

#### 1.1 string中的find和strsub实现

```
// source_str:待分割的字符串
// destination_strs:分割后的字符串,使用vector<string>
// sp：分隔符
void SplitString(const std::string& source_str, std::vector<std::string>& destination_strs, const std::string& sp)
{
  std::string::size_type pos1, pos2;
  pos2 = source_str.find(sp);
  pos1 = 0;
  while(std::string::npos != pos2)
  {
    destination_strs.push_back(source_str.substr(pos1, pos2 - pos1));
    pos1 = pos2 + sp.size();
    pos2 = source_str.find(sp, pos1);
  }
  //如果源文件的最后一个字符是分隔符，pos1的大小就等于字符串的长度
  if(pos1 != source_str.length())
    destination_strs.push_back(source_str.substr(pos1));
}

代码中pos1 = pos2 + sp.size();这一行执行完，pos1 可能超过source_str.size;但是find函数已经对此作了处理
    如果输入的pos超过了字符串长度，直接返回std::string::npos。
  
```

#### 1.2 通过c语言的strtok函数实现

```
方法2：
通过strtok函数实现
strtok为C语言中的字符串分割函数，其具体解释如下:
原型：char * strtok ( char * str, const char * delimiters );
功能：分割字符串str，delimiters为指定的分割符，可以有多个。
说明：strtok只能接受C风格的字符串，如果是string类型，可以使用c_str函数进行转换。strtok()用来将字符串分割成一个个片段。参数s指向欲分割的字符串，参数delim则为分割字符串，当strtok()在参数s的字符串中发现到参数delim的分割字符时 则会将该字符改为\0 字符。在第一次调用时，strtok()必需给予参数s字符串，往后的调用则将参数s设置成NULL。每次调用成功则返回被分割出片段的指针。

vector<string> split2(const string &str, const string &pattern)
{
    char * strc = new char[strlen(str.c_str())+1];
    strcpy(strc, str.c_str());   //string转换成C-string
    vector<string> res;
    char* temp = strtok(strc, pattern.c_str());
    while(temp != NULL)
    {
        res.push_back(string(temp));
        temp = strtok(NULL, pattern.c_str());
    }
    delete[] strc;
    return res;
}

```

#### 1.3 通过stringstream实现

注意这里面的分割符 只能是**char类型**，不能是字符串

```
vector<string> split3(const string &str, const char pattern)
{
    vector<string> res;
    stringstream input(str);   //读取str到字符串流中
    string temp;
    //使用getline函数从字符串流中读取,遇到分隔符时停止,和从cin中读取类似
    //注意,getline默认是可以读取空格的
    while(getline(input, temp, pattern))
    {
        res.push_back(temp);
    }
    return res;
}
```



### 2 读取文件并对数据操作

```
    string file_name("file_1.txt");
	std::ifstream srcFile(file_name, std::ios::in); // 以文本模式打开txt文件
    if (!srcFile.is_open())
    {
        std::cout << "the file_name " << file_name << " failed to open" << std::endl;
    }
	std::vector<std::vector<std::string>> graph_vv;	//存储文本文件中的数据
    while (getline(fin, line_str))
    {
        std::vector<std::string> v;
        SplitString(line_str, v, sp);
        for (int i = 0; i < v.size(); ++i)
        {
            if (!st_.count(v[i]))
            {
                st_.insert(std::make_pair(v[i], st_.size()));
                keys_.emplace_back(v[i]);
            }
        }
        graph_vv.emplace_back(v);
    }
```



