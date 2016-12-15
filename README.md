# learning-spring

这是一篇笔记，内容来自[spring framework 5.0.0.M2的官方文档](http://docs.spring.io/spring/docs/5.0.0.M2/spring-framework-reference/htmlsingle/)

# 1.简介
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

##Web
这层包含了spring-web,spring-webmvc,spring-websocket模块。

spring-web提供基本的web功能(如multipart文件上传)以及使用Servlet listener 和基于web的应用上下文来初始化IOC 容器。它还包含一个http 客户端，以及Spring remoting support的与web相关的部分。

spring-webmvc包含了对于MVC和REST web service的实现。它用于清晰地分离实际业务代码和前端展示代码，并能与Spring框架地其余部分完美融合。

##Test
利用这个模块，可以通过Junit和TestNG对spring组件进行单元测试和集成测试。它提供对于Spring ApplicationContext的持续载入和缓存。也提供mock object来帮助你独立地测试代码。

# 2.Usage scenarios
Spring的这些特征，使得它有极广的应用领域，从资源受限的嵌入式应用到企业级应用。

下图是完全使用Spring框架的企业级应用的架构。
![](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/images/overview-full.png)
Spring的声明式事务管理功能，使得web 应用完全地“事务化（？）”，类似于EJB容器的事务管理。所有业务逻辑都能使用POJO表达，借助IOC容器管理。
额外的服务支持邮件发送和校验，这些都独立于web层。Spring ORM可以帮助开发者轻松集成JPA或Hibernate。例如，当使用Hibernate时，你依然可以保持原来的映射文件和标准的Hibernate配置。Form Controller实现将web层和业务逻辑的无缝衔接，移除了类似于ActionForm这类东西，不需要显示将Http参数传回到业务端。
 
 下图展示了Spring中间层与第三方web框架的结合使用。
 ![](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/images/overview-thirdparty-web.png)
 当需要和已在使用中的web框架结合时，Spring也能表现优秀，它完全支持你只使用其中部分模块。现有的前端框架都能与之集成，并使用其事务特征。你仅仅需要使用ApplicationContext来组装业务逻辑，并使用WebApplicationContext来与web层集成。
 
 下图展示了在远端调用已有代码的场景。
 ![](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/images/overview-remoting.png)
 你可以使用Spring的Hessian，Rmi，HttpInvokerProxyFactoryBean 等类型轻松搭建web service。
 
 下图：EJBs - Wrapping existing POJOs（i have no idea）
 ![](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/images/overview-ejb.png)
 Spring框架也提供一种用于 Enterprise JavaBeans 的access and abstraction layer，可以使你重用已有的POJO，并将之包含于无状态的bean中，实现可扩展的，能容错的，需要declarative security的web 应用。

##依赖管理和命名惯例
依赖管理包括定位资源，保存资源，并将之加入到classpath。

依赖分为direct和inderect。inderect就是那些transitive的库，它们才是管理的难点。推荐使用成熟的依赖管理工具来使用spring的类库。

spring库的命名一般是spring-module-version.

##日志记录
spring框架中的所有模块都通过Jakarta Commons Logging API (JCL)来使用日志。JCL是一种公用接口，可与很多日志库结合，这很好地维持了向后兼容性。

spring内置了JCL的官方实现---commons-logging.它声称能够自动发现可用日志库。但这个功能很鸡肋，所以总需要用其它更好的日志库。

因此，就遇到一个“老的不去，新的不来”的问题。你需要把commons-logging从原来的依赖路径中移除，然后再导入新的日志库依赖。

spring和log4j的结合非常方便，就和在其它项目中使用log4j一样，推荐使用。

spring 应用常常运行在某个应用容器中，而应用容器本身也提供了JCL的实现。这就会导致一些冲突。

# 3.核心技术

spring的核心包括IOC,AOP。

## ioc容器

###简介
what is ioc？一个对象描述自己的依赖，而容器通过注入依赖来构造对象。所谓依赖也就是类的属性，构造函数的参数，或者工厂方法的参数。
注入依赖，所以ioc又称DI。而原本应当由使用者控制对象的构造，现在由容器代而为之。故又称ioc。

核心库：org.springframework.beans ， org.springframework.context

核心类：
1.BeanFactory提供对框架配置和基本功能。
2.ApplicationContext扩展BeanFactory，加入了简单的AOP。
3.更特殊的，与应用类型相关的，有WebApplicationContext。

what is bean？bean就是对象，是那些已经构造好的，组装完成的，或者是由容器管理的对象。
Beans以及它们的依赖，都能在配置信息元数据中找到。

###什么是容器
接口org.springframework.context.ApplicationContext代表的是IOC容器，并由它负责实例化，配置，组装beans。

容器需要获取信息，来指示它该如何操作众多beans。这些信息被称为配置元数据，以多种形式存在，如XML，java注解，java code。你用它们来组装你的应用，表示各个对象间的依赖。

ApplicationContext的常用实现 : [ClassPathXmlApplicationContext](http://docs.spring.io/spring-framework/docs/5.0.0.M3/javadoc-api/org/springframework/context/support/ClassPathXmlApplicationContext.html) ,[ FileSystemXmlApplicationContext](http://docs.spring.io/spring-framework/docs/5.0.0.M3/javadoc-api/org/springframework/context/support/FileSystemXmlApplicationContext.html)

为了实例化容器，编写代码不是必须的。例如[ Section 3.15.4, “Convenient ApplicationContext instantiation for web applications”](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/#context-create)。或是使用[Spring Tool Suite](https://spring.io/tools/sts)

**Spring IOC Container**
![IOC Container](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/images/container-magic.png)

###配置容器

元数据的形式可以是：
1.xml
2.[Annotation-based configuration](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/#beans-annotation-config)
3.[Java-based configuration](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/#beans-java)

容器要管理什么？那就是**bean**。
xml中用<beans>来包含<bean>,注解中用@Configuration来包含@Bean。

**那么beans常常是哪些对象呢？应用中的所有对象都是bean吗？**
想一想，容器是帮助你构建应用的，也就说，它作用于应用启动时，将一些基础对象关联。
如果某些对象是运行时，才能生成的，那当然就无法由容器来管理。
所以由容器来管理的对象应当是构成业务逻辑的框架型对象，可能是DAO，服务层对象，Struts Action这种表示层对象，Hibernate SeesionFactories这种基础架构对象，JMS Queues。它们的共同点是能在程序运行前就知道它们的生成时机。
而更细粒度的领域对象，比如从由数据库读取信息后构造的对象，则不是由容器管理。尽管如此，结合AspectJ，你还是能在容器外配置这些对象。


>&lt;?xml version="1.0" encoding="UTF-8"?>
&lt;beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">
>    
    &lt;bean id="..." class="...">
        &lt;!-- collaborators and configuration for this bean go here -->
    &lt;/bean>
    &lt;bean id="..." class="...">
        &lt;!-- collaborators and configuration for this bean go here -->
    &lt;/bean>
    &lt;!-- more bean definitions go here -->
>    
&lt;/beans>

<bean>标签的具体含义，见[dependencies](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/#beans-dependencies)

有了这样的xml文件之后,就可以构造容器了.容器可以加载多个xml.通常，一个XML就代表一个模块。
>ApplicationContext context =
     new ClassPathXmlApplicationContext(new String[] {"services.xml", "daos.xml"});

###使用容器
使用ApplicationContext的`T getBean(String name, Class<T> requiredType)`获取bean。
**然而，你压根就别想用这个方法。最最正确的使用方式就是，别再你的代码里显示地控制这些bean，把它们交给容器吧！**
举个栗子，web框架和spring结合，仅仅是通过ioc容器来管理controller和JSF-managed beans。

###bean概观
让我们从配置bean的细节，来一步步了解bean。
一个bean不外乎包括以下几方面：
1.全称限定类名：它将是哪个类的对象
2.说明它在容器中的行为：生命周期，作用域，回调
3.依赖：引用其它bean
4.对象初始化所需参数：例如一个线程池的初始大小

####bean的标识
bean可以有多个标识，也可以没有标识（[inner beans](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/#beans-inner-beans) ，[autowiring collaborators](http://docs.spring.io/spring/docs/5.0.0.M3/spring-framework-reference/htmlsingle/#beans-factory-autowire)）。

###bean的构造方式
bean可以通过构造函数或者工厂方法进行构造.

##依赖
一个完整的应用由多个对象构成，它们之间存在着各种依赖关系。Spring能够管理beans间的依赖关系，从而描述一个完整的应用。

###DI
有两种注入方式，它们也可以结合使用。
1.Constructor-based
 Spring推荐的方式，因为它将应用组件实现为immutable object，并且用户得到的对象是构造完全的（不包含空属性）。
 同时，构造函数可以作为一种重构提醒，如果它包含过多参数，则表明其责任太多，需要进行关注点分离。
 
2.setter-based DI
主要用于非必需的属性的设置，这些属性可以有默认值，避免了代码中随地的非空检查。
另一个好处是，使用setter的对象更利于重新配置或注入。JMX Mbeans说明了这一点。

###依赖注入过程
1.ApplicationContext加载配置元数据。
2.bean的依赖在创造bean时被构造。
3.每个bean的构造函数参数要么是直接的值，要么是对某个bean的引用。
4.如果构造函数参数是直接的值，它可以进行一定形式的类型转化。

需要某个bean，才构造它。所以参数不匹配的错误可能会在配置完成后才发生。
但是，单例模式下的bean会在容器初始化时就构造。
一个bean的构造常常会引发一系列bean的构造。

####循环依赖
如果只使用构造函数，bean配置中很可能出现循环依赖的问题。这时候，只能把有问题的依赖，使用setter来配置。

###depends-on
虽然已经有property和construct-arg来表示bean的依赖，但是它们只表示bean需要设置某些属性。有些时候，比如一个类的静态初始化方法，需要在它被使用前，就初始化某些bean。
这时就该使用depends-on，来表明这种先后顺序。

###自动组装
配置中的各个bean的依赖类型，名称都已明了，反射机制也能提供bean的构造函数信息，spring当然可以将这些bean自动组装起来，而无须用户声明bean的具体依赖。
当然，这是最理想的情况，考虑到可能出现的歧义，自动组装的过程也需要用户参与。用户可以指明某个bean将参与自动组装，或是禁止某个bean参与自动组装。

###Method Injection(lookup method injection)
用于不同scope的beans间的交互，例如某个bean只需构建一次，而它的某个方法，每调用一次就创建另一个bean。
为了解决这个问题，spring通过动态代码生成提供了对bean中方法的注入。

####我的总结
所谓注入(DI),IOC(控制反转),就是把原本需要由用户完成的事情交给容器。用户可以控制对象构造，方法调用，而今，容器也能控制这些事情。

##bean的作用域（scope）
bean的定义，实际上只是一个配方，用来说明该怎么实例化一个特定对象。
默认情况下，scope=singleton，即每个容器只许实例化一个对象。

