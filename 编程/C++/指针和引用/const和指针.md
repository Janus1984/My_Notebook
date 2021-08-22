常见的const修饰指针的情况有以下三种：

```c++
const int * p; //指向常量的指针，指针指向的值不可更改
int * const p; //常量指针，指针的指向不可更改
const int * const p; //指针的指向和指针指向的值都不可更改
```

> 主要看const右侧紧跟的是指针还是常量。



``` c++
const int *p;
int const *p;
```

> 两者意思相同，但是建议第二种写法。



[C++里 const int* 与 int const* 有什么区别？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/443195492)

[如何理解常量指针与指针常量？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/19829354)

