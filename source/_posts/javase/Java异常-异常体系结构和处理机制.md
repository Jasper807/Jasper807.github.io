---
title: Java异常｜异常体系结构和处理机制
tags:
    - Java
categories:
    - JavaSE 
date: 2021-12-02 22:14:11
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/javaexception.png
---

# 异常的概念

- 异常是程序中的一些错误，但并不是所有的错误都是异常，并且错误有时候是可以避免的。

## 异常发生的原因

- 异常发生的原因有很多，通常包含以下几大类
  - 用户输入了非法数据。
  - 要打开的文件不存在。
  - 网络通信时连接中断，或者JVM内存溢出。
- 这些异常有的是因为用户错误引起，有的是程序错误引起的，还有其它一些是因为物理错误引起的。

## 异常的三种类型

- **检查性异常**：最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。
- **运行时异常**： 运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。
- **错误**： 错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到的。

# 异常体系结构

- 所有异常类型都是内置类 Throwable 的子类，因而 Throwable 在异常类的层次结构的顶层。 
- Throwable 分成两个不同的分支
  - 一个分支是Error，它表示不希望被程序捕获或者是程序无法处理的错误。
  - 另一个分支是Exception，它表示用户程序可能捕捉的异常情况或者说是程序可以处理的异常。
- 异常类 Exception 又分为运行时异常( RuntimeException )和非运行时异常。
- Java异常又可以分为不受检查异常（ Unchecked Exception ）和检查异常（ Checked Exception ）。

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/exception.JPG)

# 异常之间的区别和联系

## Error

- Error 类对象由 Java 虚拟机生成并抛出，大多数错误与代码编写者所执行的操作无关。
- 比如说： Java虚拟机运行错误（ Virtual MachineError ），当JVM不再有继续执行操作所需的内存资源时， 将出现 OutOfMemoryError 。这些异常发生时，Java虚拟机（JVM）一般会选择线程终止。
- 还有发生在虚拟机试图执行应用时，如类定义错误（ NoClassDefFoundError ）、链接错误 （ LinkageError ）。这些错误是不可查的，因为它们在应用程序的控制和处理能力之 外，而且绝大多数是程序运行时不允许出现的状况。

## Exception

- Exception 分支中有一个重要的子类 RuntimeException （运行时异常），该类型的异常自动为你所编写的程序定义 ArrayIndexOutOfBoundsException （数组下标越界）、 NullPointerException （空指针异常）、ArithmeticException （算术异常）、 MissingResourceException （丢失资源）、 ClassNotFoundException （找不到类）等异常，这些异常是不检查异常，程序中可以选择捕获处理，也可以不处理。 这些异常一般是由程序逻辑错误引起的，程序应该从逻辑角度尽可能避免这类异常的发生。
- 而 RuntimeException 之外的异常我们统称为非运行时异常，类型上属于 Exception 类及其子类， 从程序语法角度讲是必须进行处理的异常，如果不处理，程序就不能编译通过。如 IOException 、 SQLException 等以及用户自定义的 Exception 异常，一般情况下不自定义检查异常。

## 检查异常和不受检查异常

### 检查异常

- 在正确的程序运行过程中，很容易出现的、情理可容的异常状况，在一定程度上这种异常的 发生是可以预测的，并且一旦发生该种异常，就必须采取某种方式进行处理。
- 除了RuntimeException及其子类以外，其他的Exception类及其子类都属于检查异常，当程序中可能出现这类异常，要么使用try-catch语句进行捕获，要么用throws子句抛出，否则编译无法通过。

### 不受检查异常

- 包括RuntimeException及其子类和Error。

### 区别

- 不受检查异常为编译器不要求强制处理的异常， 检查异常则是编译器要求必须处置的异常。

# Java异常处理机制

## 抛出异常

- 当一个方法出现错误引发异常时，方法创建异常对象并交付运行时系统，异常对象中包含了异常类型和异常出现时的程序状态等异常信息。运行时系统负责寻找处置异常的代码并执行。

## 捕获异常

- 在方法抛出异常之后，运行时系统将转为寻找合适的异常处理器（exception handler）。潜在的异常处理器是异常发生时依次存留在调用栈中的方法的集合。当异常处理器所能处理的异常类型与方法抛出的异常类型相符时，即为合适的异常处理器。
- 运行时系统从发生异常的方法开始，依次回查调用栈中的方法，直至找到含有合适异常处理器的方法并执行。当运行时系统遍历调用栈而未找到合适的异常处理器，则运行时系统终止。同时，意味着Java程序的终止。
- 对于运行时异常 、错误 和检查异常 ，Java技术所要求的异常处理方式有所不同
  - 由于运行时异常及其子类的不可查性，为了更合理、更容易地实现应用程序，Java规定，运行时异常将由Java运行时系统自动抛出，允许应用程序忽略运行时异常。
  - 对于方法运行中可能出现的 Error ，当运行方法不欲捕捉时，Java允许该方法不做任何抛出声明。因为，大多数 Error 异常属于永远不能被允许发生的状况，也属于合理的应用程序不该捕捉的异常。
  - 对于所有的检查异常，Java规定，一个方法必须捕捉，或者声明抛出方法之外。也就是说，当一个方法选择不捕捉检查异常时，它必须声明将抛出异常。

# 异常处理5个关键字

- try -- 用于监听。将要被监听的代码(可能抛出异常的代码)放在try语句块之内，当try语句块内发生异常时，异常就被抛出。
- catch -- 用于捕获异常。catch用来捕获try语句块中发生的异常。 
- finally -- finally语句块总是会被执行。它主要用于回收在try块里打开的物力资源(如数据库连接、网络 连接和磁盘文件)。只有finally块执行完成之后，才会回来执行try或者catch块中的return或者throw语句，如果finally中使用了return或者throw等终止方法的语句，则就不会跳回执行，直接停止。 

```java
//例子1
//如果finally中使用了return或者throw等终止方法的语句，则就不会跳回执行，直接停止。
public class test {
    public  static int testFinally(){
        try{
            throw new Exception();
        }catch(Exception e){
            System.out.println("catch is begin");
            return 1;
        }finally{
            System.out.println("finally is begin");
            return 2;
        }
    }
    public static void main(String[] args) {
        System.out.println(testFinally());
    }
}
/*
	输出结果：	
	catch is begin
	finally is begin
	2
*/

//例子2 
//只有finally块执行完成之后，才会回来执行try或者catch块中的return或者throw语句
public class test {
    public  static int testFinally(){
        try{
            throw new Exception();
        }catch(Exception e){
            System.out.println("catch is begin");
            //return 1;
        }finally{
            System.out.println("finally is begin");
            return 2;
        }
    }
    public static void main(String[] args) {
        System.out.println(testFinally());
    }
}
/*
	输出结果：	
	catch is begin
	finally is begin
	1
*/
```

- throw -- 用于抛出异常。 
- throws -- 用在方法签名中，用于声明该方法可能抛出的异常。

```java
public void test() throws Exception {
    throw new Exception();
}
//throws表示一个方法声明可能抛出一个异常，throw表示此处抛出一个已定义的异常（可以是自定义需继承Exception，也可以是java自己给出的异常类
```

## try-catch

### 语法形式

```java
try{
	//code that might generate exceptions
}catch(Exception e){
	//the code of handling exception1
}catch(Exception e){
	//the code of handling exception2
}
```

- try 后的一对大括号将一块可能发生异常的代码包起来，即为监控区域。Java方法在运行过程中发生了异常，则创建异常对象。
- 将异常抛出监控区域之外，由Java运行时系统负责寻找匹配的 catch 子句来捕获异常。若有一个 catch 语句匹配到了，则执行该 catch 块中的异常处理代码，就不再尝试匹配别的 catch 块了。
- 如果抛出的异常对象属于 catch 子句的异常类，或者属于该异常类的子类，则认为生成 的异常对象与 catch 块捕获的异常类型相匹配。

```java
//例子1
//try-catch捕获异常
public static void main(String[] args) {
        int a = 1;
        int b = 0;
        //System.out.println("a/b的值是：" + a / b);
        try { // try监控区域
            if (b == 0) throw new ArithmeticException(); // 通过throw语句抛出异常
            System.out.println("a/b的值是：" + a / b);
            System.out.println("this will not be printed!");
        }
        catch (ArithmeticException e) { // catch捕捉异常
            System.out.println("程序出现异常，变量b不能为0！");
            //若为语句System.out.println("程序出现异常"+e);
            //输出 程序出现异常java.lang.ArithmeticException
        }
        System.out.println("程序正常结束。");
    }
}
/*
	输出结果：	
    程序出现异常，变量b不能为0！
    程序正常结束。
*/

//例子2
//算术异常属于运行时异常，因而实际上该异常不需要程序抛出，运行时系统自动抛出。如果不用try-catch程序就不会往下执行了.
public class TestException {
	public static void main(String[] args) {
		int a = 1;
		int b = 0;
		System.out.println("a/b的值是：" + a / b);
		System.out.println("this will not be printed!");
	}
}
/*
	输出结果：	
    Exception in thread "main" java.lang.ArithmeticException: / by zero
    at TestException.main(TestException.java:34)
*/
```

### 使用多重的catch语句

- 很多情况下，由单个的代码段可能引起多个异常。处理这种情况，我们需要定义两个或者更多的 catch 子句，每个子句捕获一种类型的异常，当异常被引发时，每个 catch子句被依次检查，第一个匹配异常类型的子句执行，当一个 catch 子句执行以后，其他的子句将不执行。

- 编写多重catch语句块异常顺序先小后大，即先子类后父类。

```java
public static void main(String[] args) {
        int a = 1;
        int b = 0;
        //System.out.println("a/b的值是：" + a / b);
        try { // try监控区域
            if (b == 0) throw new ArithmeticException(); // 通过throw语句抛出异常
            System.out.println("a/b的值是：" + a / b);
            System.out.println("this will not be printed!");
        }
        catch (ArrayIndexOutOfBoundsException e){
            System.out.println("ArrayIndexOutOfBoundsException 数组越界！");
        }
        catch (ArithmeticException e) { // catch捕捉异常
            System.out.println("ArithmeticException 程序出现异常，变量b不能为0！");
        }catch (Exception e){
            System.out.println("Exception 程序出现异常，变量b不能为0！");
        }
}
/*
	输出结果：	
    ArithmeticException 程序出现异常，变量b不能为0！
*/
```

### 嵌套try语句

-  try 语句可以被嵌套。也就是说，一个 try 语句可以在另一个 try 块的内部。每次进入 try 语句，异常的前后关系都会被推入堆栈。如果一个内部的 try 语句不含特殊异常的 catch 处理程序，堆栈将弹出，下一个 try 语句的 catch 处理程序将检查是否与之匹配。
- 这个过程将继续直到一个 catch 语句被匹配成功，或者是直到所有的嵌套 try 语句被检查完毕。如果没有 catch 语句匹配，Java运行时系统将处理这个异常。

```java
//嵌套try的多种情况

//情况1 嵌套try，内层中没有catch语句
//最外部的try语句块中嵌套了一个try-finally语句，内部的try语句中抛出了一个异常
//但是内部没有catch语句块，所以会执行最近的一个catch语句块，但是在跳出外部try包含语句块之前，需要先执行内部的finally语句块中的代码
public static void main(String[] args) {
    try{
        try {
            throw new Exception("ex");
        }
        finally {
            System.out.println("in finally");
        }
    } catch(Exception e){
        System.out.println("out "+e);
    }
}
//输出结果：
//in finally
//out java.lang.Exception: ex

//情况2 嵌套try，但内层有catch
//内部嵌套的语句块中有catch语句，所以当内部try语句块中抛出异常时，会接着执行内部的catch语句块，然后执行finally子句
public static void main(String[] args) {
    try{
        try {
            throw new Exception("ex");
        }
        catch(Exception e){
            System.out.println("in "+e);
        }
        finally {
            System.out.println("in finally");
        }
    } catch(Exception e){
        System.out.println("out "+e);
    }
}
//输出结果：
//in java.lang.Exception: ex
//in finally

//情况3 嵌套try，但内层有catch且在内层catch再throw
//上面例子的基础上，内部的catch语句块中又抛出了一个异常,在执行完内部相应语句后，会接着执行外部的catch语句
public static void main(String[] args) {
    try{
        try {
            throw new Exception("ex");
        }
        catch(Exception e){
            System.out.println("in "+e);
            throw new Exception("ex2");
        }
        finally {
            System.out.println("in finally");
        }
    } catch(Exception e){
        System.out.println("out "+e);
    }
}
//输出结果：
//in java.lang.Exception: ex
//in finally
//out java.lang.Exception: ex2
```

## throw

### 语法形式

```java
throw ThrowableInstance;
```

- 这里的ThrowableInstance一定是 Throwable 类类型或者 Throwable 子类类型的一个对象。
- 有两种方法可以获取 Throwable 对象：在catch子句中使用参数或者使用 new 操作符创建。程序执行完 throw 语句之后立即停止； throw 后面的任何语句不被执行，最邻近的 try 块用来检查它是否含有一个与异常类型匹配的 catch 语句

```java
//该程序两次处理相同的错误，首先， main() 方法设立了一个异常关系然后调用proc()。proc()方法设立了另一个异常处理关系并且立即抛出一个 NullPointerException 实例，NullPointerException 在 main() 中被再次捕获。
public static void proc(){
    try{
        throw new NullPointerException("null pointer");
    }catch(NullPointerException e){
        System.out.println("Caught inside proc");
        throw e;//在catch子句中使用参数或者使用 new 操作符创建
    }
}
public static void main(String[] args) {
    try{
        proc();
    }catch(NullPointerException e){
        System.out.println("Recaught: "+e.getMessage());
    }
}
//输出结果：
//Caught inside proc
//Recaught: null pointer
```

## throws

### 语法形式

```java
public void info() throws Exception
{
	//body of method
}
```

- 如果一个方法可以导致一个异常但不处理它，它必须指定这种行为以使方法的调用者可以保护它们自己而不发生异常。要做到这点，我们可以在方法声明中包含一个 throws 子句。、

```java
public class Test{
	public static void throw1() throws IllegalAccessException {
		System.out.println("Inside throw1 . ");
		throw new IllegalAccessException("demo");
	}
	public static void main(String[] args){
		try {
			throw1();
		}catch(IllegalAccessException e ){
			System.out.println("Caught " + e);
		}
	}
}
//输出结果：
//Inside throw1. 
//Caught java.lang.IllegalAccessException: demo
```

- 如果是不受检查异常（ unchecked exception ），即 Error 、 RuntimeException 或它们的子类，那么可以不使用 throws 关键字来声明要抛出的异常，编译仍能顺利通过，但在运行 时会被系统抛出。

- 必须声明方法可抛出的任何检查异常（ checked exception ）。即如果一个方法可能出现受可 查异常，要么用 try-catch 语句捕获，要么用 throws 子句声明将它抛出，否则会导致编译错误。

- 仅当抛出了异常，该方法的调用者才必须处理或者重新抛出该异常。当方法的调用者无力处理该异 常的时候，应该继续抛出。
- 调用方法必须遵循任何可查异常的处理和声明规则。若覆盖一个方法，则不能声明与覆盖方法不同 的异常。声明的任何异常必须是被覆盖方法所声明异常的同类或子类。

## finally

- finally 创建的代码块在 try/catch 块完成之后另一个 try/catch 出现之前执行。finally 块无论有没有异常抛出都会执行。如果抛出异常，即使没有 catch 子句匹配， finally 也会执行。

```java
//例子1 finally 块无论有没有异常抛出都会执行
public static void main(String[] args) {
    try{
        System.out.println("begin finally");
        return;

    } finally{
        System.out.println("end finally");
    }
}
//输出结果：
//begin finally
//end finally

//例子2 如果抛出异常，即使没有catch子句匹配， finally也会执行
public static void testFinally() throws Exception{
    try{
        throw new Exception("ex");
    }finally {
        System.out.println("method finally");
    }
}
public static void main(String[] args){
    try{
        System.out.println("begin finally");
        testFinally();
    } catch (Exception e) {
        System.out.println("Exception:"+e.getMessage());
    } finally{
        System.out.println("end finally");
    }
}
//输出结果：
//begin finally
//method finally
//Exception:ex
//end finally
```

### try, catch,finally ,return 执行顺序

- 1.执行try，catch ， 给返回值赋值 
- 2.执行finally 
- 3.return

# 自定义异常步骤

- 创建自定义异常类。 
- 在方法中通过 throw 关键字抛出异常对象。 
- 如果在当前抛出异常的方法中处理异常，可以使用 try-catch 语句捕获并处理；否则在方法的 声明处通过 throws 关键字指明要抛出给方法调用者的异常，继续进行下一步操作。 
- 在出现异常方法的调用者中捕获并处理异常。

```java
class MyException extends Exception {
    private int detail;
    MyException(int a){
        detail = a;
    }
    public String toString(){
        return "MyException ["+ detail + "]";
    }
}
public class TestMyException{
    static void compute(int a) throws MyException{
        System.out.println("Called compute(" + a + ")");
        if(a > 10){
            throw new MyException(a);
        }
        System.out.println("Normal exit!");
    }
    public static void main(String [] args){
        try{
			compute(1);
			compute(20);
		}catch(MyException me){
			System.out.println("Caught " + me.toString());
		}
	}
}
//输出结果：
//Called compute(1)
//Normal exit!
//Called compute(20)
//Caught MyException [20]
```

