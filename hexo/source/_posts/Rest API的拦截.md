---
title: Rest API的拦截
tags: Rest
categories: 
copyright: true
comment: true
---
# Rest API的拦截

## 拦截顺序

filter->Interceptor->Aspect

## 异常捕获顺序

Aspect->ControllerAdvice->Inteceptor->filter

![](https://ws1.sinaimg.cn/large/a8a26f7cgy1g64bpl7z8qj20dt0cb761.jpg)

## 过滤器（Filter）

可以获取到原始http请求和响应的信息，但是取不到处理方法的信息

### 自定义Filter spring boot添加@Component

```java
package com.number47.com.number47.filter;

import org.springframework.stereotype.Component;

import javax.servlet.*;
import java.io.IOException;
import java.util.Date;

/**
 * @author number47
 * @date 2019/8/18 23:44
 * @description Rest API filter
 */
@Component
public class TimeFilter implements Filter {

	@Override
	public void init(FilterConfig filterConfig) throws ServletException {
		System.out.println("time filter init");
	}

	@Override
	public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
		System.out.println("time filter start");
		long start = new Date().getTime();
		filterChain.doFilter(servletRequest,servletResponse);
		System.out.println("time filter：" + (new Date().getTime()-start));
		System.out.println("time filter finish");
	}

	@Override
	public void destroy() {
		System.out.println("time filter destroy");
	}
}

```

### 加入第三方Filter spring boot

```
package com.number47.com.number47.config;

import com.number47.com.number47.filter.TimeFilter;
import org.springframework.boot.web.servlet.FilterRegistrationBean;
import org.springframework.context.annotation.Bean;

import java.util.ArrayList;
import java.util.List;

/**
 * @author number47
 * @date 2019/8/18 23:53
 * @description
 */
@Configuration
public class WebConfig {
   
   @Bean
   public FilterRegistrationBean timeFilter(){
      FilterRegistrationBean registrationBean = new FilterRegistrationBean();
      TimeFilter timeFilter = new TimeFilter();
      registrationBean.setFilter(timeFilter);
      List<String> urls = new ArrayList<>();
      urls.add("/*");
      registrationBean.setUrlPatterns(urls);
      return registrationBean;
   }
}
```

# 拦截器(Interceptor)

可以获取到原始http请求和响应的信息，可以获取处理方法的信息，但是获取不到参数的值

```java
package com.number47.com.number47.interceptor;

import org.springframework.stereotype.Component;
import org.springframework.web.method.HandlerMethod;
import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.util.Date;

/**
 * @author number47
 * @date 2019/8/19 00:01
 * @description
 */
@Component
public class TimeInterceptor implements HandlerInterceptor {
   /**
    * controller 之前调用
    * @param httpServletRequest
    * @param httpServletResponse
    * @param handle
    * @return
    * @throws Exception
    */
   @Override
   public boolean preHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object handle) throws Exception {
      System.out.println("preHandle");
      System.out.println(((HandlerMethod)handle).getBean().getClass().getName());
      System.out.println(((HandlerMethod)handle).getMethod().getName());
      httpServletRequest.setAttribute("startTime",new Date().getTime());
      return true;
   }

   /**
    * controller 方法处理之后调用，如果controller抛出异常，这个方法不会调用
    * @param httpServletRequest
    * @param httpServletResponse
    * @param o
    * @param modelAndView
    * @throws Exception
    */
   @Override
   public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {
      System.out.println("postHandle");
      Long start = (Long)httpServletRequest.getAttribute("startTime");
      System.out.println("time interceptor 耗时：" + (new Date().getTime() - start));
   }

   /**
    * controller 无论是正常还是抛出异常都会调用
    * @param httpServletRequest
    * @param httpServletResponse
    * @param o
    * @param e
    * @throws Exception
    */
   @Override
   public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {
      System.out.println("afterCompletion");
      Long start = (Long)httpServletRequest.getAttribute("startTime");
      System.out.println("time interceptor 耗时：" + (new Date().getTime() - start));
      System.out.println("exception is " + e);
   }
}
```

```java
package com.number47.com.number47.config;

import com.number47.com.number47.filter.TimeFilter;
import com.number47.com.number47.interceptor.TimeInterceptor;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.web.servlet.FilterRegistrationBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurerAdapter;

import java.util.ArrayList;
import java.util.List;

/**
 * @author number47
 * @date 2019/8/18 23:53
 * @description
 */
@Configuration
public class WebConfig extends WebMvcConfigurerAdapter {

   @Autowired
   private TimeInterceptor timeInterceptor;

   @Override
   public void addInterceptors(InterceptorRegistry registry) {
      registry.addInterceptor(timeInterceptor);
   }

}
```



# 切片(Aspect)

获取不到原始http请求和响应的信息，可以获取参数的值

#### Spring Aop简介

![](https://ws1.sinaimg.cn/large/a8a26f7cgy1g64an6t14gj20pi0c7wik.jpg)

```
package com.number47.aspect;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

import java.util.Date;

/**
 * @author number47
 * @date 2019/8/19 00:29
 * @description
 */
@Aspect
@Component
public class TimeAspect {

	@Before(value = "execution(* com.number47.web.controller.UserController.*(..))")
	public void before(){
		System.out.println("方法调用之前");
	}

	@After(value = "execution(* com.number47.web.controller.UserController.*(..))")
	public void after(){
		System.out.println("方法调用之后");
	}

	@AfterThrowing(value = "execution(* com.number47.web.controller.UserController.*(..))")
	public void afterThrowing(){
		System.out.println("方法异常调用之后");
	}

	@Around(value = "execution(* com.number47.web.controller.UserController.*(..))")
	public Object around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
		System.out.println("time aspect start");
		long start = new Date().getTime();
		Object object = proceedingJoinPoint.proceed();
		Object[] args = proceedingJoinPoint.getArgs();
		for (Object arg: args){
			System.out.println("arg is " + arg);
		}
		System.out.println("time aspect：" + (new Date().getTime()-start));
		System.out.println("包含上面所有情况");
		System.out.println("time aspect end");
		return object;
	}

}

```

