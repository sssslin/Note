# 					Servlet详解

在我准备了解spring mvc的时候,不可避免的要了解一个叫DispatcherServlet的类,从名字就可以看出,它是一个Servlet.那么问题来了,什么是Servlet?

首先看看,Servlet规范是怎么说的,规范内容如下:

(规范)A servlet is  java technology-based Web component,managed by a container, that generates dynamic content.

翻译:Servlet(Server Applet)是基于Java的一个web组件,被容器托管,用于生成动态内容的组件.

如果说,官方的定义说的太抽象的话,接下来去看看JDK源码的注释是怎么介绍Servlet的.

```java
A servlet is a small Java program that runs within a Web server. Servlets receive and respond to requests from Web clients, usually across HTTP, the HyperText Transfer Protocol.
```

Servlet就是一个运行在web服务器上的一小段Java代码,Servlet容器一般通过HTTP协议从客户端接收一个请求并且根据请求,做出相应.



在源码中可以看到,Servlet是一个接口,那么也就是说,所有实现Servlet的类都必须要有类似的生命周期

init()--->service()--->destory();