# spring框架学习

## spring各jar包作用介绍

### org.springframework.aop或spring-aop.jar

这个文件包含在应用中使用spring的aop特性时所需要的类。涉及切面。

外部依赖

- spring-core.jar
- spring-beans.jar
- cglib-nodep.jar
- aopalliance.jar 

==附==：aopalliance.jar这个包是AOP联盟的API包，里面包含了针对面向切面的接口。通常Spring等其他具备动态植入功能的框架依赖此包。

cglib-nodep.jar这个包是一个code生成类库。它可以在运行期扩展Java类与实现Java接口。当然这些实际的功能是asm所提供的，asm是Java字节码操控框架。cglib就是封装了asm，简化了asm的操作，实现了在运行期动态生成新的class。实际上CGlib为spring aop提供了底层的一种实现；为hibernate使用cglib动态生成VO/PO接口层对象。

### spring-asm.jar

spring独立的asm程序，spring2.5.6的时候需要asm的jar包，3.0开始提供自己独立的asm的jar包。asm是一个java字节码操纵框架。塔可以以二进制形式动态地生成stub类或其他代理类，或在装载时动态的修改类。用于注解。

### spring-beans.jar

这个jar文件是所有应用都用到的，它包含访问配置文件、创建和管理bean以及进行Inversion of Control / Dependency Injection (ioc/di)控制反转/依赖注入操作相关的所有类。如果应用只需要基本的IOC/DI支持，引入spring-core.jar以及spring-beans.jar文件就可以。

外部依赖

- spring-core.jar
- cglib-nodep.jar

### spring-core.jar

包含spring框架基本的核心工具类。spring其他组件都要使用到这个包里面的类，是其他组件的基本核心，当然你可以在自己的应用系统里面使用这些工具类。

外部依赖

- commons-Logging、Log4J

### spring-aop.jar

包含在应用中使用spring的AOP特性时所需要的类和源码级元数据支持。使用基于AOP的spring特性，如声明型事务管理（Declarative Transaction Management），也要在应用中包含这个jar包。

外部依赖

- spring-core.jar
- spring-beans.jar
- aopalliance.jar
- cglib-nodep.jar

### spring-context.jar

为spring核心提供了大量的扩展。可以找到使用Spring ApplicationContext特性时所需要的全部类，JDNI所需要的全部类，instrumentation组件以及校验Validation方面的相关类。

外部依赖

- spring-core.jar
- spring-beans.jar
- spring-aop.jar
- commons-collection.jar
- aopalliance.jar

### spring-dao.jar

包含spring DAO、Spring Transaction进行数据访问的所有类。为了使用声明型事务支持，还需要自己的应用中包含spring-aop.jar。

外部依赖

- spring-core.jar
- spring-aop.jar
- spring-context.jar
- jta.jar 事务API

### spring-jdbc.jar

包含对JDBC数据访问进行封装的所有类

外部依赖

- spring-beans.jar
- spring-dao.jar

### spring-support.jar

包含了支持UI模板（Velocity,FreeMarker,JasperReports），邮件服务，脚本服务（JRuby），缓存Cache（EHCache）,任务计划Scheduling（uartz）方面的类。

外部依赖

- spring-context.jar
- spring-jdbc.jar
- Velocity
- FreeMarker
- JasperReports
- BSH
- Groovy
- JRuby
- Quartz
- EHCache

### spring-web.jar

包含了web应用开发时用到spring框架所需要的核心类，包括自动载入web application context特性的类、struts与JSF集成类、文件上传的支持类、Filter类和大量工具辅助类。

外部依赖

- spring-context
- Servlet API
- JSP API
- JSTL
- Commons FileUpload
- COS

### spring-webmvc.jar

包含spring MVC框架相关的所有类。包括框架的Servlets，Web MVC框架，控制器和视图支持。

外部依赖

- spring-web
- spring-support
- Tiles
- iText
- POI

### spring-portlet.jar

spring自己实现的一个类似spring mvc的框架。包括一个MVC框架和控制器

外部依赖

- spring-web
- Portlet API
- spring-webmvc

### spring-struts.jar

Struts框架支持，可以更方便更容易的集成Struts框架

外部依赖

- spring-web
- Struts

### spring-remoting.jar

包含支持EJB、远程调用Remoting（RMI、Hessian、Http Invoker、JAX-RPC）方面的类。

外部依赖

- spring-aop
- spring-context,spring-web,Hessian,Burlap,JAX-RPC,EJB API

### spring-jmx.jar

提供了对JMX的支持类。

外部依赖

- spring-beans
- spring-aop
- JMX API





## xml配置

### applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:tx="http://www.springframework.org/schema/tx"
	xsi:schemaLocation="http://www.springframework.org/schema/beans 
	http://www.springframework.org/schema/beans/spring-beans.xsd
	http://www.springframework.org/schema/context
	http://www.springframework.org/schema/context/spring-context.xsd
	http://www.springframework.org/schema/aop
	http://www.springframework.org/schema/aop/spring-aop.xsd
	http://www.springframework.org/schema/tx 
	http://www.springframework.org/schema/tx/spring-tx.xsd">
  <!--扫描包下带有注解的文件注册为控件 -->
	<context:component-scan base-package="com">
		<context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
	</context:component-scan>
</beans>
```

**解释**

1. `<?xml version="1.0" encoding="UTF-8"?>`

   声明xml的版本是1.0，传输数据的时候使用UTF-8编码

2. `xmlns`是xml命名空间的意思，标识未使用其他命名空间的所有标签的默认命名空间

3. `xmln:xsi`声明xml Schema实例，声明后就可以使用schemaLocation属性

4. `xsi:context`声明前缀为context的命名空间，组件标签

5. `xmlns:aop`声明前缀为aop的命名空间，切面标签，后面的URL用于标识命名空间的地址不会被解析器用于查找信息。其唯一的作用是富裕命名控件一个唯一的名称。当命名空间被定义在元素的开始标签中时，所有带有相同前缀的子元素都会与同一个命名空间相关联。

6. `xmlns:tx`声明前缀为tx的命名空间，事务标签

7. `xsi:schemaLaction`用于配置命名空间指定的xsd规范文件，这样你在进行具体配置的时候就可以根据这些规范文件给出相应的提示，在启动服务的时候也会根据xsd规范对配置进行校验

### springmvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	   xmlns:context="http://www.springframework.org/schema/context"
	   xmlns:mvc="http://www.springframework.org/schema/mvc"
	   xsi:schemaLocation="http://www.springframework.org/schema/beans
	   http://www.springframework.org/schema/beans/spring-beans-4.3.xsd
	   http://www.springframework.org/schema/context
	   http://www.springframework.org/schema/context/spring-context.xsd
	   http://www.springframework.org/schema/mvc
	   http://www.springframework.org/schema/mvc/spring-mvc.xsd">
 
       <!-- 激活@Required @Autowired,JSR 250'S @PostConstruct @PreDestroy and @Resource等标注 -->
		<context:annotation-config />
		<!-- DispatcherServlet上下文，只搜索@Controller标注的类，不搜索其他标注的类 -->
		<context:component-scan base-package="com">
			<context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
		</context:component-scan> <!--扫描控制器所在包-->
		<!-- 让DispatcherServlet启用基于annotation的HandlerMapping -->
		<mvc:annotation-driven />
	<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" >
		<property name="viewClass" value="org.springframework.web.servlet.view.JstlView" />
		<property name="prefix" value="/WEB-INF/jsps/" />	<!-- 前缀 -->
		<property name="suffix" value=".jsp" />		<!-- 后缀 -->
	</bean>
</beans>
```

