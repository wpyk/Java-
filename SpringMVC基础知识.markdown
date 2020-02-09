# SpringMVC的基础知识  
## 什么是SpringMVC

![](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTuynSCP1QbZghxyjfRSX0kFszLhwmjwU6_elMFvq8Gn79HEhtK)

Springmvc是Spring的一个模块，Springmvc和spring是无需通过中间整合层进行整合的。  
Springmvc是基于mvc的web框架。  
servlet接到用户的请求，并返回响应。最初最早的框架中，搜索结果是静态的，即在servlet中寻找用户的请求并通过建立与用户间的io链接将这个结果返回。由于网页的请求和响应都是html的格式的，servlet需要自己去拼接字段，行程一个完整的html网页。这样的模式非常的不方便。后续进化出了jsp，其本身是一个servlet，实现html的拼接这样的一个过程，但是依然不优雅简洁。继续进化出现了ssh（Struts， spring 和 Hibernate），其存在的问题是Hibernate操作非常不便捷，後被ssm替代。

## mvc在b/s系统下的应用
mvc是一个设计模式，mvc在b/s系统下的应用
![](http://i.imgur.com/AvGipIU.jpg)

controller不对具体的业务进行处理，委托给m进行处理。然后m处理完后返回给c，c将结果进行视图渲染，放在request域中。

## Springmvc 框架
![](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcR8MYqeYT7wAUbrsz21f4ej-rXV_rxtcAEYhI163jEuJRdd5GoZ)

第一步： 发起请求到前端控制器（DispatcherServlet）。  
第二步： 前端控制器请求handlerMapping查找handler。可以根据xml配置、注解进行查找。  
第三步： 处理器映射器HandlerMapping向前端控制器返回handler。返回的执行链中可能有多个拦截器。  
第四部： 前端控制器调用处理器适配器去执行handler。  
第五步： 处理器适配器执行handler。  
第六步： handler执行完给适配器返回ModelAndView。  
第七步： 处理器适配器向前端控制器返回ModelAndView，是springmvc框架的一个底层对象，包括Model和View。  
第八步：前端控制器请求视图解析器进行试图解析，根据逻辑视图名来解析成真正的视图（jsp）
第九步： 视图解析器向前端控制器返回View。  
第十步： 前端控制器进行视图渲染。视图渲染将模型数据（在ModelAndView中）填充到request域。  
第十一步： 前端控制器对用户请求进行响应。  

重要组件：

1、前端控制器：接收请求，响应结果。相当于一个转发器，中央处理器。程序员不需要写这一部分，是架构里自带的，但是自己设计架构的时候可以参照。有了dispatch而servlet，减少其他组件之间的耦合度。controller中没有业务逻辑。  
2、处理器映射器 HandlerMapping： 根据请求的url查找handler。（不需要程序员开发）  
3、处理器适配器HandlerAdapter：执行handler，按照特定的规则（HandlerAdapter要求的规则）执行。 注意：在开发handler时要按照HandlerAdapter的要求去做，这样适配器才能正确执行handler。   
4、 **处理器Handler**：（需要程序员开发）按照adapter的要求去进行编写。   
5、视图解析器：进行视图解析，根据逻辑视图名解析成真正的视图（在springmvc当中就是view）。  
6、**视图view**：是一个接口。其实现类是用来支持不同的view类型，比如freemarker，jsp，pdf etc。（需要程序员开发jsp）



## SpringMVC 框架原理
### 前端控制器、处理器映射器、处理器适配器、视图解析器
## Springmvc 入门程序：对前端控制器、处理器映射器、处理器适配器、视图解析器进行理解
### 非注解的处理器映射器、处理器适配器
### 注解的处理器映射器、处理器适配器（掌握）
## Springmvc和mybatis整合应用
## Springmvc注解开发：
### 常用的注解学习
### 参数绑定（简单、pojo、集合类型）
### 自定义参数绑定（掌握）
## Springmvc和struts2区别

# Springmvc的高级应用
## 参数绑定（集合类型）
## 参数回显
## 上传图片
## json数据交互
## RESTful支持
## 拦截器
