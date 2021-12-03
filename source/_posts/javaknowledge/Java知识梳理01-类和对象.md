---
title: Java知识梳理01｜类和对象
tags:
    - Java
categories:
    - Java Difficult Analysis 
date: 2021-12-03 15:39:02
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/classandobj.png
---
# 面向过程和面向对象

## 面向过程

- 面向过程是一种以事件为中心的编程思想，编程的时候把解决问题的步骤分析出来，然后用函数把这些步骤实现，再按一定顺序调用函数将事件完成。
- 比如把大象放进冰箱面向过程需要三个步骤，第一步：打开冰箱；第二步：把大象放进冰箱；第三步：关上冰箱。面向过程关注的是怎么样一步一步的把大象放进冰箱。

```java
把大象放冰箱{
    打开冰箱();
    把大象放进冰箱();
    关上冰箱();
}
```

## 面向对象

- 面向对象是一种以“对象”为中心的编程思想，把要解决的问题分解成各个对象，建立对象的目的不是为了完成一个步骤，而是为了描叙某个对象在整个解决问题的步骤中的属性和行为。
- 比如把大象放冰箱面向对象的思维可以把大象当作对象，把冰箱当作对象，通过操作大象和冰箱这两个对象，完成将大象放入冰箱的过程。

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javaknowcomb/ele.png)

```java
//大象类
public class Elephant {
    private int eHeight=3;
    public int geteHeight() {
        return eHeight;
    }
}
//冰箱类
public class Refrigerator {
    private int rHeight=1;
    public int getrHeight() {
        return rHeight;
    }
    public void openRe(){
        System.out.println("打开冰箱");
    }
    public void closeRe(){
        System.out.println("关上冰箱");
    }
}
//操作类
public class Operate {
    public static void main(String[] args) {
        Elephant elephant=new Elephant();
        Refrigerator refrigerator=new Refrigerator();
        putIntoRe(elephant,refrigerator);
    }
    //把大象放进冰箱
    public static void putIntoRe(Elephant elephant, Refrigerator refrigerator){
        if (elephant.geteHeight()<=refrigerator.getrHeight()){
            refrigerator.openRe();
            System.out.println("大象成功装进冰箱");
            refrigerator.closeRe();
        }else {
            refrigerator.openRe();
            System.out.println("大象不可能装进冰箱");
            refrigerator.closeRe();
        }
    }
}
/*  输出结果：
	打开冰箱
	大象不可能装进冰箱
	关上冰箱 
*/
```

- 我们将繁琐的步骤，通过行为、功能，模块化，这就是面向对象。面向对象更多的是要进行子模块化的设计，每一个模块都需要单独存在，并且可以被重复利用，面向对象具有封装、继承和多态三个基本特征。

# 类和对象

## 类和对象的概念

- 类是对象的集合，对象是类的实例。对象是通过new className产生的，用来调用类的方法、类的构造方法。总之，类就是有相同特征的事物的集合，而对象就是类的一个具体实例。
- 类表示的是一个共性的产物，类中定义的是属性和行为（方法）；对象表示的是一个独立的个体，每个对象拥有自己独立的属性。
- 比如我们创建一个Dog类，类中有姓名、大小、颜色和年龄四个属性，并且有吃、跑和睡觉三种行为。与此同时，创建dog1和dog2两个对象。

```java
//Dog类
public class Dog {
    String name;
    int size;
    String colour;
    int age;
    void eat() {
    }
    void run() {
    }
    void sleep(){
    }
}
//操作类
public class Operate {
    public static void main(String[] args) {
        Dog dog1=new Dog();
        Dog dog2=new Dog();
    }
}
```

## 类和对象的定义和使用

1. 类的定义

```java
public class 类名称 {
    属性 (变量) ;
    行为 (方法) ;
}
/* 
    public class Dog {
       String name;
       public void eat(){
            System.out.println("吃东西");
       }
    }
*/
```

2. 对象的两种声明

- 声明并实例化对象。

```java
类名称 对象名称 = new 类名称 (); //比如Dog dog=new Dog();
```

- 先声明对象，然后实例化对象。

```java
类名称 对象名称 = null ;
对象名称 = new 类名称 () ;
//比如Dog dog=null dog=new Dog();
```

- 对象.属性：表示调用类之中的属性；
  对象.方法()：表示调用类之中的方法。

```java
//Dog类
public class Dog {
       String name;
       public void eat(){
            System.out.println("吃东西");
       }
}
//操作类
public class Operate {
    public static void main(String[] args) {
       Dog dog=new Dog();
       dog.name="牧羊犬";
       System.out.println(dog.name);
       dog.eat();
    }//输出结果：牧羊犬 吃东西
}
```

# 创建对象具体过程

## 1.两种内存空间概念

- 栈内存：保存的是堆内存的地址（可以理解为保存的是创建对象的名字）。
- 堆内存：保存对象的属性内容，使用new关键字就是在堆内存分配空间。

![](C:\Users\54023\Desktop\博客\Java知识梳理\图片\栈内存堆内存.png)

- 这属于先声明对象再实例化对象，如果将两步合并就是声明并实例化对象

## 2.创建对象具体过程

```java
//Dog类
public class Dog {
    String name="哈士奇";
    int age=4;
    public Dog() {
    }
    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
}
//操作类
public class Operate {
    public static void main(String[] args) {
        Dog dog=new Dog("柯基",7);
        dog.setName("哈士奇");
        dog.setAge(8);
        System.out.println("名字:"+dog.getName()+",年龄："+dog.getAge());
    }//输出结果：名字:哈士奇,年龄：8
}
```

- **执行完Dog dog=new Dog("柯基",7)语句，做了那些事情？**

1. 把Dog.class文件加载到内存(方法区)。

2. 在栈内存为对象地址(dog)开辟空间。
3. 在堆内存为Dog类中的属性内容申请空间。
4. 给Dog类中的成员变量进行默认初始化。
5. 给Dog类中的成员变量进行显示初始化。
6. 通过构造方法给Dog类中的成员变量进行初始化。
7. 对象构造完毕，把堆内存的地址赋值给栈内存dog变量。

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javaknowcomb/startobj.JPG)

# 值传递和引用传递

## 值传递和引用传递的定义

- 值传递：实际参数把它的值传递给对应的形式参数，函数接收的是原始值的一个copy，此时内存中存在两个相等的基本类型，即实际参数和形式参数，后面方法中的操作都是对形式参数这个值的修改，不影响实际参数的值。
- 引用传递：也称为传地址。方法调用时，实际参数的引用(地址，而不是参数的值)被传递给方法中相对应的形式参数，函数接收的是原始值的内存地址。在方法执行中，形参和实参内容相同，指向同一块内存地址，方法执行中对引用的操作将会影响到实际对象。

## 基本数据类型的值传递

- 代码中的swap函数，其实是将实际参数num1和num2的值进行一次copy，对copy出来的形式参数a和b的值进行交换，而不影响实际参数的值。

```java
public class Operate {
    public static void main(String[] args) {
        int num1 = 10;
        int num2 = 20;

        swap(num1, num2);

        System.out.println("num1 = " + num1);
        System.out.println("num2 = " + num2);
    }
    public static void swap(int a, int b) {
        int temp = a;
        a = b;
        b = temp;

        System.out.println("a = " + a);
        System.out.println("b = " + b);
    }
}
/*  输出结果：
	a = 20
    b = 10
    num1 = 10
    num2 = 20
*/
```

## String,Integer,Double等包装类的传值

- String,Integer,Double等包装类类似基本类型，值传递，不会改变实际参数的值。

```java
public class Operate {
    public static void main(String[] args) {
        String str1="I'm";//等价于String str1=new String("I'm");
        Double d1=3.14;
        Integer i1=3;
        System.out.println("str1="+str1+",d1="+d1+",i1="+i1);
        changeString(str1,d1,i1);
        System.out.println("str1="+str1+",d1="+d1+",i1="+i1);
    }
    public static void changeString(String string,Double dou,Integer in){
        string=new String("I'm Jasper");
        dou=3.1415;//等价于dou=new Double(3.1415)
        in=new Integer(4);
    }
}
/*  输出结果：
	str1=I'm,d1=3.14,i1=3
    str1=I'm,d1=3.14,i1=3
*/
```

## StringBuffer和StringBuilder的引用传递

- 实参strBuffer1将地址传递给形参stringBuffer1，此时实参和形参存的是相同的内存地址。在changeBuffer函数中，形参stringBuffer1通过new开辟新的空间，改变了内存地址，而实参strBuffer1内存地址和指向的内容不变，所以输出不变。
- 实参strBuffer2将地址传递给形参stringBuffer2，此时实参和形参存的是相同的内存地址。在changeBuffer函数中，形参stringBuffer2通过append追加新字符串，而实参和形参内存地址不变，指向的内容发生改变，所以输出改变。

```java
public class Operate {
    public static void main(String[] args) {
        StringBuffer strBuffer1 = new StringBuffer("Hello");
        StringBuffer strBuffer2 = new StringBuffer("Happy");
        System.out.println("strBuffer1="+strBuffer1+",strBuffer2="+strBuffer2);
        changeBuffer(strBuffer1,strBuffer2);
        System.out.println("strBuffer1="+strBuffer1+",strBuffer2="+strBuffer2);
    }
	public static void changeBuffer(StringBuffer stringBuffer1,StringBuffer stringBuffer2) {
        stringBuffer1=new StringBuffer("Hello World");
        stringBuffer2.append(" New Year");
    }
}
/*  输出结果：
	strBuffer1=Hello,strBuffer2=Happy
	strBuffer1=Hello,strBuffer2=Happy New Year
*/
```

## 对象类型的引用传递

- 原理同4

```java
//person类
public class Person {
    private String name;
    public Person() {
    }
    public Person(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
}
//操作类
public class Operate {
    public static void main(String[] args) {
        Person person1 = new Person("张三");
        Person person2 = new Person("张三");
        System.out.println("person1="+person1.getName()+",person2="+person2.getName());
        changePerson(person1,person2);
        System.out.println("person1="+person1.getName()+",person2="+person2.getName());
    }
	 public static void changePerson(Person p1,Person p2) {
        p1= new Person("李四");
        p2.setName("李四");
    }
}
/*  输出结果：
	person1=张三,person2=张三
	person1=张三,person2=李四
*/
```

