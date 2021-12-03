---
title: Java知识梳理02|关键字及部分重点作用详解
tags:
    - Java
categories:
    - Java Difficult Analysis 
date: 2021-12-03 15:43:12
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/keysolution.png
---

# Java关键字的概念

- Java关键字是电脑语言里事先定义的，有特别意义的标识符，有时又叫保留字，还有特别意义的变量。Java的关键字对Java的编译器有特殊的意义，他们用来表示一种数据类型，或者表示程序的结构等，关键字不能用作变量名、方法名、类名、包名和参数。

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javaknowcomb/key.JPG)

# 部分关键字重点作用详解

## 访问控制

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javaknowcomb/acccontrol.JPG)

### 包结构

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javaknowcomb/packageconstruction.JPG)

```java
//Person类 当前类
package keyword.keyfunction;
public class Person {
    public String name="张三";
    protected String age="男";
    private int height=178;
    double weight=70;

    public static void main(String[] args) {
        //public 当前类 √
        System.out.println(new Person().name);

        //protected 当前类 √
        System.out.println(new Person().age);

        //private 当前类 √
        System.out.println(new Person().height);

        //default 当前类 √
        System.out.println(new Person().weight);
    }
}
//Doctor类 同一包内
package keyword.keyfunction;
public class Doctor {
    public static void main(String[] args) {
        //public 同一包内 √
        System.out.println(new Person().name);

        //protected 同一包内 √
        System.out.println(new Person().age);

        //private 同一包内 ×
        //System.out.println(new Person().height);

        //default 同一包内 √
        System.out.println(new Person().weight);
    }
}
//Student类 子孙类（同一包）
package keyword.keyfunction;
public class Student extends Person {
    public static void main(String[] args) {
        //public 子孙类（同一包） √
        System.out.println(new Person().name);

        //protected 子孙类（同一包） √
        System.out.println(new Person().age);

        //private 子孙类（同一包） ×
        //System.out.println(new Person().height);

        //default 子孙类（同一包） √
        System.out.println(new Person().weight);
    }
}
//Teacher类 子孙类（不同包）
package keyword.others;
import keyword.keyfunction.Person;
public class Teacher extends Person {
    public static void main(String[] args) {
        //public 子孙类（不同包） √
        System.out.println(new Person().name);

        //protected 子孙类（不同包） ×
        //System.out.println(new Person().age);

        //private 子孙类（不同包） ×
        //System.out.println(new Person().height);

        //default 子孙类（不同包） ×
        //System.out.println(new Person().weight);
    }
}
//Worker类 其他包
package keyword.others;
import keyword.keyfunction.Person;
public class Worker {
    public static void main(String[] args) {
        //public 其他包 √
        System.out.println(new Person().name);

        //protected 其他包 ×
        //System.out.println(new Person().age);

        //private 其他包 ×
        //System.out.println(new Person().height);

        //default 其他包 ×
        //System.out.println(new Person().weight);
    }
}
```

## static

### static 静态变量

- 在类中，使用static修饰的成员变量，就是静态变量,反之为非静态变量。
- 静态变量属于类的，可以使用类名来访问，非静态变量是属于对象的，必须使用对象来访问。

```java
public class StaticTest {
    public static String name="张三";
    public static void main(String[] args) {
        //使用类名的形式修改静态变量的值
        StaticTest.name="李四";
        //使用类名来访问
        System.out.println("类名形式修改之后类名访问:"+StaticTest.name);
        StaticTest st=new StaticTest();
        //使用对象来访问
        System.out.println("类名形式修改之后对象名访问:"+st.name);
        //使用对象名的形式修改静态变量的值
        st.name="王五";
        System.out.println("对象名形式修改之后对象名访问:"+st.name);
        System.out.println("对象名形式修改之后类访问:"+st.name);
    }
}
//输出结果:
类名形式修改之后类名访问:李四
类名形式修改之后对象名访问:李四
对象名形式修改之后对象名访问:王五
对象名形式修改之后类访问:王五
```

#### 静态变量值的问题

- Java中变量主要分为：局部变量、成员变量，而成员变量又分为实例变量和类变量。

```java
public class StaticTest {
	static int i = 6; // 定义静态成员变量
    int n = 0;	
	public static void main(String[] args) { 
		StaticTest t1 = new StaticTest(); // 创建t1对象
		StaticTest t2 = new StaticTest(); // 创建t2对象
 
        t1.n = 100; // 修改t1的变量n的值100
		t2.i = 60; // 修改t2的变量i的值为60
 
		// 使用第一个对象调用类成员变量
		System.out.println("第一个实例对象变量i：" + t1.i); // 输出60
		System.out.println("第一个实例对象变量n：" + t1.n); // 输出100
 
		// 使用第二个对象调用类成员变量
		System.out.println("第二个实例对象变量i：" + t2.i); // 输出60
		System.out.println("第二个实例对象变量n：" + t2.n); // 输出0
	}
}
//输出结果：
第一个实例对象变量i：60
第一个实例对象变量n：100
第二个实例对象变量i：60
第二个实例对象变量n：0
```

- 局部变量：在方法内部声明（定义）的变量，只在这个方法内部有效，出了这个方法就无法使用，可以理解为销毁。
  - 比如代码中的 t1 和 t2 ，只在main方法中可用。
- 实例变量：成员变量中的实例变量，没有使用static关键字修饰的成员变量，随着对象的创建，会在堆空间分配实例变量空间，进行默认赋值。
  - 如代码中的变量 n 。他在每一个实例化的对象中都是独立的，每个对象修改其值后，只是修改该对象自己的这个变量 n ，其他对象的 n 不受影响。用底层的理解就是，每个对象的变量 n 有独立的内存，他们互不影响。
- 类变量：成员变量中的类变量，是使用static关键字修饰的成员变量。
  - 如代码中的变量 i 。之所以叫做类变量，是因为这个类只有这一个变量 i ，不管实例化多少个对象，他的 i 只有这一个，所以会出现一个对象修改了 i 的值后，其他对象的 i 也跟着变的现象。用底层的理解就是，所有这个类实例化的对象使用的变量 i ，指向的是同一个内存。

### static 静态方法

- 在类中，使用static修饰的成员方法,就是静态方法,反之为非静态方法。
- 静态方法数属于类的，可以使用类名来调用，非静态方法是属于对象的，必须使用对象来调用。

```java
public class StaticTest {
    public static String name="张三";
    public static void sayHello(){
        System.out.println("Hello");
    }
    public static void main(String[] args) {
        //使用类名来访问
        StaticTest.sayHello();
        //使用对象来访问
        StaticTest st=new StaticTest();
        st.sayHello();
    }
}
//输出结果：
Hello
Hello
```

### 其他注意事项

- 静态方法中可以直接调用同类中的静态变量，但不能直接调用非静态变量。如果希望在静态方法中调用非静态变量，可以通过创建类的对象，然后通过对象来访问非静态变量。

```java
public static String name="张三";
public int age=18;
public static void sayHello(){
    System.out.println("姓名："+name);
    
    //静态方法不能直接调用非静态变量
    //System.out.println("年龄："+age);
    
    StaticTest st=new StaticTest();
    System.out.println("年龄："+st.age);
}
```

- 在普通成员方法中，则可以直接访问同类的非静态变量和静态变量。

```java
public static String name="张三";
public int age=18;
public void originalMethod(){
    System.out.println("姓名："+name);
    System.out.println("年龄："+age);
}
```

- 静态方法中能直接调用静态方法，不能直接调用非静态方法，需要通过对象来访问非静态方法。而在普通成员方法中，能直接调用静态方法和非静态方法。

```java
public static String name="张三";
public int age=18;
public void run(){
    System.out.println(name+"正在跑步");
}

public void originalMethod(){
    //非静态方法调用普通成员方法
    introduce();
    //非静态方法调用静态方法
    run();
}

public static void introduce(){
    System.out.println("=========");
    System.out.println("姓名："+name);

    StaticTest st=new StaticTest();
    System.out.println("年龄："+st.age);


}

public static void main(String[] args) {
    //静态方法调用普通成员方法
    StaticTest st=new StaticTest();
    st.originalMethod();
    //静态方法调用静态方法
    introduce();   
}
//输出结果：
=========
姓名：张三
年龄：18
张三正在跑步
=========
姓名：张三
年龄：18
```

- 父类的静态方法可以被子类继承,但是不能被子类重写。

```java
public class Person {
    public static void test() {
    	System.out.println("Person");
    }
}
//编译通过,但不是重写
public class Student extends Person {
    public static void test(){
    	System.out.println("Student");
    }
}
//和非静态方法重写后的效果不一样
public static void main(String[] args) {
    Perosn p = new Student();
    p.test(); //输出Person
    p = new Person();
    p.test(); //输出Perosn
}
```

- 父类的非静态方法不能被子类重写为静态方法。同理，父类的静态方法也不能被子类重写为非静态方法。

```java
public class Person {
    public void test() {
    	System.out.println("Person");
    }
}
//编译报错
/*
    public class Student extends Person {
        public static void test(){
            System.out.println("Student");
        }
    }
*/

```

### 匿名代码块和静态代码块

- 代码块因为没有名字，在程序并不能主动调用这些代码块。 
- 匿名代码块是在创建对象的时候自动执行的,并且在构造器执行之前。同时匿名代码块在每次创建对象的时候都会自动执行。
- 静态代码块是在类加载完成之后就自动执行,并且只执行一次。
- 注意：每个类在第一次被使用的时候就会被加载,并且一般只会加载一次。

```java
public class Student {
    {
        System.out.println("匿名代码块");
    }
    static{
        System.out.println("静态代码块");
    }
    public Person(){
        System.out.println("构造器");
    }
    public static void main(String[] args) {
        Student s1 = new Student();
        Student s2 = new Student();
        Student s3 = new Student();
    }
}
//输出结果：
静态态代码块
匿名代码块
构造器
    
匿名代码块
构造器
    
匿名代码块
构造器
```

- 匿名代码块的作用是给对象的成员变量初始化赋值，但是因为构造器也能完成这项工作，所以匿名代码块使用的并不多。
- 静态代码块的作用是给类中的静态成员变量初始化赋值。

```java
public class Animal {
    public static String name="Jeff";
    public int age;
    static{
        name = "Tom";
        //age="17";
    }
    public Animal(){
        name = "Mike";
        age=18;
    }
    public static void main(String[] args) {
        System.out.println(Animal.name);
        //构造器在创建对象的时候自动执行的
        System.out.println(new Animal().age);
        System.out.println(new Animal().name);
    }
}
//输出结果：
Tom
18
Mike
```

### 静态导入

- 静态导包就是Java包的静态导入，用import static代替import静态导入包是JDK1.5中的新特性。意思是导入这个类里的静态方法。

```java
import static java.lang.Math.random;
import static java.lang.Math.PI;
public class Test {
    public static void main(String[] args) {
        //之前是需要Math.random()调用的
        System.out.println(random());
        System.out.println(PI);
	}
}
```

## this

### 区分局部变量和成员变量

- 当局部变量和成员变量重名的时候，在方法中使用this表示成员变量以示区分。

```java
public class Test{
   private int a = 0;
   public void thisTest(int a){
      this.a = a; //左侧this.a表示位置1的成员变量a，右侧的表示局部变量a
   }
}
```

### return this

- 首先，区分实例，对象和引用。很多人说c就是Cat类的一个实例，这是非常错误的，c就是引用，不是对象！不是实例！我们new出来的这个东西，真正在内存中的这个东西，相当于一个new Cat()叫做一个对象，叫做一个实例。

```java
Cat c = new Cat();
```

- return this就是返回当前所用的对象，其实理解的时候也可以理解成返回当前所用的对象的引用

```java
//实现i多次自增之后打印
public class ThisTest {
    int i = 0;
    //increment()通过this关键字返回当前所用的对象的引用，所以很容易对一个对象执行多次操作
    ThisTest increment(){
        i += 2; 
        return this;//返回当前所用的对象或者实例，相当于返回x引用
    }
    void print(){
        System.out.println("i = " + i);
    }
    public static void main(String args[]){
        ThisTest x = new ThisTest();
        //通过x.increment()计算得到i=2，然后返回当前所用的对象的引用，也就是x，随后又可以进行自增打印操作
        x.increment().increment().print();
        //上面这行代码相当于下面两行代码
        /*
        	ThisTest y = x.increment(); 相当于y引用指向new ThisTest()的内存
        	y.increment().print();
        */
    }
}
//输出结果:
i = 4
```

### this把当前对象传递给其他方法

- this的意思是当前所用的对象，其实理解的时候也可以理解成当前所用的对象的引用

```java
/*
	1.首先看main函数，new Person创建一个人类，new Apple()此时new了一块内存空间出来，内存中的flag=0.未削皮。调用Person类的eat方法，然后方法的参数中传入new Apple()，此时Apple apple=new Apple()，其中apple为new Apple()这个对象的引用
	2.再看eat方法，eat方法传递的参数是对象的引用也就是apple，为了将传进来的苹果变成削了皮的苹果，调用Apple的getPeeled方法
	3.Apple的getPeeled方法返回的是Peeler类的peel方法所返回的apple引用，而这个传入的this其实就是apple引用
	4.然后创建新的peeled引用指向new Apple()这块内存，并且内存中的flag已经更改，相当于这个苹果已经削了皮
	注意：其实至始至终都是在操作new Apple()这个对象的apple引用，而所操作的内存空间也就是最开始new出来的那块
*/
//实现人吃削了皮的苹果
class Person{
    public void eat(Apple apple){
        Apple peeled = apple.getPeeled();
        System.out.println("Yummy");
    }
}
class Peeler{
    static Apple peel(Apple apple){
        //....remove peel
        apple.flag=1;//表示削了皮
        return apple;
    }
}
class Apple{
    int flag=0;//表示没削皮
    Apple getPeeled(){
        return Peeler.peel(this);
    }
}
public class ThisTest{
    public static void main(String args[]){
        new Person().eat(new Apple());
    }
}
//输出结果：
Yummy
```

### this可以用于传递多个参数

- this传递多个参数，其实就是使用this把自身对象作为参数传递给一个工具方法。

```java
public class ParamTest {
    int param1=1;
    int param2=2;

    static void test(ParamTest paramTest){
        System.out.println(paramTest.param1+" "+paramTest.param2);
    }

    void show(){
        test(this);
    }

    public static void main(String[] args) {
        ParamTest p=new ParamTest();
        p.show();
    }
}
//输出结果：
1 2
```

### 在构造器中调用构造器需要使用this

- 一个类有许多构造函数，有时候想在一个构造函数中调用其他构造函数，以避免代码重复，可以使用this关键字。

```java
public class StructureTest {
    private String name;

    public StructureTest(){
        //调用一个参数的构造器,并且参数的类型是String
        this("Tom");//必须放在第一句
        System.out.println("无参构造函数");
    }

    public StructureTest(String name){
        this.name = name;
        System.out.println("姓名:"+name);
    }

    public static void main(String[] args) {
        StructureTest s=new StructureTest();
    }
}
//输出结果：
姓名:Tom
无参构造函数
```

### 其他注意事项

```java
//例子1
package keyword.keyfunction;
public class ThisTest {
    private String name;
    public void test(){
        System.out.println(this);
    }
    public static void main(String[] args) {
        ThisTest t1 = new ThisTest();
        ThisTest t2 = new ThisTest();
        t1.test();
        t2.test();
    }
}
//输出结果：
keyword.keyfunction.ThisTest@12a3a380
keyword.keyfunction.ThisTest@29453f44
    
//例子2
package keyword.keyfunction;
public class ThisTest {

    public ThisTest getThisTest(){
        return this;
    }

    public static void main(String[] args) {
        ThisTest s1 = new ThisTest();
        ThisTest s2 = s1.getThisTest();
        System.out.println(s1 == s2);
    }
}
//输出结果：
true
```

## super

### 静态方法中不能用this和super关键字

- *this*代表的是调用本类的对象，super代表的是调用父类的对象，而静态方法是属于类的，不属于对象，静态方法成功加载后，对象还不一定存在。

```java
public class Father {
    public static String name="father";
}
public class Son extends Father {
    public static String name="son";

    public static void main(String[] args) {
        //System.out.println("Father:"+super.name); 报错
        System.out.println("Son:"+name);
    }
}
```

### 子类重写父类的变量

```java
public class Father {
    protected String name = "father";
}
public class Son extends Father {
    private String name = "son";
    public void test(String name){
        System.out.println(name);
        System.out.println(this.name);
        System.out.println(super.name);
    }
}
public class Test {
    public static void main(String[] args) {
        new Son().test("other");
    }
}
//输出结果：
other
son
father
```

### ③子类重写父类的方法

```java
public class Father {
    protected void print(){
        System.out.println("Father");
    }
}
public class Son extends Father {
	//方法重写的时候，子类的权限修饰符必须要大于或者等于父类的权限修饰符
    public void print(){
        System.out.println("Son");
    }

    public void test(){
        print();
        this.print();
        super.print();
    }
}
public class Test {
    public static void main(String[] args) {
        new Son().test();
    }
}
//输出结果：
Son
Son
Father
```

### super用来调用父类的构造器

- 子类构造器中会隐式的调用父类的无参构造器

```java
public class Father {
    public Father() {
        System.out.println("父类无参构造");
    }
}
public class Son extends Father {
    public Son() {
        //super() 隐藏着这句代码
        System.out.println("子类无参构造");
    }
}
public class Test {
    public static void main(String[] args) {
        new Son();
    }
}
//输出结果：
父类无参构造
子类无参构造
```

- 父类没有无参构造

```java
//例子1
public class Father {
    public Father(String name) {
        System.out.println("父亲："+name);
    }
}
public class Son extends Father {
    /* 
     	编译报错,子类构造器中会隐式的调用父类的无参构造器,但是父类中没有无参构造器
        public Son() {
            System.out.println("子类无参构造");
        }
    */
}
//例子2
public class Father {
    public Father(String name) {
        System.out.println("父亲："+name);
    }
}
public class Son extends Father {
    //编译通过
    public Son() {
        super("张三");
        System.out.println("子类无参构造");
    }
}
//注意：不管是显式还是隐式的父类的构造器,super语句一定要出现在子类构造器中第一行代码。所以this和super不可能同时使用它们调用构造器的功能,因为它们都要出现在第一行代码位置。
```

### super和this的区别

- this：代表本类对象；super：代表父类对象。

- this：在非继承的条件下也可以使用；super：只能在继承的条件下才能使用。
- this：调用本类的构造方法；super：调用的父类的构造方法

## final

### final修饰类

- 用final修饰的类不能被继承，没有子类。

```java
public final class Father{
}
//编译报错
public class Son extends Father{
}
```

### final修饰方法

- 用final修饰的方法可以被继承，但是不能被子类的重写。

```java
public class Father{
    public final void print(){}
    }
}
//编译报错
public class Son extends Father{
    public void print(){
    }
}
```

- 用final修饰的变量表示常量，只能被赋一次值.其实使用final修饰的变量也就成了常量了，因为值不会再变了。

### final修饰局部变量

```java
//例子1
public class FinalTest {
    public void print(){
        final int a;
        a = 1;
        //编译报错,不能再次赋值
        //a = 2;
    }
}

//例子2
public class FinalTest {
    /*
        public void print(final int a) {
            //编译报错,不能再次赋值,传参的时候已经赋过了
            a = 1;
        }
    */
}
```

### final修饰成员变量

- final修饰成员变量时，该成员变量必须在创建对象之前进行赋值，否则编译失败。

#### 修饰非静态成员变量

```java
public class FinalTest{
    //编译失败
	//private final int a; final修饰成员变量，该成员变量必须在创建对象之前进行赋值，否则编译失败
    
    //用final修饰成员变量时，只有一次机会,可以给此变量a赋值，有以下几种赋值方法
    //方法1 声明的同时赋值 private final int a=0;
    
    //方法2 匿名代码块中赋值
    /*
    	private final int a;
        {
            a=0;
        }
    */
    
    //方法3 构造器中赋值(类中出现的所有构造器都要写) 代码实现方法3
    private final int a;
    //类中出现的所有构造器都要写
    public FinalTest(int a) {
        this.a = a;
    }
    public FinalTest(){
        int a=3;
        this.a=a;
        /*
        	如果加上这两句就报错了，因为只有一次机会,可以给此变量a赋值
        	int b=4;
        	this.a=b;
        */
    }
    public static void main(String[] args) {
        FinalTest f1=new FinalTest();
        FinalTest f2=new FinalTest(2);
        //这里并不是final修饰的a被赋值多次，而是new了两个内存空间出来，每个内存空间的final修饰的a有且仅被赋值1次
        System.out.println(f1.a+" "+f2.a);
    }
}
//输出结果：
3 2
```

#### 修饰静态成员变量

```java
public class Person{
	private static final int a;
}

//和非静态成员变量同理，只有一次机会,可以给此变量a赋值,有以下几种赋值方法
//方法1 声明的同时赋值
//方法2 静态代码块中赋值
```

#### 修饰引用变量

```java
public class FinalTest {
    private String name;
    public void setName(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
    public static void main(String[] args) {
        final FinalTest f=new FinalTest();
        f.setName("张三");
        f.setName("李四");
        System.out.println(f.getName());//输出结果：李四
        
        //编译报错,不能修改引用s指向的内存地址
        //f=new FinalTest();
    }
}
```

## abstract

### 抽象类和抽象方法的关系

- 抽象类中可以没有抽象方法，但是有抽象方法的类一定要声明为抽象类。
- 抽象类，不能使用new关键字来创建对象，它是用来让子类继承的。 
- 抽象方法，只有方法的声明,没有方法的实现，它是用来让子类实现的。

```java
public abstract class Action{//抽象类
	public abstract void doSomething();//抽象方法
}
```

## interface

### 接口中的方法和变量

- 接口中的方法都是抽象方法。接口中的变量都是静态常量(public static final修饰)

```java
public interface Behavior{
    public static final String NAME = "jasper";
	//默认就是public static final修饰的
	int AGE = 18;
    
	public abstract void run();
	//默认就是public abstract修饰的
	void eat();
	public void sleep();
}
```

### 一个类可以实现多个接口

```java
public interface A {
    public abstract void run();
}

public interface B {
    public abstract void sleep();
}
//Student需要实现接口A,B中所有的抽象方法
//否则Student类就要声明为抽象类,因为有抽象方法没实现
public class C implements A,B{
    @Override
    public void run() {
        System.out.println("run");
    }

    @Override
    public void sleep() {
        System.out.println("sleep");
    }
}

public static void main(String[] args) {
    A a=new C();//A只能调用接口A中声明的方法以及Object中的方法
    B b=new C();//B只能调用接口B中声明的方法以及Object中的方法
    a.run();
    b.sleep();
    
    if(a instanceof B){
		((B)a).sleep();
	}
}
//输出结果：
run
sleep
sleep
```

### 一个接口可以继承多个父接口

```java
public interface A{
    public void testA();
}
public interface B{
    public void testB();
}
//接口C把接口A,B中的方法都继承过来了
public interface C extends A,B{
	public void testC();
}

//Student相当于实现了A B C三个接口,需要实现所有的抽象方法
//Student的对象也就同时属于A类型 B类型 C类型
public class Student implements C{
    public void testA(){}
    public void testB(){}
    public void testC(){}
}

public class Teacher{
    
}

public static void main(String[] args) {
    C o = new Student();
    System.out.println(o instanceof A);//true
    System.out.println(o instanceof B);//true
    System.out.println(o instanceof C);//true
    System.out.println(o instanceof Student);//true
    System.out.println(o instanceof Object);//true
    System.out.println(o instanceof Teacher);//false
    //编译报错
    System.out.println(o instanceof String);//String类final修饰
    //System.out.println(o instanceof X);
    //如果o是一个接口类型声明的变量,那么只要X不是一个final修饰的类,该代码就能通过编译,至于其结果
	//是不是true,就要看变量o指向的对象的实际类型,是不是X的子类或者实现类了
}
```

