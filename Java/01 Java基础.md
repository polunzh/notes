## Java的体系
- Java SE (J2SE) (Java 2 Platform Standard Edition, java平台标准版，【桌面版】)
- Java EE (J2EE) (Java 2 Platform Enterprise Edition java企业平台，【用于构建大型网站】)
- Java ME(J2ME) (Java 2 Platform Micro Edition, java平台微型版,【一般用于手机移动终端】)

## Java程序的运行
    Java虚拟机JVM (Java Virtual Machine)，它是Java运行环境的一部分，Java运行环境又称为JRE
(Java Runtime Environment)

## 如何进行Java开发
1. JDK是Java语言的开发包，可以将*.java文件编译为可执行Java程序
2. 可执行Java程序需要JVM才可以运行
3. JRE包含了JVM
4. JDK包含了JRE

### JRE
    运行Java程序所必须的环境的集合，包含JVM标准实现及Java核心类库。仅能够完成Java的运行，
而无法对Java进行编译、调试等。
    JRE有独立运行的版本，如果一个用户仅需要运行Java，安装JRE即可。

### JDK
    JDK是Java语言的软件开发工具包(SDK)。是面向Java开发者发布的Java套件

    JDK包含的基本组件包括：编译器、Jar打包工具、Javadoc文档生成器、Debug调试器、头文件生成器
、反汇编器、监控工具等。
    JDK中包含完整的JRE。如果安装了JDK，则不必要再次安装JRE。