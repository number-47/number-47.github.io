title: Java运行机制/JVM/JRE/JDK
tags:
  - Java基础
categories:
  - Java
author: number-47
date: 2017-11-25 12:56:00
---
## JAVA运行机制
Java语言编写的程序需要经过编译步骤，这个编译步骤并不会生成特定平台的机器骂，而是生成一种与平台无关的字节码（也就是\*.class文件），这种字节码不是可执行性的，必须使用Java解释器来解释执行。
Java程序的执行过程需要想编译、后解释，如下：

java源文件\*.java—使用javac编译—>编译生成\*.class文件（字节码文件）—使用java解释执行—>特定平台的机器码。<!--more-->

## JVM

Java语言里负责解释执行字节码文件的Java虚拟机，即JVM(Java Virtual Machine)。

**问：为什么Java可以跨平台？**

答：当使用Java编译器编译Java程序时，生成的是与平台无关的字节码，这些字节码不面向任何具体平台，只面向JVM。不同平台上的JVM都是不同的，但是它们提供了相同的接口。只要不同平台实现了相应的虚拟机，编译后的Java字节码就可以在该平台上运行。

## JRE

JRE（Java Runtime Environment，Java运行环境），包括Java虚拟机JVM和Java程序所需要的核心库等，如果要运行一个开发好的Java程序，计算机中只需要安装JRE。

## JDK

JDK（Java Development Kit，Java开发工具包），提供给Java开发人员使用的，其中包含了Java的开发工具（javac.exe 编译工具/jar.exe 打包工具），也包含了**JRE**。所以，安装了JDK后，不需要再单独安装JRE。

