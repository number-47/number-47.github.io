---
title: spring security 学习(一)-spring boot 整合
date: 2019-10-24 12:56:35
tags: Spring Security
categories: Spring Security
copyright: true
comment: true
---
# Spring Security(一)-Spring Boot 整合

## 创建spring boot项目，引入spring-boot-start-security

```java
  <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
  </dependency>
```
## 创建/spring-security的访问接口

```java
@RestController
public class DemoController {
	@GetMapping("spring-security")
	public String hello() {
		return "hello spring security";
	}
}

```
## 表单认证

创建配置类WebSecurityConfig继承`WebSecurityConfigurerAdapter`,`WebSecurityConfigurerAdapter`是由Spring Security提供的Web应用安全配置的适配器。

```java
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http.formLogin() // 表单方式
				.and()
				.authorizeRequests() 
				.anyRequest()  // 所有请求
				.authenticated(); // 都需要认证
	}

}
```

## 设置启动端口

application.properties
```
server.port=8081
```
启动程序，启动时控制台Using generated security password: 9aac6105-0752-4bf1-9f54-c247e94086ab，每次都不一样，这个为用户user的密码。
访问<http://localhost:8080/spring-security>，页面跳转到<http://localhost:8080/login>
![image.png](http://ww1.sinaimg.cn/large/a8a26f7cgy1g7x16jb1ylj20i709tmxe.jpg)
登录后，访问到http://localhost:8080/spring-security

