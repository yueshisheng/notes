### Java的流知识

Java的io流分类：

1：按流向分为输入流和输出流

如何区分输入流和输出流呢？

输入流是从文件、数据库，数据流向目的地

输出流是从源头流向文件、数据库等

![image-20200718100119983](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200718100119983.png)

![image-20200718100135441](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200718100135441.png)

2：按操作单元分为字节流（inputstream）或字符流（reader）

一般来说，	图像音频直接用字节流，文本一般用字符流，小心乱码

3：按流的角色分为：节点流和处理流

节点流就是在固定的地方进行读取数据（不带buffer）：FileReader、StringReader。接的数据类型

处理流是指将输入输出流进行封装，然后调用被封装流的功能实现数据的读写，例如

BufferedReader，加入缓冲，避免重复读写磁盘

流的分类

![IO-操作方式分类](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-6/IO-%E6%93%8D%E4%BD%9C%E6%96%B9%E5%BC%8F%E5%88%86%E7%B1%BB.png)

BIO、NIO是什么呢？

这些都是Java对操作系统的io操作的封装，使用时，直接调用api即可

同步：必须等每一个任务执行完才能继续去执行

异步：任务来回切换来执行

阻塞：	当前线程会挂起

非阻塞：会继续执行其他线程

同步或异步指的是一种行为，会不会等

阻塞是指一种状态，指的是当前线程是不是不能继续执行下去

### Blocking  io

同步且阻塞

是一对一的请求和数据读取，数据必须让一个进程来读取

![image-20200718092916537](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200718092916537.png)

有一个Acceptor来一直在监听是否有连接请求（accept（）方法），如果有一个请求，就建立socket连接

socket.accept()、socket.read()、socket.write()，进行数据的读取和写入，那socket是什么呢？

如下图，socket是介于应用层（进程）和传输层的抽象层，负责这两个的通信，在这里就是，thread与客户进程进行通信，socket是插头的意思，socket通过将传输层以下的所有层抽象，只提供几个接口供进程来调用，这样就很好的实现进程之间的网络通信，利用了门面的设计模式

必须明白，socket实现的是进程的网络通信，进程的本地通信可以用shared memory，信号量，临界区实现

​            ![img](https://qqadapt.qpic.cn/txdocpic/0/c131e3461dfa2195a6724f6fcb178bba/0?w=669&h=487)            

这是socket通信的详细过程

bind（）时将ip地址和端口号的组合给了socket，只有服务器才能来调用

![image-20200718094333070](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200718094333070.png)

要想处理多个请求，必须用多线程，访问量太大的话，无法承受

### 伪异步的BIO

加入一个线程池，通过线程的调度来实现假的异步

![image-20200718094712758](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200718094712758.png)

### NIO

想处理更大数量级的客户请求，必须用NIO

非阻塞，同步

Java中的流本身都是阻塞的，但可以用NIO来实现非阻塞的IO操作

线程通过selector来在合适的时候选择合适的chanel来进行数据的读入和写入

NIO三个最重要的：channel、selector、buffer

![image-20200718105953771](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200718105953771.png)

![image-20200718105851197](C:\Users\yueshisheng\AppData\Roaming\Typora\typora-user-images\image-20200718105851197.png)

### AIO

aio是同步io，是nio的2.0版本

异步io是通过事件和回调机制来实现

总结：BIO是阻塞同步、NIO是非阻塞同步、AIO是异步非阻塞