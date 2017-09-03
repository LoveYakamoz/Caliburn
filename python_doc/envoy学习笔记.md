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


 * subprocess

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
    