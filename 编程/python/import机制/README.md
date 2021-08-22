#### 存在的坑：

1. 无法直接在tests目录下运行测试单元，会显示无法找到模块。
2. 跨包导入模块时，无法使用相对引用。



#### 解决方案：

1. 在根目录写一个入口脚本，把测试案例当做模块，把tests文件夹当做包。
2. 尽量使用绝对引用，除非导入名称特别冗余。
3. 在测试脚本开头加入 `sys.path.append('根目录')`，脚本运行后失效。



#### 问题复现:

文件目录

```python
import_test
|_______ modules
| |____ __init__.py
| |____ a.py
| |____ b.py
| |____ c.py
|_______ tests
| |____ __init__.py
| |____ test_a.py
| |____ test_b.py
| |____ test_c.py
|_______ step.py
```

问题1. cd到tests目录下，运行test_a.py显示无法找到modules。

问题2. test_b.py导入b模块时，使用` from ..modules import b ` ,报错。



#### 参考

https://docs.python.org/zh-cn/3/reference/import.html#importlib

https://zhuanlan.zhihu.com/p/109036573

https://zhuanlan.zhihu.com/p/63143493