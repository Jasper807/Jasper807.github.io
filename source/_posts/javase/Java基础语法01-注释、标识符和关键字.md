---
title: Java基础语法01｜注释、标识符和关键字
tags:
    - Java
categories:
    - JavaSE 
date: 2021-12-02 21:14:41
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/javagrammar.png
---
# 注释

1. **单行注释（只能注释当前行，以//开始，直到行结束）**

```java
public class HelloWorld {
    public static void main(String[] args) {
        //输出Hello World
        System.out.println("Hello World");
    }
}
```

2. **多行注释（注释一段文字，以/开始， /结束）**

```java
public class HelloWorld {
    public static void main(String[] args) {
        /*
            输出Hello World
         */
        System.out.println("Hello World");
    }
}
```

3. **文档注释（在开始的 **/\**** 之后，第一行或几行是关于类、变量和方法的主要描述）**

```java
/**
 * @Author Jasper
 * @Description 注释理解
 */
public class HelloWorld {
    /**
     * 计算a+b的和
     * @param a
     * @param b
     * @return a+b
     */
    public static int getSum(int a, int b){
        return a+b;
    }
    public static void main(String[] args) {
        //将计算得到的int值赋值给sum
        int sum = getSum(1, 2);
        //控制台输出sum
        System.out.println(sum);
    }
}
```



# 标识符

1. 每个人都有自己的名字，而在Java中，标识符是为方法、变量或其他用户定义项所定义的名称。类名、变量名以及方法名都被称为标识符。

```java
//其中HelloWorld就是类名,mian就是方法名,args就是变量名
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

2. 表示类名的标识符用大写字母开始。类名类似于HelloWorld、PostMan等等

3. 表示方法和变量的标识符用小写字母开始，后面的描述性词以大写开始，尽量使用规范的驼峰命名原则。

   变量名类似于drinkMilk、doSport等等
   方法名类似于getSum()、makeFriend()等等

# 关键字

1. Java关键字是电脑语言里事先定义的，又叫保留字，是整个语言范围内预先保留的标识符，需要注意的是，Java中已经规定的关键字，我们自己就不能拿它当做名字。

2. Java的关键字对Java的编译器有特殊的意义，他们用来表示一种数据类型，或者表示程序的结构等，关键字不能用作变量名、方法名、类名、包名和参数。比如public、static就是关键字，我们无法用此命名。

   ![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/keyword.JPG)

#  标识符的注意事项

1. 所有的标识符都应该以字母（A-Z 或者 a-z）,美元符（$）、或者下划线（_）开始。


```java
int Apple; //正确
int $cash; //正确
int _sale; //正确
int +cd; //错误，只能字母、美元符、下划线开头
int #children //错误，只能字母、美元符、下划线开头
```

2. 首字符之后可以是字母（A-Z 或者 a-z）,美元符（$）、下划线（_）或数字的任何字符组合。

```java
int a1$c; //正确
int a#c； //错误，只能是字母、美元符、下划线、数字的组合不能使用关键字作为变量名或方法名
```

3. 不能使用关键字作为变量名或方法名。

```java
public class HelloWorld {
    /*
    	这样命名就不行，因为作为方法名的public是关键字，作为变量名的static也是关键字
        public int public(int staic){
            return 1；
        }
    */
}
```

4. 标识符是大小写敏感的。

```java
//我下面定义的是两个变量，而并非一个变量
int Book;
int book;
```

5. 在Java语言的使用中，一般不建议中文命名，也不建议拼音命名。
