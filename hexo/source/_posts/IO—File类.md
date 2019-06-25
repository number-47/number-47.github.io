---
title: IO流——File类
date: 2018-01-01 12:56:00
tags: Java基础
categories: Java
---
## File类

### 创建文件对象

**注：**只是创建File对象，以下程序并不会在文件系统中创建这些目录或文件。

```
package io;
import java.io.File;
public class CreateFile {
	public static void main(String[] args) {
		// 绝对路径
        File f1 = new File("d:/TestFolder");
        System.out.println("f1的绝对路径：" + f1.getAbsolutePath());
        // 相对路径,相对于工作目录，如果在eclipse中，就是项目目录
        File f2 = new File("text.exe");
        System.out.println("f2的绝对路径：" + f2.getAbsolutePath());
        // 把f1作为父目录创建文件对象
        File f3 = new File(f1, "text.exe");
        System.out.println("f3的绝对路径：" + f3.getAbsolutePath());
	}
}
```
<!--more-->
运行结果如下：

![img-创建File对象](/images/img-创建File对象.png)



## 常用方法

### 访问文件名相关的方法

- String getName()：返回此File对象所表示的文件名或路径名（如果是路径，则返回最后一级子路径名）。

- String getPath()：返回此File对象所对应的路径名。

- File getAbsoluteFile()：返回此File对象的绝对路径。

- String getAbsolutePath()：返回此File对象所对应的绝对路径名。

- String getParent()：返回此File对象所对应目录（最后一级子目录）的父目录名。

- boolean ranameTo(File newName)：重命名此File对象所对应的文件或目录。

### 文件检测相关的方法

- boolean exists()：判断File对象所对应的文件或目录是否存在。
- boolean canWrite()：判断File对象所对应的文件或目录是否可写。
- boolean canRead()：判断File对象所对应的文件或目录是否可读。
- boolean isFile()：判断File对象所对应的是文件，而不是目录。
- boolean isDirectory()：判断File对象所对应的是否是目录，而不是文件。

## 获取常规文件信息

- long lastModified()：返回文件的最后修改时间。
- long length()：返回文件内容的长度。
- boolean setLastModified(long time)：设置文件或目录的最后修改时间。 


## 文件操作相关的方法

- boolean creatNewFile()：当此FIle对象所对应的文件不存在时，该方法将新建一个该File对象所指定的新文件。
- boolean delete()：删除File对象所对应的文件或路径。

##目录操作相关的方法

- boolean mkdir()：创建一个File对象所对应的目录。
- boolean mkdirs()：创建此抽象路径名指定的目录，包括所有必需但不存在的父目录。
- String[] list()：列出File对象的所有子文件名和路径名，返回String数组。
- File[] listFiles()：列出File对象的所有子文件名和路径名，返回File数组。
- static File[] listRoot()：列出系统所有根路径。