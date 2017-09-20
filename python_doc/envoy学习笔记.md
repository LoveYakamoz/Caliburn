# envoy学习笔记

开源代码作者：[Kenneth Reitz](https://www.kennethreitz.org/)

![](../image/kennethreitz.jpg)





## 简介
Python .....

* 文件目录

|=======envoy

&emsp;　|___ core.py

|=======ext

&emsp;　|___ in_action.png


| .gitignore :github过滤的配置文件

| .travis.yml：持续集成travis的配置文件

| LICENSE

| README.rst

| AUTHORS

| MANIFEST.in

| setup.cfg

| setup.py ：打包工具

| test_envoy.py


## 开发历程



## 代码剖析
注：删除部分代码，便于理清代码结构

### envoy
* 核心类：


* 对外接口：


* 使用方法：

    

## 新知识点
 * sys.version_info
    sys.version字符串提供了安装的python版本信息。sys.version_info返回的是元组形式

        import sys
        print (sys.version)
        输出： 3.6.2 (v3.6.2:5fd33b5, Jul  8 2017, 04:57:36) [MSC v.1900 64 bit (AMD64)]
        
        print (sys.version_info)
        输出： sys.version_info(major=3, minor=6, micro=2, releaselevel='final', serial=0)

    如envoy代码中，判断当前安装的python版本是否是3.x

        if sys.version_info[0] >= 3:
            pass


 * subprocess
    在python中，可以通过标准库中的subprocess包来fork一个子进程， 用于运行一个外面的程序。subprocess包中定义了多个创建子进程的函数。如下：

    subprocess.call()
    
    subprocess.check_call()

    subprocess.check_output()

    以上三个用法类似，以subprocess.call做为例子，来讲解：

        import subprocess
        retcode = subprocess.call(["ls", "-l"])
        print retcode

    实际上以上三个方法均是对subprocess.Popen()方法的封装。这些封装的目的是为了更方法的使用子进程。但是如果有个性化需求时，就要转向Popen类。该类生成的对象用来代码子进程。与上述三个接口不同， Popen创建后，主进程并不会自动等待子进程完成，即是非阻塞的。 如果要实现阻塞式，需要显式的调用wait()方法。如：

        import subprocess
        child = subprocess.Popen(['ping','-c','4','blog.linuxeye.com'])
        child.wait() #如果省略此行代码，则子进程在结束前就会执行下面的打印
        print 'parent process'

 * threading
    python提供了两个模块来实现多线程，即基本的，低级别的thread和高级别的threading. 在这里我们主要学习threading模块。以做饭为例：

    前期自己经验不足，一次只能做一个菜，如下：

        from time import ctime,sleep

        def CookVegetable():
            ''' 素菜，需要5个单位时间'''
            print("I am cooking Vegetable, at", ctime())
            sleep(5)

        def CookMeat():
            '''荤菜，需要20个单位时间'''
            print("I am cooking Meat, at", ctime())
            sleep(20)

        if __name__ == '__main__':
            print("Start cooking...at", ctime())
            CookVegetable()
            CookMeat()
            print("Finish Cooking, at", ctime())

    运行结果如下：

        Start cooking...at Sun Sep  3 21:58:40 2017
        I am cooking Vegetable, at Sun Sep  3 21:58:40 2017
        I am cooking Meat, at Sun Sep  3 21:58:45 2017
        Finish Cooking, at Sun Sep  3 21:59:05 2017

        可以看到，一共用时25个时间单位。

    经过一个月实践，自己逐渐熟练起来，所以可以同时做两道菜，如下：

        import threading
        from time import ctime,sleep

        def CookVegetable(menu):
            ''' 素菜，需要5个单位时间'''
            print("I am cooking Vegetable, at", ctime())
            sleep(5)

        def CookMeat(menu):
            '''荤菜，需要20个单位时间'''
            print("I am cooking Meat, at", ctime())
            sleep(20)

        cook_threads = []
        t1 = threading.Thread(target=CookVegetable)
        cook_threads.append(t1)
        t2 = threading.Thread(target=CookMeat)
        cook_threads.append(t2)

        if __name__ == '__main__':
            print("Start cooking...at", ctime())
            for t in cook_threads:
                t.setDaemon(True) #声明为守护线程
                t.start()   #开始行动
            
            t.join() # 阻塞父线程，直到所有子线程完成工作

            print("Finish Cooking, at", ctime())
    运行结果如下：

        Start cooking...at Sun Sep  3 22:00:10 2017
        I am cooking Vegetable, at Sun Sep  3 22:00:10 2017
        I am cooking Meat, at Sun Sep  3 22:00:10 2017
        Finish Cooking, at Sun Sep  3 22:00:30 2017
        
        可以看到，一共用时20个时间单位

    
 * shlex库
    
    shlex库让我们非常方便地为类似Shell的简单语法写一个词法分析器。