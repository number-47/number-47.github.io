---
title: Tomcat
tags: Tomcat
categories: Java_Web
date: 2017-11-27 00:00:00
---
## Tomcat

  Tomcat服务器是一种Servlet/JSP容器，负责处理客户请求，把请求传送给Servlet并把结果返回给客户。

当用户访问某个Servlet时，Servlet容器将创建一个ServletRequest对象和ServletResponse对象。在ServletRequest对象中封装了客户请求信息，然后Servlet容器（Tomcat）把ServletRequest对象和ServletResponse对象传给客户所请求的Servlet。Servlet把响应结果写到ServletResponse中，然后由Servlet容器（Tomcat）把响应结果传给客户。<!--more-->

![Alt text](/images/img-Servlet容器响应客户请求过程.png)

## 修改端口

安装目录为D:\Tomcat

打开D:\Tomcat\conf\server.xml，修改8080端口

```
 <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```
## 运行多个服务
如果需要让Tomcat运行多个服务，只需要复制server.xml文件中的<Service>元素，并修改相应的参数，便可以实现一个Tomcat运行多个服务。
## Tomcat的结构
每个Tomcat组件在server.xml文件中对应一种配置元素。以下为Tomcat组件之间的关系。
```
<Server>                             //顶层类元素，可以包括多个Service   
    <Service>                        //顶层类元素，可包含一个Engine，多个Connecter
        <Connector>                  //连接器类元素，代表通信接口
                <Engine>             //容器类元素，为特定的Service组件处理客户请求，要包含多个Host
                        <Host>       //容器类元素，为特定的虚拟主机组件处理客户请求，可包含多个Context
                          <Context>  //容器类元素，为特定的Web应用处理所有的客户请求
                          </Context>
                        </Host>
                </Engine>
        </Connector>
    </Service>
</Server>
```

- `<Server>`元素

`<Server>`元素代表整个Servlet容器，是Tomcat实例的顶层元素。`<Server>`元素中包含一个或多个`<Server>`元素。

- `<Service>`元素

 `<Service>`元素包含一个`<Engine>`元素，以及一个或多个`<Connector>`元素，这些`<Connector>`元素共享同一个\<Engine>元素

- `<Connector>`元素

  `<Connector>`元素代表和客户程序实际交互的组件，它负责接收客户请求，以及向客户返回响应结果。

- `<Engine>`元素

  每个`<Service>`元素只能包含`<Engine>`元素。`<Engine>`元素处理在同一个`<Service>`中所有`<Connector>`元素接收到的客户请求。

- `<Host>`元素

  一个`<Engine>`元素可以包含多个`<Host>`元素。每个`<Host>`元素定义了一个虚拟主机，它可以包含一个或多个Web应用。

- `<Context>`元素

  `<Context>`元素是使用最频繁的元素，每个`<Context>`元素代表了运行在虚拟主机上的单个Web应用。一个`<Host>`元素中可以包含多个`<Context>`元素。

  ## 进入控制台

  Server Status控制台：监控服务器状态

  Manager App控制台：部署、监控Web应用

  Host Manager控制台

  ### 增加控制台用户

  打开D:\Tomcat\conf\tomcat-users.xml文件

  在`<tomcat-users>`元素中增加用户

  ```
  <tomcat-users>
  	<role rolename="tomcat"/>
  	<!--增加一个用户-->
  	<user username='admin' password = '123456' roles = 'manager-gui'/>
  </tomcat-users>
  ```

  ## 部署Web应用

  ### 方式一：利用Tomact的自动部署

  只要将一个Web应用复制到Tomcat的webapps下，系统就会把应用部署到Tomcat中。

  ### 方式二：利用控制台部署

  进入控制台，按照下图输入即可

  ！![img-Tomcat控制台部署web应用](/images/img-Tomcat控制台部署web应用.png)

  将会在Tomcat的webapps目录多了一个名为tmall_ssh的文件夹，文件内容和D:\JAVA\workspace\路径tmall_ssh文件夹内容一样

## Tomcat各个组件之间的嵌套关系

![img_Tomcat各个组件之间的关系](/images/img-Tomcat各个组件之间的关系.png)

## Tomcat Server处理一个HTTP请求的过程

![img_Tomcat Server处理一个HTTP请求的过程](/images/img-Tomcat Server处理一个HTTP请求的过程.png)

1. 用户点击网页内容，请求被发送到本机端口8080，被在那里监听的Coyote HTTP/1.1 Connector获得。 
2. Connector把该请求交给它所在的Service的Engine来处理，并等待Engine的回应。 
3. Engine获得请求localhost/index.jsp，匹配所有的虚拟主机Host。 
4. Engine匹配到名为localhost的Host（即使匹配不到也把请求交给该Host处理，因为该Host被定义为该Engine的默认主机），名为localhost的Host获得请求/index.jsp，匹配它所拥有的所有的Context。Host匹配到路径为/test的Context（如果匹配不到就把该请求交给路径名为“ ”的Context去处理）。 
5. path=“/”的Context获得请求/index.jsp，在它的mapping table中寻找出对应的Servlet。Context匹配到URL PATTERN为*.jsp的Servlet,对应于JspServlet类。 
6. 构造HttpServletRequest对象和HttpServletResponse对象，作为参数调用JspServlet的doGet（）或doPost（）.执行业务逻辑、数据存储等程序。 
7. Context把执行完之后的HttpServletResponse对象返回给Host。 
8. Host把HttpServletResponse对象返回给Engine。 
9. Engine把HttpServletResponse对象返回Connector。 
10. Connector把HttpServletResponse对象返回给客户Browser。