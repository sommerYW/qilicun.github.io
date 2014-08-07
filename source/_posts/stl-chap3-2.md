title: 《C++ STL》学习笔记二 第三章
date: 2014-03-03 16:01:58
tags: 
 - C++
 - STL
categories: C++ STL
------
接上篇继续学习第三章内容。
##Variadic Templates
从C++11开始允许模板使用多个arguments，例如：
```c
void print()
{
}
template <typename T, typename... Types>
void print(const T& firsrArg, const Types&... args)
{
    std::cout << firstArgs << std::endl;
    print(args...);
}
```
例如，
```c
print(7.5, "hello", std::bitset<16>(337), 42);
```
##模板别名
现在可以在模板中使用别名，有点像*typedef*
```c
template<typename T>
using Vec = std::vector<T, MyAlloc<T>>;
```
这时候`Vec<int> coll` 就等价与`std::vector<int, MyAlloc<int>> coll`
##Lambda 函数
C++ 引入了**Lambda**函数，说实话，没看这本书之前我都没有听过这个函数，好像Python已经有支持这个函数了。下面是一些**Lambda**函数的用法，貌似还是挺有用的。
```c
[] {
	std::cout << "Hello Lambda" << std::endl;
}
```
可以这样直接调用
```c
[] {
	std::cout << "Hello Lambda" << std::endl;
} (); //打印 "Hello Lambda"
```
或者也可以直接传递给一个对象
```c
auto 1 = [] {
	std::cout << "Hello Lambda" << std::endl;
};
...
1();  //打印"Hello Lambda"
```
或者还可以传递参数
```c
auto 1 = [](const std::string& s) {
	std::cout << s << std::endl;
};
...
1("Hello Lambda");  //打印"Hello Lambda"
```
Lambda 函数还支持传递引用，
- [=] 这样表示给Lambda函数传递值。
- [&] 这样就可以传递引用了，然后可以修改变量。

第三章大致就这些内容，当然还有很多别的细节，自己目前理解的就这样。
