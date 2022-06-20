# Spring面试题01
## 1.什么是 Spring Framework？

Spring 是一个开源应用框架，旨在降低应用程序开发的复杂度。它是轻量级、松散耦合的。它具有分层体系结构，允许用户选择组件，同
时还为 J2EE 应用程序开发提供了一个有凝聚力的框架。它可以集成其他框架，如 Structs、Hibernate、EJB 等，所以又称为框架的框架。 

## 2.列举 Spring Framework 的优点。

由于 Spring Frameworks 的分层架构，用户可以自由选择自己需要的组件。Spring Framework 支持 POJO(Plain Old Java Object) 编程，
从而具备持续集成和可测试性。由于依赖注入和控制反转，JDBC 得以简化。它是开源免费的。 

## 3.Spring Framework 有哪些不同的功能？

轻量级 - Spring 在代码量和透明度方面都很轻便。IOC - 控制反转 AOP - 面向切面编程可以将应用业务逻辑和系统服务分离，以实现高内
聚。容器 - Spring 负责创建和管理对象（Bean）的生命周期和配置。MVC - 对 web 应用提供了高度可配置性，其他框架的集成也十分方
便。事务管理 - 提供了用于事务管理的通用抽象层。Spring 的事务支持也可用于容器较少的环境。JDBC 异常 - Spring的 JDBC 抽象层提供
了一个异常层次结构，简化了错误处理策略。 

## 4.Spring Framework 中有多少个模块，它们分别是什么？

**Spring 核心容器 – 该层基本上是 Spring Framework 的核心。它包含以下模块：**

Spring Core

Spring Bean

SpEL (Spring Expression Language)

Spring Context

**数据访问/集成 – 该层提供与数据库交互的支持。它包含以下模块：**

JDBC (Java DataBase Connectivity)

ORM (Object Relational Mapping)

OXM (Object XML Mappers) 

JMS (Java Messaging Service)

Transaction

**Web – 该层提供了创建 Web 应用程序的支持。它包含以下模块：**

Web

Web – Servlet

Web – Socket

Web – Portlet

**AOP**

该层支持面向切面编程

**Instrumentation**

该层为类检测和类加载器实现提供支持。

**Test**

该层为使用 JUnit 和 TestNG 进行测试提供支持。

**几个杂项模块:** 

Messaging – 该模块为 STOMP 提供支持。它还支持注解编程模型，该模型用于从 WebSocket 客户端路由和处理 STOMP 消息。Aspects –
该模块为与 AspectJ 的集成提供支持。 

## 5.什么是 Spring 配置文件？

Spring 配置文件是 XML 文件。该文件主要包含类信息。它描述了这些类是如何配置以及相互引入的。但是，XML 配置文件冗长且更加干
净。如果没有正确规划和编写，那么在大项目中管理变得非常困难 

## 6.什么是 Spring IOC 容器？

Spring 框架的核心是 Spring 容器。容器创建对象，将它们装配在一起，配置它们并管理它们的完整生命周期。Spring 容器使用依赖注入来
管理组成应用程序的组件。容器通过读取提供的配置元数据来接收对象进行实例化，配置和组装的指令。该元数据可以通过 XML，Java 注
解或 Java 代码提供。

## 7.什么是依赖注入？

在依赖注入中，您不必创建对象，但必须描述如何创建它们。您不是直接在代码中将组件和服务连接在一起，而是描述配置文件中哪些组件
需要哪些服务。由 IoC容器将它们装配在一起。

## 8.列举 IoC 的一些好处。
IoC 的一些好处是：

## 9.spring 提供了哪些配置方式？
**基于 xml 配置**

bean 所需的依赖项和服务在 XML 格式的配置文件中指定。这些配置文件通常包含许多 bean 定义和特定于应用程序的配置选项。它们通常
以 bean 标签开头。例如： 
```java
<bean id="studentbean"class="org.edureka.firstSpring.StudentBean">
    <property name="name"value="Edureka"></property>
</bean>
```

**基于注解配置**

您可以通过在相关的类，方法或字段声明上使用注解，将 bean 配置为组件类本身，而不是使用 XML 来描述 bean 装配。默认情况下，
Spring 容器中未打开注解装配。因此，您需要在使用它之前在 Spring 配置文件中启用它。

例如：

```java
<beans>
    <context:annotation-config/>
    <!-- bean definitions go here -->
</beans>
```

**基于 Java API 配置**

Spring 的 Java 配置是通过使用 @Bean 和 @Configuration 来实现。

1、 @Bean 注解扮演与 元素相同的角色。

2、 @Configuration 类允许通过简单地调用同一个类中的其他 @Bean 方法来定义 bean 间依赖关系。 

例如：

```java
@Configuration
public class StudentConfig {
    @Bean
    public StudentBean myStudent() {
        return new StudentBean();
    }
}
```

## 10.spring 支持集中 bean scope？

Spring bean 支持 5 种 scope：

Singleton - 每个 Spring IoC 容器仅有一个单实例。Prototype - 每次请求都会产生一个新的实例。Request - 每一次 HTTP 请求都会产生一
个新的实例，并且该 bean 仅在当前 HTTP 请求内有效。Session - 每一次 HTTP 请求都会产生一个新的 bean，同时该 bean 仅在当前
HTTP session 内有效。Global-session - 类似于标准的 HTTP Session 作用域，不过它仅仅在基于portlet 的 web 应用中才有意义。Portlet
规范定义了全局 Session 的概念。

它被所有构成某个 portlet web 应用的各种不同的 portlet 所共享。在 globalsession 作用域中定义的 bean 被限定于全局 portlet Session
的生命周期范围内。如果你在 web 中使用 global session 作用域来标识 bean，那么 web会自动当成 session 类型来使用。
仅当用户使用支持 Web 的 ApplicationContext 时，最后三个才可用。 

## 11.spring bean 容器的生命周期是什么样的？

spring bean 容器的生命周期流程如下：

1、Spring 容器根据配置中的 bean 定义中实例化 bean。 

2、Spring 使用依赖注入填充所有属性，如 bean 中所定义的配置。

3、如果 bean 实现BeanNameAware 接口，则工厂通过传递 bean 的 ID 来调用setBeanName()。 

4、如果 bean 实现 BeanFactoryAware 接口，工厂通过传递自身的实例来调用 setBeanFactory()。 5、如果存在与 bean 关联的任何BeanPostProcessors，则调用 preProcessBeforeInitialization() 方法。

6、如果为 bean 指定了 init 方法（ 的 init-method 属性），那么将调用它。

7、最后，如果存在与 bean 关联的任何 BeanPostProcessors，则将调用 postProcessAfterInitialization() 方法。

8、如果 bean 实现DisposableBean 接口，当 spring 容器关闭时，会调用 destory()。 

9、如果为bean 指定了 destroy 方法（ 的 destroy-method 属性），那么将调用它。

## 12.什么是 spring 的内部 bean？

只有将 bean 用作另一个 bean 的属性时，才能将 bean 声明为内部 bean。为了定义 bean，Spring 的基于 XML 的配置元数据在 或 中提
供了元素的使用。内部 bean 总是匿名的，它们总是作为原型。

例如，假设我们有一个 Student 类，其中引用了 Person 类。这里我们将只创建一个 Person 类实例并在 Student 中使用它。

Student.java

```java
public class Student {
    private Person person;
}

public class Person {
    private String name;
    private String address;
}
```

bean.xml

```java
<bean id="StudentBean" class="com.edureka.Student">
    <property name="person"> <!--This is inner bean -->
        <bean class="com.edureka.Person">
            <property name="name" value="Scott"></property>
            <property name="address" value="Bangalore"></property>
        </bean>
    </property>
</bean>
```

