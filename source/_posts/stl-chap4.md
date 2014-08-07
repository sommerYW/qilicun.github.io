title: 《C++ STL》学习笔记三 第四章
date: 2014-03-04 16:18:45
tags: 
- C++
- STL
categories: C++ STL
---
第四章介绍了一些C++的通用部分，基本只要用到C++都会接触到。

##标准命名空间std
以前学习C++的时候我喜欢在文件开头就写``using namespace std``，不过后来意识到这样子不太安全，也不是太好，于是喜欢下面的风格。
```c
std::cout << std::hex << 3.4 << std::endl;
```
当然你可以这样用
```c
using std::cout;
using std::endl;
cout << std::hex << 3.4 << endl;
```
##头文件
和C不一样，C++的标准库文件不需要出现``.hpp``等字样，推荐使用
```c
#include <iostream> // c++ header file
#include <cmath>  // c header file
```
C中有很多C++可以用到的库，比如**math**，**string**，这样在C++中只需要
```c
#include <cstring>
#include <cmath>
```
即可，不需要
```c
#include <stdio.h>
```
##exception
对于exception我接触的不多，而且处理异常需要很深的经验，这点可以以后再看，不过如果要想程序稳健，还是需要异常处理的。
