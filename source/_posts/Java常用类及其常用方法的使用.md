---
title: Hello World3
---

# Java常用类及其常用方法的使用

# 一.Object类

## 1.Object类的结构

![](/Users/qiujiajie/Desktop/博客/JavaSE/图片/Object类的结构.JPG)

## 2.clone()方法

### Java语言中创建对象的方式

- 使用new操作符创建一个对象

new操作符的本意是分配内存。程序执行到new操作符时， 首 先去看new操作符后面的类型，因为知道了类型，才能知道要分配多大的内存空间。分配完内存之后， 再调用构造函数，填充对象的各个域，这一步叫做对象的初始化，构造方法返回后，一个对象创建完 毕，可以把他的引用(地址)发布到外部，在外部就可以使用这个引用操纵这个对象。

- 使用clone方法复制一个对象

clone在第一步 是和new相似的， 都是分配内存，调用clone方法时，分配的内存和源对象(即调用clone方法的对象) 相同，然后再使用原对象中对应的各个域，填充新对象的域， 填充完成之后，clone方法返回，一个新 的相同的对象被创建，同样可以把这个新对象的引用发布到外部。

### 复制引用 vs 复制对象

```java
public class Salary implements Cloneable{
    private double price;

    public Salary(double price) {
        this.price = price;
    }
}
public class Person implements Cloneable{
    private String name;
    private int age;
    private Salary salary;
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    @Override
    protected Object clone() throws CloneNotSupportedException {
        Person person=(Person)super.clone();
        return person;
    }
  
    public String getName() {
        return name;
    }
    public int getAge() {
        return age;
    }
}

public class TestObject{
    public static void main(String[] args) throws CloneNotSupportedException {

        Person p = new Person("张三",18);
        System.out.println("====引用====");
        //复制引用
        //打印的地址值是相同的，既然地址都是相同的，那么肯定是同一个对象。
        //p和p1只是引用而已，他们都指向了一个相同的对象，可以把这种现象叫做引用的复制
        Person p1 = p;
        System.out.println(p);
        System.out.println(p1);

        System.out.println("====clone====");
        //复制对象
        //两个对象的地址是不同的，也就是说创建了新的对象， 而不是把原对象的地址赋给了一个新的引用变量
        Person p2 = (Person) p.clone();
        System.out.println(p);
        System.out.println(p2);
    }
}
//输出结果
====引用====
javabase.javacommonclass.Person@5cad8086
javabase.javacommonclass.Person@5cad8086
====clone====
javabase.javacommonclass.Person@5cad8086
javabase.javacommonclass.Person@6e0be858
```

![](/Users/qiujiajie/Desktop/博客/JavaSE/图片/引用和复制.png)

### 深拷贝 vs 浅拷贝

- clone方法默认执行的是浅拷贝。

```java
public class Person implements Cloneable{
    private String name;
    private int age;
    private Salary salary;

    public Person(String name, int age,Salary salary) {
        this.name = name;
        this.age = age;
        this.salary= salary;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        Person person=(Person)super.clone();
        return person;
    }

    public Salary getSalary() {
        return salary;
    }
}

public class TestObject{

    public static void main(String[] args) throws CloneNotSupportedException {

        Person p = new Person("张三",18,new Salary(100));

        System.out.println("====clone====");
        //复制对象
        Person p1 = (Person) p.clone();

        String result= p.getSalary() == p2.getSalary()
                ? "clone是浅拷贝的" : "clone是深拷贝的";

        System.out.println(result);
    }
}
//输出结果
clone是浅拷贝的
```

- java里除了8种基本类型传参数是值传递，其他的类对象传参数都是引用，我们有时候不希望在 方法里将参数改变，这是就需要在类中复写clone方法，实现深拷贝。

```java
public class Salary implements Cloneable{
    private double price;

    public Salary(double price) {
        this.price = price;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
public class Person implements Cloneable{
    private String name;
    private int age;
    private Salary salary;

    public Person(String name, int age,Salary salary) {
        this.name = name;
        this.age = age;
        this.salary= salary;
    }
    @Override
    protected Object clone() throws CloneNotSupportedException {
        Person person=(Person)super.clone();
        person.salary=(Salary) salary.clone();
        return person;
    }
    public Salary getSalary() {
        return salary;
    }
}
public class TestObject{

    public static void main(String[] args) throws CloneNotSupportedException {

        Person p = new Person("张三",18,new Salary(100));

        System.out.println("====clone====");
        //复制对象
        Person p1 = (Person) p.clone();

        String result= p.getSalary() == p2.getSalary()
                ? "clone是浅拷贝的" : "clone是深拷贝的";

        System.out.println(result);
    }
}
//输出结果
clone是深拷贝的
```

![](/Users/qiujiajie/Desktop/博客/JavaSE/图片/浅拷贝和深拷贝.png)

## 3.toString()方法

- Object 类的 toString 方法返回一个字符串，该字符串由类名(对象是该类的一个实例)、at 标记符“@” 和此对象哈希码的无符号十六进制表示组成。

```java
public String toString() {
   return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

- 一般子类都有覆盖toString方法。

```java
public class Person {
    private String name;
    private int age;

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
public class TestObject{
    public static void main(String[] args) throws CloneNotSupportedException {
        Object object = new Object();
        System.out.println(object.toString());
      
        Person person=new Person("张三",18);
        System.out.println(person.toString());
    }
}
//输出结果
java.lang.Object@5cad8086
Person{name='张三', age=18}
```

## 4.getClass()方法

```java
public final native Class<?> getClass();
```

- 返回运行时类类型。不可重写，要调用的话，一般和getName()联合使用。

```java
public class Person{
    public Person() {
    }
}
public class TestObject{
    public static void main(String[] args) throws CloneNotSupportedException {
        Object object = new Object();
        System.out.println(object.getClass());
        System.out.println(object.getClass().getName());

        Person person = new Person();
        System.out.println(person.getClass());
        System.out.println(person.getClass().getName());
    }
}
//输出结果
class java.lang.Object
java.lang.Object
class javabase.javacommonclass.Person
javabase.javacommonclass.Person
```

## 5.finalize()方法
- 当对象被判定为垃圾对象时，由JVM自动调用此方法，用以标记垃圾对象，进入回收队列。
  - 垃圾对象：没有有效引用指向此对象时，为垃圾对象。
  - 垃圾回收：由GC销毁垃圾对象，释放数据存储空间。
  - 自动回收机制：JVM的内存耗尽，一次性回收所有垃圾对象。
  - 手动回收机制：使用System.gc()，通知JVM执行垃圾回收。

```java
//person类重写finalize()方法
@Override
protected void finalize() throws Throwable {
    System.out.println(this.name+"对象被回收了");
}

public class TestObject{
    public static void main(String[] args) {
        Person person=new Person("李四");
        new Person("张三");
        System.gc();
   }
}
//输出结果：
张三对象被回收了
```

## 6.equals()方法

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

- Object中的equals方法是直接判断this和obj本身的值是否相等，即用来判断调用equals的对象和形参obj所引用的对象是否是同一对象。

- 所谓同一对象就是指内存中同一块存储单元，如果this和obj指向的同一块内存对象，则返回true,如果this和obj指向的不是同一块内存对象，则返回false。即便是内容完全相等的两块不同的内存对象，也返回false。

```java
public static void main(String[] args) throws CloneNotSupportedException {
    Person person1=new Person("张三");
    Person person2=new Person("张三");
    System.out.println(person1.equals(person2));
}
//输出结果：
false
```

## 7.hashCode()方法

- 一般必须满足obj1.equals(obj2)==true。可以推出obj1.hash Code() == obj2.hashCode()，但是hashCode相等不一定就满足equals。不过为了提高效率，应该尽量使上面两个条件接近等价。

```java
public static void main(String[] args) throws CloneNotSupportedException {
    Person person1=new Person("张三");
    Person person2=new Person("张三");
    Person person3=person1;
    System.out.println("person1="+person1.hashCode());
    System.out.println("person2="+person2.hashCode());
    System.out.println("person3="+person3.hashCode());
}
//输出结果：
person1=1554874502
person2=1846274136
person3=1554874502
```

## 8.wait()、notify()、notifyAll()方法

```java
/**
* 唤醒在此对象监视器上等待的单个线程
**/
void notify()
/*
* 唤醒在此对象监视器上等待的所有线程
**/
void notifyAll() 
/*
* 导致当前的线程等待，直到其他线程调用此对象的notify( ) 方法或 notifyAll( ) 方法
*/
void wait( ) 
/*
* 导致当前的线程等待，直到其他线程调用此对象的notify() 方法或 notifyAll() 方法，或者指定的时间过完。
*/
void wait(long timeout) 
/*
* 导致当前的线程等待，直到其他线程调用此对象的notify() 方法或 notifyAll() 方法，或者其他线程打断了当前线程，或者指定的时间过完。
*/
void wait(long timeout, int nanos) 
```

- 调用以上方法时，一定要对竞争资源进行加锁，如果不加锁的话，则会报IllegalMonitorStateException 异常，当想要调用wait( )进行线程等待时，必须要取得这个锁对象的控制权(对象监视器)，一般是放到synchronized(obj)代码中。

- 当调用obj.notify()或obj.notifyAll后，调用线程依旧持有obj锁。因此，其他线程虽被唤醒，但是仍无法获得obj锁。直到调用线程退出synchronized块，释放obj锁后，其他线程中的一个才有机会获得锁继续执行。

### 为何上述方法定义在object类中

- 因为这些方法在操作同步线程时，都必须要标识它们操作线程的锁，只有同一个锁上的被等待线程，可以被同一个锁上的notify唤醒，不可以对不同锁中的线程进行唤醒。也就是说，等待和唤醒必须是同一个锁。而锁可以是任意对象，所以可以被任意对象调用的方法是定义在object类中。

```java
//调用线程方法1 继承Thread类，重写run()方法，调用start()方法开启线程

public class WaitNotifyTest {
    // 在多线程间共享的对象上使用wait
    public static void main(String[] args) {
        WaitNotifyTest test = new WaitNotifyTest();
        ThreadWait threadWait1 = test.new ThreadWait("wait thread1");
        ThreadWait threadWait2 = test.new ThreadWait("wait thread2");
        ThreadNotify threadNotify = test.new ThreadNotify("notify thread");
        threadNotify.start();
        threadWait1.start();
        threadWait2.start();
    }
    class ThreadWait extends Thread {
        public ThreadWait(String name){
            super(name);
        }
        public void run() {
            //每个类被加载之后，系统就会为该类生成一个对应的字节码对象 WaitNotifyTest.class
            synchronized (WaitNotifyTest.class) {
                    System.out.println("线程"+ this.getName() + "开始等待");
                    long startTime = System.currentTimeMillis();
                    try {
                        WaitNotifyTest.class.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    long endTime = System.currentTimeMillis();
                    System.out.println("线程" + this.getName()
                            + "等待时间为：" + (endTime - startTime));

            }
            System.out.println("线程" + getName() + "等待结束");
        }
    }
    class ThreadNotify extends Thread {
        public ThreadNotify(String name){
            super(name);
        }
        public void run() {
            try {
                // 给等待线程等待时间
                sleep(3000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (WaitNotifyTest.class) {
                System.out.println("线程" + this.getName() + "开始准备通知");
                WaitNotifyTest.class.notifyAll();
                System.out.println("线程" + this.getName() + "通知结束");
            }
            System.out.println("线程" + this.getName() + "运行结束");
        }
    }
}
//输出结果：
线程wait thread1开始等待
线程wait thread2开始等待
线程notify thread开始准备通知
线程notify thread通知结束
线程notify thread运行结束
线程wait thread2等待时间为：3004
线程wait thread2等待结束
线程wait thread1等待时间为：3005
线程wait thread1等待结束
```

### Java中sleep()与wait()区别

- 每个对象都有一个锁来控制同步访问，Synchronized关键字可以和对象的锁交互，来实现同步方法或同步块。
- Sleep()方法
  - sleep()使当前线程进入停滞状态（阻塞当前线程），让出CPU的使用，目的是不让当前线程独自霸占该进程所获的CPU资源，以留一定时间给其他线程执行的机会。
  - sleep()是Thread类的static(静态)的方法；因此他不能改变对象的机锁，所以当在一个Synchronized块中调用Sleep()方法时，线程虽然被阻塞了，但是对象的机锁并木有被释放，其他线程无法访问这个对象（即使被阻塞也持有对象锁）。
  - 在sleep()阻塞时间到了之后，该线程不一定会立即执行，这是因为其它线程可能正在运行而且没有被调度为放弃执行，除非此线程具有更高的优先级。

- Wait()方法
  - wait()方法是Object类里的方法；当一个线程执行到wait()方法时，它就进入到一个和该对象相关的等待池中，同时失去（释放）了对象的机锁（暂时失去机锁，wait(long timeout)超时时间后被唤醒还是有机会得到对象锁）。
  - 可以使用notify或者notifyAlll或者指定睡眠时间wait(long timeout)来唤醒当前等待池中的线程。

```java
//调用线程方法2 实现Runnable接口，重写run()方法，实现接口需要丢入Runnable接口实现类，调用start()方法开启线程

//例子1 Sleep()方法没在Synchronized块中调用时，不占用对象锁
public class MultiThread {
    static class Thread1 implements Runnable{
        @Override
        public void run() {
            // 使用MultiThread.class这个字节码对象，当前虚拟机里引用这个变量时指向的都是同一个对象
            synchronized(MultiThread.class){
                System.out.println("thread1开始等待");
                long startTime = System.currentTimeMillis();
                try{
                    MultiThread.class.wait(1000);
                }catch(InterruptedException e){
                    e.printStackTrace();
                }
                long endTime = System.currentTimeMillis();
                System.out.println("线程thread1" + "等待时间为：" + (endTime - startTime));
                System.out.println("thread1等待结束");
            }
        }
    }
    static class Thread2 implements Runnable{
        @Override
        public void run() {
            System.out.println("thread2开始等待");
            long startTime = System.currentTimeMillis();
            try {
                Thread.sleep(5000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            long endTime = System.currentTimeMillis();
            System.out.println("线程thread2" + "等待时间为：" + (endTime - startTime));
            System.out.println("thread2等待结束");
        }
    }
    public static void main(String[] args) {
        new Thread(new Thread1()).start();
        new Thread(new Thread2()).start();
    }
}
//输出结果：
thread1开始等待
thread2开始等待
线程thread1等待时间为：1006
thread1等待结束
线程thread2等待时间为：5007
thread2等待结束
  
//例子2 Sleep()方法在Synchronized块中调用时，占用对象锁，其他线程无法访问这个对象
//使用下列代码替换Thread2静态类try-catch代码块
synchronized(MultiThread.class) {
    try {
      Thread.sleep(5000);
    } catch (InterruptedException e) {
      e.printStackTrace();
    }
}
//输出结果：
thread1开始等待
thread2开始等待
线程thread2等待时间为：5003
thread2等待结束
线程thread1等待时间为：5005
thread1等待结束
```

# 二.包装类

![](/Users/qiujiajie/Desktop/博客/JavaSE/图片/包装类.png)

## 1.(自动)装箱和(自动)拆箱

- 由基本类型向对应的包装类转换称为装箱，例如把 int 包装成 Integer 类的对象。

- 包装类向对应的基本类型转换称为拆箱，例如把 Integer 类的对象重新简化为 int。

```java
public class PackingClass {
    public static void main(String[] args) {
        int num1=18;
        System.out.println("---装箱---");
        Integer integer1=new Integer(num1);
        Integer integer2=Integer.valueOf(num1);
        System.out.println("integer1="+integer1);
        System.out.println("integer2="+integer2);

        System.out.println("---拆箱---");
        Integer integer3=new Integer(99);
        int num2=integer3.intValue();
        System.out.println("num2="+num2);

        //JDK1.5之后，提供自动装箱和拆箱
        System.out.println("---自动装箱---");
        int num3=100;
        Integer integer4=num3; //相当于Integer.valueOf(xxx)
        System.out.println("integer4="+integer4);
        System.out.println("---自动拆箱---");
        int num4=integer4; //相当于xxx.intValue()
        System.out.println("num4="+num4);
    }
}
//输出结果：
---装箱---
integer1=18
integer2=18
---拆箱---
num2=99
---自动装箱---
integer4=100
---自动拆箱---
num4=100
```

## 2.基本数据类型和字符串之间的转换

```java
public class PackingClass {
    public static void main(String[] args) {
        System.out.println("---基本类型转换为字符串---");
        int n1 = 15;
        //方法1 使用+号
        String s1 = n1 + "";
        //方法2 使用toString()方法
        String s2 = Integer.toString(n1);
        String s3 = Integer.toString(n1, 16);//n1以16进制显示
        System.out.println("s1=" + s1);
        System.out.println("s2=" + s2);
        System.out.println("s3=" + s3);

        System.out.println("---字符串转换为基本类型---");

        String[] str = {"123","123abc","abcxyz"};
        for (String str1 : str) {
            try {
                int m = Integer.parseInt(str1, 10);
                System.out.println(str1 + " 可以转换为整数 " + m);
            } catch (Exception e) {
                System.out.println(str1 + " 无法转换为整数");
            }
        }

        System.out.println("---boolean字符串形式转成基本类型---");
        //"true"--->true "非true"--->false
        String s4="true";
        boolean b1=Boolean.parseBoolean(s4);
        String s5="notrue";
        boolean b2=Boolean.parseBoolean(s5);
        System.out.println("b1="+b1);
        System.out.println("b2="+b2);
    }
}
//输出结果
---基本类型转换为字符串---
s1=15
s2=15
s3=f
---字符串转换为基本类型---
123 可以转换为整数 123
123abc 无法转换为整数
abcxyz 无法转换为整数
---boolean字符串形式转成基本类型---
b1=true
b2=false
```

## 3.整数缓存区

```java
public class IntegerTest {
    public static void main(String[] args) {
        Integer integer1=new Integer(100);
        Integer integer2=new Integer(100);
        System.out.println(integer1==integer2);

        Integer integer3=100;//等价于Integer integer3=Integer.valueOf(100);
        Integer integer4=100;//等价于Integer integer4=Integer.valueOf(100);
        System.out.println(integer3==integer4);

        Integer integer5=Integer.valueOf(200);
        Integer integer6=Integer.valueOf(200);
        System.out.println(integer5==integer6);
    }
}
/*      
			  low=-128 high=127 如果数字在这个范围就在cache缓存区取，否则创建新的Integer对象
        public static Integer valueOf(int i) {
            if (i >= Integer.IntegerCache.low && i <= Integer.IntegerCache.high)
               return Integer.IntegerCache.cache[i + (-Integer.IntegerCache.low)];
           return new Integer(i);
        }
*/
//输出结果
false
true
false
```

# 三.Math类

- Java 的 Math 包含了用于执行基本数学运算的属性和方法。 Math 的方法都被定义为 static 形式，通过 Math 类可以在主函数中直接调用。

```java
public class MathTest {
    public static void main(String[] args) {
        /**
         *Math.sqrt()//计算平方根
         *Math.cbrt()//计算立方根
         *Math.pow(a, b)//计算a的b次方
         *Math.max( , );//计算最大值
         *Math.min( , );//计算最小值
         */
        System.out.println(Math.sqrt(16)); //4.0
        System.out.println(Math.cbrt(8)); //2.0
        System.out.println(Math.pow(3,2)); //9.0
        System.out.println(Math.max(2.3,4.5));//4.5
        System.out.println(Math.min(2.3,4.5));//2.3
        /**
         * abs求绝对值
         */
        System.out.println(Math.abs(-10.4)); //10.4
        System.out.println(Math.abs(10.1)); //10.1
        /**
         * ceil天花板的意思，就是返回大的值
         */
        System.out.println(Math.ceil(-10.1)); //-10.0
        System.out.println(Math.ceil(10.7)); //11.0
        System.out.println(Math.ceil(-0.7)); //-0.0
        System.out.println(Math.ceil(0.0)); //0.0
        System.out.println(Math.ceil(-0.0)); //-0.0
        System.out.println(Math.ceil(-1.7)); //-1.0
        /**
         * floor地板的意思，就是返回小的值
         */
        System.out.println(Math.floor(-10.1)); //-11.0
        System.out.println(Math.floor(10.7)); //10.0
        System.out.println(Math.floor(-0.7)); //-1.0
        System.out.println(Math.floor(0.0)); //0.0
        System.out.println(Math.floor(-0.0)); //-0.0
        /**
         * random 取得一个大于或者等于0.0小于不等于1.0的随机数 [0,1)
         */
        System.out.println(Math.random()); //大于或者等于0.0小于不等于1.0的double类型的数
        System.out.println(Math.random()+1);//大于或者等于1.0小于不等于2.0的double类型的数
        /**
         * rint 四舍五入，返回double值
         * 注意.5的时候会取偶数
         */
        System.out.println(Math.rint(10.1)); //10.0
        System.out.println(Math.rint(10.7)); //11.0
        System.out.println(Math.rint(11.5)); //12.0
        System.out.println(Math.rint(10.5)); //10.0
        System.out.println(Math.rint(10.51)); //11.0
        System.out.println(Math.rint(-10.5)); //-10.0
        System.out.println(Math.rint(-11.5));  //-12.0
        System.out.println(Math.rint(-10.51)); //-11.0
        System.out.println(Math.rint(-10.6));  //-11.0
        System.out.println(Math.rint(-10.2));  //-10.0
        /**
         * round 四舍五入，float时返回int值，double时返回long值
         * x为正数：小数部分≥0.5时，整数取值向右一个整数，即+1。表现为四舍五入。
         * x为负数：小数部分≤0.5时，相近整数更靠近右侧，所以取值右侧的整数，即原负数的整数部分不变。
         */
        System.out.println(Math.round(10.1));  //10
        System.out.println(Math.round(10.7));  //11
        System.out.println(Math.round(10.5));  //11
        System.out.println(Math.round(10.51)); //11
        System.out.println(Math.round(-10.5)); //-10
        System.out.println(Math.round(-10.51)); //-11
        System.out.println(Math.round(-10.6)); //-11
        System.out.println(Math.round(-10.2)); //-10
    }
}
```

# 四.Random类

### 1.java.lang.Math.Random

- 调用这个Math.Random()函数能够返回带正号的double值，该值大于等于0.0且小于1.0，即取值范围是 [0.0,1.0)的左闭右开区间，返回值是一个伪随机选择的数，在该范围内(近似)均匀分布。

```java
public static void main(String[] args) {
    // 结果是个double类型的值，区间为[0.0,1.0) 
  	System.out.println("Math.random()=" + Math.random());
    int num = (int) (Math.random() * 3);
    // 注意不要写成(int)Math.random()*3，这个结果为0或1，因为先执行了强制转换 
  	System.out.println("num=" + num);
    }
//结果
Math.random()=0.44938147153848396
num=1
```

### 2.java.util.Random

```java
public class RandomTest {
    public static void main(String[] args) {
        //Random(long seed):使用单个 long 种子创建一个新的随机数生成器。
        //在创建一个Random对象的时候可以给定任意一个合法种子数，种子数只是随机算法的起源数字，和生成的随机数区间没有任何关系。
       
        //Random():创建一个新的随机数生成器
        Random rand = new Random();
        System.out.println("rand.nextBoolean():" + rand.nextBoolean());
        // 生成0.0-1.0之间的伪随机double数
        System.out.println("rand.nextDouble():" + rand.nextDouble());
        // 生成0.0-1.0之间的伪随机float数
        System.out.println("rand.nextFloat():" + rand.nextFloat());
        // 生成一个处于int整数取值范围的伪随机数
        System.out.println("rand.nextInt():" + rand.nextInt());
        // 生成0-20之间的伪随机整数,不包括20
        System.out.println("rand.nextInt(20):" + rand.nextInt(20));
        // 生成一个处于long整数取值范围的伪随机数
        System.out.println("rand.nextLong():" + rand.nextLong());
        //为byte数组里的元素随机赋值,即使原本数组里面有值，也会重新覆盖掉
        byte[] bytes=new byte[5];
        rand.nextBytes(bytes);
        for (int i=0;i< bytes.length;i++) {
            System.out.println("byte["+i+"]="+bytes[i]);
        }
    }
}
//输出结果：
rand.nextBoolean():true
rand.nextDouble():0.9888610718956184
rand.nextFloat():0.1866427
rand.nextInt():1598002054
rand.nextInt(20):12
rand.nextLong():8658833840448427432
byte[0]=-107
byte[1]=-127
byte[2]=10
byte[3]=-17
byte[4]=-47
```

# 五.String类

## 1.创建字符串对象的方式

```java
String str1="hello";//直接赋值的方式
String str2=new String("hello");//实例化的方式
```

## 2.字符串创建与内存场景分析(JDK 1.8)

```java
//注意：==在对字符串比较的时候，对比的是内存地址，而equals比较的是字符串内容，
//		 在开发的过程中，equals()通过接受参数，可以避免空指向。
public static void main(String[] args) {
        String name1="hello";
        //给字符串直接赋值的时候，并不是修改原来的数据，而是重新在字符串常量池开辟一个空间
        name1="world";
        String name2="world";
        System.out.println("name1==name2｜"+(name1==name2));
        //通过实例化方式创建，会先在字符串常量池中查看是否有相同的字符串
        //如果有，则只需要在堆中创建一个对象，并且该引用存的是堆中对象的地址
        //如果没有，则需要在栈和堆中各创建一个对象，并且该引用存的是堆中对象的地址
        String name3=new String("apple");
        String name4=new String("apple");
        System.out.println("name3==name4｜"+(name3==name4));
        String name5="apple";
        System.out.println("name5==name3｜"+(name5==name3));
        System.out.println("name5==name4｜"+(name5==name4));
}
//输出结果：
name1==name2｜true
name3==name4｜false
name5==name3｜false
name5==name4｜false
```

![](/Users/qiujiajie/Desktop/博客/JavaSE/图片/String字符串常量池内存分析.png)

## 3.String常用方法

### String的判断方法

```java
boolean equals(Object obj):比较字符串的内容是否相同
boolean equalsIgnoreCase(String str): 比较字符串的内容是否相同,忽略大小写 
boolean startsWith(String str): 判断字符串对象是否以指定的str开头 
boolean endsWith(String str): 判断字符串对象是否以指定的str结尾
  
//例子
public static void main(String[] args) { // 创建字符串对象
      String s1 = "hello";
      String s2 = "hello";
      String s3 = "Hello";
      // boolean equals(Object obj):比较字符串的内容是否相同 
      System.out.println(s1.equals(s2)); //true 
      System.out.println(s1.equals(s3)); //false 
      System.out.println("-----------");
      // boolean equalsIgnoreCase(String str):比较字符串的内容是否相同,忽略大小写
      System.out.println(s1.equalsIgnoreCase(s2)); //true 
      System.out.println(s1.equalsIgnoreCase(s3)); //true 
      System.out.println("-----------");
      // boolean startsWith(String str):判断字符串对象是否以指定的str开头 
      System.out.println(s1.startsWith("he")); //true 
      System.out.println(s1.startsWith("ll")); //false
      //boolean endsWith(String str): 判断字符串对象是否以指定的str结尾
      System.out.println(s1.endsWith("he")); //false
      System.out.println(s1.endsWith("lo")); //true
}
//输出结果：
true
false
-----------
true
true
-----------
true
false
-----------
false
true
```

### String的截取方法

```java
int length():获取字符串的长度，其实也就是字符个数
char charAt(int index):获取指定索引处的字符
int indexOf(String str):获取str在字符串对象中第一次出现的索引
String substring(int start):从start开始截取字符串
String substring(int start,int end):从start开始，到end结束截取字符串。包括start，不包括end
boolean contains(String str):判断是否包含某个子字符串
  
//例子
public static void main(String[] args) { // 创建字符串对象
      // 创建字符串对象
      String s = "helloworld";
      // int length():获取字符串的长度，其实也就是字符个数
      System.out.println(s.length()); //10
      System.out.println("--------");
      // char charAt(int index):获取指定索引处的字符
      System.out.println(s.charAt(0)); //h
      System.out.println(s.charAt(1)); //e
      System.out.println("--------");
      // int indexOf(String str):获取str在字符串对象中第一次出现的索引
      System.out.println(s.indexOf("l")); //2
      System.out.println(s.indexOf("owo")); //4
      System.out.println(s.indexOf("ak")); //-1
      System.out.println("--------");
      // String substring(int start):从start开始截取字符串
      System.out.println(s.substring(0)); //helloworld
      System.out.println(s.substring(5)); //world
      System.out.println("--------");
      // String substring(int start,int end):从start开始，到end结束截取字符串
      System.out.println(s.substring(0, s.length())); //helloworld
      System.out.println(s.substring(3, 8)); //lowor
      //boolean contains(String str):判断是否包含某个子字符串
      System.out.println(s.contains("hello"));
}
//输出结果：
10
--------
h
e
--------
2
4
-1
--------
helloworld
world
--------
helloworld
lowor
-----------
true

```

### String的转换方法

```java
char[] toCharArray():把字符串转换为字符数组 
String toLowerCase():把字符串转换为小写字符串 
String toUpperCase():把字符串转换为大写字符串
  
//例子
public static void main(String[] args) { // 创建字符串对象
      String s = "abcde";
      // char[] toCharArray():把字符串转换为字符数组
      char[] chs = s.toCharArray();
      for (int x = 0; x < chs.length; x++) {
        System.out.println(chs[x]);
      }
      System.out.println("-----------");
      // String toLowerCase():把字符串转换为小写字符串
      System.out.println("HelloWorld".toLowerCase());
      // String toUpperCase():把字符串转换为大写字符串
      System.out.println("HelloWorld".toUpperCase());
}
//运行结果：
a
b
c
d
e
-----------
helloworld
HELLOWORLD
```

### String的比较方法

```java
boolean equals(Object anObject):比较两个字符串的值是否相等
int compareTo(String anotherString):字符串比较，根据情况返回对应的int值

//例子
 public static void main(String[] args) { // 创建字符串对象
      String str1="abc";
      String str2="abc";
      String str3="abcde";
      String str4="afghij";
      String str5="ABC";
      //boolean equals(Object anObject):比较两个字符串的值是否相等
      System.out.println(str1.equals(str2));
      System.out.println(str1.equals(str3));
      System.out.println(str1.equalsIgnoreCase(str5));
      System.out.println("-----------");
      //int compareTo(String anotherString):字符串比较，根据情况返回对应的int值
      //如果这两个字符串前面部分都相等，比较的是两个字符串的长度
      System.out.println(str1.compareTo(str2));
      System.out.println(str1.compareTo(str3));
      System.out.println(str3.compareTo(str1));
      System.out.println("-----------");
      //如果这两个字符串前面部分不相等，从第一个开始比ASCII码，相等就继续往后比，不相同比较结束
      System.out.println(str1.compareTo(str4));
      System.out.println(str4.compareTo(str1));
      System.out.println(str4.compareTo(str5));
}
//输出结果：
true
false
true
-----------
0
-2
2
-----------
-4
4
32
```

### String的其他方法

```java
String trim():去除字符串两端空格
String[] split(String str):按照指定符号分割字符串
boolean endWith(String Str):是否以指定字符串为结尾
boolean startWith(String Str):是否以指定字符串为开头
  
//例子
public static void main(String[] args) { // 创建字符串对象
      //String trim():去除字符串两端空格
      String s1="   Hello World   ";
      System.out.println(s1.trim());
      System.out.println("-----------");
      //String[] split(String str):按照指定符号分割字符串
      String s2="The hard part isn’t making the decision. It’s living with it.";
      String[] array1=s2.split(" ");//通过空格分成数组
      System.out.println("array1="+Arrays.toString(array1));
      String[] array2=s2.split("[ .]");//通过空格或.来分成数组
      System.out.println("array2="+Arrays.toString(array2));
      String s3="The hard part isn’t making the decision. . . It’s living with it.";
      String[] array3=s3.split("[ .]");//通过空格或.来分成数组
      System.out.println("array3="+Arrays.toString(array3));
      String[] array4=s3.split("[ .]+");//通过多个或一个空格或.来分成数组
      System.out.println("array4="+Arrays.toString(array4));
      System.out.println("-----------");
      //boolean endWith(String Str):是否以指定字符串为结尾
      String s4="Hello World";
      System.out.println(s4.endsWith("ld"));
      System.out.println(s4.startsWith("Hell"));
}
//输出结果：
Hello World
-----------
array1=[The, hard, part, isn’t, making, the, decision., It’s, living, with, it.]
array2=[The, hard, part, isn’t, making, the, decision, , It’s, living, with, it]
array3=[The, hard, part, isn’t, making, the, decision, , , , , , It’s, living, with, it]
array4=[The, hard, part, isn’t, making, the, decision, It’s, living, with, it]
-----------
true
true
```

# 六.String、StringBuilder和StringBuffer

## 1.StringBuilder常用方法(StringBuffer类似)

### insert方法

```java
public static void insert(){
    StringBuilder sb1=new StringBuilder();
    // 在位置0处插入字符数组
    sb1.insert(0, new char[]{'a', 'b', 'c', 'd', 'e'});
    System.out.println(sb1);
    // 在位置1处插入字符数组。2表示字符数组起始位置，3表示长度
    sb1.insert(1, new char[]{'A', 'B', 'C', 'D', 'E'}, 2, 3);
    System.out.println(sb1);
    // 在位置3处插入float,其他数据类型类似
    sb1.insert(3, 1.414f);
    System.out.println(sb1);
    System.out.println("------------");
    StringBuilder sb2=new StringBuilder();
    //在位置0处插入StringBuilder对象
    sb2.insert(0, new StringBuilder("StringBuilder"));
    System.out.println(sb2);
    // 在位置1处插入StringBuffer对象。2表示被在位置插入对象的起始位置(包括)，3是结束位置(不包括)
    sb2.insert(1, new StringBuilder("Hello"), 2, 3);
    System.out.println(sb2);
    System.out.println("------------");
    // 在位置0处插入Object对象。此处以HashMap为例 HashMap map = new HashMap(); map.put("1", "one");
    StringBuilder sb3=new StringBuilder();
    Map<String,String> map=new HashMap();
    map.put("2", "two");
    map.put("3", "three");
    sb3.insert(0, map);
    System.out.println(sb3);
}
//输出结果：
abcde
aCDEbcde
aCD1.414Ebcde
------------
StringBuilder
SltringBuilder
------------
{2=two, 3=three}
```

### append方法

```java
public static void append(){
    StringBuilder sb1=new StringBuilder();
    // 追加字符数组
    sb1.append(new char[]{'a','b','c','d','e'});
    System.out.println(sb1);
    // 追加字符数组。1表示字符数组起始位置，3表示长度
    sb1.append(new char[]{'A','B','C','D','E'}, 1, 3);
    System.out.println(sb1);
    // 追加float
    sb1.append(1.414f);
    System.out.println(sb1);
    System.out.println("------------");
    StringBuilder sb2=new StringBuilder();
    // 追加StringBuilder对象
    sb2.append(new StringBuilder("StringBuilder"));
    System.out.println(sb2);
    // 追加StringBuilder对象。2表示被追加对象的起始位置(包括)，4是结束位置(不包括)
    sb2.append(new StringBuilder("Hello"), 2, 4);
    System.out.println(sb2);
    System.out.println("------------");
    StringBuilder sb3=new StringBuilder();
    // 追加Object对象。此处以HashMap为例
    HashMap map = new HashMap();
    map.put("1", "AA");
    map.put("2", "BB");
    sb3.append(map);
    System.out.println(sb3);
    System.out.println("------------");
    StringBuilder sb4=new StringBuilder();
    // 追加unicode编码
    sb4.appendCodePoint(0x5b57); // 0x5b57是“字”的unicode编码
    sb4.appendCodePoint(0x7b26); // 0x7b26是“符”的unicode编码
    sb4.appendCodePoint(0x7f16); // 0x7f16是“编”的unicode编码
    sb4.appendCodePoint(0x7801); // 0x7801是“码”的unicode编码
    System.out.println(sb4);
}
//输出结果：
abcde
abcdeBCD
abcdeBCD1.414
------------
StringBuilder
StringBuilderll
------------
{1=AA, 2=BB}
------------
字符编码
```

### replace方法

```java
public static void replace(){
    StringBuilder sb;
    sb = new StringBuilder("0123456789");
    //将字符串索引1到4(不包括4)替换为A
    sb.replace(1, 4, "A");
    System.out.println("sb="+sb);
    sb = new StringBuilder("0123456789");
    sb.reverse();
    System.out.println("sb="+sb);
    sb = new StringBuilder("0123456789");
    sb.setCharAt(0, 'M');
    System.out.println("sb="+sb);
    System.out.println();
}
//输出结果：
sb=0A456789
sb=9876543210
sb=M123456789
```

### delete方法

```java
public static void delete(){
    StringBuilder sb = new StringBuilder("0123456789");
    // 删除位置0的字符，剩余字符是“123456789”。
    sb.deleteCharAt(0);
    System.out.println(sb);
    // 删除位置3(包括)到位置6(不包括)之间的字符，剩余字符是“123789”。
    sb.delete(3,6);
    System.out.println(sb);
    // 获取sb中从位置1开始的字符串
    String str1 = sb.substring(1);
    System.out.println(str1);
    // 获取sb中从位置3(包括)到位置5(不包括)之间的字符串
    String str2 = sb.substring(3, 5);
    System.out.println(str2);
    // 获取sb中从位置3(包括)到位置5(不包括)之间的字符串，获取的对象是CharSequence对象，此处转型为String
    String str3 = (String)sb.subSequence(3, 5);
    System.out.println(str3);
}
//输出结果：
123456789
123789
23789
78
78
```

### index方法

```java
public static void index(){
    StringBuilder sb = new StringBuilder("abcAbcABCabCaBcAbCaBCabc");
    //从前往后，找出"bc"第一次出现的位置
    System.out.println(sb.indexOf("bc"));
    //从位置5开始，从前往后，找出"bc"第一次出现的位置
    System.out.println(sb.indexOf("bc", 5));
    //从后往前，找出"bc"第一次出现的位置
    System.out.println(sb.lastIndexOf("bc"));
    //从位置4开始，从后往前，找出"bc"第一次出现的位置
    System.out.println(sb.lastIndexOf("bc", 4));
}
//输出结果：
1
22
22
4
```

## 其他方法

```java
public static void others(){
    //StringBuffer( ); 分配16个字符的缓冲区
    StringBuilder sb1 = new StringBuilder();
    //capacity()返回的是字符串缓冲区的容量
    System.out.println(sb1.capacity());
    System.out.println("---------");
    StringBuilder sb2 = new StringBuilder("0123456789");
    //除了按照s的大小分配空间外,再分配16个字符的缓冲区
    System.out.println(sb2.capacity());
    System.out.println("---------");
    StringBuilder sb3 = new StringBuilder(7);
    //StringBuffer(int len); 分配len个字符的缓冲区
    System.out.println(sb3.capacity());
}
```

##  2.StringBuilder与StringBuffer的区别，StringBuilder与String的区别

- StringBuilder效率高，线程不安全，StringBuffer效率低，线程安全。

- String是不可变字符串，是因为源码中由final进行修饰，StringBuilder是可变字符串。

- 如果是简单的声明一个字符串没有后续过多的操作，使用String,StringBuilder均可，若后续对字符串做频繁的添加，删除操作,或者是在循环当中动态的改变字符串的长度应该用StringBuilder。使用String会产生多余的字符串，占用内存空间。

# 七.日期时间类

## 1.Date类

```java
public static void dateTest(){
    Date date = new Date();
    // 使用 toString() 函数显示日期时间
    System.out.println(date);
    System.out.println(date.toLocaleString());
    System.out.println("-----------");
    //日期按(自1970年1月1日经历的毫秒数值)进行比较
    long time = date.getTime();
    long time2 = date.getTime();
    System.out.println(time==time2);
    System.out.println("-----------");
    //使用方法 before()，after() 和 equals()
    boolean before = new Date(2021, 11, 18).before(new Date(2021, 11, 19));
    System.out.println(before);
    boolean after = new Date(2021, 11, 18).after(new Date(2021, 11, 19));
    System.out.println(after);
    boolean eq = new Date(2021, 11, 18).equals(new Date(2021, 11, 18));
    System.out.println(eq);
    System.out.println("-----------");
    Date date1 = new Date();
    Date date2 = new Date(date1.getTime()-(60*60*24*1000));
    //相等返回0，大于返回1，小于返回-1
    System.out.println(date1.compareTo(date2));
    System.out.println(date2.compareTo(date1));
    System.out.println(date1.compareTo(date1));
}
//输出结果：
Sat Nov 27 15:26:06 CST 2021
2021-11-27 15:26:06
-----------
true
-----------
true
false
true
-----------
1
-1
0
```

## 2.SimpleDateFormat类

- SimpleDateFormat 是一个以语言环境敏感的方式来格式化和分析日期的类。
- SimpleDateFormat 允许你选择任何用户自定义日期时间格式来运行。

```java
public static void sdfTest(){
    Date dNow = new Date( );
    //其中 yyyy 是完整的公元年，MM 是月份，dd 是日期，HH:mm:ss 是时、分、秒。
    //有的格式大写，有的格式小写，例如 MM 是月份，mm 是分;HH 是 24 小时制，而 hh 是 12 小时制
    SimpleDateFormat ft = new SimpleDateFormat ("yyyy-MM-dd hh:mm:ss");
    System.out.println("当前时间为: " + ft.format(dNow));
}
//输出结果：
当前时间为: 2021-11-27 03:30:01
```

## 3.Calendar类

```java
public static void calTest(){
    Calendar c1 = Calendar.getInstance();
    System.out.println(c1.getTime().toLocaleString());
    System.out.println("---------------");
    c1.set(2021, 11-1, 27);
    // 获得年份
    int year = c1.get(Calendar.YEAR);
    // 获得月份
    int month = c1.get(Calendar.MONTH)+1;
    // 获得日期
    int date = c1.get(Calendar.DATE);
    // 获得小时
    int hour = c1.get(Calendar.HOUR_OF_DAY);
    // 获得分钟
    int minute = c1.get(Calendar.MINUTE);
    // 获得秒
    int second = c1.get(Calendar.SECOND);
    // 获得星期几(注意(这个与Date类是不同的):1代表星期日、2代表星期一、3代表星期二，以此类推)
    int day = c1.get(Calendar.DAY_OF_WEEK);
    System.out.println("今天星期"+day);
    System.out.println(year+":"+month+":"+date+" "+hour+":"+minute+":"+second);
    System.out.println("---------------");
    Calendar c2 = Calendar.getInstance();
    //设置完整日期
    c2.set(2021,11-1,20,11,11,11);//把Calendar对象c1的年月日分别设这为:2009、6、12
    //设置某个字段
    System.out.println(c2.getTime().toLocaleString());
    c2.set(Calendar.DATE,10);
    c2.set(Calendar.YEAR,2008); //其他字段属性set的意义以此类推
    System.out.println(c2.getTime().toLocaleString());
}
//输出结果：
2021-11-27 15:48:21
---------------
今天星期7
2021:11:27 15:48:21
---------------
2021-11-20 11:11:11
2008-11-10 11:11:11
```

# 八.Bigdecimal类

- 不论是float 还是double都是浮点数，而计算机是二进制的，浮点数会失去一定的精确度。十进制值通常没有完全相同的二进制表示形式，十进制数的二进制表示形式可能不精确。只能无限接近于那个值。

```java
public static void main(String[] args) {
      System.out.println(0.1+0.2);
      System.out.println(0.3-0.1);
      //BigDecimal大浮点数精确计算
      BigDecimal b1=new BigDecimal("0.1");
      BigDecimal b2=new BigDecimal("0.2");
      //加法
      System.out.println(b1.add(b2));
      //减法
      System.out.println(b1.subtract(b2));
      //乘法
      System.out.println(b1.multiply(b2));
      //除法
      System.out.println(b1.divide(b2));
}
//输出结果：
0.30000000000000004
0.19999999999999998
0.3
-0.1
0.02
0.5
```

# 九.System类

```java
static void arraycopy(Object src,int srcPos,Object dest,int destPos,int length):复制数组
static long currentTimeMillis():获取当前系统时间，返回的是毫秒值
static void gc():建议JVM赶快启动垃圾回收器回收垃圾
static void exit(int status):退出JVM，如果参数是0表示正常退出JVM，非0表示异常退出JVM
  
//例子
public static void main(String[] args) {
      //static void arraycopy(Object src,int srcPos,Object dest,int destPos,int length):复制数组
      //src：原数组，srcPos：原数组从哪个位置开始复制
      //dest：目标数组，destPos：目标数组从哪个位置开始复制，length：复制的长度
      int[] arr={1,2,3,4,5,6};
      int[] dest=new int[8];
      System.arraycopy(arr,1,dest,2,3);
      for (int i=0;i<dest.length;i++){
        System.out.printf("%d ",dest[i]);
      }
      System.out.printf("\n");
      System.out.println("-----------");
      //static long currentTimeMillis():获取当前系统时间，返回的是毫秒值
      long start=System.currentTimeMillis();
      for (int i=0;i<999999999;i++){
        for (int j=0;j<999999999;j++){
          int result=i+j;
        }
      }
      long end=System.currentTimeMillis();
      System.out.println("用时:"+(end-start));
}
//输出结果：
0 0 2 3 4 0 0 0 
-----------
用时:15
```

# 十.File类

## 1.File的构造方法

```java
public static void main(String[] args) {
      //路径分隔符
      String pathSeparator= File.pathSeparator;
      System.out.println(pathSeparator);
      //文件名分隔符
      String separator=File.separator;
      System.out.println(separator);
      System.out.println("-------------");
      //File的构造方法
      //1.File(String pathname):通过将给定路径名字符串转换为抽象路径名来创建一个新File实例
      //路径可以是文件末尾，也可以是文件夹末尾；路径可以是相对路径，也可以是绝对路径；路径可以存在，也可以不存在
      //创建File对象，只是把字符串路径封装为File对象，不考虑路径真假情况
      File f1=new File("/Users/test/photo1.jpeg");
      System.out.println(f1);
      File f2=new File("photo2.jpeg");
      System.out.println(f2);
      File f3=new File("/Users/test");
      System.out.println(f3);
      System.out.println("-------------");
      //2.File(String parent,String child) 根据parent路径名字符串和child路径名字符串创建一个新File实例
      File f4=new File("/Users/test/","photo1.jpeg");
      System.out.println(f4);
      System.out.println("-------------");
      //3.File(File parent,String child) 根据parent抽象路径名和child路径名字符串创建一个新File实例
      File parent=new File("/Users/test/");
      File f5=new File(parent,"photo1.jpeg");
      System.out.println(f5);
}
//输出结果
:
/
-------------
/Users/test/photo1.jpeg
photo2.jpeg
/Users/test
-------------
/Users/test/photo1.jpeg
-------------
/Users/test/photo1.jpeg
```

## 2.File的获取方法

```java
public String getAbsolutePath():返回此File的绝对路径名字符串
public String getPath():将此File转换为路径名字符串
public String getName():返回此File表示的文件或文件夹(目录)名称
public long length():返回此File表示的文件的长度，获得的是构造方法指定的文件的大小，以字节为单位
  
//例子
 public static void main(String[] args) {
      File f1=new File("/Users/test/photo1.jpeg");
      File f2=new File("photo2.jpeg");
      File f3=new File("/Users/test");
      //public String getAbsolutePath():返回此File的绝对路径名字符串
      System.out.println(f1.getAbsolutePath());
      System.out.println(f2.getAbsolutePath());
      System.out.println("-------------");
      //public String getPath():将此File转换为路径名字符串
      System.out.println(f1.getPath());
      System.out.println(f2.getPath());
      System.out.println("-------------");
      //public String getName():返回此File表示的文件或文件夹(目录)名称
      System.out.println(f1.getName());
      System.out.println(f2.getName());
      System.out.println(f3.getName());
      System.out.println("-------------");
      //public long length():返回此File表示的文件的长度,获得的是构造方法指定的文件的大小，以字节为单位
      //文件夹是没有大小概念的，不能获取文件夹的大小
      //如果构造方法中给出的路径不存在，那么length方法返回0
      System.out.println(f1.length());
      System.out.println(f2.length());//路径错误
}
//输出结果：
/Users/test/photo1.jpeg
/Users/xxx/IdeaProjects/JavaSE/photo2.jpeg
-------------
/Users/test/photo1.jpeg
photo2.jpeg
-------------
photo1.jpeg
photo2.jpeg
test
-------------
800574
0
```

## 3.File的判断方法

```java
public boolean exists():此File表示的文件或目录是否存在
public boolean isDirectory():此File表示的是否为目录
public boolean isFile():此File表示的是否为文件
```

## 4.File的创建删除方法

```java
public boolean createNewFile():当且仅当具有该名称的文件尚不存在时，创建一个新的空文件
public boolean delete():删除由此File表示的文件或目录
public boolean mkdir():创建由此File表示的目录
public boolean mkdirs():创建由此File表示的目录，包括任何必须但不存在的父目录

//例子
  public static void main(String[] args) {
        /*
          public boolean createNewFile():当且仅当具有该名称的文件尚不存在时，创建一个新的空文件
          true 文件不存在，创建文件；false 文件存在，不会创建
          此方法只能创建文件，不能创建文件夹，创建文件的路径必须存在，否则会抛出异常
        */
        File f1=new File("/Users/test/infor.txt");
        try{
            System.out.println(f1.createNewFile());
        }catch (IOException e){
            System.out.println("文件路径不存在");
        }
        File f2=new File("/Us/test/infor.txt");
        try{
            System.out.println(f2.createNewFile());
        }catch (IOException e){
            System.out.println("文件路径不存在");
        }
        System.out.println("-------------");
        /*public boolean mkdir():创建单级空文件夹
          public boolean mkdirs():既可以创建单极空文件夹，也可以创建多级文件夹
          true 文件夹不存在，创建文件；false 文件夹存在，不会创建；构造方法中路径不存在
          这两个方法只能创建文件夹，不能创建文件
        */
        File f3=new File("/Users/test/animal/dog");
        System.out.println(f3.mkdirs());
        File f4=new File("/Users/test/plant");
        System.out.println(f4.mkdir());
        File f5=new File("/Us/test/plant");
        System.out.println(f5.mkdir());//不会抛出异常，路径不存在，不会创建
        System.out.println("-------------");
        /*
           public boolean delete():删除由此File表示的文件或目录
           true 文件/文件夹删除成功，创建文件；false 文件夹中有内容，不会删除；构造方法中路径不存在
           delete方法是直接在硬盘删除文件/文件夹。不走回收站，删除需谨慎
         */
        File f6=new File("/Users/test/animal");
        System.out.println(f6.delete());
        System.out.println(f2.delete());
        System.out.println(f1.delete());
}
//输出结果：
true
文件路径不存在
-------------
true
true
false
-------------
false
false
true
```

## 5.File的遍历方法

```java
public String[] list():返回一个String数组，表示该File目录中所有字文件或目录
public File[] listFiles():返回一个File数组，表示该File目录中所有的字文件或目录

//例子
public static void main(String[] args) {
      //public String[] list():返回一个String数组，表示该File目录中所有字文件或目录
      File f1=new File("/Users/test");
      String[] arr=f1.list();
      for (String s : arr) {
        System.out.printf("%s ",s);
      }
      System.out.println("-------------");
      //public File[] listFiles():返回一个File数组，表示该File目录中所有的字文件或目录
      File f2=new File("/Users/test");
      File[] files=f2.listFiles();
      for (File file : files) {
        System.out.println(file);
      }
}
//输出结果：
photo1.jpeg .DS_Store plant animal photo2.jpeg 
-------------
/Users/test/photo1.jpeg
/Users/test/.DS_Store
/Users/test/plant
/Users/test/animal
/Users/test/photo2.jpeg
```

