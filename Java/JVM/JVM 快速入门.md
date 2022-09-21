Java 程序执行流程图

>栈中不会存在垃圾，垃圾存在于堆中：方法区和堆。JVM 调优也多只存在于针对堆的调优。

![[Pasted image 20220921114457.png]]

## JVM 架构图

![[Pasted image 20220921114953.png]]

## 类加载器

作用：加载 Class 文件

![[Pasted image 20220921120414.png]]

Class 是一个抽象的模板，Car 对应的 Class 只有一个，但是 Car 对象可以有多个。

```java
public class Main
{
    
    public String name;
    
    public static void main(String[] args) {
        Main m1 = new Main();
        Main m2 = new Main();
        Main m3 = new Main();
        
        m1.name = "test m1";
        m2.name = "test m2";
        
        System.out.println(m1.hashCode());
        System.out.println(m2.hashCode());
        System.out.println(m3.hashCode());
        
        Class aClass1 = m1.getClass();
        Class aClass2 = m2.getClass();
        Class aClass3 = m3.getClass();
        System.out.println(aClass1.hashCode());
        System.out.println(aClass2.hashCode());
        System.out.println(aClass3.hashCode());
    }
}
```

```java
515132998
474675244
932583850
32374789
32374789
32374789


** Process exited - Return Code: 0 **
```

加载器：

1. 虚拟器自带的加载器
2. 启动类（根）加载器
3. 扩展类加载器
4. 应用程序（系统类）加载器

## Native

带了 native 关键字，说明 Java 作用范围达不到了，会去调用底层 C 语言的库。程序进入 `本地方法栈`，调用本地方法接口：JNI

JNI作用：扩展 Java 的使用，融合不同的编程语言为 Java 使用。

Native 会在内存区域中专门开辟一块编辑区域：Native Method Stock ，登记 native 方法，最终执行的时候，通过 JNI 加载本地方法库中的方法。

## 方法区

方法区是所有线程共享，所有字段和方法字节码，以及一些特殊方法，如构造方法，接口代码也在此定义。简单的说：所有定义的方法的信息都保存在该区域，此区域属于共享区域。

==静态变量、常量、类信息（构造方法、接口定义）、运行时的常量池存在此方法区中，但 实例变量 存在堆内存中，与方法区无关==

包含内容：

* static
* finial
* Class
* 常量池

## 栈

栈：先进后出，后进先出

队列：先进先出，FIFO：First Input First Output


喝多了吐就是栈，吃多了拉就是队列

为什么 main 方法最先执行，最后结束？

栈内存，主管程序的运行，生命周期和线程同步；线程结束，栈内存也就是释放。==对于栈来说，不垃圾回收问题。==

栈里面包含的内容：

* 8 大基本类型
* 对象引用
* 实例的方法

栈运行原理：栈帧

## 堆

Heap，一个 JVM 只有一个堆内存，堆内存大小是可以调节的。

类加载读取了类文件后，一般会把什么东西放到堆中？类，方法，常量，变量……保存我们所有引用类型的真实对象。

堆内存的细分区域：

* 新生区（伊甸园区）：Young/New
	* 伊甸园区：Eden Space
	* 幸存 0 区
	* 幸存 1 区
* 养老区：Old
* 永久区：Perm

GC 垃圾回收，主要是在新生区和养老区。

在 JDK8 以后，永久存储区改了名字：元空间。元空间逻辑上存在，物理上不存在。

### 调优

![[Pasted image 20220921161044.png]]

**新生区**

类：诞生 和 成长 的地方，甚至死亡

* 伊甸园区：所有对象都是在伊甸园区 new 出来的
* 幸存者区（0， 1）

**永久区**

这个区域常驻内存。用来存放 JDK 自身携带的 Class 对象，Interface 元数据，Java 运行时的一些环境或类信息，这个区域不存的垃圾回收。关闭虚拟机就会释放此区域内容。

* jdk 1.6 之前：永久代，常量池在方法区
* jdk 1.7：永久代，慢慢在退化，去永久代，常量池在堆中
* jdk 1.8：无永久代，常量池在元空间

**OOM**

1. 尝试扩大堆内存，再次运行程序查看结果
2. 分析内存，看具体出问题的地方

## 三种 JVM

* Sun 公司：HotSpot
* BEA：JRockit
* IBM：J9VM

## GC

GC 大部分都是在新生代

GC 有两种类型：轻GC 和 重GC