### 声明（declaration）

使得名字为程序所知，一个文件如果想使用别处定义的名字则必须包含对那个名字的声明。

> 只给变量、函数、结构体、联合体命名，表明程序有该变量、函数、结构体、联合体。

### 定义（definition）

负责创建与名字关联的实体。

> 具体给变量分配存储空间、给出函数的具体实现、指明结构体和联合体成员。

### 原则

声明可以出现多次，而定义有且只能出现一次。



声明和定义可以分为以下几类：

变量

``` C++
//声明
extern int i;

//定义
int i;             
int i = 1;		   
extern int i = 1;  
```

> 变量这边特别注意，`int i；`是定义，但是加上extern后就是声明；但是又有extern又有初始化时，是定义。**任何包含了显式初始化的声明即成为定义。**[^1]

函数

``` c++
//声明
int sum(int a, int b);          
extern int sum(int a, int b);   

//定义
int sum(int a, int b)          
{
    return a+b;
}
```

结构体或联合体

``` c++
//声明
struct stduent;

//定义
struct student
{
    char name[10];
};

struct student stu1,stu2;

struct
{
    char name[10];
}stu1;
```

数组

```c++
//声明
extern int a[100];
extern int a[];

//定义
int a[100];
```



### 参考

[必须知道的C语言知识细节：声明和定义 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/162578969)

[^1]:C++ primer  p.41

