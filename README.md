# learning-spring

这是一篇笔记，内容来自[spring framework 5.0.0.M2的官方文档](http://docs.spring.io/spring/docs/5.0.0.M2/spring-framework-reference/htmlsingle/)

# 简介
spring可以帮助你仅仅通过POJO来构建软件，它来负责框架搭建，各对象间的依赖，而你仅仅需要描述每个对象的职责。

spring包含一整套的软件构建工具，同时也是高度模块化的，你可以只选择你所需要的功能。

spring是为了帮助程序员更好地应用设计模式，并且不需要程序员在代码中重新实现这些模式。

# spring module
![spring module](http://docs.spring.io/spring/docs/5.0.0.M2/spring-framework-reference/htmlsingle/images/spring-overview.png "来自http://docs.spring.io/spring/docs/5.0.0.M2/spring-framework-reference/")

## core-container
core和beans构成了spring的最基础的部分,包括IOC和DI。BeanFactory实现了工厂模式，无需程序员自己实现单例模式，并且实现了对配置和依赖说明的解耦。

Context构建在Core and Beans之上：它类似于JNDI registry，用于登记和访问对象。它延续了Beans的特征，在此之上，还支持了国际化，事件分发, 资源加载, 某些容器上下文的无痕创建.同时也支持了某些JAVA EE的特征。ApplicationContext是它的核心。spring-context-support提供了对集成常见第三方库的支持。

spring-expression使得程序员可以在运行时查询和操控对象。有点类似于反射。他在JSP2.1的unified expression language (unified EL) 加以扩展。

##AOP and instrumentation
spring-aop支持aop编程，它允许程序员定义拦截器和切入点（pointcut）来方便地实现功能代码的解耦。同时，与.NET相似的一点，它可以使用元数据（例如，注解）来向已有代码中附加功能。

spring-aspects是为了支持与AspectJ的结合。

spring-instrument提供类级别的注入和一些能够用于特定应用服务器的classloader。spring-instrument-tomcat包含了对Tomcat的注入代理（instrumentation agent）。

##Messaging
从spring framework 4开始引进spring-messaging以及一些源自于*Spring Integration project*的关键元素（如Message,MessageChannel,MessageHandler）。由此来提供对基于消息的应用的支持。这个模块与Spring MVC一样，提供了注解来实现消息和方法的映射。

##Data Access/Integration
它包含了JDBC, ORM, OXM, JMS, and Transaction。

spring-jdbc提供了对JDBC的封装抽象，不必再有繁琐的编码，也不用再理会那些各种不同数据库的错误码。

spring-tx支持程序化(programmatic)和声明式(declarative)的事务管理，用于那些实现特殊接口的类型，或是POJO。

spring-orm支持与流行的对象-关系映射框架的集成，例如JPA，Hibernate。在使用O/R映射的同时，还能获得其余spring模块所给予的便利。

spring-oxm提供一种抽象，用于支持那些具体实现了对象-XML映射的框架，如JAXB,Castor,Jibx,XStream.

spring-jms包含对消息的处理（产生和消费）。自Spring Framework 4.1始，它还提供与spring-message的集成。



