------

首先了解一下Java的基本数据类型：
![image.png](https://upload-images.jianshu.io/upload_images/12913154-7a4a475def2a353f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
byte-1字节 short--2字节 int--4 long-8 char-2 float--4 double-8 Boolean是1bit
如下图所示，byte，int，short，long的包装类实现了常量池的技术，会不会好奇常量池在哪里呢？
在jvm虚拟机中的方法区中，刚才那四种变量如果数值是[-128,127]，就直接在常量池的缓存数据中去找，如果超出这个范围，就需要在堆中，重新来创建对象
对于char的包装类的话是[0,127]这个范围，Boolean直接返回true或false
对于float和double，没有使用常量池技术
![image.png](https://upload-images.jianshu.io/upload_images/12913154-703a8708759e4f9d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/12913154-82bd8c935ff1427f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
具体的应用
直接用Integer来 进行定义的，如果范围在[-128,127]，会使用常量池的对象，否则会在堆中创建对象，和Integer.valueOf(40)等价
![image.png](https://upload-images.jianshu.io/upload_images/12913154-0727e24249519b79.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
两个用Integer定义的常量池的对象是一样的，值一样，常量池的对象也一样，但是堆对象就不一样了
![image.png](https://upload-images.jianshu.io/upload_images/12913154-1f4390e52e159bf1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
其实就是+号，只能用在基本数据类型，需要进行拆箱后，直接来比较数值，所以值一样就可以了
![image.png](https://upload-images.jianshu.io/upload_images/12913154-49342b723e3ca57e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## Java中只有值传递
在函数参数传递中，Java只能将原件的复制品传递到函数，不会影响原变量的结果
像C语言和c++语言可以引用传递
最经典的例子，就是互换两个数的值时，如果只有值传递则无法成功
![image.png](https://upload-images.jianshu.io/upload_images/12913154-bee9ca7a7fa98068.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/12913154-530606849a8120c0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
上述例子说明，对于参数是基本数据类型的，只能是值传递，只能修改变量的复制版，对原版不会造成影响
如果要对值进行改变，参数可以是引用传递，例如下图举例，如果参数是引用，函数会复制一个引用，和之前的引用一样，共同指向数组，这样的话，如果数组发生变化，两个引用所引用的值也会发生变化
![image.png](https://upload-images.jianshu.io/upload_images/12913154-3333991cf36f7f5b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/12913154-e01b220593e94234.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
因为是值传递，无法改变基本数据类型，可以修改对象引用的对象的状态，但也无法指向一个新的对象
![image.png](https://upload-images.jianshu.io/upload_images/12913154-3fd264882fa7d6f9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##重写和重载的区别
重写发生在运行期，且名字，参数和返回类型必须一致，且一旦被static和final以及private来修饰父类后，无法重写
![image.png](https://upload-images.jianshu.io/upload_images/12913154-f39800645b7c4768.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/12913154-2772e790e7cf00a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 浅复制和深复制的区别
对于基本的数据类型都是值传递，对于引用对象，浅复制只复制一个引用，一般常用，深复制，会复制一个引用以及引用的对象，其实就是两个对象
![image.png](https://upload-images.jianshu.io/upload_images/12913154-0b540fda56d9fdf2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##面向对象和面向过程的区别
面向过程的性能更高，但可维护性，可扩展性差
面向对象正相反，维护性、扩展性，适合大型项目开发
构造器可以被重载，不能被重写
![image.png](https://upload-images.jianshu.io/upload_images/12913154-25c7c9ea35cfd988.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
如果子类的构造方法是有参数的，但无法super父类与之对应的有参数的构造方法，会发生编译错误，如果加上无参构造函数，就去执行该构造函数
![image.png](https://upload-images.jianshu.io/upload_images/12913154-5896309c4794e004.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
成员变量是属于类的变量，局部变量是属于一个方法的变量

![image.png](https://upload-images.jianshu.io/upload_images/12913154-cc858fa5a835ab21.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)