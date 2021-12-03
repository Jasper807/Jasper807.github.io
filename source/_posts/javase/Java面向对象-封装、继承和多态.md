---
title: Java面向对象｜封装、继承和多态
tags:
    - Java
categories:
    - JavaSE 
date: 2021-12-02 22:10:27
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/javaobj.png
---

# 什么是面向对象

- Java的编程语言是面向对象的，采用这种语言进行编程称为面向对象编程(Object-Oriented Programming, OOP)。

- 面向对象的方法主要是把事物给对象化，包括其属性和行为。面向对象编程更贴近实际生活的思想。总体来说面向对象的底层还是面向过程，面向过程抽象成类，然后封装，方便使用就是面向对象。
- 面向对象的三个基本特征：封装、继承和多态。

# 抽象(Abstract)

- 忽略一个主题中与当前目标无关的那些方面，以便更充分地注意与当前目标有关的方面。抽象并不打算了解全部问题，而只是选择其中的一部分，暂时不用关注细节。 
- 比如：需要设计一个学生体检的系统，我们只需要关注学生的身高、体重和肺活量等信息，而不需要关注学生的兴趣爱好等信息。所以说，抽象就是将多个物体的共同点归纳出来，就是抽出像的部分！

# 封装(Encapsulation)

- 封装是把过程和数据包围起来，对数据的访问只能通过指定的方式。也就是说把复杂的内部细节全部封装起来，只暴露简单的接口。

- 我们程序设计要追求“高内聚，低耦合”。
  - 高内聚就是类的内部数据操作细节自己完成，不允许外部干涉。
  - 低耦合：仅暴露少量的方法给外部使用。

## 封装的步骤

- 修改属性的可见性来限制对属性的访问（一般限制为private）。

```java
public class Person {
    private String name;
    private int age;
}
```

- 提供一个公开的方法设置或者访问私有的属性 。
  - 设置 通过set方法，命名格式： set属性名（）; 属性的首字母要大写 。
  - 访问 通过get方法，命名格式： get属性名（）; 属性的首字母要大写。

```java
public class Person{
    private String name;
    private int age;
    public int getAge(){
      return age;
    }
    public String getName(){
      return name;
    }
    public void setAge(int age){
      this.age = age;
    }
    public void setName(String name){
      this.name = name;
    }
}
```

## 作用和意义

- 提高程序的安全性，保护数据 。
- 隐藏代码的实现细节。
- 统一用户的调用接口。
- 提高系统的可维护性。
- 便于调用者调用。

## 方法的重载

- 方法重载必须满足的条件
  - 方法名必须相同。
  - 参数列表必须不同(参数的类型、个数、顺序的不同)。
  - 方法的返回值可以不同，也可以相同。
  - 修饰符可以不同，也可以相同。

- Java中，判断一个类中的俩个方法是否相同，主要参考俩个方面：方法名字和参数列表

```java
//参数类型不同
public void test(Strig str){}
public void test(int a){}
//参数个数不同
public void test(Strig str,double d){}
public void test(Strig str){}
//参数顺序不同
public void test(Strig str,double d){}
public void test(double d,Strig str){}
```

# 继承

## 继承的概述

- 继承是类和类之间的一种关系。除此之外，类和类之间的关系还有依赖、组合、聚合等。
- 继承关系的俩个类，一个为子类(派生类)，一个为父类(基类)。子类继承父类，使用关键字extends来表示。
- 子类中继承了父类中的属性和方法后，在子类中能不能直接使用这些属性和方法，是和这些属性和方法原有的修饰符(public protected default private)相关的。
  - 父类中的属性和方法使用public修饰，在子类中继承后"可以直接"使用。
  - 父类中的属性和方法使用private修饰，在子类中继承后"不可以直接"使用。

## 继承的格式

```java
class 父类 {
}
 
class 子类 extends 父类 {
}
```

## extends关键字

- 在 Java 中，类的继承是单一继承，也就是说，一个子类只能拥有一个父类，所以 extends 只能继承一个类。

```java
public class Animal { 
    private String name;   
    private int id; 
    public Animal(String myName, String myid) { 
        //初始化属性值
    } 
    public void eat() {  //吃东西方法的具体实现  } 
    public void sleep() { //睡觉方法的具体实现  } 
} 
 
public class Dog extends Animal{ 
}
```

## implements关键字

- implements 关键字可以变相的使java具有多继承的特性，使用范围为类继承接口的情况，可以同时继承多个接口.

```java
public interface A {
    public void eat();
    public void sleep();
}
 
public interface B {
    public void show();
}
 
public class C implements A,B {
}
```

## super 与 this 关键字

- 如果不显示调用父类有参构造函数，系统会默认调用父类无参构造函数super();

```java
public class Animal {
    private String name;
    public Animal() {
        System.out.println("Animal创建了");
    }
}

public class Cat extends Animal {
    public Cat() {
        //super();
        System.out.println("Cat创建了");
    }
}

public class Test {
    public static void main(String[] args) {
        Cat cat=new Cat();
    }
}
//输出结果：
//Animal创建了
//Cat创建了
```

- 不管是显式还是隐式的父类的构造器，super语句一定要出现在子类构造器中第一行代码。

```java
public class Animal {
    private String name;
    public Animal(String name) {
        this.name = name;
    }
}

public class Cat extends Animal {
    public Cat(String name) {
        super(name);
        System.out.println("super语句要在第一行");
    }
}
```

-  super只能出现在子类的方法或者构造方法中。

```java
public class Animal {
    private String name;

    public Animal(){
		System.out.println("Animal无参");
    }

    public Animal(String name) {
        this.name = name;
        System.out.println("小狗:"+name);
    }
}

public class Cat extends Animal {
    private String color;
    public Cat(){
        this("黄色");
    }

    public Cat(String color) {
        super("柯基");
        this.color=color;
        System.out.println("颜色:"+color);
    }

}

public class Test {
    public static void main(String[] args) {
        Cat cat=new Cat();
        //这里因为父类显示调用有参构造，所以系统不会默认调用无参构造,也就不会输出"Animal无参"。
    }
}
//输出结果：
//
```

- super与this的区别
  - this：代表所属方法的调用者对象；super：代表父类对象的引用空间。
  - this：在非继承的条件下也可以使用；super：只能在继承的条件下才能使用。
  - this：调用本类的构造方法；super：调用的父类的构造方法。

## final关键字

- final 关键字声明类可以把类定义为不能继承的，即最终类；或者用于修饰方法，该方法不能被子类重写。

```java
//声明类
final class 类名 {//类体}
//声明方法
修饰符(public/private/default/protected) final 返回值类型 方法名(){//方法体}
```

## 重写

- 方法重写只存在于子类和父类(包括直接父类和间接父类)之间。在同一个类中方法只能被重载，不能被重写。
- 静态方法不能重写。 
  - 父类的静态方法不能被子类重写为非静态方法。//编译出错 
  - 父类的非静态方法不能被子类重写为静态方法。//编译出错
  - 子类可以定义与父类的静态方法同名的静态方法。(但是这个不是覆盖)

```java
public class Person {
    private String name;
    public static void show(){
        System.out.println("我是人");
    }
}

public class Student extends Person{
    public static void show(){
        System.out.println("我是学生");
    }
}
//可以看出静态方法的调用只和变量声明的类型相关，这个和非静态方法的重写之后的效果完全不同
public class Test {
    public static void main(String[] args) {
        Person person=new Student();
        Student student=new Student();
        person.show();
        student.show();
    }
}
//输出结果：
//我是人
//我是学生
```

- 私有方法不能被子类重写，子类继承父类后，是不能直接访问父类中的私有方法的，那么就更谈不上重写了。

```java
public class Person{
	private void run(){}
}
//编译通过,但这不是重写,只是俩个类中分别有自己的私有方法
public class Student extends Person{
	private void run(){}
}
```

- 重写的语法
  - 方法名必须相同
  - 参数列表必须相同
  - 访问控制修饰符可以被扩大，但是不能被缩小： public protected default private 
  - 抛出异常类型的范围可以被缩小，但是不能被扩大： ClassNotFoundException ---> Exception 
  - 返回类型可以相同，也可以不同，如果不同的话，子类重写后的方法返回类型必须是父类方法返回类型的子类型。比如，父类方法的返回类型是Person,子类重写后的返回类可以是Person也可以是Person的子类型。

```java
public class Person {
    private String name;
    public void show(){
        System.out.println("我是人");
    }
}

public class Student extends Person{
    public static void show(){
        System.out.println("我是学生");
    }
}
//可以看出静态方法的调用只和变量声明的类型相关，这个和非静态方法的重写之后的效果完全不同
public class Test {
    public void main(String[] args) {
        Person person=new Student();
        Student student=new Student();
        person.show();
        student.show();
    }
}
//输出结果：
//我是学生
//我是学生
```

# 多态

## 多态的概述

- 多态是同一个行为具有多个不同表现形式或形态的能力。
- 多态就是同一个接口，使用不同的实例而执行不同操作。

## 多态存在的三个条件

- ①继承 ②重写 ③父类引用子类对象
- 当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误；如果有，再去调用子类的同名方法。

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/polymorphic.JPG)

```java
class Shape {
    void draw() {}
}
 
class Circle extends Shape {
    void draw() {
        System.out.println("Circle.draw()");
    }
}
 
class Square extends Shape {
    void draw() {
        System.out.println("Square.draw()");
    }
}
 
class Triangle extends Shape {
    void draw() {
        System.out.println("Triangle.draw()");
    }
}
```

## 重写、重载和多态的关系

- 重载是编译时多态。调用重载的方法，在编译期间就要确定调用的方法是谁,如果不能确定则编译报错。
- 重写是运行时多态。调用重写的方法，在运行期间才能确定这个方法到底是哪个对象中的。这个取决于调用方法的引用，在运行期间所指向的对象是谁，这个引用指向哪个对象那么调用的就是哪个对象中的方法。(java中的方法调用, 是运行时动态和对象绑定的)

## 无法表现多态特性的三种情况

- static方法，因为被static修饰的方法是属于类的，而不是属于实例的 
- final方法，因为被final修饰的方法无法被子类重写 
- private方法和protected方法，前者是因为被private修饰的方法对子类不可见，后者是因为尽管被 protected修饰的方法可以被子类见到，也可以被子类重写，但是它是无法被外部所引用的，一个不能被外部引用的方法，怎么能谈多态呢。

## 方法绑定

- 执行调用方法时，系统根据相关信息，能够执行内存地址中代表该方法的代码。分为静态绑定和动态绑定。
  - 静态绑定。在编译期完成，可以提高代码执行速度。
  - 动态绑定。通过对象调用的方法，采用动态绑定机制。这虽然让我们编程灵活，但是降低了代码的执行速度。这也是Java比C/C++速度慢的主要因素之一。Java中除了final类、final方、static方法，所有方法都是JVM在运行期才进行动态绑定的。

## instance of和类型转换

- instance of

```java
public class Person{
    public void run(){}
    }
}
public class Student extends Person{
}
public class Teacher extends Person{
}

public class test {
   	//Object-->Person-->Student
    //Object-->Person-->Teacher
    public static void main(String[] args) {
    	Object o = new Student();
        System.out.println(o instanceof Student);//true
        System.out.println(o instanceof Person);//true
        System.out.println(o instanceof Object);//true
        System.out.println(o instanceof Teacher);//false
        System.out.println(o instanceof String);//false
        System.out.println("=====================");
        Person p = new Student();
        System.out.println(p instanceof Student);//true
        System.out.println(p instanceof Person);//true
        System.out.println(p instanceof Object);//true
        System.out.println(p instanceof Teacher);//false
        //System.out.println(p instanceof String); 编译报错
        System.out.println("=====================");
        Person q = new Person();
        System.out.println(q instanceof Student);//false
        System.out.println(q instanceof Person);//true
        System.out.println(q instanceof Object);//true
        System.out.println(q instanceof Teacher);//false
        //System.out.println(q instanceof String); 编译报错
    }
}
//System.out.println(x instanceof Y); 
//该代码能否编译通过,主要是看声明变量x的类型和Y是否存在子父类的关系.有子父类关系就编译通过, 没有子父类关系就是编译报错。
//System.out.println(x instanceof Y);
//输出结果是true还是false,主要是看变量x所指向的对象实际类型是不是Y类型的"子类型"。
```

- 类型转换

```java
public class Person{
    public void run(){}
    }
public class Student extends Person{
	public void go(){}
}
public class Teacher extends Person{
}

public static void main(String[] args) {
    //编译报错,因为p声明的类型Person中没有go方法
    Person p = new Student();
    p.go();
    //需要把变量p的类型进行转换
    Person p = new Student();
    Student s = (Student)p;
    s.go();
    //或者下面这种形式，注意这种形式前面必须要俩个小括号
    ((Student)p).go();
    /*
        编译通过 运行没问题
        Object o = new Student();
        Person p = (Person)o;
        编译通过 运行没问题
        Object o = new Student();
        Student s = (Student)o;
        编译通过,运行报错
        Object o = new Teacher();
        Student s = (Student)o;
    */
    
    //X x = (X)o;
	//运行是否报错,主要是变量o所指向的对象实现类型,是不是X类型的子类型,如果不是则运行就会报错。
}
```

- 总结
  - 父类引用可以指向子类对象，子类引用不能指向父类对象。
  - 把子类对象直接赋给父类引用叫向上转型（upcasting），向上转型不用强制转型。 如Father father = new Son();
  - 把指向子类对象的父类引用赋给子类引用叫向下转型（downcasting），要强制转型。如father就是一个指向子类对象的父类引用，把father赋给子类引用son 即Son son =（Son） father。
  - upcasting 会丢失子类特有的方法,但是子类overriding 父类的方法，子类方法有效。

```java
public class Person {
    private String name;
    public void show(){
        System.out.println("我是人");
    }
}
public class Student extends Person{
    public void show(){
        System.out.println("我是学生");
    }
}
public static void main(String[] args) {
    Person person=new Student();//upcasting 会丢失子类特有的方法,但是子类overriding 父类的方法，子类方法有效
    person.show();
}
//输出结果：我是学生
```

# 接口和抽象类

## abstract修饰符

- abstract修饰符可以用来修饰方法也可以修饰类，如果修饰方法，那么该方法就是抽象方法；如果修饰类，那么该类就是抽象类。
- 抽象类中可以没有抽象方法，但是有抽象方法的类一定要声明为抽象类。
- 抽象类，不能使用new关键字来创建对象，它是用来让子类继承的。
- 抽象方法，只有方法的声明，没有方法的实现，它是用来让子类实现的。

```java
//抽象类
public abstract class Action{
    //抽象方法
    public abstract void doSomething();
    }
}

//子类继承父类
public class Sleep extends Action{
	//实现父类中没有实现的抽象方法
	public void doSomething(){
	//code
	}
}

public static void main(String[] args) {
    //编译报错,抽象类不能new对象
    Action a = new Action();
    
    //调用子类的重写方法
    Action a = new Sleep();
	a.doSomething();
}
```

## 接口和抽象类的区别

- 抽象类也是类，除了可以写抽象方法以及不能直接new对象之外,其他的和普通类没有什么不一样的。接口已经另一种类型了，和类是有本质的区别的，所以不能用类的标准去衡量接口。
- 声明类的关键字是class,声明接口的关键字是interface。
- 抽象类是用来被继承的，Java中的类是单继承。 类A继承了抽象类B,那么类A的对象就属于B类型了，可以使用多态 一个父类的引用，可以指向这个父类的任意子类对象。
- 接口是用来被类实现的，Java中的接口可以被多实现。 类A实现接口B、C、D，那么类A的对象就属于B、C、D类型了，可以使用多态，一个接口的引用,可以指向这个接口的任意实现类对象

## 接口的特征

- 接口中的方法都是抽象方法。接口中的变量都是静态常量(public static final修饰)。

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

- 一个类可以实现多个接口

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
//run
//sleep
//sleep
```

- 一个接口可以继承多个父接口

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

## 接口的作用

- 接口的最主要的作用是达到统一访问，就是在创建对象的时候用接口创建 【接口名】 【对象名】= new 【实现接口的类】 这样你像用哪个类的对象就可以new哪个对象了，不需要改原来的代码。 
- 假如我们两个类中都有个function()的方法，如果我用接口，那样我new a()；就是用a的方法，new b()；就是用b的方法 这个就叫统一访问，因为你实现这个接口的类的方法名相同，但是实现内容不同。

## 接口的总结

- Java接口中的成员变量默认都是public，static,final类型的(都可省略),必须被显示初始化,即接口中的成员变量为常量(大写,单词之间用"_"分隔)。
- Java接口中的方法默认都是public，abstract类型的(都可省略)，没有方法体，不能被实例化。
- Java接口中只能包含public，static，final类型的成员变量和public，abstract类型的成员方法。
- 一个接口不能实现(implements)另一个接口，但它可以继承多个其它的接口。
- Java接口必须通过类来实现它的抽象方法。
- 当类实现了某个Java接口时,它必须实现接口中的所有抽象方法,否则这个类必须声明为抽象类。
- 不允许创建接口的实例(实例化)，但允许定义接口类型的引用变量，该引用变量引用实现了这个接口的类的实例。
- 一个类只能继承一个直接的父类,但可以实现多个接口，间接的实现了多继承。
