---
title: Java基础语法04｜包机制和用户交互Scanner
tags:
    - Java
categories:
    - JavaSE 
date: 2021-12-2 21:42:22
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/javagrammar.png
---
# 包机制

## 概述

- 在java中，包（package），相当于文件夹。包里通常存放的是类文件，因为我们在编写程序的时候，难免会有类名相同的情况。为了对类进行分类管理，java提出了包机制解决方案，在不同包中可以有相同的类名，调用的时候连同包名一起就行。
- Java允许将一组功能相关的类放在同一个包下，从而组成逻辑上的类库单元。包也限定了访问权限，拥有包访问权限的类才能访问某个包中的类。
- Java默认所有源文件导入java.lang包下的所有类。

## 访问权限

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/accessright.JPG)

## package关键字

- package语句必须作为源文件的第一条非注释性语句，且一个源文件只能指定一个包，即只能包含一条package语句。
- 如果没有显式指定package语句，则处于默认包下。
- 一般利用公司域名倒置作为包名，比如域名：www.baidu.com 包名：com.baidu.www。

```java
//包的语法格式
package pkg1[．pkg2[．pkg3…]];
//比如 Something.java文件的路径就是net/java/util/Something.java这样保存的。
package net.java.util; 
public class Something{ ... }
```

## import关键字

- 为了能够使用某一个包的成员，我们需要在 Java 程序中明确导入该包。使用 import 语句可完成此功能。

- 在 java 源文件中 import 语句应位于 package 语句之后，所有类的定义之前，可以没有，也可以有多条。

```java
//import 语法格式
import package1[.package2…].(classname|*); 
```

- 如果两个类重名，需要导入对应的包，否则就需要写出完整地址。

```java
com.javabase.Hello hello = new com.javabase.Hello()
```

# 用户交互Scanner

## 概述

- 可以通过 Scanner 类来获取用户的输入。

```java
//Scanner对象的基本语法
Scanner s = new Scanner(System.in);
```

## next & nextLine

- Scanner 类的 next() 与 nextLine() 方法获取输入的字符串，在读取前我们一般需要使用 hasNext() 与 hasNextLine() 判断是否还有输入的数据。

```java
public class JavaBase04 {
    public static void main(String[] args) {
        //创建扫描器对象，用于接收键盘数据
        Scanner scanner1 = new Scanner(System.in);
        Scanner scanner2 = new Scanner(System.in);
        //next方式接收字符串
        System.out.println("Next方式接收:");
        //判断用户还有没有输入字符
        if (scanner1.hasNext()){
            String str = scanner1.next();
            System.out.println("输入内容："+str);
        }
        //凡是属于IO流的类如果不关闭会一直占用资源.要养成好习惯用完就关掉.
        System.out.println("nextLine方式接收：");
        if (scanner2.hasNextLine()) {
            String str2 = scanner2.nextLine();
            System.out.println("输入内容：" + str2);
        }
        scanner1.close();
        scanner2.close();
    }
}
/*
	输出结果：
	Next方式接收:
    Hello World
    输入内容：Hello
    nextLine方式接收：
    Hello World
    输入内容：Hello World
*/
```

- **next()**

1.一定要读取到有效字符后才可以结束输入。 

2.对输入有效字符之前遇到的空白，next() 方法会自动将其去掉。 

3.只有输入有效字符后才将其后面输入的空白作为分隔符或者结束符。 

4.next() 不能得到带有空格的字符串。

- **nextLine()**

1.以Enter为结束符,也就是说 nextLine()方法返回的是输入回车之前的所有字符。 

2.可以获得空白。

