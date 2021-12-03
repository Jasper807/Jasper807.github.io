---
title: Java方法｜方法的定义、调用和重载
tags:
    - Java
categories:
    - JavaSE 
date: 2021-12-02 22:01:43
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/javamethod.png
---
# 方法的定义

## 什么是方法

- 在我们的日常生活中，方法可以理解为要做某件事情，而采取的解决办法。而Java方法是语句的集合，它们在一起执行一个功能。

- Java中方法是解决一类问题的步骤的有序组合，包含于类或对象中，在程序中被创建，在其他地方被引用。
- 我们经常使用到 System.out.println()中，println() 是一个方法。System 是系统类。 out 是标准输出对象。 这句话的用法是调用系统类 System 中的标准输出对象 out 中的方法 println()。

## 设计方法的原则

- 方法的本意是功能块，就是实现某个功能的语句块的集合。我们设计方法的时候，最好保持方法的原子性，就是一个方法只完成1个功能，这样利于我们后期的扩展。

## 方法的优点

- 使程序变得更简短而清晰。

- 有利于程序维护。

- 可以提高程序开发的效率。

- 提高了代码的重用性。

## 方法的定义

```java
修饰符 返回值类型 方法名(参数类型 参数名){
    ...
    方法体
    ...
    return 返回值;
}
```

- **修饰符：**修饰符，这是可选的，告诉编译器如何调用该方法。定义了该方法的访问类型。 
- **返回值类型 ：**方法可能会返回值。returnValueType 是方法返回值的数据类型。有些方法执行所需的操作，但没有返回值。在这种情况下，returnValueType 是关键字void。 
- **方法名：**是方法的实际名称。方法名和参数类型共同构成方法签名。 

```java
//方法声明的两个组件构成了方法签名 - 方法的名称和参数类型。
public double calculateAnswer(double number1, double number2) {
    //do the calculation here
}
//上面方法的签名：calculateAnswer(double,double)
```

- **参数类型：**参数像是一个占位符。当方法被调用时，传递值给参数。这个值被称为实参或变量。参数列表是指方法的参数类型、顺序和参数的个数。参数是可选的，方法可以不包含任何参数。 
  - **形式参数：**在方法被调用时用于接收外界输入的数据。 
  - **实际参数：**调用方法时实际传给方法的数据。

- **方法体：**方法体包含具体的语句，定义该方法的功能。

```java
//例子
public static int add(int num1, int num2) {
    int result;
    result=num1+num2;
    return result;
}

public static void sayHello() {
    System.out.println("Hello");
}
```

# 方法的调用

- Java 支持两种调用方法的方式，根据方法是否返回值来选择。

- 当程序调用一个方法时，程序的控制权交给了被调用的方法。

- 当被调用方法的返回语句执行或者到达方法体闭括号时候交还控制权给程序。

- 当方法返回一个值的时候，方法调用通常被当做一个值。

```java
int larger = add(10, 20);
```

- 当方法返回值是void，方法调用一定是一条语句。

```java
//调用add方法
public class JavaMethod {
    public static int add(int num1, int num2) {
        int result;
        result=num1+num2;
        return result;
    }
    public static void main(String args[]) {
        int number1=1;
        int number2=2;
        int result = add(number1, number2);
        System.out.println("number1+number2="+result);
    }
}
//输出结果：number1+number2=3
```

# 方法的重载

- 所谓方法重载就是如果你调用add方法时传递的是int型参数，则int型参数的add方法就会被调用；如果传递的是double型参数，则double型的add方法会被调用。

```java
public static int add(int num1, int num2) {
    int result;
    result=num1+num2;
    return result;
}

public static double add(double num1, double num2) {
    double result;
    result=num1+num2;
    return result;
}
```

- 方法重载可以让程序更清晰易读。执行密切相关任务的方法应该使用相同的名字。
- 重载的方法必须拥有不同的参数列表。你不能仅仅依据修饰符或者返回类型的不同来重载方法。

# 可变参数

```java
typeName... parameterName //声明格式
```

- 在方法声明中，在指定参数类型后加一个省略号(...) 。
- 一个方法中只能指定一个可变参数，它必须是方法的最后一个参数。任何普通的参数必须在它之前声明。

```java
public static void main(String args[]) {
    double[] d={4, 2, 3};
    // 调用可变参数的方法
    printMax(59,44,77);
    printMax(d);
}
public static void printMax(double... numbers) {
    if (numbers.length == 0) {
        System.out.println("No argument passed");
        return;
    }
    double result = numbers[0];
    //排序！
    for (int i = 1; i < numbers.length; i++){
        if (numbers[i] > result) {
            result = numbers[i];
        }
    }
    System.out.println("The max value is " + result);
}
//输出结果：
//The max value is 77.0
//The max value is 4.0
```

# 递归

- **递归头。**什么时候不调用自身方法。如果没有头，将陷入死循环。

- **递归体。**什么时候需要调用自身方法。

```java
public static int f(int n) {
        if (1 == n) {
            return 1;
        } else{
            return n*f(n-1);
        }
    }

public static void main(String args[]) {
    //5*4*3*2*1
    System.out.println(f(5));
}
//输出结果：120
```

