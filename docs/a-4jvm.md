### jvm的内存区域

在Java的1.6前，有方法区，是线程共享的，运行常量池就在那里。堆也是共享的

![image-20200718111303429](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200718111303429.png)

在Java1.8后，方法区被元空间代替，元空间在直接内存

![image-20200718111434961](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200718111434961.png)

线程私有的：程序计数器、虚拟机栈、native method stack

共享的：heap以及method area

#### 程序计数器

记录当前执行的字节码文件的行号，为了保证，在线程切换后，还能回到当前的程序位置，所以这个是线程私有的

#### jvm stack

因为栈一般存放方法的局部变量，所以是私有的

虚拟机栈会抛出：StackOverflow和outofmemory的异常

### Native method  stack

本地方法栈

​	



