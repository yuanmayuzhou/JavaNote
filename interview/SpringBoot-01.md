# SpringBoot面试题01
## 1.什么是 Spring Boot？

多年来，随着新功能的增加，spring变得越来越复杂。 只需访问https://spring.io/projects页面，我们就会看到可以在我们的应用程序中使用的所有 Spring 项目的不同功能。 如果必须启动一个新的Spring项目，我们必须添加构建路径或添加Maven依赖
关系，配置应用程序服务器，添加spring配置 。因此，开始一个新的 spring 项目需要很多努力，因为我们现在必须从头开始
做所有事情。

Spring Boot 是解决这个问题的方法 。Spring Boot 已经建立在现有spring框架之上 。使用spring启动，我们避免了之前我们必须做的所有样板代码和配置 。因此，Spring Boot 可以帮助我们以最少的工作量，更加健壮地使用现有的Spring功能 

## 2.为什么要用SpringBoot

Spring Boot 优点非常多，如：

**一、独立运行**

Spring Boot而且内嵌了各种servlet容器，Tomcat、Jetty等，现在不再需要打成war包部署到容器中，Spring Boot只要打成一个可执行的
jar包就能独立运行，所有的依赖包都在一个jar包内。

**二、简化配置**

spring-boot-starter-web启动器自动依赖其他组件，简少了maven的配置。

**三、自动配置**

Spring Boot能根据当前类路径下的类、jar包来自动配置bean，如添加一个spring-boot-starter-web启动器就能拥有web的功能，无需其他
配置。

**四、无代码生成和XML配置**

Spring Boot配置过程中无代码生成，也无需XML配置文件就能完成所有配置工作，这一切都是借助于条件注解完成的，这也是Spring4.x的
核心功能之一。

**五、应用监控**

Spring Boot提供一系列端点可以监控服务及应用，做健康检测 

## 3.Spring Boot 有哪些优点？

**Spring Boot 的优点有：**

1、减少开发，测试时间和努力。

2、使用 JavaConfig 有助于避免使用 XML。 3、避免大量的 Maven 导入和各种版本冲突。

4、提供意见发展方法。

5、通过提供默认值快速开始开发。

6、没有单独的 Web 服务器需要。这意味着你不再需要启动 Tomcat，Glassfish或其他任何东西。

7、需要更少的配置 因为没有 web.xml 文件。只需添加用@ Configuration 注释的类，然后添加用@Bean 注释的方法，Spring 将自动加载
对象并像以前一样对其进行管理。您甚至可以将@Autowired 添加到 bean 方法中，以使 Spring 自动装入需要的依赖关系中。

8、基于环境的配置 使用这些属性，您可以将您正在使用的环境传递到应用程序：-Dspring.profiles.active = {enviornment}。在加载主应
用程序属性文件后，Spring 将在（application{environment} .properties）中加载后续的应用程序属性文件。 

## 4.Spring Boot 的核心注解是哪个？它主要由哪几个注解组成的？

启动类上面的注解是@SpringBootApplication，它也是 Spring Boot 的核心注解，主要组合包含了以下

**3个注解：**

`@SpringBootConfiguration`：组合了 @Configuration 注解，实现配置文件的功能。

`@EnableAutoConfiguration`：打开自动配置的功能，也可以关闭某个自动配置的选项，如关闭数据源自动配置功能：

`@SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })`。

`@ComponentScan`：Spring组件扫描 

## 5.运行Spring Boot有哪几种方式

1）打包用命令或者放到容器中运行

2）用 Maven/Gradle 插件运行

3）直接执行 main 方法运行