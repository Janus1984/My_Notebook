## is & ==

- `is `，`is not` 对比的是两个变量的内存地址

- `==`， `!= `对比的是两个变量的值

  

> 如果比较的两个变量，指向的都是**地址不可变的类型（str、数值、元组等）**，那么`is`，`is not `和 `==`，`!=`是完全等价的。

> 如果比较的两个变量，指向的是**地址可变的类型（list，dict，set等**），则两者是有区别的。

例子：

```python
a = "hello"
b = "hello"
print(a is b, a == b)
>> True,True
```

