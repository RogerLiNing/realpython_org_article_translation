- [简要概括](https://realpython.com/absolute-vs-relative-python-imports/#a-quick-recap-on-imports)
  - [工作原理](https://realpython.com/absolute-vs-relative-python-imports/#how-imports-work)
  - [语法](https://realpython.com/absolute-vs-relative-python-imports/#syntax-of-import-statements)
  - [规范](https://realpython.com/absolute-vs-relative-python-imports/#styling-of-import-statements)
- [绝对导入](https://realpython.com/absolute-vs-relative-python-imports/#absolute-imports)
  - [语法和实例](https://realpython.com/absolute-vs-relative-python-imports/#syntax-and-practical-examples)
  - [优缺点](https://realpython.com/absolute-vs-relative-python-imports/#pros-and-cons-of-absolute-imports)
- [相对导入](https://realpython.com/absolute-vs-relative-python-imports/#relative-imports)
  - [语法和实例](https://realpython.com/absolute-vs-relative-python-imports/#syntax-and-practical-examples_1)
  - [优缺点](https://realpython.com/absolute-vs-relative-python-imports/#pros-and-cons-of-relative-imports)
- [总结](https://realpython.com/absolute-vs-relative-python-imports/#conclusion)



如果你曾写过包含有一个文件以上的项目，你可能会使用过`import`语句。对于写过多个项目的Python老鸟来说，<ruby>
导入<rt style="font-size: 16;color: green"> import </rt>
</ruby>也会让他们费解。而你正在阅读这篇教程的原因有可能是因为你想要更深入的了解Python的导入 ，特别是在绝对和相对导入方面。

通过阅读本教程，你将能了解到这两种方式的不同之处,以及其优缺点。让我们开始吧！



### 简要概括

你需要对Python的，<ruby>
模块<rt style="font-size: 16;color: green"> module</rt>
</ruby>和<ruby>
包<rt style="font-size: 16;color: green"> package</rt>
</ruby>有一个良好的理解才能更好的明白导入的工作原理。一个Python模块实际上就是一个文件，它的文件格式为`.py` 。一个Python包就是一个<ruby>
文件夹<rt style="font-size: 16;color: green"> folder</rt>
</ruby>，里面含有模块文件（在Python 2中，这个文件夹要有一个`__init__.py`文件）。

当你在一个模块中写的代码需要使用到其他模块或者包的代码要怎么办？导入它！



##### 工作原理

但是这个导入到底是如何工作的呢？假如你导入了一个模块，代码如下：

```python
import abc
```

Python首先要做的就是在`sys.modules`中查找这个`abc`名称。它是先前曾被导入过的所有模块的缓存。简单来说，就是之前被导入过的模块，都被暂时保存在里面。

如果在这个缓存中找不到这个名称，Python接下来会去<ruby>
内置的模块 <rt style="font-size: 16;color: green"> built-in modules</rt>
</ruby>中查找。这些内置模块是Python预装的，可以在Python标准库中查看详情。假如还是没能在内置模块中找到它，Python将会去`sys.path` 定义的文件夹列表中搜索。通常来说，这个列表会包括当前目录，并且会先在里面搜索。

当Python找到了模块，它会将这个模块绑定到局部作用域。这就表示当前这个                                                                                                                                                                `abc`已经被定义了并且在被当前文件使用而不会抛`NameError`的异常。

如果这个模块名没有被找到，有就会抛出`ModuleNotFoundError`这个异常。你可以在Python的官方文档找到更多内容。



> 注意 ：安全问题
>
> 要注意当前的导入系统有一些重大的安全风险。这是大部分是由于Python本身的灵活性。例如缓存的模块是可写并且有可能可以通过导入系统重写Python的核心函数。从第三方包中导入也会让你的应用暴露于安全隐患中。
>
> 以下是一些有用的资源关于这些安全隐患，并且关于如何解决：
>
> - 10个常见的Python陷阱以及如何避免（https://hackernoon.com/10-common-security-gotchas-in-python-and-how-to-avoid-them-e19fbe265e03）
> - #168节：10个Python安全漏洞以及如何修补（https://talkpython.fm/episodes/show/168/10-python-security-holes-and-how-to-plug-them）



##### 语法

现在你已经了解导入的工作原理了，让我们来看一下它的语法吧。你可以导入包和模块。（要注意一下，导入一个包的时候，实际上就是导入包里面的`__init__.py`作为模块）你也可以从一个包或者模块中导入指定的对象。

一般有两种导入的方法。当你使用第一个，你可以直接导入该资源，如下：

```python
import abc
```

`abc`可以是一个包或者模块

当你使用第二种语法，你从其他包或者模块中导入资源。看下面这个例子：

```python
from abc import xyz
```

`xyz`可以是一个模块、<ruby>
子包<rt style="font-size: 16;color: green"> subpackage</rt>
</ruby>、<ruby>
对象<rt style="font-size: 16;color: green"> object</rt>
</ruby>，例如<ruby>
类<rt style="font-size: 16;color: green"> class</rt>
</ruby>或者<ruby>
函数<rt style="font-size: 16;color: green"> function</rt>
</ruby>。

你也可以选择重命名导入的资源，如下：

```python
import abc as other_name
```

这会在脚本中重命名这个已经导入的模块`abc`为`other_name`。现在必须使用`other_name`进行引用，不然就不被识别。



##### 规范

PEP8 是Python的官方编码规范，里面有几个点也是适用于导入规范，以下是总结：

1. 导入应该总是写在最前面，但需尾随任何模块单行注释和文档注释。
2. 导入应该根据导入的内容进行分类，一般有三种：
   - 导入标准库（Python的内置模块）
   - 导入相关的第三方包（不属于当前应用的第三方包）
   - 导入本地应用的模块（属于当前应用的模块）
3. 每一组的导入都应该用空白行分隔



请看下面这个例子：

```python
"""展示一个标准的导入规范

注意，导入语句应该位于文档注释之后

"""

# 导入标准库
import datetime
import os

# 导入第三方库
from flask import Flask
from flask_restful import Api
from flask_sqlalchemy import SQLAlchemy

# 导入本地模块
from local_module import local_class
from local_package import local_function

```

以上的导入语句被分成了三个部分，通过空白行分隔。并在每一个部分中，是根据字母排序的。



### 绝对导入

你已经了解到了如何写导入语句并且像一个专家一样知道如何写规范的导入语句。现在是时候学习关于绝对引入的内容了。

绝对导入通过使用被导入资源在项目根目录的完整路径进行导入。



##### 语法与实例

假如你有以下目录结构：

```shell
└── project
    ├── package1
    │   ├── module1.py
    │   └── module2.py
    └── package2
        ├── __init__.py
        ├── module3.py
        ├── module4.py
        └── subpackage1
            └── module5.py
```

这里有个目录`project`，它包含了两个子目录：`package1`和`package2`。其中`package1`有两个文件：`module1.py`和`module2.py`。

`package2`目录有三个文件：两个模块, `module3.py`和`module4.py`，也有一个初始化文件 `__init__.py`。并且也包括一个目录,`subpackage`，它包含一个文件，`module5.py`。



我们假设以下内容：

1. `package1/module2.py`有一个函数，叫`function1`
2. `package2/__init.py`有一个类，叫`class1`
3. `package2/subpackage1/module5.py`有一个函数，叫`function2`



以下是绝对导入的例子：

```python
from package1 import module1
from package1.module2 import function1
from package2 import class1
from package2.subpackage1.module5 import function2
```

要注意你必须在<ruby>
顶级包目录<rt style="font-size: 16;color: green"> top-level package</rt>
</ruby>下提供每个包或者文件具体的路径。某种程度上和其文件路径相似，但是我们会使用<ruby>
点<rt style="font-size: 16;color: green"> dot</rt>
</ruby>(.)，而不用<ruby>
斜线<rt style="font-size: 16;color: green"> slash</rt>
</ruby>(/)。



##### 优缺点

应该优先考虑使用绝对路径，因为其更简单明了。使用它后，仅通过导入语句，就知道资源是从哪里导入的。而且，即使当前位置的导入语句改变了，绝对导入还是会保持有效。并且事实上，PEP8 推荐使用绝对导入。

当然，有时候绝对路径会变得冗长，取决于目录结构的复杂程度。想象一下以下这个语句：

```python
from package1.subpackage2.subpackage3.subpackage4.module5 import function6
```

这是不是很可笑？幸运的是，相对导入在这种情况下是一个绝佳的选择！



### 相对导入

相对导入指定了被导入资源是相对于当前的位置 - 也就是，这个位置就是导入语句所在的地方。有两种类型的相对导入：隐式和显式。隐式相对导入已经在Python3中被弃用了，所以这里我就不多讲了。



##### 语法和实例

相对导入的语法取决于当前的位置和被导入模块、包以及对象的位置。以下是一些例子：

```python
from .some_module import some_class
from ..some_package import some_function
from . import some_class
```

你能看到至少有一个点在每一个导入语句的前面。相对导入利用点符号来指定位置。

单个点表示模块或者包的引用是在同一个位置的同一个目录下。两个点表示它是在当前位置的父目录中 - 意思是指上一级目录。三个点表示它位于祖父母目录中，以此类推。如果你使用类Unix系统的话，一定有熟悉的感觉！



假设你有和之前一样的目录结构：

```shell
└── project
    ├── package1
    │   ├── module1.py
    │   └── module2.py
    └── package2
        ├── __init__.py
        ├── module3.py
        ├── module4.py
        └── subpackage1
            └── module5.py
```

这里有个目录`project`，它包含了两个子目录：`package1`和`package2`。其中`package1`有两个文件：`module1.py`和`module2.py`。

`package2`目录有三个文件：两个模块, `module3.py`和`module4.py`，也有一个初始化文件 `__init__.py`。并且也包括一个目录,`subpackage`，它包含一个文件，`module5.py`。



重温以下内容：

1. `package1/module2.py`有一个函数，叫`function1`
2. `package2/__init.py`有一个类，叫`class1`
3. `package2/subpackage1/module5.py`有一个函数，叫`function2`



你可以通过以下方法在`package1/module1.py文件中导入`导入`function1`：

```python
# package1/module1.py

from .module2 import function1
```

你在这里只需要使用一个点，因为`module2.py`和当前的模块`module1.py`是在同一个路径下面。

你也可以在`package2/module3.py`中导入`class1`和`function2`通过以下方法：

```python
# package2/module3.py

from . import class1
from .subpackage1.module5 import function2
```

在第一个导入语句中，单个点代表你从当前包中导入`class1`。要谨记，导入一个包实际上是导入包里的`__init__.py`文件作为模块。

第二个导入语句中，你再次使用了单个点，这是因为`subpackage1`和当前模块`module3.py`是在同一个目录中。



##### 优缺点

相对导入最明显的优点就是非常简洁。取决于当前的位置，它可以将之前那可笑的冗长语句缩减到以下：

```python
from ..subpackage4.module5 import function6
```

不幸的是，相对导入可能会引起混乱，特别是一些目录结构可能会改变的共享项目。且相对导入不像绝对导入那样可读，不能轻易的从导入语句中查看资源被导入的位置。



### 结论

好样的！你学完了这个关于绝对导入和相对导入<ruby>
速成课<rt style="font-size: 16;color: green"> crash course </rt>
</ruby>。你现在已经掌握了导入的工作原理。并且你也学到了编写导入语句的最佳实践，以及了解了绝对导入和相对导入的异同之处。

现在你可以用你刚刚学到的新技能自信满满的在Python中导入标准库、第三方包和你自己的本地包了。要记住，一般情况下，你应该选择使用绝对导入而不使用相对导入，除非路径非常的复杂，不然会使导入语句冗长。



### 作者

Hi there, I’m Mbithe! I’m an experienced software engineer with interests in artificial intelligence and machine learning. I’m currently a postgraduate student at The University of Manchester, studying Advanced Computer Science with a specialisation in AI.



大家好,我是Mbithe! 我是一个资深的软件开发工程师，我喜欢人工智能和机器学习。我目前在<ruby>
曼彻斯特大学<rt style="font-size: 16;color: green"> The University of Manchester </rt>
</ruby>读研，学习<ruby>
高级计算机科学<rt style="font-size: 16;color: green"> Advanced Computer Science </rt>
</ruby>，主攻人工智能。