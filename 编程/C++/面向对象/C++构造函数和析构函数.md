# 构造函数&析构函数

- **构造函数其实就相当于python里的 ` __init__() `，是对类的一个初始化，在调用对象时自动调用**
- **析构函数是在销毁对象时自动调用（这个貌似python里没有？）**



### 构造函数

**构造函数语法：**类名(){}

1. 构造函数，没有返回值也不写void
2. 函数名称与类名相同
3. 构造函数**可以有参数**，因此可以发生重载
4. 程序在调用对象时候会自动调用构造，无须手动调用,而且只会调用一次



### 析构函数

**析构函数语法：** ~类名(){}

1. 析构函数，没有返回值也不写void
2. 函数名称与类名相同,在名称前加上符号 ~
3. 析构函数**不可以有参数**，因此不可以发生重载
4. 程序在对象销毁前会自动调用析构，无须手动调用,而且只会调用一次



### 代码示例


```c++
class Person
{
public:
        //构造函数
        Person()
        {
                cout << "Person的构造函数调用" << endl;
        }
        //析构函数
        ~Person()
        {
                cout << "Person的析构函数调用" << endl;
        }


};


void test01()
{
        Person p;
}


int main() {
        
        test01();


        system("pause");


        return 0;
}
//输出：Person的构造函数调用
//     Person的析构函数调用
```



## 构造函数

### 构造函数分类

按照参数分类分为 有参和无参构造  无参又称为默认构造函数

按照类型分类分为 普通构造和拷贝构造

- [x] C++这里就很骚气，构造函数可以重载，根据实例化时的参数，选择调用哪个构造函数

```c++
class Person {
public:
        //无参（默认）构造函数
        Person() {
                cout << "无参构造函数!" << endl;
        }
        //有参构造函数
        Person(int a) {
                age = a;
                cout << "有参构造函数!" << endl;
        }
        //拷贝构造函数
        Person(const Person& p) {
                age = p.age;
                cout << "拷贝构造函数!" << endl;
        }
        //析构函数
        ~Person() {
                cout << "析构函数!" << endl;
        }
public:
        int age;
};


//2、构造函数的调用//调用无参构造函数void test01() {
        Person p; //调用无参构造函数
}


//调用有参的构造函数void test02() {


        //2.1  括号法，常用
        Person p1(10);
        //注意1：调用无参构造函数不能加括号，如果加了编译器认为这是一个函数声明（返回Person类型的函数）
        //Person p2();


        //2.2 显式法
        Person p2 = Person(10);
        Person p3 = Person(p2);
        //Person(10)单独写就是匿名对象  当前行结束之后，马上析构


        //2.3 隐式转换法
        Person p4 = 10; // Person p4 = Person(10);
        Person p5 = p4; // Person p5 = Person(p4);


        //注意2：不能利用 拷贝构造函数 初始化匿名对象 编译器认为是对象声明
        //Person p5(p4);
}


int main() {


        test01();
        //test02();


        system("pause");


        return 0;
}C
```

