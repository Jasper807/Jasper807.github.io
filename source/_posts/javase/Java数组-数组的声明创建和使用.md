---
title: Java数组｜数组的声明创建和使用
tags:
    - Java
categories:
    - JavaSE 
date: 2021-12-02 22:05:24
cover: https://cdn.jsdelivr.net/gh/jasper807/picgo/cover/javaarr.png
---
# 数组的定义

- 数组是相同类型数据的有序集合。
- 数组描述的是相同类型的若干个数据，按照一定的先后次序排列组合而成。 
- 其中，每一个数据称作一个数组元素，每个数组元素可以通过一个下标来访问它们。

# 数组的基本特点

- 数组的长度是确定的。数组一旦被创建，它的大小就是不可以改变的。
- 数组元素必须是相同类型,不允许出现混合类型。
- 数组中的元素可以是任何数据类型，包括基本类型和引用类型。
- 数组变量属引用类型，数组也可以看成是对象，数组中的每个元素相当于该对象的成员变量。数组本身就是对象，Java中对象是在堆中的，因此数组无论保存原始类型还是其他对象类型，数组对象本身是在堆中的。

# 数组的声明创建

## 声明数组变量

```java
dataType[] arrayRefVar;   // 首选的方法
或
dataType arrayRefVar[];  // 效果相同，但不是首选方法
```

## 创建数组

```java
arrayRefVar = new dataType[arraySize];
```

- 使用 dataType[arraySize] 创建了一个数组
- 把新创建的数组的引用赋值给变量 arrayRefVar

```java
或者 dataType[] arrayRefVar = {value0, value1, ..., valuek};
```

## 内存分析

- Java内存

  - 堆  存放new的对象和数组，可以被所有线程共享，不会存放别的对象引用。
  - 栈  存放基本变量类型（会包含这个基本类型的具体数值）

  ​            引用对象的变量（会存放这个引用在堆里面的具体地址）

  - 方法区  可以被所有的线程共享，包含了所有的class和static变量。

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/arraymemory.JPG)

- 声明的时候并没有实例化任何对象，只有在实例化数组对象时，JVM才分配空间，这时才与长度有关。因此，声明数组时不能指定其长度(数组中元素的个数)，例如： int arr[5]; //非法。
- 声明一个数组的时候并没有数组被真正的创建。
- 构造一个数组，必须指定长度。

# 数组初始化

```java
class Person{
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public Person(String name) {
        this.name = name;
    }
}
```

## 静态初始化

- 除了用new关键字来产生数组以外,还可以直接在定义数组的同时就为数组元素分配空间并赋值。

```java
int[] a = {1,2,3};
Person[] persons = {new Person("张三"),new Person("李四")};
```

## 动态初始化

- 数组定义、为数组元素分配空间、赋值的操作、分开进行。

```java
Person[] person=null;
person=new Person[2];
person[0]=new Person("张三");
person[1]=new Person("李四");
for (int i=0;i<person.length;i++){
    System.out.println(person[i].getName());
}
```

## 默认初始化

- 数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也被按照实例变量同样的方式被隐式初始化。

# 多维数组

- 多维数组可以看成是数组的数组，比如二维数组就是一个特殊的一维数组，其每一个元素都是一个一维数组。
- arr.length获取的二维数组第一维数组的长度，arr[0].length才是获取二维第一个数组长度。

```java
type[][] typeName = new type[typeLength1][typeLength2] //多维数组格式
//比如    
int arr[][] = new int[2][3];//二维数组arr可以看成一个两行三列的数组
```

# Arrays类

![](https://cdn.jsdelivr.net/gh/jasper807/picgo/javase/arraysclass.JPG)

```java
//binarySearch
int[] numbers={1, 2, 3, 4};
System.out.println(Arrays.binarySearch(numbers,6));//输出-(插入点) 即-5
System.out.println(Arrays.binarySearch(numbers,2));//输出1
//equals
int[] numbers2={1,2,3,4};
System.out.println(Arrays.equals(numbers,numbers2));//输出true
//tostring
System.out.println(Arrays.toString(numbers));//输出[1, 2, 3, 4]
//fill
Arrays.fill(numbers,1,3,100);
System.out.println(Arrays.toString(numbers));//输出[1, 100, 100, 4]
//sort
int[] numbers3=numbers;
Arrays.sort(numbers3);
System.out.println(Arrays.toString(numbers3));//输出[1, 4, 100, 100]
```

# 常见排序算法

## 冒泡排序

```java
public class BubbleSort {
/**
 * N个数字要排序完成，总共进行N-1趟排序，每i趟的排序次数为(N-i)次，所以可以用双重循环语句，外层控制循环多少趟，内层控制每一趟的循环次数。
 * @param args
 */
    public static void main(String[] args) {
       int arr[] = {26,15,29,66,99,88,36,77,111,1,6,8,8};
        for(int i=0;i < arr.length-1;i++) {//外层循环控制排序趟数
            for(int j=0; j< arr.length-i-1;j++) {
                //内层循环控制每一趟排序多少次
                // 把小的值交换到前面
                if (arr[j]>arr[j+1]) {
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
            System.out.print("第"+(i+1)+"次排序结果：");
            //列举每次排序的数据
            System.out.println(Arrays.toString(arr));
        }
        System.out.println("最终排序结果："+Arrays.toString(arr));
    }
}
/*
	输出结果：
    第1次排序结果：[15, 26, 29, 66, 88, 36, 77, 99, 1, 6, 8, 8, 111]
    第2次排序结果：[15, 26, 29, 66, 36, 77, 88, 1, 6, 8, 8, 99, 111]
    第3次排序结果：[15, 26, 29, 36, 66, 77, 1, 6, 8, 8, 88, 99, 111]
    第4次排序结果：[15, 26, 29, 36, 66, 1, 6, 8, 8, 77, 88, 99, 111]
    第5次排序结果：[15, 26, 29, 36, 1, 6, 8, 8, 66, 77, 88, 99, 111]
    第6次排序结果：[15, 26, 29, 1, 6, 8, 8, 36, 66, 77, 88, 99, 111]
    第7次排序结果：[15, 26, 1, 6, 8, 8, 29, 36, 66, 77, 88, 99, 111]
    第8次排序结果：[15, 1, 6, 8, 8, 26, 29, 36, 66, 77, 88, 99, 111]
    第9次排序结果：[1, 6, 8, 8, 15, 26, 29, 36, 66, 77, 88, 99, 111]
    第10次排序结果：[1, 6, 8, 8, 15, 26, 29, 36, 66, 77, 88, 99, 111]
    第11次排序结果：[1, 6, 8, 8, 15, 26, 29, 36, 66, 77, 88, 99, 111]
    第12次排序结果：[1, 6, 8, 8, 15, 26, 29, 36, 66, 77, 88, 99, 111]
    最终排序结果：[1, 6, 8, 8, 15, 26, 29, 36, 66, 77, 88, 99, 111]
*/
```

## 选择排序

```java
public class JavaArray{
	public int[] sort(int arr[]) {
		int temp = 0;
		for (int i = 0; i < arr.length - 1; i++) {// 认为目前的数就是最小的, 记录最小数的下标
			int minIndex = i;
			for (int j = i + 1; j < arr.length; j++) {
				if (arr[minIndex] > arr[j]) {// 修改最小值的下标
				minIndex = j;
				}
			}// 当退出for就找到这次的最小值,就需要交换位置了
        	if (i != minIndex) {//交换当前值和找到的最小值的位置
            	temp = arr[i];
            	arr[i] = arr[minIndex];
            	arr[minIndex] = temp;
        	}
		}
		return arr;
	}
	public static void main(String[] args) {
		JavaArray javaArray=new JavaArray();
        int[] array = {2, 5, 1, 4, 8, 0, 7};
        int[] sort = javaArray.sort(array);
        for (int num : sort) {
            System.out.print(num + "\t");
        }
	}
}//输出0	1	2	4	5	7	8	
```

