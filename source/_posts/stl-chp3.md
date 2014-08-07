title: 《C++ STL》学习笔记一 第三章
date: 2014-03-03 15:05:32
tags: 
 - C++
 - STL
categories: C++ STL
---
**《The C++ Standard Library: A tutorial and Reference》** 这本书是学习**C++ STL**的经典书目，现在已经有了第二版，主要是更新了一些**C++11**标准的新特性。刚上班的时候买来的，上周才算正式开始阅读，倒不是自己不想读，只是之前连C++了解的都甚少，于是乎托了这么久，anyway，再晚都不算晚，打算从头到尾好好读读这本书，学习方式采用读书加笔记的方法，当然还要自己完全实现一遍书里的例子程序，希望自己会有很大的进步。

##模板表达式的空格
```c
   vector<list<int> >; // Ok in each C++ version
   vector<list<int>>;  // Ok since C++11
```
其实以前不怎么注意这个特点，只是觉得第一种的排版看起来有点奇怪，现在可以直接使用第二种了，很紧凑，不错。

##nullptr 和 nullptr_t
如果一个指针是空的，以前的版本可以使用**0**和**NULL**来赋值，在C++11中，有专门表示空指针的关键字**nullptr**，避免有时候错误的被当作整数参数传递进去，比如：
```c
void f(int);
void f(void*)

f(0);          //calls f(int)
f(NULL);       //calls f(int) if NULL is 0
f(nullptr);    //calls f(void*)
```
##auto
在C++中有时候指定变量类型是很麻烦的一件事，因为高度模板化的原因，有时候类型定义很长一串，自己也很容易搞错。现在C++11中的关键字**auto** 解决了这个问题，还是很方便的。
```c
vector<string> v;
...
auto pos = v.begin();   //pos has type vector<string>::iterator
```

##初始化列表
C++11提供了初始化列表来初始化变量，下面这些变成了可能。
```c
int value[] {1, 2, 3};
std::vector<int> v {2, 3, 5, 7, 11, 13, 17};
std::vector<std::string> cities {
    "Beijing", "Shanghai", "Guangzhou"
};
std::complex<double> c{4.0, 3.0}; //equivalent to c(4.0, 3.0)
```
另外，现在使用空的初始化列表可以给变量赋0或者nullptr
```c
int i;  // i 未定义初始值
int i{}; // i的初始值为0
int *p;  //p 未定义初始值
int *p{}; //p的初始值为nullptr
```
但是初始化列表对于类型转换不支持，比如不能用**double**初始化**int**
```c
int x{3.0} //Error，非法
```

##Range-Based for Loops
对于 **for**循环，C++11引进了一个非常大的变化，**foreach**。这种有点类似**Matlab**的处理方式，对于程序的可读性和可写性都提高了很多，这是目前为止我最为高兴的变化，你不用再未各种变量的类型，范围发愁了，并且这种特点还支持**初始化列表**。
```c
for (int i : {2, 3, 4, 5, 6}) {
    std::cout << i << std::endl;
}

std::vector<double> vec;
...
for (auto& elem : vec) {
    elem *= 3;
}

template <typename T>
void printElements(const T& coll)
{
    for (const auto& elem : coll) {
	std::cout << elem << std::endl;
    }
}
```
##Move Semantics and Rvalue References
这两个特性目前还没有看懂，需要进一步理解以及应用。
##关键字 noexcept
对于有些函数，如果你不想让他抛出异常的话请使用**noexcept**.
```c
void foo() noexcept;
```
