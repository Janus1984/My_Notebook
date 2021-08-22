# python工程目录组织

关于如何组织一个较好的Python工程目录结构，已经有一些得到了共识的目录结构。在Stackoverflow的[这个问题](https://stackoverflow.com/questions/193161/what-is-the-best-project-structure-for-a-python-application)上，能看到大家对Python目录结构的讨论。

假设项目名为foo, 比较建议的最方便快捷目录结构这样就足够了:

```python
Foo/
|-- bin/
|   |-- foo
|
|-- foo/
|   |-- tests/
|   |   |-- __init__.py
|   |   |-- test_main.py
|   |
|   |-- __init__.py
|   |-- main.py
|
|-- docs/
|   |-- conf.py
|   |-- abc.rst
|
|-- setup.py
|-- requirements.txt
|-- README
```

1. `bin/`: 存放项目的一些可执行文件，当然可以起名`script/`之类的也行。
2. `foo/`: 存放项目的所有源代码。(1) 源代码中的所有模块、包都应该放在此目录。不要置于顶层目录。(2) 其子目录`tests/`存放单元测试代码； (3) 程序的入口最好命名为`main.py`。
3. `docs/`: 存放一些文档。
4. `setup.py`: 安装、部署、打包的脚本。
5. `requirements.txt`: 存放软件依赖的外部Python包列表。
6. `README`: 项目说明文件。

除此之外，有一些方案给出了更加多的内容。比如`LICENSE.txt`,`ChangeLog.txt`文件等，没有列在这里，因为这些东西主要是项目开源的时候需要用到。



### 关于README

**这个我觉得是每个项目都应该有的一个文件**，目的是能简要描述该项目的信息，让读者快速了解这个项目。

它需要说明以下几个事项:

1. 软件定位，软件的基本功能。
2. 运行代码的方法: 安装环境、启动命令等。
3. 简要的使用说明。
4. 代码目录结构说明，更详细点可以说明软件的基本原理。
5. 常见问题说明。

我觉得有以上几点是比较好的一个`README`。在软件开发初期，由于开发过程中以上内容可能不明确或者发生变化，并不是一定要在一开始就将所有信息都补全。但是在项目完结的时候，是需要撰写这样的一个文档的。



### 关于 requirements

python项目中必须包含一个 requirements.txt 文件，用于记录所有依赖包及其精确的版本号。以便新环境部署。

官方文档：

> Pip’s documentation states
>
> pip description
>
> freeze Output installed packages in requirements format.
>
> list List installed packages.
>

在虚拟环境中使用pip生成(否则会生成大量本地数据包，安装或升级包后，最好更新这个文件)：

````python
pip freeze >requirements.txt # 输出本地包环境至文件
````

当需要创建这个虚拟环境的完全副本，可以创建一个新的虚拟环境，并在其上运行以下命令：

```python
pip install -r requirements.txt # 根据文件进行包安装
```

需求文件requirements.txt的内容示例如下：

```txt
alembic==0.8.6
bleach==1.4.3
click==6.6
dominate==2.2.1
```



### 关于setup.py

一般来说，用`setup.py`来管理代码的打包、安装、部署问题。业界标准的写法是用Python流行的打包工具[setuptools](https://pypi.org/project/setuptools/)来管理这些事情。这种方式普遍应用于开源项目中。不过这里的核心思想不是用标准化的工具来解决这些问题，而是说，**一个项目一定要有一个安装部署工具**，能快速便捷的在一台新机器上将环境装好、代码部署好和将程序运行起来。

这个我是踩过坑的。

我刚开始接触Python写项目的时候，安装环境、部署代码、运行程序这个过程全是手动完成，遇到过以下问题:

1. 安装环境时经常忘了最近又添加了一个新的Python包，结果一到线上运行，程序就出错了。
2. Python包的版本依赖问题，有时候我们程序中使用的是一个版本的Python包，但是官方的已经是最新的包了，通过手动安装就可能装错了。
3. 如果依赖的包很多的话，一个一个安装这些依赖是很费时的事情。
4. 新同学开始写项目的时候，将程序跑起来非常麻烦，因为可能经常忘了要怎么安装各种依赖。

`setup.py`可以将这些事情自动化起来，提高效率、减少出错的概率。"复杂的东西自动化，能自动化的东西一定要自动化。"是一个非常好的习惯。

setuptools的[文档](https://setuptools.readthedocs.io/en/latest/)比较庞大，刚接触的话，可能不太好找到切入点。学习技术的方式就是看他人是怎么用的，可以参考一下Python的一个Web框架，flask是如何写的: [setup.py](https://github.com/pallets/flask/blob/master/setup.py)

当然，简单点自己写个安装脚本（`deploy.sh`）替代`setup.py`也未尝不可。



### 关于conf.py

注意，在上面的目录结构中，没有将`conf.py`放在源码目录下，而是放在`docs/`目录下。

很多项目对配置文件的使用做法是:

1. 配置文件写在一个或多个python文件中，比如此处的conf.py。
2. 项目中哪个模块用到这个配置文件就直接通过`import conf`这种形式来在代码中使用配置。

这种做法我不太赞同:

1. 这让单元测试变得困难（因为模块内部依赖了外部配置）。
2. 另一方面配置文件作为用户控制程序的接口，应当可以由用户自由指定该文件的路径。
3. 程序组件可复用性太差，因为这种贯穿所有模块的代码硬编码方式，使得大部分模块都依赖`conf.py`这个文件。

所以，我认为配置的使用，更好的方式是，

1. 模块的配置都是可以灵活配置的，不受外部配置文件的影响。
2. 程序的配置也是可以灵活控制的。

能够佐证这个思想的是，用过nginx和mysql的同学都知道，nginx、mysql这些程序都可以自由的指定用户配置。

所以，不应当在代码中直接`import conf`来使用配置文件。上面目录结构中的`conf.py`，是给出的一个配置样例，不是在写死在程序中直接引用的配置文件。可以通过给`main.py`启动参数指定配置路径的方式来让程序读取配置内容。当然，这里的`conf.py`你可以换个类似的名字，比如`settings.py`。或者你也可以使用其他格式的内容来编写配置文件，比如`settings.yaml`之类的。



### 关于main.py

`__name__ == '__main__'`是Python的`main函数`入口。并非说，加入这句才能使用`python xxx.py`来执行，而是说，这里可以判断，当前是否是直接被python调用执行。

`getopt`是一个包装方法，用以读取`main函数`后面跟着的参数。`getopt.getopt(args, options[, long_options])`有三个变量，args就是`python xxx.py`后面跟着的参数，通常就是`sys.argv`数组，不过我们一般会去除第一个元素，因为`sys.argv`的第一个元素，就是`文件名`本身。所以，我们的写法是`sys.argv[1:]`。

`options`是一个字符串，描述了需要解析哪些参数。如果一个参数，不需要跟变量，比如`-h`，那么直接使用参数名即可。如果一个参数需要传入变量，则在后面加`:`，比如`n:`。所以本案例中`hn:w:`的意思是，我们有三个参数，分别是`-h`, `-n`, `-w`，其中`-h`无需传入变量，而`-n`, `-w`需要传入变量。

`long_options`是一个字符串数组，也表示需要解析哪些参数。`long_options`是相对`options`而言的，我们在linux中，经常会看到一个命令的参数有多种写法，最常见的就是帮助参数，它有两种写法：`-h`, `--help`。前一种是就是我们的`options`，而后一种就是`long_options`。

假如我们有一个`--help`，那么在`long_options`中就是`['help']`。如果一个参数需要传入参数，比如`--name 'Good'`，那么在`long_options`中就是`['name=']`，是的，就是多一个`=`。

`getopt.getopt`返回一个元组(opts, args)，其中`opts`就是我们解析出来的参数，而`args`则是剩余没有解析的参数。`opts`是元组数组，每个元组，相当于key-value。`key`就是我们的参数名，而`value`就是参数的内容。

经典例子：

```python
# coding=utf-8

import getopt

import sys



if __name__ == '__main__':
    opts, args = getopt.getopt(sys.argv[1:], 'hn:w:', ['name=', 'word=', 'help'])
    name = 'No Name'
    word = 'Hello'
    for key, value in opts:
        if key in ['-h', '--help']:
            print'一个向人打招呼的程序'
            print'参数：'
            print'-h\t显示帮助'
            print'-n\t你的姓名'
            print'-w\t想要说的话'
			sys.exit(0)
		if key in ['-n', '--name']:
            name = value
		if key in ['-w', '--word']:
            word = value
        print'你好，我叫', name, '，', word
```

类class中调用的优先级：

1、`def__new__(cls):`

2、`def__init__(self):`

3、`def__call__(self, x):`



## 参考

https://zhuanlan.zhihu.com/p/36221226

