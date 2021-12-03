---
title: Java知识梳理03|内部类详解
tags:
    - Java
categories:
    - Java Difficult Analysis 
date: 2021-12-03 15:45:44
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/outerclass.png
---

# 内部类的定义

- 可以将一个类的定义放在另一个类的定义内部，这就是内部类。

# 内部类的种类

- 在 Java 中内部类主要分为成员内部类、局部内部类、匿名内部类、静态内部类。

## 成员内部类

- 成员内部类定义格式。

```java
class A{
    class B{

    }
}
```

- 成员内部类无条件访问外部类的属性和方法。

```java
public class Outer {
    private String name = "Outer";
    public void run(){
        System.out.println("Outer run");
    }

    class Inner{
        public void say(){
            System.out.println(name);
            run();
        }
    }

}
```

- 外部类想要访问内部类属性或方法时，必须要创建一个内部类对象，然后通过该对象访问内部类的属性或方法。

- Inner类定义在Outer类的内部，相当于Outer类的成员变量的位置，Inner类可以使用任意访问修饰符。
- 成员内部类中不能定义static成员，但是可以存在static域，前提是需要使用final关键字进行修饰。

```java
public class Outer {
    private static String oName = "name = Outer";
    public void run(){
        System.out.println("Outer run");
    }

    public static void main(String[] args) {
        Outer outer=new Outer();
        Outer.Inner inner=outer.new Inner();
        System.out.println(inner.iName);
        inner.say();
    }

    class Inner{
        private String iName="name = Inner";
        public static final int age=18;
        public void say(){
            System.out.println(oName);
            System.out.println("age = "+age);
            run();
        }
    }
}
//输出结果：
name = Inner
name = Outer
Outer run
```

- 如果成员内部类的属性或者方法与外部类的同名，将导致外部类的这些属性与方法在内部类被隐藏，可按照该格式调用，外部类.this.属性/方法。

```java
public class Outer {
    private static String name = "name = Outer";
    public void run(){
        System.out.println("Outer run");
    }

    public static void main(String[] args) {
        Outer outer=new Outer();
        Outer.Inner inner=outer.new Inner();
        inner.show();
    }

    class Inner{
        private String name="name = Inner";
        public void run(){
            System.out.println("Inner run");
        }
        public void show(){
            System.out.println(new Inner().name);
            System.out.println(name);
            run();
            System.out.println(new Outer().name);
            System.out.println(Outer.this.name);
            Outer.this.run();
        }
    }

}
//输出结果：
name = Inner
name = Inner
Inner run
name = Outer
name = Outer
Outer run
```

## 局部内部类

- 局部内部类定义格式

```java
class A{
    public void show(){
        class B{
            
        }
    }
}
```

- 局部内部类无条件访问外部类的属性和方法。

```java
public class Person {

    private String name="张三";
    public void introduce(){
        System.out.println("他是"+name);
    }

    public void show(){
        class Hobby{
            private String hobby="跳舞";
            public void say(){
                introduce();
                System.out.println(name+"爱"+hobby);
            }
        }
    }
}
```

- 局部内部类嵌套在方法和作用域内的，只是它的作用域发生了改变，它只能在该方法和属性中被使用，出了该方法和属性就会失效。
- 局部内部类中不能定义static成员，但是可以存在static域，前提是需要使用final关键字进行修饰。

```java
public class Person {

    private String name="张三";
    public void introduce(){
        System.out.println("他是"+name);
    }

    public void show(){
        class Hobby{
            public static final String intr="介绍:";
            private String hobby="跳舞";
            public void say(){
                System.out.println(intr);
                introduce();
                System.out.println(name+"爱"+hobby);
            }
        }
        Hobby hobby=new Hobby();
        hobby.say();
    }

    public static void main(String[] args) {
        Person person=new Person();
        person.show();
//      Hobby hobby=new Hobby(); 编译错误
//      Person.Hobby hobby=new Person.new Hobby(); 编译错误
    }
}
//输出结果：
介绍:
他是张三
张三爱跳舞
```

- 如果局部内部类的属性或者方法与外部类的同名，将导致外部类的这些属性与方法在内部类被隐藏，可按照该格式调用，外部类.this.属性/方法。

```java
public class Person {
    private String name="Person";
    public void say(){
        System.out.println(name);
    }
    public void show(){
        class Hobby{
            private String name="Hobby";
            public void say(){
                System.out.println(name);
            }
        }
        Hobby hobby=new Hobby();
        System.out.println(hobby.name);
        hobby.say();
        System.out.println(Person.this.name);
        Person.this.say();
    }
    public static void main(String[] args) {
        Person person=new Person();
        person.show();
    }
}
//输出结果：
Hobby
Hobby
Person
Person
```

## 匿名内部类

- 匿名内部类也就是没有名字的内部类。正因为没有名字，所以匿名内部类只能使用一次，它通常用来简化代码编写。但使用匿名内部类还有个前提条件：必须继承一个父类或实现一个接口。

```java
//不使用匿名内部类来实现抽象方法
abstract class Person {
    public abstract void say();
}

class Student extends Person {
    public void say() {
        System.out.println("say");
    }
}

public class Test {
    public static void main(String[] args) {
        Person p = new Student();
        p.say();
    }
}
//输出结果:
say
```

- 使用匿名内部类实现抽象方法和接口。

```java
//抽象方法
abstract class Animal {
    public abstract void shout();
}

public class Test{
    public static void main(String[] args) {
        Animal animal=new Animal(){
            public void shout() {
                System.out.println("shout");
            }
        };
        animal.shout();
    }
}
//输出结果:
shout
    
//接口
interface Animal {
    void shout();
}

public class Test{
    public static void main(String[] args) {
        //可用此代码替代下面代码 Animal animal= () -> System.out.println("shout");
        Animal animal=new Animal(){
            public void shout() {
                System.out.println("shout");
            }
        };
        animal.shout();
    }
}
//输出结果:
shout
```

- 匿名内部类最常用的情况就是在多线程的实现上，因为要实现多线程必须继承 Thread 类或是继承 Runnable 接口。

```java
//Thread类的匿名内部类实现
public class Test {
    public static void main(String[] args) {
        Thread t = new Thread() {
            public void run() {
                for (int i = 1; i <= 5; i++) {
                    System.out.print(i + " ");
                }
            }
        };
        t.start();
    }
}
//输出结果
1 2 3 4 5
    
//Runnable接口的匿名内部类实现
public class Test {
    public static void main(String[] args) {
        Runnable r = new Runnable() {
            public void run() {
                for (int i = 1; i <= 5; i++) {
                    System.out.print(i + " ");
                }
            }
        };
        Thread t = new Thread(r);
        t.start();
    }
}
//输出结果
1 2 3 4 5
```

## 静态内部类

- 静态内部类定义格式

```java
class U {
    static class I {
        
    }
}
```

- static 不仅可以修饰成员变量、方法、代码块，它还可以修饰内部类，使用 static 修饰的内部类我们称之为静态内部类。

- 静态内部类只能访问外围类的静态成员变量和方法，不能访问外围类的非静态成员变量和方法。

```java
public class OutClass {
    private String name="张三";
    private static int age=18;

    public static void staticMethod(){
        System.out.println("outer staticMethod");
    }

    public void method(){
        System.out.println("outer method");
    }

    static class InClass{
        private static String hobby="跳舞";
        public static void dance(){
            System.out.println(new OutClass().name+"爱"+hobby);
        }

        public void show(){
            //System.out.println(name); 错误
            System.out.println("姓名："+new OutClass().name);
            System.out.println("年龄："+age);
            staticMethod();
            new OutClass().method();
            //method(); 错误
        }
    }

    public static void main(String[] args) {
        //System.out.println(InCLass.name2); 错误
        InClass inClass=new InClass();
        inClass.show();
        InClass.dance();
    }
}
//输出结果:
姓名：张三
年龄：18
outer staticMethod
outer method
张三爱跳舞
```

