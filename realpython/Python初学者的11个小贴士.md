> 原文链接：https://realpython.com/python-beginner-tips/
>
> 发布时间：2018-04-03
>
> 作者：Krishelle Hardson-Hurley
>
> 译者：Roger Lee

### 目录

- 持之以恒
  - 贴士 #1: 坚持每日敲代码
  - 贴士 #2: 烂笔头
  - 贴士 #3: 使用交互模式！
  - 贴士 #4: 学会休息
  - 贴士 #5: 成为Bug赏金猎人

- 合作学习
  - 贴士 #6: 与志同道合者结伴而行
  - 贴士 #7: 教别人
  - 贴士 #8: 对结编程
  - 贴士 #9: 正确的提问方式

- 尝试做点东西
  - 贴士 #10: 做点东西，啥都行
  - 贴士 #11: 为开源项目做贡献

- 开始行动吧!




我们非常的兴奋，你终于决定踏上学习Python之旅了！我们最常收到读者的提问就是“学习Python最好的方法是什么？”

我认为学习任何语言的第一步都应该是确保你理解该*如何*去学习。学习如何去学是计算机编程中最关键的技能。

为什么如何去学习是如此重要的呢？答案其实很简单：随着编程语言的发展、各种库的创建以及编程工具的升级。知道如何学习对于不断了解这些新的改变和成为一个成功的程序员是至关重要的。

在本文教程中，我们会提供不同的学习策略来助你启动成为Python编程巨星的旅程！



**持之以恒**

作为一个名新手Python程序员，下面的这些贴士是你应该学习和遵守的概念：

### 贴士 #1: 坚持每日敲代码

 在学习一门新的编程语言时，连贯性是非常重要的。我们建议你应该下决心每天都敲代码。这也许很难相信，但是在编程里肌肉记忆是非常重要的。下决心每天都敲代码能够帮助强化肌肉记忆。尽管开始的时候会感到困难，每天坚持花25分钟编程，一定能到达成功的顶点。

### 贴士 #2: 好记性不如烂笔头

随着你在编程的道路上不断地前行，你可能会疑惑是否在学习的时候做笔记。是的，你应该做笔记！事实上，研究表明，动手做笔记是对增强长期记忆最有用的方法。特别是对那些立志成为全职开发者的小伙伴来说是非常受益的，因为很多公司在面试的时候要求在白板上写代码。



一旦你开始着于一些小的项目或者程序，手写代码也能够在你在计算机上编写代码前帮助你构思你的代码。如果你提前手写那些你所需要的函数和类以及它们的交互逻辑，会让你省下大量的时间。

### 贴士 #3: 善用交互模式命令行！

不管你是刚开始学习Python基础的数据结构（字符串、列表、字典等等）还是在调试一个应用程序，Python的交互模式命令行将是你最好的学习工具之一。

在使用Python交互模式命令行（有时也被称为[Python REPL](https://realpython.com/interacting-with-python/)）之前，需要确保你电脑已经安装了Python。我们已经写了一个教程来帮助你安装Python了。要激活Python交互模式，只需要打开你的终端，然后输入python或者python3执行，这也取决于你的安装路径。

现在你知道了如何启动命令行，接下来展示几个例子让你知道在学习的时候如何使用它：



**使用dir()来查看可以对一个元素进行什么样的操作：**

```python
>>> my_string = 'I am a string'

>>> dir(my_string)

['__add__', ..., 'upper', 'zfill']  # 为可读性做了截取
```





注意到我们调用了upper()方法。你明白它能做什么了吗？它让字符串里所有的字母都变成了大写！在“Manipulating strings” 教程中学习更多关于这些内建方法。



**了解元素的类型**

 ```python
>>> type(my_string)

str
 ```

**通过内建帮助系统获取完整的使用文档：**

```python
>>> help(str)
```

**导入库并使用：**

```python
>>> from datetime import datetime

>>> dir(datetime)

['__add__', ..., 'weekday', 'year']  # 为可读性做了截取
>>> datetime.now()

datetime.datetime(2018, 3, 14, 23, 44, 50, 851904)
```

**运行终端命令：**

```python
>>> import os

>>> os.system('ls')

python_hw1.py python_hw2.py README.txt
```

### 贴士 #4: 劳逸结合

当你在学习的时候，短暂的停下和吸收所学内容是至关重要的。番茄时间管理法是一个广泛使用并且能够帮助你的东西：在进行25分钟的学习之后，做短暂的休息，然后再重复步骤。做笔记是高效学习的重要手段，特别是在学习大量新知识的时候。

当你在调试的时候，休息特别的重要。如果你碰到一个bug并且不知道哪里出错，就休息一下。起身离开电脑，散一下步或者和朋友聊天。

在编程的时候，你的代码必须跟遵守程语言的规范和逻辑。因为即使是缺少了一个引号都会影响所有。用新的目光看待旧的事物效果大不相同。

### 贴士 #5: 成为Bug赏金猎人

说到bug,只要你开始编写复杂的程序，不可避免的会出现bug。而且每个人都会遇到！不要让bug困扰你，相反的，你应该自豪的拥抱这些时刻，并且把自己想象成bug赏金猎人。

关于调试，找到一个科学的方法来检查出问题的地方是非常重要的。从执行顺序上过一遍你的代码，确保每一个部分是最好的方式。

只要你想到了哪里可能会出现问题，在你的脚本里写入下面这行代码 *import pdb; pdb.set_trace()* 并运行它。这就是Python 调试器 ，它会使你的脚本进入交互模式。调试器也能够在命令行运行 *python -m pdb <我的文件.py>*。

## 合作学习

一旦你进入了坚持的状态，通过合作可以加速你的学习进度。下面是一些如何帮助你和他人合作加强学习效率的几个建议。

### 贴士 #6: 与志同道合者结伴而行

虽然编程看似一个独自一人的行为，但实际上如何一起学习效果更好。如果你在学习Python的时候周围也有小伙伴在一起学习是极其重要的。这样就可以在学习的过程中大家相互分享各自所学到的小贴士和小技巧。



也不要担心你没有认识的人。因为有很多种途径可以结交哪些热爱学习Python的小伙伴。找本地的活动、会面或者加入PythonistaCafe - 像你一样的一对一的Python爱好者学习社区。

### 贴士 #7: 教授知识

据说学习最好的方法就是去教会别人。尤其是你学Python的时候特别对。有很多方法可以实现：和其他Python爱好者共享白板、写博客总结最新学到的知识和概念、记录视频解释你学到的东西或者简单的在电脑上对你自己说话。以上的每一个方法都能加强你对知识的理解并很好的知道你理解的差距。

### 贴士 #8: 对结编程

对结编程是指两个开发者共同在一个工作站里完成一项任务。这两个开发者在“司机”和“导航员”之间切换。“司机”负责编写代码，而“导航员”则负责在代码编写的过程中问题的解决和审查代码。经常切换不同的角色双方都可以受益。

对结编程有很多好处：它不仅可以有机会让别人审查你的代码，而且还能知道别人在同一个问题上的不同见解。在不同的想法和思考的方法环境下，有助于提升在你独自一人编程的时候解决问题的能力。

### 贴士 #9: 正确的提问方式

人们总说世上无“差劲的问题”这种东西，但是提到编程，就很有可能会提一个非常差劲的问题。特别当你求助于一个对该问题仅有一点或者没有理解背景的人帮你解决问题时。最好的提问方式应该遵从以下首字母缩写：

**G：**写出你目前所做的编程背景，详细的描述问题。

**O：**列出你已经尝试的解决办法。

**O：**提出你认为这个问题产生的猜测。这样有助于帮助你的人知道你的想法，以及能够知道你自己已经想到的想法。

**D：**展示发生的问题。包括代码、追溯的错误信息和解释你所执行的每一步。只有这样，帮助你的人才不需要再重新复现这个问题。

好的提问方式可以节省很多时间。跳过这些步骤可能会造成引起冲突的反复对话。作为一个新手，你一定要确保你提出好的问题，这样可以锻炼你交流的思考过程，最重要的是帮助你的人才会更乐意继续帮助你。

## 尝试做点东西

### 贴士 #10: 做点东西，啥都行

对于新手，有很多可以用来增强对学Python信心和我们之前提到肌肉记忆的小练习。只要你掌握基本的数据结构（字符串、列表、字典和元祖）、面向对象编程和编写类，你就可以开始构建一个程序了。

你所构建的程序并没有你如何编写它重要。编写的过程才是你学到最多的时候。你从Real Python 文章和课程学到的东西是有限的。你大部分的学习都来自于你使用Python去构建的过程。你都能从你所解决的每一个问题学到很多东西。

有很多新手可以用来练手的项目。以下可供你参考：

● 猜数字游戏

● 简单的计算器

● 筛子模拟器

● 比特币价格通知服务

如果你觉得还是很难找到一个练手的项目，看这个视频。它里面讲了当你感到困惑的时候如何产生上千个项目想法。

### 贴士 #11: 为开源项目做贡献

在开源的模式下，软件的源代码是公开的，并且任何人都可以协作。Python有很多的开源库项目并且支持让任何人做出贡献。另外，很多公司也发布了开源项目。这意味着你可以和这些公司编写代码的工程师一起合作。

对一个Python开源库做出贡献能够对你的学习经历产生巨大的价值。比如说，你决定去提交一个修复bug的请求：你提交了一个用来给你修复你代码bug的“pull request”。 

然后，项目的管理员会审查你的代码，提供评论和建议。这不仅可以让你更好的锻炼你的Python编程技巧，而且能锻炼如何与其他程序员沟通。

### 开始行动吧!

现在你已经学习了这些学习策略，你已经准备好开始学习Python的旅程了！

享受编程吧！

