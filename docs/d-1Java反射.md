### Java的反射

反射指：在运行情况下，能获得任一个类的属性和方法，以及动态调用一个实例化对象的属性和方法（关键是在运行情况下）

想要动态的获取上述的信息，需要找到该类对应的class对象

那如何来获取class对象呢？利用属性来获得class对象是最常见的方法

1：调用类的属性class来获得class对象，其实就是得到类的class文件，就是那个编译后得到的

```java
Class alunbarClass = TargetObject.class;
```

2：直接利用forName方法，参数是该类的全限定名，如 Person的全限定名:java.lang.Person; 

```java
Class alunbarClass1 = Class.forName("cn.javaguide.TargetObject");
```

3：在实例化对象后，调用对象的getClass方法

Person p = new Person(); 	Class<?> clazz = p.getClass();

根据class对象来创造实例

1：直接调用class的方法，适应有无参的构造函数，如果没有无参的构造函数，会有异常，这也就是为什么必须有一个无参的构造函数

TargetObject targetObject = (TargetObject) tagetClass.newInstance();

2：对于有参的构造函数，调用class对象的方法得到构造器对应的对象，然后利用构造器的对象实例化（先调用构造函数，然后传入具体参数）

![image-20200717202627419](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200717202627419.png)

创建对象的五种方法

![image-20200717203144630](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200717203144630.png)

反射的优点：能动态的调用对象，代码灵活度比较高

反射的缺点：效率有点慢

动态编译和静态编译的区别？

我们需要知道在编译中，对于一些import的Java.util的库，需要调用这些对应的类定义，静态编译是指在编译时，直接将这些代码全部替换，但动态编译是指在运行时，运行到哪一个，就去调用哪一个

各自的优缺点：静态编译的代码太庞大了，优点是执行时，不用去调用，比较快。动态编译比较灵活



