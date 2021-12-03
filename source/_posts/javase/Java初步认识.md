---
title: Java初步认识
tags:
	- Java
categories:
	- JavaSE 
date: 2021-12-02 20:43:02
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/javafirststep.png
---
# JDK、JRE 和 JVM

## JDK

1. JDK是Java Development Kit 的缩写，意思是Java程序开发的工具包，也可以说Java 语言的软件开发工具包(SDK)。

2. JDK是整个Java开发的核心，它包含了Java的运行环境，Java工具和Java基础的类库。

3. JDK是给开发者提供的开发工具箱，是给程序开发者用的。

## JRE

1. JRE是Java Runtime Environment 的缩写，意思是Java程序的运行环境。

2. 普通用户并不需要安装JDK来运行Java程序，而只需要安装JRE，而程序开发者必须安装JDK来编译、调试程序。

## JVM

1. JVM是Java Virtual Machine 的缩写，意思是Java虚拟机。

2. JVM是一种规范，可以使用软件来实现，也可以使用硬件来实现。它是一个虚构出来的计算机，是通过在实际的计算机上仿真模拟各种计算机功能来实现的。

3. Java的跨平台实现的核心是不同平台使用不同的虚拟机。Java 虚拟机机制屏蔽了底层运行平台的差别，实现了“一次编译，随处运行”。


## 区别和联系

1. JDK是给开发人员用的，JRE和JVM是普通用户用的。 如果只是要运行Java程序，只需要JRE就可以， JRE通常非常小，其中也包含了JVM。如果要开发Java程序，就需要安装JDK。简单来说JDK包含JRE，JRE又包含JVM。

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/threerelationship.jpg)

# Java程序运行机制

1. 计算机的高级编程语言类型: 编译型 ，解释型。Java 语言是两种类型的结合。

2. 所谓编译型就是有一个负责翻译的程序来对我们的源代码进行转换，生成相对应的可执行代码，而负责编译的程序自然就称为编译器。打个比方你看不懂这本英文书，找了名翻译，翻译官将这本书从头到尾全部翻译成中文供你阅读。

3. 所谓解释型就是在运行的时候将程序翻译成机器语言，所以运行速度相对于编译型语言要慢。打个比方你看不懂这本英文书，找了名翻译，翻译官将一本英文书一句句帮你翻译成中文。

4. 编译型由于程序执行速度快，同等条件下对系统要求较低，因此像开发操作系统、大型应用程序、数据库系统等时都采用它；而一些网页脚本、服务器脚本及辅助开发接口这样的对速度要求不高、对不同系统平台间的兼容性有一定要求的程序通常使用解释性语言。

5. 简单来说Java程序的运行机制分为编写、编译和运行三个步骤。从编写出来的Java源文件，到编译为字节码文件，再到通过JVM解释执行Class字节码文件，然后将程序的运行结果展示给用户，这是一个完整的Java运行流程。

![Java程序运行机制](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/operatingmechanism.jpg)
