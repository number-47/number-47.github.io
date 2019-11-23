title: 导入import com.sun.rowset.CachedRowSetImpl，报错
type: categories
tags:
  - JAVA Web问题
categories:
  - Java
copyright: true
date: 2018-01-10 12:56:00
---

## 报错内容
Access restriction: The type CachedRowSetImpl is not accessible due to restriction on required library C:\glassfish3\jdk7\jre\lib\rt.jar
## 解决方法
项目右键project build path中先移除JRE System Library，再添加库JRE System Library，之后就可以了。