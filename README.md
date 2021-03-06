![](./image/caliburn.png)
### 缘起

2012年，我在研究最大熵模型时，第一次接触到了python, 而正是这惊鸿一瞥，让我对它有了莫名的好感。

虽然工作中主要使用C语言，但在日志分析中，python却发挥着重要作用。也仅限于寥寥几行的python代码，自己终究未能驾驭它。尤其最近一年，我不禁感慨自己遇到了瓶颈。

当前自己可以根据需求来写出符合功能要求的python代码，并交付一个可靠的模块，但是自己的能力似乎也就到此为止了。但我深刻地意识到与其他高手的水平相差很大。

终于在GITHUB上遇到了[wangshunping](https://github.com/wangshunping), 两人有非常多的相似，并深受启发。

于是，自己也开始向大师学习，学习其代码中的精髓。

记得大学时代，教我们《人工智能》及《专业英语》的老师，向我们讲述了他的学习英文写作的经历：
自己把《参考消息》中的翻译成中文的报道，再用自己方式翻译成英文，与原作者的英文报道进行对比。一遍又一遍，一天又一天，终于在英语学习上，克服了瓶颈，获益良多。后来他总结说是把AI中的监督学习用在了英文写作。

于是该怎么做， 我也茅塞顿开。于是就有了本系列学习笔记。


### 目的

让自己的代码更加Pythonic

帮助他人，学习Python代码


### HOW
以下项目资源列表，由[Dongmingwei](https://zhuanlan.zhihu.com/p/22275595?refer=python-cn)整理，也非常符合自己的学习之路。因此记录下来。

入门项目
1. [pip-pop](https://github.com/kennethreitz/pip-pop): Tools for managing requirements files.

2. [envoy](https://github.com/kennethreitz/envoy): Python Subprocesses for Humans™.

3. [delegator.py](https://github.com/kennethreitz/delegator.py.git) Delegator.py is a simple library for dealing with subprocesses for Humans 2.0, inspired by both envoy and pexpect (in fact, it depends on it!).

4. [records](https://github.com/kennethreitz/records): SQL for Humans™

5. GitHub - mitsuhiko/pluginbase: A simple but flexible plugin system for Python.

6. GitHub - mitsuhiko/pipsi: pip script installer

7. GitHub - mitsuhiko/unp: Unpacks things.

8. GitHub - chrisallenlane/cheat

9. GitHub - jek/blinker: A fast Python in-process signal/event dispatching system.

10. GitHub - mitsuhiko/platter: A useful helper for wheel deployments.

11. GitHub - kennethreitz/tablib: Python Module for Tabular Datasets in XLS, CSV, JSON, YAML, &c.

12. [docopt](https://github.com/docopt/docopt.git): Creates beautiful command-line interfaces.

进阶项目

1. faif/python-patterns。使用Python实现一些设计模式的例子。

2. pallets/werkzeug。flask的WSGI工具集。其中包含了实现非常好的LocalProxy、cached_property、import_string、find_modules、TypeConversionDict等。

3. bottlepy/bottle。阅读一个Web框架对Web开发就会有更深刻的理解，flask太大，bottle就4k多行，当然如果你有毅力和兴趣直接看flask是最好了的。

4. msiemens/tinydb。了解用Python实现数据库。

5. coleifer/peewee。了解ORM的实现。

6. pallets/click。click已经内置于在flask 0.11里，提供命令行功能，值得阅读。

7. mitsuhiko/flask-sqlalchemy。了解一个flask插件是怎么实现的。

除此之外Web开发者可以阅读一些相关的项目：

1. runscope/httpbin。使用flask，网站是httpbin(1): HTTP Client Testing Service。

2. jahaja/psdash。使用flask和psutils的获取Linux系统信息的面板应用。

3. pallets/flask-website。 flask官方网站应用。

4. pypa/warehouse。如果你使用pyramid，这个新版的PYPI网站，可以帮助你理解很多。

当然，2个学习flask重要的资源必须爆一爆：

1. GitHub - realpython/discover-flask: Full Stack Web Development with Flask。

2. The Flask Mega-Tutorial。 这个就是《Flask Web开发：基于Python的Web应用开发实战》的原始博客。

500lines

推荐一个非常厉害的项目 GitHub - aosabook/500lines: 500 Lines or Less, 它里面包含了22个由该领域的专家完成，用不到500行的代码实现一个特定功能的子项目。连Guido van Rossum都亲自来写基于asyncio爬虫了，Nick Coghlan、ajdavis也出场了。

### 贡献

如果你对文章的内容有建议和观点，欢迎PR给我，我尽可能的merge进来，把你添加到贡献名单中。

最后，功不唐捐。

### 感谢

[Wangshunping](https://github.com/wangshunping)

[Dongmingwei](https://zhuanlan.zhihu.com/p/22275595?refer=python-cn)

