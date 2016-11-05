# learning-spring

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




