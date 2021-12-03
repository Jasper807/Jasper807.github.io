---
title: Java基础语法02｜数据类型
tags:
    - Java
categories:
    - JavaSE 
date: 2021-12-2 21:35:11
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/javagrammar.png
---
# 计算机相关知识

## 计算机采用二进制进行数据运算和处理

1. 计算机不像人一样会列式子算算术，它更喜欢用高低两个电平来表示两个不同的状态，因为这样对它来说处理数据更加容易。
2. 计算机内部采用二进制进行数据运算和处理，其中0和1两个数码，刚好数码1可以表示高电平，数码0可以表示低电平。将数据转换为二进制这样计算机就能分的清楚了。
3. 举个简单的例子，以8位运算为例（现在计算机大多32位或者64位），将1和2进行相加，计算机先将这两个数转换为自己看的懂的二进制补码00000001和00000010，然后通过加法器相加为00000011，最后再将结果转换为3。

## 计算机位和字节的概念

1. 位是计算机内部数据存储的最小单位，通常也称为比特（bit），简称为b。每1个二进制数字0或1就是1个位。

   比如说1100就是一个4位二进制数，01101011就是一个8位二进制数。

2. 字节（Byte），简称B，是计算机中数据处理的基本单位，每8位就是一个字节。

3. 字符是计算机中字母、数字、符号的统称。

```java
1B(字节，Byte)=8b（位，bit，比特）
1KB=1024B 
1MB=1024KB 
1GB=1024MB
1001100110011001是一个16位二进制数，可表示为2个字节
```

## 原码、反码、补码之间的关系

```java
以8位运算为例
+3(真值)--00000011(原码)--00000011(反码)--00000011(补码)
-3(真值)--10000011(原码)--11111100(反码)--11111101(补码)
```



![原反补关系](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/threecode.jpg)

# 数据类型

![数据类型](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/datatype.jpg)

## 1.基本数据类型及大小、封装类

![基本数据类型](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/basicdatatype.jpg)

## 2.基本数据类型在编译器中的实践

```java
public class JavaBase02 {
    public static void main(String[] args) {
        //基本类型byte
        System.out.println("二进制位数：" + Byte.SIZE);
        System.out.println("字节：Byte.BYTE="+Integer.BYTES);
        System.out.println("包装类：java.lang.Byte");
        System.out.println("最小值：Byte.MIN_VALUE=" + Byte.MIN_VALUE);
        System.out.println("最大值：Byte.MAX_VALUE=" + Byte.MAX_VALUE);

        //基本类型int
        System.out.println("二进制位数：" + Integer.SIZE);
        System.out.println("字节：Byte.BYTE="+Integer.BYTES);
        System.out.println("包装类：java.lang.Integer");
        System.out.println("最小值：Byte.MIN_VALUE=" + Integer.MIN_VALUE);
        System.out.println("最大值：Byte.MAX_VALUE=" + Integer.MAX_VALUE);
        /*输出结果：
          二进制位数：8
          字节：Byte.BYTE=4
          包装类：java.lang.Byte
          最小值：Byte.MIN_VALUE=-128
          最大值：Byte.MAX_VALUE=127
          二进制位数：32
          字节：Byte.BYTE=4
          包装类：java.lang.Integer
          最小值：Byte.MIN_VALUE=-2147483648
          最大值：Byte.MAX_VALUE=2147483647
        */
        
        //其他数据类型也同理
    }
}
```

## 3.字节型/整型/短整型/长整型（byte/int/short/long）

```java
//Java语言的整型常数默认为int型，浮点数默认是Double
//byte、int、short和long都可以用十进制、16进制以及8进制的方式来表示
//byte
byte b1=50;
//int
int i1=10; //十进制形式表示 输出10
int i2=010; //八进制形式，以0开头 输出8
int i3=0x10; //十六进制形式，以0x/0X开头 输出16
int i4=0X10;
//short
short s1=20;
//long
long l1=10000000000l;
long l2=10000000000L; 
```

## 4.单精度浮点型/双精度浮点型（float/double）

```java
//Java语言的整型常数默认为int型，浮点数默认是Double
//double
double d1=3.14d;
double d2=3.14D; 
//float
float f1=3.14f;
float f2=3.14F; 
/*浮点数在计算机中大部分都是表示近似值
  并不是所有的小数都能可以精确的用二进制浮点数表示
  因此浮点数之间不能比较大小，避免比较中使用浮点数 */
System.out.println(d1==f1); //false
System.out.println(d1==d2); //true
```

## 5.字符型（char）

- char 类型是一个单一的 16 位 Unicode 字符，char 数据类型可以储存任何字符。

- char类型最小值是 \u0000（十进制等效值为0），最大值是 \uffff（十进制等效值为65535）。

- ASCII编码是1个字节，而Unicode编码通常是2个字节。
  比如说字母A用ASCII编码表示是十进制的65，二进制的01000001；

  而在Unicode中，只需要在前面补0，即为：00000000 01000001。

- char类型的字符转换为int类型，即将字母转换为对应的ASCII编码值


```java
public class JavaBase02 {
    public static void main(String[] args) {
        //char
        char c1='a';
        int i5 = c1;//char自动类型转换为int
        System.out.println("char->int i5值="+i5); //输出结果：i5=97 因为a的ASCII码=97
        char c2 = 'A';//定义一个char类型
        int i6 = c2+1;//char 类型和 int 类型计算
        System.out.println("char->int i6值="+i6);//输出结果：i6=66 因为A的ASCII码=65，65+1=66
    }
}
```

## 6.布尔型（boolean）

```java
//boolean数据类型表示一位的信息
boolean b1=true;
boolean b2=false;
if (b1){ //b1等价于b1==true
    System.out.println("true");
}else {
    System.out.println("false");
}
```

# 类型转换

## 1.类型转换注意事项

```java
byte,short,char—> int —> long—> float —> double 
低------------------------------------------>高
```

1. 不能对boolean类型进行类型转换。

```java
//boolean b3=(boolean) 3; 错误，不能将int类型的3转换为boolean类型
//int i7=(int) true; 错误 不能将boolean类型的true转换为int类型
```

2. 不能把对象类型转换成不相关类的对象。

- 类是对象的集合，对象是类的实例。对象是通过new className产生的，用来调用类的方法、类的构造方法。总之，类就是有相同特征的事物的集合，而对象就是类的一个具体实例。
- Java中的一切都可以称为对象，基本数据类型都有对应的包装类（比如int的包装类是Integer），包装类自然就是对象，比如我创建了peron类和plant类，有姓名、身高和体重三个对象，我总不能把人(person)类的名字转换成植物(plant)类的名字吧。

```java
public class Person {
    private String name=new String(); //姓名
    private int height=new Integer(0); //身高
    private int weight=new Integer(0); //体重

    public Person() {}
    public Person(String name, int height, int weight) {
        this.name = name;
        this.height = height;
        this.weight = weight;
    }
    public void doSth() {
        //... do something
    }

    //some methods...

    public static void main(String[] args) {
        Person personA=new Person();
        personA.name="张三";
        personA.height=178;
        personA.weight=70;
        System.out.println("姓名:"+personA.name+";身高:"+personA.height+"m;体		重:"+personA.weight+"斤");
		//输出结果：姓名:张三;身高:178m;体重:70斤
    }
}
```

3. 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。

```java
int i7=97;
char c3=(char)i7;
System.out.println("c3="+c3); //输出结果:c3=a
```

4. 转换过程中可能导致溢出或损失精度。
5. 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入。

```java
int i8 =128;
byte b3 = (byte)i8;
System.out.println("b3="+b3);
//输出结果：b3=-128 因为byte类型是8位，最大值为127，值128时候就会导致溢出
double d4=3.14;
int i9= (int) d4;
System.out.println("i9="+i9);
//输出结果：i9=3 因为浮点数转换为整数损失精度，舍弃小数而不是四舍五入
```

## 2.自动类型转换

- 容量小的数据类型可以自动转换为容量大的数据类型，比如内存空间16位的short可以自动转换为内存空间32位的int，内存空间32位的float可以自动转换为内存空间64位的double，既不会溢出，也不会损失精度。

```java
public class JavaBase02 {
    public static void main(String[] args) {
        short s3=12;
        int i10=s3;
        System.out.println("i10="+i10);//输出结果：i10=12

        float f3 = 12.5F;
        double d5 = f3;
        System.out.println("d5="+d5);//输出结果：d5=12.5
    }
}
```

## 3.强制类型转换

- 在有可能丢失信息的情况下进行的转换，但可能造成精度降低或溢出。
- 格式：(type)value，其中type是要强制类型转换后的数据类型。

```java
public class JavaBase02 {
    public static void main(String[] args) {
        int money=1000000000; //10亿
        int years=20;
        int all1=money*years;
        //返回的是负数,将money*years算出来的结果转换为int类型的时候发生溢出
        long all2=money*years;
        //返回的是负数,将money*years算出来的结果转换为int类型的时候已经发生溢出
        //当int类型再自动转换为long类型时已经是负数
        long all3=money*((long)years);
        //返回的结果正常，将int类型的years强制转换为long类型，int*long，全部用long来计算。
        System.out.println(all1);
        System.out.println(all2);
        System.out.println(all3);
        //输出结果：
        //-1474836480 -1474836480 20000000000
    }
}
```

