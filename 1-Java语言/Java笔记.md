# 错题集合

### 1、Java虚拟机运行时数据区域

![img](https://img-blog.csdn.net/20170621113028178?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU3RyaWRlQmlu/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

在Java虚拟机运行时，主要有以下几个数据区域：

1. **程序计数器（Program Counter Register）**：
   - 程序计数器是一块较小的内存空间，它可以看作是当前线程所执行的字节码的行号指示器。
   - 在多线程环境下，每个线程都有自己独立的程序计数器，互不影响。
2. **Java虚拟机栈（JVM Stack）**：
   - Java虚拟机栈是每个线程私有的，用于存储方法调用的栈帧（Stack Frame）。
   - 每个方法在执行时会创建一个栈帧，栈帧中存储了方法的局部变量表、操作数栈、动态链接、方法返回地址等信息。
   - 栈帧的大小在编译时就确定了，它会随着方法的调用和返回而动态地压入和弹出栈中。
3. **本地方法栈（Native Method Stack）**：
   - 本地方法栈类似于Java虚拟机栈，但是用于执行本地方法（Native Method）。
   - 本地方法栈也是每个线程私有的，与Java虚拟机栈类似。
4. **堆（Heap）**：
   - 堆是Java虚拟机中所有线程共享的内存区域，用于存储对象实例。
   - 在堆中，对象实例的内存分配是动态的，由垃圾回收器负责回收不再被引用的对象实例。
   - Java虚拟机的堆区域可以分为新生代（Young Generation）、老年代（Old Generation）和永久代（Perm Generation）等。
5. **方法区（Method Area）**：
   - 方法区也是所有线程共享的内存区域，用于存储类的结构信息、常量、静态变量、即时编译器编译后的代码等。
   - 在方法区中，还包括运行时常量池（Runtime Constant Pool）等。
6. **运行时常量池（Runtime Constant Pool）**：
   - 运行时常量池是方法区的一部分，用于存放编译时生成的各种字面量和符号引用。
   - 在类加载后，将常量池中的符号引用转换为直接引用。
7. **直接内存（Direct Memory）**：
   - 直接内存不是虚拟机运行时数据区域的一部分，但是通过Native方法使用到。
   - 直接内存是由操作系统管理的，通过Native方法来直接分配堆外内存，它的大小不受Java堆大小的限制。

### 2、字节流和字符流

字节流是以字节（8个bit）为单位进行读取的，一般使用Stream为结尾的类。字符流是以字符（16个bit）为单位进行读取的，常见的如Reader和Writer类。

在读取视频、图片、音频等文件时，应当采取字节流。在读取文本文件时，应当使用字符流。如果使用字节流，那么还应该进行选择字符集，以及编码方式的转换。

### 3、HashMap采用哪种方式来解决哈希冲突？

首先采用链地址法来解决，其次还可以考虑开放地址法来解决。

### 4、Java虚拟机的功能

![image-20240301130700478](D:\Post_Graduation\java_learn\找工作\java学习路线及过程\2-Java基础巩固\刷题\image-20240301130700478.png)

这里尤其需要注意D答案，Java虚拟机是运行在操作系统之上的，因此并不和硬件直接接触，而是与直接使用系统调用。

### 5、TreeSet的存储是按照元素排好序的

TreeSet类的底层实现数据结构是红黑树，即带有特殊自平衡方法的二叉搜索树。



### 6、取模运算的结果

```java
public class Test3{
 public static void main(String args[]){
    System.out.println(100%3);
    System.out.println(100%3.0);
 }
}
```

结果是1和1.0



### 7、垃圾回收机制

以下哪项陈述是正确的？

A垃圾回收线程的优先级很高，以保证不再使用的内存将被及时回收

B垃圾收集允许程序开发者明确指定释放哪一个对象

C垃圾回收机制保证了JAVA程序不会出现内存溢出

D进入”Dead”状态的线程将被垃圾回收器回收

E以上都不对

a:在运行一个Java程序时，会启动至少两个线程一个是主程序线程，一个是垃圾回收线程。垃圾回收线程的优先级比较低，等有空的时候才执行。

b:垃圾回收机制并不允许开发者去指定清楚哪一个，但程序开发者可以推荐，至于是否执行，是垃圾回收线程所做的事情了。

c:仍然可能存在溢出的情况

d:进入Dead状态的线程，还有一次机会，垃圾回收器会给两次机会。，真正宣布一个对象死亡，至少需要经历2次标记过程。当第一次标记时会同时进行一次筛选(判断此对象是否有必要执行finalize方法)。如果对象没有覆盖该方法，就面临死亡，所以说这个方法是对象逃脱死亡命运的最后一次机会。  大家顶我上去，让更多的人看到。看前面没人讲的很详细，如果想深究，去看书。



### 8、一个static变量，不能在方法中申请，只能在类主体中定义

```java
public class Test {
    public int aMethod(){
        static int i = 0;
        i++;
        return i;
    }
public static void main(String args[]){
    Test test = new Test();
    test.aMethod();
    int j = test.aMethod();
    System.out.println(j);
    }
}
```

编译失败



### 9、以下关于对象序列化描述正确的是

A使用FileOutputStream可以将对象进行传输

B使用PrintWriter可以将对象进行传输

C使用transient修饰的变量不会被序列化

D对象序列化的所属类需要实现Serializable接口

能进行对象传输的类主要是ObjectOutputStream和ObjectInPutStream，这两个可以将对象进行传输。

而FileOutPutStream是写文件的类。将ObjectOutputStream所传输的类写入文件。

使用transient修饰的变量不会被序列化



### 10、关于捕获异常的执行返回问题

```java
    static int testException(){
        try{
            throw new IOException("this is a test");
        }catch (Exception e){
            System.out.println("this is catch");

        }finally {
            System.out.println("this is finally");

        }
        System.out.println("this is end");
        return 1;
    }
```

不管catch是否有return，finally都会执行。如果二者都有return，那么最终只会以finally的为终点输出。如果finally没有，而catch有，那么会先把catch里面的非return语句执行完，再去执行finally的语句，最后以catch的return作为返回。如果二者都没有return，那么程序会继续往下执行。



### 11、可以把任何一种数据类型的变量赋给Object类型的变量。

A对

B错

别忘了自动装箱和自动拆箱



### 12、注意finally和static变量的区别。

static是对象共享的。而finally是不可改变的，但最开始可以不赋予初值，一旦赋予初值之后就不能再改变。



### 13、已知有下列Test类的说明，在该类的main方法的横线处，则下列哪个语句是正确的？（）

```java
public class Test

{

private float f = 1.0f;

int m = 12;

static int n = 1;

public static void main (String args[])

{

Test t = new Test();

————————

}
}
```

A t.f = 1;

B this.n = 1;

C Test.m = 1;

D Test.f = 1;

A 虽然f是私有变量，但是main方法是在Test类的内部，因此可以直接通过对象.私有变量的方式访问到f。

B static是类加载之前就会加载的，因此static方法里面，不允许出现this，只能使用类内的static变量和方法



### 14、以下代码执行后输出结果为（ ）

```java
public class Test
{
    public static Test t1 = new Test();
    {
         System.out.println("blockA");
    }
    static
    {
        System.out.println("blockB");
    }
    public static void main(String[] args)
    {
        Test t2 = new Test();
    }
 }
```

blockAblockBblockA

加载顺序

  (1) 父类静态对象和静态代码块

  (2) 子类静态对象和静态代码块 

   (3) 父类非静态对象和非静态代码块

   (4) 父类构造函数

   (5) 子类  非静态对象和非静态代码块

   (6) 子类构造函数



### 15、将下列（A、B、C、D）哪个代码替换下列程序中的【代码】不会导致编译错误？



```java
interface Com{
    int M=200;
    int f();
}
class ImpCom implements Com{
    【代码】
}
```

A

public int f(){return 100+M;}

B

int f(){return 100;}

C

public double f(){return 2.6;}

D

public abstract int f();

在接口中如果定义了成员变量，那么这个成员变量将不会是普通的成员变量，而是默认为public static final。而在实现类去实现的时候，访问限权一定不能比原来的接口小，而原来接口中的方法访问限权一定是public，因此实现时也一定得是public。



### 16、类访问修饰符

类的修饰符主要分成三个，public、默认、final。

public和默认的区别在于，public的类可以在其它任何一个地方的类进行import导入。而默认的类，只能被在同一个包下的类进行import导入。

final指的是这个类不会被继承



### 17、成员访问修饰符

![image-20240302151021127](D:\Post_Graduation\java_learn\找工作\java学习路线及过程\2-Java基础巩固\刷题\image-20240302151021127.png)

说明一下，这个的protected，可以访问分为三种情况：

+ 同一个包中，如果其他类的方法中new了这个类，那么可以直接在这个同包的类的方法中直接通过对象.成员的方式获取protected成员；
+ 子类也可以无条件获得protected；



default：

+  只能是在同一个包中，如果其他类的方法中new了这个类，那么可以直接在这个同包的类的方法中直接通过对象.成员的方式获取protected成员；
