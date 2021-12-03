---
title: Java基础语法03｜变量和常量
tags:
    - Java
categories:
    - JavaSE 
date: 2021-12-2 21:40:15
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/javagrammar.png
---

# 变量

## 变量的定义

- 在程序执行的过程中变量的值会发生变化，直白来说就是用来存储可变化的数据。从本质上讲，变量其实指代的是内存中的一小块存储空间，空间位置是确定的，但是里面放置什么值不确定。
- 比如屋子里有多个鞋柜，而你有很多双不同品牌的鞋，鞋柜里可以放A品牌的鞋，也可以放B品牌的鞋等等，你给每一个鞋柜设计个标签，至于这些鞋柜里放哪些品牌的鞋需要你自己去放。这些标签相当于我们定义的变量，至于变量里放什么，你可以自行决定。

## 变量的声明格式

```java
type identifier [ = value][, identifier [= value] ...] ;
//数据类型 变量名 = 值；可以使用逗号隔开来声明多个同类型变量。
//比如int a = 1, b = 2, c = 3;
```

## 变量的注意事项

- 每个变量都有类型，类型可以是基本类型，也可以是引用类型。

- 变量名必须是合法的标识符。

- 变量声明是一条完整的语句，因此每一个声明都必须以分号结束
- 逐一声明每一个变量可以提高程序可读性。

## 变量的作用域

- 类变量（静态变量： static variable）：独立于方法之外的变量，用 static 修饰。

- 实例变量（成员变量：member variable）：独立于方法之外的变量，不过没有 static 修饰。

- 局部变量（lacal variable）：类的方法中的变量。

### 类变量（静态变量）

- 类变量也称为静态变量，在类中以 static 关键字声明，但必须在方法之外。无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。
- Java 中被 static 修饰的成员称为静态成员或类成员。它属于整个类所有，而不是某个对象所有，即被类的所有对象所共享。
- 静态变量从属于类，生命周期伴随类始终，从类加载到卸载。
- 静态变量默认值和实例变量相似。数值型变量默认值是 0，布尔型默认值是 false，引用类型默认值是 null。变量的值可以在声明的时候指定，也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。

```java
public class JavaBase03 {
    public static String name;//静态变量 方法之外

    public static void main(String[] args) {
        name="Jasper";
        System.out.println("我的名字是"+name);
    }
}
//输出结果：我的名字是Jasper
```

### 实例变量

- 实例变量声明在一个类中，但在方法、构造方法和语句块之外。当一个对象被实例化之后，每个实例变量的值就跟着确定。
- 实例变量从属于对象，生命周期伴随对象始终，在对象创建的时候创建，在对象被销毁的时候销毁。
- 实例变量可以声明在使用前或者使用后，访问修饰符可以修饰实例变量，一般情况下应该把实例变量设为私有。
- 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在初始化块和构造方法中指定。

```java
public class JavaBase03 {
    // 这个实例变量对子类可见
    public String animal;
    // 这个实例变量是私有变量，仅在该类可见
    private int age;
    private String hobby="奔跑";//1.声明赋值
    {
        animal="老虎";//2.代码块赋值
    }
    public JavaBase03(int age) {
        this.age = age;
    }
    public void show(){
        System.out.println("animal="+animal+",age="+age+",hobby="+hobby);
    }
    public static void main(String[] args) {

        JavaBase03 info=new JavaBase03(4);//3.构造方法赋值
        info.show();
    }
}
//输出结果：animal=老虎,age=4,hobby=奔跑
```

### 局部变量

- 局部变量声明在方法、构造方法或者语句块中，在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁。
- 访问修饰符不能用于局部变量，局部变量是在栈上分配的。
- 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。

```java
public class JavaBase03 {
    private int number=0;//全局变量
    public int sum(){
        int number=1;//局部变量
        int sum=0;
        for (;number<3;number++){
            sum=sum+number;
        }
        return sum;
    }//当函数执行完毕，变量被销毁
 	public static void main(String[] args) {
        JavaBase03 info=new JavaBase03();
        System.out.println("sum="+info.sum()+";number="+info.number);
    }   
}
//输出结果：sum=3;number=0
```

# 常量

- 所谓常量可以理解成一种特殊的变量，它的值被设定后，在程序运行过程中不允许被改变。
- 常量名一般使用大写字符。程序中使用常量可以提高代码的可维护性。

```java
//常量声明格式 final 常量名=值;
final double PI=3.14;
final String SEX="男";
```

# 命名规范

- 所有变量、方法、类名：见名知意。

- 类变量、实例变量和局部变量首字母小写，并且遵循驼峰原则。比如：nextMonth。
- 常量大写字母和下划线。比如：MIN_VALUE。
- 类名首字母大写，并且遵循驼峰原则。比如：HelloWorld。
- 方法名首字母小写，并且遵循驼峰原则。比如：twiceJump()。

# 运算符

## 算术运算符

```java
public static void main(String[] args) {
    int a = 10;
    int b = 20;
    int c = 25;
    int d = 25;
    System.out.println("a + b = " + (a + b) );
    System.out.println("a - b = " + (a - b) );
    System.out.println("a * b = " + (a * b) );
    System.out.println("b / a = " + (b / a) );
    System.out.println("b % a = " + (b % a) );
    System.out.println("c % a = " + (c % a) );
    System.out.println("a++   = " +  (a++) );
    System.out.println("a--   = " +  (a--) );
    // 查看  d++ 与 ++d 的不同
    //首先在控制台输出，然后d自增为26
    System.out.println("d++   = " +  (d++) );
    //首先将d自增为27，然后在控制台输出
    System.out.println("++d   = " +  (++d) );
}
/*  输出结果：
	a + b = 30
    a - b = -10
    a * b = 200
    b / a = 2
    b % a = 0
    c % a = 5
    a++ = 10
    a-- = 11
    d++ = 25
    ++d = 27
*/
```

## 关系运算符

```java
public static void main(String[] args) {
    int a = 10;
    int b = 20;
    System.out.println("a == b = " + (a == b) );
    System.out.println("a != b = " + (a != b) );
    System.out.println("a > b = " + (a > b) );
    System.out.println("a < b = " + (a < b) );
    System.out.println("b >= a = " + (b >= a) );
    System.out.println("b <= a = " + (b <= a) );
}
/*
	输出结果：
	a == b = false
    a != b = true
    a > b = false
    a < b = true
    b >= a = true
    b <= a = false
*/
```

## 位运算符

```java
public static void main(String[] args) {
    int a = 60; /* 60 = 0011 1100 */ 
    int b = 13; /* 13 = 0000 1101 */
    int c = 0;
    //& 如果相对应位都是1，则结果为1，否则为0
    c = a & b;       /* 12 = 0000 1100 */
    System.out.println("a & b = " + c );
    //| 如果相对应位都是0，则结果为0，否则为1
    c = a | b;       /* 61 = 0011 1101 */
    System.out.println("a | b = " + c );
    //^ 如果相对应位值相同，则结果为0，否则为1
    c = a ^ b;       /* 49 = 0011 0001 */
    System.out.println("a ^ b = " + c );
    //~ 按位取反运算符翻转操作数的每一位，即0变成1，1变成0
    c = ~a;          /*-61 = 1100 0011 */
    System.out.println("~a = " + c );
    //<< 按位左移运算符。左操作数按位左移右操作数指定的位数
    c = a << 2;     /* 240 = 1111 0000 */
    System.out.println("a << 2 = " + c );
    //>> 按位右移运算符。左操作数按位右移右操作数指定的位数
    c = a >> 2;     /* 15 = 1111 */
    System.out.println("a >> 2  = " + c );
    //>>> 按位右移补零操作符。左操作数的值按右操作数指定的位数右移，移动得到的空位以零填充
    c = a >>> 2;     /* 15 = 0000 1111 */
    System.out.println("a >>> 2 = " + c );
}
/*
	输出结果：
	a & b = 12
    a | b = 61
    a ^ b = 49
    ~a = -61
    a << 2 = 240
    a >> 2  = 15
    a >>> 2 = 15
*/
```

## 逻辑运算符

```java
 public static void main(String[] args) {
     boolean a = true;
     boolean b = false;
     //&& 称为逻辑与运算符。当且仅当两个操作数都为真，条件才为真
     System.out.println("a && b = " + (a&&b));
     //|| 称为逻辑或操作符。如果任何两个操作数任何一个为真，条件为真
     System.out.println("a || b = " + (a||b) );
     //! 称为逻辑非运算符。用来反转操作数的逻辑状态。如果条件为true，则逻辑非运算符将得到false
     System.out.println("!(a && b) = " + !(a && b));
}
/*
	输出结果：
    a && b = false
    a || b = true
    !(a && b) = true
*/
```

## 赋值运算符

```java
public static void main(String[] args) {
    int a = 10;
    int b = 20;
    int c = 0;
    c = a + b;
    System.out.println("c = a + b = " + c );
    c += a ;
    System.out.println("c += a  = " + c );
    c -= a ;
    System.out.println("c -= a = " + c );
    c *= a ;
    System.out.println("c *= a = " + c );
    a = 10;
    c = 15;
    c /= a ;
    System.out.println("c /= a = " + c );
    a = 10;
    c = 15;
    c %= a ;
    System.out.println("c %= a  = " + c );
    c <<= 2 ;
    System.out.println("c <<= 2 = " + c );
    c >>= 2 ;
    System.out.println("c >>= 2 = " + c );
    c >>= 2 ;
    System.out.println("c >>= 2 = " + c );
    c &= a ;
    System.out.println("c &= a = " + c );
    c ^= a ;
    System.out.println("c ^= a = " + c );
    c |= a ;
    System.out.println("c |= a = " + c );
}
/*
	输出结果：
	c = a + b = 30
    c += a  = 40
    c -= a = 30
    c *= a = 300
    c /= a = 1
    c %= a  = 5
    c <<= 2 = 20
    c >>= 2 = 5
    c >>= 2 = 1
    c &= a = 0
    c ^= a = 10
    c |= a = 10
*/
```

## 条件运算符

```java
//基本格式：variable x = (expression) ? value if true : value if false
public static void main(String[] args){
    int a , b;
    a = 10;
    // 如果 a 等于 1 成立，则设置 b 为 20，否则为 30
    b = (a == 1) ? 20 : 30;
    System.out.println( "Value of b is : " +  b );

    // 如果 a 等于 10 成立，则设置 b 为 20，否则为 30
    b = (a == 10) ? 20 : 30;
    System.out.println( "Value of b is : " + b );
}
/*
	输出结果：
	Value of b is : 30
	Value of b is : 20
*/
```

## 字符串连接符

- 只要有一个是字符串(String)类型，系统会自动将另一个操作数转换为字符串然后再进行连接。

```java
String a="Hello world";
String b=3.14+a;
System.out.println("b="+b);
//输出结果：b=3.14Hello world
```

## 运算符优先级

- 下表中具有最高优先级的运算符在的表的最上面，最低优先级的在表的底部。

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/operator.JPG)
