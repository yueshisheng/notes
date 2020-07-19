### 静态方法

静态方法其实就是类方法，与类有关的，普通的方法在类被实例化后，被对象来调用，静态方法无法调用非静态方法，因为非静态方法必须依赖于对象的实例化才能存在，相反，非静态方法中，可以有静态方法
静态变量是类变量，所有的对象都会对其引用，在内存中只能有一个副本，但非静态变量，一个对象有一个副本，互不影响

![image.png](https://upload-images.jianshu.io/upload_images/12913154-873281b4c7e7164e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

静态代码块**只能在类加载时被执行一次**，可以有多个静态代码块

![image.png](https://upload-images.jianshu.io/upload_images/12913154-53d0092145a684a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### final、static、this、super关键字总结

被final修饰的类，无法被继承，所有方法被标记为final类型的

被final修饰的方法，无法被重写

被final修饰的变量，如果是基本数据类型，一旦声明就无法修改值，如果是引用，不能再指向其他对象

那我们为什么要使用final关键字呢？

1：方法声明为final关键字，就不能被重写

2：早期用final，可以提升方法的效率，现在的private是隐形的final类型的

this关键字是用来引用当前实例的变量或方法

super是在子类来访问父类的属性和方法

![image-20200717152555264](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200717152555264.png)

注意：this和super不能用在static方法，this是因为和实例相关，super体现在继承，其实也和实例有关，先有实例才能有继承

### 接口和抽象类

1:接口不能有实现的方法，抽象类可以有实现的方法

2：接口的默认修饰为public，且只能用static和final来修饰，抽象类不能用static和final修饰，因为这样修饰完，就不能被继承，但抽象类的主要目的是重写

3：一个类只能有一个抽象类，但可以有多个接口

4：抽象类是对类的抽象和设计，但接口是对方法的抽象设计

### String、StringBuilder、StringBuffer

String为什么是不可修改的对象？

string是用final关键字修饰过的：

private final byte[] value（Java 9后）

StringBuilder、StringBuffer都是继承抽象类：AbstractStringBuilder，都是用char[]value来保存数据的，没有用final关键字来修饰的，所以是可变的

以下是AbstractStringBuilder的源码

```java
abstract class AbstractStringBuilder implements Appendable, CharSequence {
    /**
     * The value is used for character storage.
     */
    char[] value;

    /**
     * The count is the number of characters used.
     */
    int count;

    AbstractStringBuilder(int capacity) {
        value = new char[capacity];
    }}
```

安全性和性能：String是不可变的对象，所以肯定是安全的，是私有的，别人也篡改不了

StringBuilder没有加同步锁，是线程不安全的，性能更优，因为上锁和解锁是很费时间的，与之对应的，StringBuffer有线程锁，性能低

![image-20200717154358882](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200717154358882.png)

### Object的常见方法

常见的方法：hashcode（），equal（），clone（）（创建一份当前对象的拷贝），tostring（）等等

sleep方法没有释放锁，但wait却释放了锁

```java
public final native Class<?> getClass()//native方法，用于返回当前运行时对象的Class对象，使用了final关键字修饰，故不允许子类重写。

public native int hashCode() //native方法，用于返回对象的哈希码，主要使用在哈希表中，比如JDK中的HashMap。
public boolean equals(Object obj)//用于比较2个对象的内存地址是否相等，String类对该方法进行了重写用户比较字符串的值是否相等。

protected native Object clone() throws CloneNotSupportedException//naitive方法，用于创建并返回当前对象的一份拷贝。一般情况下，对于任何对象 x，表达式 x.clone() != x 为true，x.clone().getClass() == x.getClass() 为true。Object本身没有实现Cloneable接口，所以不重写clone方法并且进行调用的话会发生CloneNotSupportedException异常。

public String toString()//返回类的名字@实例的哈希码的16进制的字符串。建议Object所有的子类都重写这个方法。

public final native void notify()//native方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。

public final native void notifyAll()//native方法，并且不能重写。跟notify一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。

public final native void wait(long timeout) throws InterruptedException//native方法，并且不能重写。暂停线程的执行。注意：sleep方法没有释放锁，而wait方法释放了锁 。timeout是等待时间。

public final void wait(long timeout, int nanos) throws InterruptedException//多了nanos参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上nanos毫秒。

public final void wait() throws InterruptedException//跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间这个概念

protected void finalize() throws Throwable { }//实例被垃圾回收器回收的时候触发的操作
```

### equals和==区别

对于基本数据类型，==和equal比较的都是值

对于引用对象，==比较的是对象的值是否一样，equal比较的是对象的值，比如要比较String类型的对象值是否相等，只能用equal

a和b引用不一样，只是值一样，aa和bb都在常量池，所以引用地址也一样

```java
public class test1 {
    public static void main(String[] args) {
        String a = new String("ab"); // a 为一个引用
        String b = new String("ab"); // b为另一个引用,对象的内容一样
        String aa = "ab"; // 放在常量池中
        String bb = "ab"; // 从常量池中查找
        if (aa == bb) // true
            System.out.println("aa==bb");
        if (a == b) // false，非同一对象
            System.out.println("a==b");
        if (a.equals(b)) // true
            System.out.println("aEQb");
        if (42 == 42.0) { // true
            System.out.println("true");
        }
    }
}
```

### hashcode和equal

为什么要有hashcode？

![image-20200717173135209](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200717173135209.png)

比较时先看hashcode是不是一样，然后再用equal来进行比较

![image-20200717173310278](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200717173310278.png)

equal函数默认是比较两个对象的地址是不是一样，因为用的是==



```java
public boolean equals(Object obj) {
    return (this == obj);
}
```



通常我们重写equal函数，让他们值相等就可以了

就是说：不重写，只有是一个对象才能是true，重写后，对象可以不是一个，只要值一样就可以

下边是不重写的示例

```Java
public static void main(String[] args) {
        // 新建2个相同内容的Person对象，
        // 再用equals比较它们是否相等
        Person p1 = new Person("eee", 100);
        Person p2 = new Person("eee", 100);
        System.out.printf("%s\n", p1.equals(p2));
    }
```

结果是false

Hashcode的使用得分情况

1：对于不是HashSet, Hashtable, HashMap的数据结构中，hashcode函数没啥用

2：在HashSet, Hashtable, HashMap数据结构中，如果出现对象值不一样，但hashcode值是一样的，这就是哈希冲突

所以，如果仅仅来重写equal方法，即使对象一样，而hashcode（）原始的方法只是获得当前对象的地址值，这样的话，出现对象一样，可能hashcode的值不一样，因为，毕竟不是一个对象，重写equal方法是因为，不重写值一样，结果也是false

### 获得键盘输入的

scanner那种太熟了，不写了

```java
BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
String s = input.readLine();
```

