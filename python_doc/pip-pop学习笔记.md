# pip-pop学习笔记

作者：[Kenneth Reitz](https://www.kennethreitz.org/)

![](../image/kennethreitz.jpg)

目前为止， pip-pop提交了41个commit, 看来学习会稍微简单一些。

该库包含两个小工具：pip-diff 和 pip-grep



## 简介
Python项目中必须包含一个 requirements.txt 文件，用于记录所有依赖包及其精确的版本号。以便新环境部署。也正是因此，平时需要处理很多requirements.txt文件，令人烦恼。所以K神就自己搞了这个小工具
文件目录

=======bin

&emsp;　|___ pip-diff.py  : 比较给定的两个requirements文件的不同，列出 stale or fresh packages.

&emsp;　|___ pip-grep.py  : 在给定的一个requirements文件中，搜索指定的package

=======tests

&emsp;　|___ test-requirements.txt   用于测试的requirements文件

&emsp;　|___ test-requirements2.txt  用于测试的requirements文件

.gitignore :github过滤的配置文件

.travis.yml：持续集成travis的配置文件

LICENSE

README.rst

requirements.txt

setup.py ：打包工具

tox.ini ：openstack的测试工具配置文件


## 开发历程

 * Jul 23, 2014（第一天）：主要是初始化工程，包括License文件， Readme，requirement,setup.py等文件。从这一开发过程来看，还是属于RDD（Readme Driven Develop)方法. 而这与公司推行的敏捷开发方法大体相同。不过Github中的项目文档要求更加简洁化。另外markdown是写文档的利器。

 * Jul 25, 2014：pip-diff工具开发完毕，后又经过部分修改，在Jul 30, 完成diff工具

 * Aug 1, 2014 ~ Aug 22, 2014: 完成pip-grep，至此第一个v0.1.0版本完成

 * 后续每年也就只有3或5个更新，版本变化不大，毕竟此库相对比较简单

## 代码剖析
注：删除部分代码，便于理清代码结构
### pip-diff
核心类：

    class Requirements(object):
    
    def __init__(self, reqfile=None):
        super(Requirements, self).__init__()
        self.path = reqfile
        self.requirements = []

        if reqfile:
            self.load(reqfile)

    def load(self, reqfile):
        """ 主要是获得该requirement文件中的依赖包， 注意不统计被注释的行"""
        if not os.path.exists(reqfile):
            raise ValueError('The given requirements file does not exist.')

        with open(reqfile) as f:
            data = []

            for line in f:
                line = line.strip()

                # Skip lines that start with any comment/control charecters.
                if not any([line.startswith(p) for p in IGNORABLE_LINES]):
                    data.append(line)

            for requirement in parse_requirements(data):
                self.requirements.append(requirement)


    def diff(self, requirements, ignore_versions=False):
        """ 统计出两个requirements文件的 fresh及stale依赖包"""
        r1 = self
        r2 = requirements
        results = {'fresh': [], 'stale': []}

        # Generate fresh packages.
        other_reqs = (
            [r.project_name for r in r1.requirements]
            if ignore_versions else r1.requirements
        )

        for req in r2.requirements:
            r = req.project_name if ignore_versions else req

            if r not in other_reqs:
                results['fresh'].append(req)

        # Generate stale packages.
        other_reqs = (
            [r.project_name for r in r2.requirements]
            if ignore_versions else r2.requirements
        )

        for req in r1.requirements:
            r = req.project_name if ignore_versions else req

            if r not in other_reqs:
                results['stale'].append(req)

        return results

对外接口：

    提供diff接口，注意该接口与Requirements类中的接口名相同。PS: 不知道为何这样命名？
    def diff(r1, r2, include_fresh=False, include_stale=False):
        try:
            r1 = Requirements(r1)
            r2 = Requirements(r2)
        except ValueError:
            print 'There was a problem loading the given requirements files.'
            exit(os.EX_NOINPUT)

        results = r1.diff(r2)
        print results

使用方法：

    kwargs = {
        'r1': args['<reqfile1>'],
        'r2': args['<reqfile2>'],
        'include_fresh': args['--fresh'],
        'include_stale': args['--stale']
    }

    diff(**kwargs)


### pip-grep



## 新知识点
### super
### raise ValueError
### format
### docopt
### kwargs使用
### __repr__使用，以及与str的不同
### setup.py打包工具
  www.cnblogs.com/maociping/p/6633948.html
