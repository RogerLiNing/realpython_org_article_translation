> 原文链接：https://realpython.com/python-string-formatting/
>
> 发布时间：2018-07-04
>
> 作者：Dan Bader
>
> 译者：Roger Lee



### 目录 

1. “旧式”字符串解析（%操作符）
2. “新式”字符串格式化（str.format）
3.  字符串插值/f-Strings（Python 3.6+）
4. 字符串模板（Python标准库）
5. 应该使用哪种字符串格式化方法？
6. 总结重点



你是还否记得Python之禅(The Zen of Python )中那条“一种明显的解决方案”？当你了解到在Python中竟然有四种主要的字符串格式化(string formating)方法时，你可能会感到困惑。



通过本教程，你将学会如何使用这四种主要的字符串格式化方法，并且了解它们的优缺点。以及你会知道如何根据经验法则（ simple rule of thumb）去选择最适合你程序的最合适且通用的字符串格式化方法。



前面已经讲了那么多，现在就直接开始吧！为了保证教程有一个简单的例子，假设你已经设置好了以下变量（或者常量）：



```python
>>>  errno = 50159747054
>>>  name = 'Bob'
```



基于以上的变量，你想要输入带有一个简单错误提示语的字符串：

```python
'Hey Bob, there is a 0xbadc0ffee error!'
```



该错误提示可能会影响开发者周一美好的早上。。。但是我们现在就是要讨论字符串格式化。让我们正式开始吧！





### 01 “旧式”字符串解析（%操作符）



在Python中，有一个独特的内建操作可以使用%操作符来操作字符串。它可以让你很轻松的做基于位置的字符串格式化。如果你使用过C语言中的 printf-style 函数，你马上就能理解它的工作原理。来看下面这个简单的例子：

```python
>>> 'Hello, %s' % name

"Hello, Bob"
```



这里我使用了 %s 格式说明符来告诉Python哪个位置应该替换成 name 的值，它代表了类型为字符串。



除了这个格式说明符，另外还有其他的格式操作符可供选择，让你可以控制输出的格式。例如，它可以让你更容易的将数字转成十六进制或者添加空白来生成一个整洁的格式化表格和报告。



看下面这个例子，你可以使用 %x 格式说明符把一个类型为 Int 的值转成 字符串 使它代表十六进制数：

```python
>>> '%x' % errno

'badc0ffee'
```



如果你想要在单个字符串里做多个替换的话，这个“旧式”字符串格式化语法就需要稍加改变。因为%操作符只能传入一个参数，你需要把右操作符放入一个元组中，就像这样：

```python
>>> 'Hey %s, there is a 0x%x error!' % (name, errno)

'Hey Bob, there is a 0xbadc0ffee error!'
```

假如你在字符串中给 % 操作符传入一个映射，它也能够让你通过变量名来替换：

```python
>>> 'Hey %(name)s, there is a 0x%(errno)x error!' % {

"name": name, "errno": errno }

'Hey Bob, there is a 0xbadc0ffee error!'
```



这样可以让你将来更简单方便的维护和修改的格式化字符串。你也不需要去担心你需要确保将值传入正确的位置，通过映射，值会自动的被放到正确的地方。 当然啦，它的缺点就是需要写很多代码。



我相信你一定感到疑惑为什么这个 printf-style 字符串格式化方法会被称为“旧式”字符串格式化。因为严格来说它已经被Python3的“新式”字符串格式化方法代替了。这也是我们接下来要讲的。





### 02 “新式”字符串格式化（str.format）



在Python3引入了一个新的字符串格式化的方法，并且随后支持了Python2.7。这个“新式”的字符串格式化方法摆脱了%操作符并且使得字符串格式化的语法更规范了。 现在时候通过调用字符串对象的.format() 方法进行格式化。



你可以使用 format() 来做简单的基于位置的字符串格式化，和你使用“旧式”格式化是一样的：

```python
>>> 'Hello, {}'.format(name)

'Hello, Bob'
```



或者你可以通过变量名来进行替换，且不用担心变量的位置。这个强大的特性可以在不改变format()的传入参数的情况下，允许重新调整显示的位置。

```python
>>> 'Hey {name}, there is a 0x{errno:x} error!'.format(     name=name, errno=errno)

'Hey Bob, there is a 0xbadc0ffee error!'
```



这个例子也说明了用来将 int 变量格式化成十六进制字符串的语法也不一样了。现在你需要通过添加 :x 后缀传入格式说明符。字符串格式化语法已经变得越来越强大，无需再将简单的用例复杂化。阅读官方文档**string formatting mini-language in the Python documentation。**



在Python 3中，这个“新式”字符串格式化被认为在 %-style上。同时“旧式”字符串格式化也已经不再被强调，它也没有被弃用。并且也支持最新的版本。根据Python开发的邮件和Python开发bug跟踪讨论中，在将来很长一段时间里也会继续使用 %-formating。



不过，在Python 3的官方文档中不太推荐使用“旧式”字符串格式化方法或者也没有提到很喜欢它：

> The formatting operations described here exhibit a variety of quirks that lead to a number of common errors (such as failing to display tuples and dictionaries correctly). Using the newer formatted string literals or the str.format() interface helps avoid these errors. These alternatives also provide more powerful, flexible and extensible approaches to formatting text.” (Source)



这也是为什么我个人在写新的代码时一直使用 str.format的原因。从Python 3.6 开始，目前又有了一个新的字符串格式化方法。我将在下个部分告诉你。





### 03 字符串插值/f-Strings(Python 3.6+)



在Python 3.6 中添加了一个新的字符串格式化方法，被称为字面量格式化字符串或者“f-strings”。这个新的方法让你能够在字符串常量中嵌入Python表达式。以下这个简单的例子让你对这个特性有一个初步的体验：

```python
>>> f'Hello, {name}!'

'Hello, Bob!'
```

你可以看到它在字符串前面放置了“f”作为前缀 - 因此被称为“f-strings”。这个新的格式化语法非常的强大。你可以使用任何Python表达式，甚至可以做内联计算。看这个例子：

```python
>>> a = 5

>>> b = 10

>>> f'Five plus ten is {a + b} and not {2 * (a + b)}.'

'Five plus ten is 15 and not 30.'
```



格式化字符串字面量是Python的解析特性，它可以把 f-strings转成一连串的字符串常量和表达式。它们随后在一起组合成最终的字符串。

设想你有以下这个函数 greet()，它包含了f-string：

```python
>>> def greet(name, question):

...     return f"Hello, {name}! How's it {question}?"

...

>>> greet('Bob', 'going')

"Hello, Bob! How's it going?"
```





当你分解函数并检查代码执行时发生什么事情时，你会发现函数中的f-string实际上被转成了和以下相似的情况：

```python
\>>> def greet(name, question):

...    return "Hello, " + name + "! How's it " + question + "?"
```

真正运行的时候是比这个快很多的因为它使用了*BUILD_STRING opcode as an optimization* 中提到的优化。但是功能层面从它们是一样的：

```python
>>> import dis

>>> dis.dis(greet)  

    2      0 LOAD_CONST               1 ('Hello, ')              

            2 LOAD_FAST                    0 (name)              

            4 FORMAT_VALUE            0              

            6 LOAD_CONST                2 ("! How's it ")              

            8 LOAD_FAST                    1 (question)             

            10 FORMAT_VALUE           0             

            12 LOAD_CONST               3 ('?')             

            14 BUILD_STRING             5             

            16 RETURN_VALUE
```



字符串字面量同时也支持现有的 str.format() 字符串格式化方法。这样就能解决我们上次遇到的同一个格式化问题：

```python
>>> f"Hey {name}, there's a {errno:#x} error!"

"Hey Bob, there's a 0xbadc0ffee error!"
```

Python的新格式字符串字面量和JavaScript在ES2015里添加的模板字面量类似。我认为对于Python来说就是如虎添翼，我也早就在日常工作中写Python3代码时使用它们了。你也可以在 in-depth Python f-strings tutorial 学习更多关于格式化字符串字面量的内容。





### 04 字符串模板（Python标准库）



在Python里还有另一个字符串格式化工具：模板字符串。它是一个更简单，也不太强大的方法，但是在某些情况下恰恰是你想要的。



让我们来看以下这个欢迎词例子：

```python
>>> from string import Template

>>> t = Template('Hey, $name!')

>>> t.substitute(name=name)

'Hey, Bob!'
```



你可以看到我们需要先从Python的内建 string 模块中导入 Template 类。模板字符串并不是核心的语言特征，但是它们由Python标准库的string提供的。



另外一个不同的地方是这个模板字符串不支持使用格式说明符。所以想要让先前的错误提示信息能够使用，你还需要手动转换这个int 错误号码为十六进制字符串：

```python
>>> templ_string = 'Hey $name, there is a $error error!'

>>> Template(templ_string).substitute(

...     name=name, error=hex(errno))

'Hey Bob, there is a 0xbadc0ffee error!'
```

顺利运行！

但是该什么时候才在你的代码中使用模板字符串呢？在我看来，使用模板字符串的最佳的时机就是当你的程序需要处理由用户提供的输入内容时。模板字符串是最保险的选择，因为可以降低复杂性。

其他一些复杂的字符串格式化技巧的可能会给你的程序带来安全漏洞，例如，格式化字符串可以访问你程序里任意的变量。

这意味着，如果一个恶意用户可以提供一个格式化字符串，他们就有可能泄露安全密匙以及其他敏感的信息！下面是一个简单的例子证明这些可能可以用来影响你的代码：

```python
>>> # This is our super secret key:

>>> SECRET = 'this-is-a-secret'

>>> class Error:

...      def __init__(self):

...          pass

>>> # A malicious user can craft a format string that

>>> # can read data from the global namespace:

>>> user_input = '{error.__init__.__globals__[SECRET]}'

>>> # This allows them to exfiltrate sensitive information,

>>> # like the secret key:

>>> err = Error()

>>> user_input.format(error=err)

'this-is-a-secret'
```





看到攻击者如何通过从恶意的格式化字符串访问__globals__ 字典并获取我们安全密匙了吗？是不是很可怕？模板字符串关闭了这个攻击载体。如果你的程序会处理来自用户的输入内容，这使得它是一个更安全的选择

```python
>>> user_input = '${error.__init__.__globals__[SECRET]}'

>>> Template(user_input).substitute(error=err)

ValueError:

"Invalid placeholder in string: line 1, col 1"
```





### 05 应该使用哪种字符串格式化方法？



我完全能理解Python中有那么多字符串格式化可供选择的带来的困惑。来看下面我给你们准备的选择路程图：



![img](http://img.xiumi.us/xmi/ua/19nZN/i/4ecf0148fd8765f8b3521922f47dff14-sz_29902.png)

Python字符串格式化经验法则

这个流程图是基于我在写Python时会用到的经验法则：

**Python字符串格式化经验法则：**如果你的格式化字符串是由用户提供的，那么就是用模板字符串（#4）避免安全问题。不然如果是Python 3.6+的话，就使用字符串插值/f-Strings，如果不是就使用“新式”字符串格式化（str.format）。

### 06 总结重点



● 也许感到惊讶，Python在处理字符串格式化时不只有一种方法。

● 每个方法都有其优缺点。你应该根据你的用例来选择合适的方法

● 如果你在决定该使用哪个字符串格式化方法时感到困难，试试我们的**Python字符串格式化经验**法则。