---
title: Servlet
tags: Servlet
categories: Java_Web
date: 2018-1-7 00:00:00
---

## doGet()
当浏览器使用get方式提交数据的时候，servlet需要提供doGet()方法。
**哪些是get方式呢？**
- form默认的提交方式
- 如果通过一个超链访问某个地址
- 如果在地址栏直接输入某个地址
- ajax指定使用get方式的时候
## doPost()
当浏览器使用post方式提交数据的时候，servlet需要提供doPost()方法
**哪些是post方式呢？**
- 在form上显示设置 method="post"的时候
- ajax指定post方式的时候
## service()
在执行doGet()或者doPost()之前，都会先执行service()。
由service()方法进行判断，到底该调用doGet()还是doPost()。
可以发现，service(), doGet(), doPost() 三种方式的参数列表都是一样的。
所以，有时候也会直接重写service()方法，在其中提供相应的服务，就不用区分到底是get还是post了。

## 生命周期

一个Servlet的生命周期由 实例化，初始化，提供服务，销毁，被回收几个步骤组成。

## request
request对象的类是HttpServletRequest，提供了很多有实用价值的方法。
### request常见方法
request.getRequestURL(): 浏览器发出请求时的完整URL，包括协议 主机名 端口(如果有)" 
request.getRequestURI(): 浏览器发出请求的资源名部分，去掉了协议和主机名" + 
request.getQueryString(): 请求行中的参数部分，只能显示以get方式发出的参数，post方式的看不到
request.getRemoteAddr(): 浏览器所处于的客户机的IP地址
request.getRemoteHost(): 浏览器所处于的客户机的主机名
request.getRemotePort(): 浏览器所处于的客户机使用的网络端口
request.getLocalAddr(): 服务器的IP地址
request.getLocalName(): 服务器的主机名
request.getMethod(): 得到客户机请求方式一般是GET或者POST。

### 获取参数

request.getParameter(): 是常见的方法，用于获取单值的参数
request.getParameterValues(): 用于获取具有多值得参数，比如注册的时候提交的爱好，可以使多选的。
request.getParameterMap(): 用于遍历所有的参数，并返回Map类型。

### 获取头信息

request.getHeader() 获取浏览器传递过来的头信息。 
比如getHeader("user-agent") 可以获取浏览器的基本资料，这样就能判断是firefox、IE、chrome、或者是safari浏览器
request.getHeaderNames() 获取浏览器所有的头信息名称，根据头信息名称就能遍历出所有的头信息。
## response

response是HttpServletResponse的实例，用于提供给浏览器的响应信息。

### 设置响应内容

response.getWriter()

通过response.getWriter(); 获取一个PrintWriter 对象。
可以使用println(),append(),write(),format()等等方法设置返回给浏览器的html内容。

