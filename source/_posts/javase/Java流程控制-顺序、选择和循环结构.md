---
title: Java流程控制｜顺序、选择和循环结构
tags:
    - Java
categories:
    - JavaSE 
date: 2021-12-2 22:00:13
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/javacontrol.png
---
# 顺序结构

- Java的基本结构就是顺序结构，除非特别指明，否则就按照顺序一句一句执行。顺序结构是最简单的算法结构

```java
public static void main(String[] args) {
    System.out.println("one");
    System.out.println("two");
    System.out.println("three");
    System.out.println("four");
}
//按照自上而下的顺序执行！依次输出。
```

# 选择结构

## if单选择结构

- if语句对条件表达式进行一次测试，若测试为真，则执行下面的语句，否则跳过该语句。

```java
if(布尔表达式){
  //如果布尔表达式为true将执行的语句
}
//如果布尔表达式为false则跳过上面的if语句
//例子
public static void main(String[] args) {
    String s1="hello";
    if (s1.equals("hello")){
        System.out.println("YES");
    }
}
//输出结果：YES
```

## if双选择结构

- 我们需要有两个判断，需要一个双选择结构，所以就有了if-else结构。

```java
if(布尔表达式){
	//如果布尔表达式的值为true
}else{
	//如果布尔表达式的值为false
}
//例子
public static void main(String[] args) {
    boolean s2=false;
    if (s2){
        System.out.println("true");
    }else {
        System.out.println("false");
    }
}
//输出结果：false
```

## if多选择结构

- if 语句至多有 1 个 else 语句，else 语句在所有的 else if 语句之后。 
- if 语句可以有若干个 else if 语句，它们必须在 else 语句之前。
- 一旦其中一个 else if 语句检测为 true，其他的 else if 以及 else 语句都将跳过执行。

```java
if(布尔表达式 1){
//如果布尔表达式 1的值为true执行代码
}else if(布尔表达式 2){
//如果布尔表达式 2的值为true执行代码
}else if(布尔表达式 3){
//如果布尔表达式 3的值为true执行代码
}else {
//如果以上布尔表达式都不为true执行代码
}
//例子
public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    System.out.print("请输入成绩：");
    int score = scanner.nextInt();
    if (score>100){
        System.out.println("成绩输入有误");
    }else if (score>=60){
        System.out.println("成绩合格");
    }else {
        System.out.println("成绩不合格");
    }
}
/*
	输出结果：
	请输入成绩：80
	成绩合格
*/
```

## 嵌套的if结构

```java
if(布尔表达式 1){
	//如果布尔表达式 1的值为true执行代码
    if(布尔表达式 2){
        //如果布尔表达式 2的值为true执行代码
    }else{
        //如果布尔表达式 2的值为false执行代码
    }
}else{
    //如果布尔表达式 1的值为false执行代码
}
```

## switch多选择结构

```java
switch(expression){
    case value :
    //语句
    break; //可选
    case value :
    //语句
    break; //可选
    //你可以有任意数量的case语句
    default : //可选
    //语句
}
```

- switch 语句中的变量类型可以是： byte、short、int 或者 char。从 Java SE 7 开始，switch 支持字符串 String 类型了，同时 case 标签必须为字符串常量或字面量。

```java
public static void main(String[] args) {
    String name="张三";
    switch(name)
    {
        case "张三":
            System.out.println("张三在");
            break;
        case "李四":
            System.out.println("李四在");
        default:
            System.out.println("未知姓名");
    }
}
//输出结果：张三在
```

- switch 语句可以拥有多个 case 语句。每个 case 后面跟一个要比较的值和冒号。case 语句中值的数据类型必须与变量的数据类型相同。
- 当变量的值与 case 语句的值相等时，那么 case 语句之后的语句开始执行，直到 break 语句出现 才会跳出 switch 语句。
- 当遇到 break 语句时，switch 语句终止。程序跳转到 switch 语句后面的语句执行。case 语句不必要包含 break 语句。如果没有 break 语句出现，程序会继续执行下一条 case 语句，直到出现 break 语句。

```java
public static void main(String[] args) {
    int a=2;
    switch(a)
    {
        case 1:
            System.out.println("我是1");
            break;
        case 2:
            System.out.println("我是2");
        case 3:
            System.out.println("我是3");
            break;
        default:
            System.out.println("跳出");
    }
}
//输出结果:
//我是2
//我是3
```

- switch 语句可以包含一个 default 分支，该分支一般是switch语句的最后一个分支（可以在任何位置，但建议在最后一个）。default 在没有 case 语句的值和变量值相等的时候执行。

```java
public static void main(String[] args) {
    char character='b';
    switch(character)
    {
        case 'a':
            System.out.println("我是a");
            break;
        case 'b':
            System.out.println("我是b");
        default:
            System.out.println("跳出");
        case 'c':
            System.out.println("我是c");
            break;
    }
}
/*
	当character='b'时输出结果：    
	我是b						
	跳出
	我是c
	
	当character='c'时输出结果：
	我是c
	
	当character='d'时输出结果：
	跳出
	我是c
*/
```

# 循坏结构

## while循环

- 循环条件一直为true就会造成无限循环，正常的业务编程中应该尽量避免死循环。

```java
while( 布尔表达式 ) {
	//循环内容
}
//例子
public static void main(String[] args) {
    int i = 0;
    int sum = 0;
    while (i <= 100) {
        sum = sum+i;
        i++;
    }
    System.out.println("Sum= " + sum);
}
//输出结果：Sum= 5050
```

## do…while 循环

- while先判断后执行。dowhile是先执行后判断。dowhile总是保证循环体会被至少执行一次，这是他们的主要差别。

```java
do {
	//代码语句
}while(布尔表达式);
//例子
public static void main(String[] args) {
    int i = 0;
    int sum = 0;
    do {
    sum = sum+i;
    i++;
    }while (i <= 100);
    System.out.println("Sum= " + sum);
}
//输出结果：Sum= 5050
```

## for循环

```java
for(初始化; 布尔表达式; 更新) {
	//代码语句
}
//例子 打印99乘法表
public static void main(String[] args) {
    for (int i = 1; i <= 9 ; i++) {
        for (int j = 1; j <= i; j++) {
            System.out.print(j + "*" + i + "=" + (i * j)+ "\t");
        }
        System.out.println();
    }
}
/*
	输出结果:
	1*1=1	
    1*2=2	2*2=4	
    1*3=3	2*3=6	3*3=9	
    1*4=4	2*4=8	3*4=12	4*4=16	
    1*5=5	2*5=10	3*5=15	4*5=20	5*5=25	
    1*6=6	2*6=12	3*6=18	4*6=24	5*6=30	6*6=36	
    1*7=7	2*7=14	3*7=21	4*7=28	5*7=35	6*7=42	7*7=49	
    1*8=8	2*8=16	3*8=24	4*8=32	5*8=40	6*8=48	7*8=56	8*8=64	
    1*9=9	2*9=18	3*9=27	4*9=36	5*9=45	6*9=54	7*9=63	8*9=72	9*9=81
*/
```

## 增强for循环

```java
for(声明语句 : 表达式)
{
//代码句子
}
//例子
public static void main(String[] args) {
    int [] numbers = {10, 20, 30, 40, 50};
    for(int x : numbers ){
        System.out.print( x );
        System.out.print("\t");
    }
}
//输出结果：10	20	30	40	50
```

