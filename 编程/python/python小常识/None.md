## None

- ==`None`表示空，在python里是个单例对象，一个变量如果是`None`，它一定和`None`指向同一个地址内存。==所以`None`不等于空字符串、空列表，也不等同于`False`。

- `If not a：`通过这样一个判空操作，不管a是None还是空字符串、空列表或者布尔值，你都会得到想要的值。
- `if a is None：`是判断a是否非为`class'Nonetype'`

- 对象存在并不一定是True。对象返回什么取决于内置方法__bool__，如果__len__返回0，则bool默认为False，如果len不为0，则bool默认为True；如果自定义了bool，则返回自定义bool。



### 具体展开

#### 1.None表示空，但它不等于空字符串、空列表，也不等同于False

None表示空，但它不等于空字符串、空列表，也不等同于False，通过下面的代码进行验证。

```python
a = ''
b = False
c = []

print(a==None) #比较值
print(b==None)
print(c==None)

print(a is None)

False
False
False
False
```



#### 2. `if not a`和`if a is None`

在写代码的过程中，会对某些代码进行判空操作。比如有一个变量a，那么`if not a`和`if a is None`两者有区别吗？如果说没有区别，那么不管a为何值时，这两个判断语句会返回相同的结果，但事实是这样吗？一起看下面这段代码，体会一下对None的判空操作

```python
def fun():
return None

a =fun()
if not a: #逻辑运算
print('S')
else:
print('F')

if a is None:
print('S')
else:
print('F')


S
S
```

运行代码发现，结果是一样的，这是由于我们调用函数时，会返回None，那么此时两个判断语句返回的结果是一样的，但是如果我们将a的值换成一个空列表，会出现什么结果呢？

```python
def fun():
return None

a = []
if not a: #逻辑运算
print('S')
else:
print('F')

if a is None:
print('S')
else:
print('F')

S
F
```

运行结果，发现会打印不一样的值。那么这是为什么呢？对于not a它的意思相当于True，所以会打印出S，而a is None是比较运算，它们不属于同一种类型，因此会出现不一样的打印值。

==那么对于判空操作语法调用，我一般推荐这样操作==

==`If not a：`==

==通过这样一个判空操作，不管a是None还是空字符串、空列表或者布尔值，你都会得到想要的值。==

#### 3. None和False

很多时候，当我们运行if None和if False会得到相同的结果，但结果相同并不代表意义一样。

从类型层面上，False是布尔类型，而None是class 'NoneType'；从意义层面上，None表示不存在，而False表示真假。

#### 4. 对象存在并不一定是True

通过编写一个具体实例来进行说明，代码如下

```python
class Test():
def __len__(self):
return 0

test = Test()

if test: #存在
print('S')
else:
print('F')

F
```

所以说，永远不要认为对象实例化后一定会进入if分支中，即使实例化对象不取 None它也有可能进入else分支中。

我们可以用bool来说明一下原因，代码如下

```python
class Test():
def __len__(self):
return 0

test = Test()

print(bool(None))
print(bool([]))
print(bool(test))


if test: #存在
print('S')
else:
print('F')

False
False
False
F
```

可以直观的看出来，test的布尔值是False，所以它最终是会进入else分支的。所以，对于自定义的对象，千万不要认为只要对象存在就一定打印True。

#### 5.`__len__`与`__bool__`内置方法

那么对象到底是True还是False取决于类下面的内置方法，具体代码如下

```python
class Test():
# def __bool__(self):
# return False #不能返回整形，
def __len__(self):
return 0 #可以返回布尔值,特例


print(bool(Test()))

False
```

首先运行len方法，注释掉bool方法，我们会发现，如果len方法返回0，那么对象布尔值是False，如果返回其他数字则是True，但是len方法下面的return只能返回整形和布尔值，其他的返回值，比如字符串、浮点数，都会报错的，有兴趣的同学可以验证一下。

然后，再加入bool方法后，对象的布尔值则由bool方法确定，代码如下

```python
class Test():
def __bool__(self):
return False #不能返回整形，
def __len__(self):
return 0 #可以返回布尔值,特例

print(bool(Test()))

False
```

这里需要强调的是，bool类型的return只能返回False或True，为什么说这个呢？因为我们都知道，Python中False相当于0，True相当于1，但这里如果我们将False改为0，那么结果会出错，如下

```python
TypeError: __bool__ should return bool, returned int
```



### 参考

https://zhuanlan.zhihu.com/p/65193194

[python 中None，is和==的深入探讨 - 简书 (jianshu.com)](https://www.jianshu.com/p/627232777efd)

