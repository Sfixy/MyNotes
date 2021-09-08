# java

## Java运行机制及运行过程

### Java语言特点

1. 面向对象
   - 两个基本概念：类、对象
   - 三大特性：封装、继承、多态
2. 健壮性
   - 吸收了C\C++语言的优点，但去掉了其影响健壮性的部分（如指针、内存的申请与释放等），提供了相对安全的内存管理和访问机制
3. 跨平台性
   - 跨平台性：通过Java语言编写的应用程序在不同的系统上都可以运行
   - 原理：只要在需要运行Java应用程序的操作系统上，先安装一个Java虚拟机即可，由JVM来负责Java系统在该系统中的运行

![image-20210713144451775](D:\Github\MyNotes\java\image-20210713144451775.png)

#### 核心机制——垃圾回收

- 不在使用的内存空间应该回收——垃圾回收
  - 在c/c++语言中，由程序员负责回收无用内存
  - 在Java语言消除了程序员回收无用内存空间的责任；它提供了一种系统线程跟踪储存空间的分配情况。并在JVM空闲时，检查并释放那些可被释放的存储空间
- 垃圾回收在Java程序运行的过成中自动进行，程序员无法精确控制和干预

**Java程序还会出现内存泄露和内存溢出问题吗：Yes**

## JDK、JRE、JVM关系

![image-20210713150004509](D:\Github\MyNotes\java\image-20210713150004509.png)

![image-20210713150122165](D:\Github\MyNotes\java\image-20210713150122165.png)

**不同的操作系统安装不同的jdk，jvm不相同**

**字节码文件名对应类名，不是文件名**

## 注释

单行注释

多行注释

文档注释

### 单行注释和多行注释作用

对程序进行解释说明，增强可读性。方便自己，方便别人

对代码进行调试

### 特点

注释的内容不参与编译。换句话说，编译以后生成的.class字节码文件，不包含注释掉的信息

### 文档注释（Java特有）

```java
package day01;

/**
 @author 指定java程序的作者
 @version 指定源文件的版本
 */

public class HelloJava {
    /**
     * 这是个main（）方法
     * 参数
     * @param args
     */
    public static void main(String[] args) {
        System.out.println("你好");
    }

}

```

注释内容被jdk提供的工具javadoc所解析，生成一套以网页文件形式体现的该程序的说明文件

## java文件

一个java文件可以有多个Java类，但是只有和文件同名的类才能声明为public，且最多只能有一个类声明为public

```java
package day01;

public class Hello {

    public static void main(String[] args) {//arguments:参数，args可以被定义为其他名字比如a，[]可以加在args后面
        System.out.println("文件");
    }

}

class Person{
}

class Animal{
}
```

程序的入口是main（）方法。格式是固定的

输出语句：

System.out.println("文件");//换行

System.out.print("文件");//不换