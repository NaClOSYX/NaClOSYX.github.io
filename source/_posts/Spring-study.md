---
title: Spring 学习笔记
date: '2020-07-08 00:00:00 +0800'
updated: '2020-07-08 00:00:00 +0800'
categories:
  - 博客
  - 后端
tags:
  - 学习
  - 后端
  - java
  - Spring
author: NaClO
abbrlink: 941381954
---

## 1. Spring概述

* 百度百科
  * Spring框架是一个==开源==的J2EE应用程序==框架==，是针对bean的生命周期进行管理的==轻量级容器==。 
  * Spring解决了开发者在J2EE开发中遇到的许多常见的问题，提供了功能强大==IOC==、==AOP==及==Web MVC==等功能。
  * Spring可以单独应用于构筑应用程序，也可以和Struts、Webwork、Tapestry等众多Web框架组合使用，并且可以与 Swing等桌面应用程序AP组合。
  * Spring框架主要由七部分组成，分别是 Spring Core、 Spring AOP、 Spring ORM、 Spring DAO、Spring Context、 Spring Web和 Spring Web MVC。
* 官网https://spring.io/
* 英文文档https://docs.spring.io/spring/docs/5.2.7.RELEASE/spring-framework-reference/
* API文档https://docs.spring.io/spring/docs/5.2.7.RELEASE/javadoc-api/
* 组成
  * ==Spring Core==：核心容器提供 Spring 框架的基本功能。核心容器的主要组件是 BeanFactory，它是工厂模式的实现。BeanFactory 使用控制反转 模式将应用程序的配置和依赖性规范与实际的应用程序代码分开。
  * ==Spring Context==：Spring 上下文是一个配置文件，向 Spring框架提供上下文信息。Spring 上下文包括企业服务，例如JNDI、EJB、电子邮件、国际化、校验和调度功能。
  * ==Spring AOP==：通过配置管理特性，Spring AOP 模块直接将面向切面的编程功能集成到了 Spring 框架中。所以，可以很容易地使 Spring 框架管理的任何对象支持AOP。Spring AOP 模块为基于 Spring 的应用程序中的对象提供了事务管理服务。通过使用 Spring AOP，不用依赖 EJB 组件，就可以将声明性事务管理集成到应用程序中。
  * ==Spring DAO==：JDBCDAO抽象层提供了有意义的异常层次结构，可用该结构来管理异常处理和不同数据库供应商抛出的错误消息。异常层次结构简化了错误处理，并且极大地降低了需要编写的异常代码数量（例如打开和关闭连接）。Spring DAO 的面向 JDBC 的异常遵从通用的 DAO 异常层次结构。
  * ==Spring ORM==：负责框架中对象关系映射，提供相关ORM 接入框架的关系对象管理工具 。Spring 框架插入了若干个ORM框架，从而提供了 ORM 的对象关系工具，其中包括JDO、Hibernate和iBatisSQL Map。所有这些都遵从 Spring 的通用事务和 DAO 异常层次结构。
  * ==Spring Web== ：Web 上下文模块建立在应用程序上下文模块之上，为基于 Web 的应用程序提供了上下文。所以，Spring框架支持与 Jakarta Struts 的集成。Web 模块还简化了处理多部分请求以及将请求参数绑定到域对象的工作。
  * ==Spring MVC== ：MVC框架是一个全功能的构建 Web应用程序的 MVC 实现。通过策略接口，MVC框架变成为高度可配置的，MVC 容纳了大量视图技术，其中包括 JSP、Velocity、Tiles、iText 和 POI。模型由javabean构成，存放于Map；视图是一个接口，负责显示模型；控制器表示逻辑代码，是Controller的实现。Spring框架的功能可以用在任何J2EE服务器中，大多数功能也适用于不受管理的环境。Spring 的核心要点是：支持不绑定到特定 J2EE服务的可重用业务和数据访问对象。毫无疑问，这样的对象可以在不同J2EE 环境、独立应用程序、测试环境之间重用。
* ss

## 2. 第一个程序HelloSpring

1. 新建maven项目

2. 引入pom依赖

   ````xml
   <dependency>
       <groupId>org.springframework</groupId>
       <artifactId>spring-webmvc</artifactId>
       <version>5.2.7.RELEASE</version>
   </dependency>
   ````

3. 编写实体类

   ````java
   public class Student {
       String name;
       //getter-setter，全参无参构造
   }
   ````

4. 编写配置文件

   ````xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
   http://www.springframework.org/schema/beans/spring-beans.xsd">
       <!-- 使用bean元素定义一个由容器创建的对象-->
   	<!-- class属性指定用于创建bean的全类名-->
   	<!-- id属性指定用于引用bean实例的名称-->
       <bean id="student" class="com.naclo.pojo.Student">
           <!-- 使用property子元素为bean的属性赋值-->
           <property name="name" value="NaClO"/>
       </bean>
   </beans>
   ````

5. 编写测试类

   ````java
   @Test
   public void test() {
       //创建容器对象
       ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
       //根据配置的id获取bean对象实例
       Student student = (Student)context.getBean("student");
       System.out.println("student = " + student);
   }
   ````

   输出：`student = Student(name=NaClO)`

## 3. bean

### 1. bean标签

* 用于创建对象

  ````xml
  <bean id="" class="" scope="">
  
  </bean>
  ````

  * id：对象名；
  * class：类的全类名；
  * scope：对象的作用域
    * singleton：单例对象；
    * prototype：多例对象；
    * request：创建对象并放入request中；
    * session：创建对象并放入session中；

### 2. 实例化Bean的方式

1. 使用默认无参构造函数

   * 默认情况下调用无参构造函数创建对象，如果没有无参构造函数，会创建失败

     ````xml
     <bean id="initStudent" class="com.naclo.pojo.Student">
     </bean>
     ````

2. 使用静态工厂的方法创建对象

   * 模拟一个静态工厂

     ````java
     public class StaticFactory {
         public static Student createStudent() {
             return new Student();
         }
     }
     ````

   * 使用静态工厂创建对象

     ````xml
     <bean id="staticStudent" class="com.naclo.factory.StaticFactory" 
           factory-method="createStudent">
     </bean>
     ````

     * class：静态工厂的全类名；
     * factory-method：创建对象的静态方法；

3. 使用实例工厂的方法创建对象

   * 模拟一个实例工厂

     ````java
     public class InstanceFactory {
         public Student createStudent() {
             return new Student();
         }
     }
     ````

   * 使用实例工厂创建对象

     ````xml
     <!-- 先创建工厂实例，再调用方法创建对象 -->
     <bean id="instanceFactory" class="com.naclo.factory.InstanceFactory"></bean>
     <bean id="instanceStudent" factory-bean="instanceFactory" 
           factory-method="createStudent">
     </bean>
     ````

     * factory-bean：实例工厂的id；
     * factory-method：创建对象的方法；

### 3. 依赖注入==DI==

#### 无参构造函数，使用set注入

````xml
<bean id="student" class="com.naclo.pojo.Student">
    <property name="name" value="NaClO"/>
</bean>
````

* name：属性名；
* value：给属性赋值，值为基本数据类型；
* ref：给属性赋值，值为其他bean类型；

#### 有参构造函数，使用构造函数注入

````xml
<bean id="student" class="com.naclo.pojo.Student">
    <constructor-arg value="NaClO"/>
</bean>
````

* 使用`constructor-arg`指定参数赋值
  * 自动匹配合适的参数位置

    ````xml
    <constructor-arg value="NaClO"/>
    ````

  * 通过参数名字指定参数位置

    ````xml
    <constructor-arg name="name" value="NaClO"/>
    ````

  * 通过索引值指定参数位置

    ````xml
    <constructor-arg index="0" value="NaClO"/>
    ````

  * 通过类型指定参数位置

    ````xml
    <constructor-arg type="java.lang.String" value="NaClO"/>
    ````

#### 集合属性注入

* 当参数变量是集合类型的时候注入。

  * 创建一个实体对象

    ````java
    public class CollectionTest {
        String[] array;
        List<String> list;
        Set<String> set;
        Map<String, String> map;
        Properties properties;
        //getter-setter，全参无参构造
    }
    ````

  * 实例化对象

    ````xml
    <bean id="collectionTest" class="com.naclo.pojo.CollectionTest">
        <!-- array -->
        <property name="array">
            <array>
                <value>A</value>
                <value>B</value>
                <value>C</value>
            </array>
        </property>
        <!-- list -->
        <property name="list">
            <list>
                <value>A</value>
                <value>B</value>
                <value>C</value>
            </list>
        </property>
        <!-- set -->
        <property name="set">
            <set>
                <value>A</value>
                <value>B</value>
                <value>C</value>
            </set>
        </property>
        <!-- map -->
        <property name="map">
            <map>
                <entry key="A" value="A" />
                <entry key="b" value="b" />
                <entry key="C" value="C" />
            </map>
        </property>
        <!-- properties -->
        <property name="properties">
            <props>
                <prop key="A">A</prop>
                <prop key="B">B</prop>
                <prop key="C">C</prop>
            </props>
        </property>
    </bean>
    ````

#### 其他注入方式

* P命名空间注入

  * 格式：`p:属性名="属性值"`或``p:属性名-ref="id"``

  * 导入约束

    ````xml
    xmlns:p="http://www.springframework.org/schema/p"
    ````

  * 例子

    ````xml
    <bean id="student" class="com.naclo.pojo.Student" p:name="NaClO"/>
    ````

* c 命名空间注入

  * 格式：`c:属性名="属性值"`或`c:属性名-ref="id"`

  * 导入约束

    ````xml
    xmlns:c="http://www.springframework.org/schema/c"
    ````

  * 例子

    ````xml
    <bean id="student" class="com.naclo.pojo.Student" c:name="NaClO"/>
    ````

### 4. 引入外部配置文件

1. 编写外部配置文件xxx..properties放在resources目录下

   ````properties
   name=NaClO
   ````

2. 引入context 名称空间

   ````xml
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
               http://www.springframework.org/schema/beans/spring-beans.xsd
               http://www.springframework.org/schema/context
               https://www.springframework.org/schema/context/spring-context.xsd">
   ````

3. 指定配置文件位置

   ````xml
   <context:property-placeholder location="classpath:student.properties"/>
   ````

4. 读取配置文件

   ````xml
   <bean id="student" class="com.naclo.pojo.Student">
       <property name="name" value="${name}"/>
   </bean>
   ````

### 5. 自动装配

1. 概念
   * 手动装配
     * 以value 或ref 的方式明确指定属性值
   * 自动装配
     * 根据指定的装配规则，不需要明确指定，Spring 自动将匹配的属性值注入
       bean 中。
   
2. 装配方式

   1. 根据类型自动装配：将类型匹配的bean 作为属性注入到另一个bean 中。若IOC 容器中
      有多个与目标bean 类型一致的bean，Spring 将无法判定哪个bean 最合适该属性，所
      以不能执行自动装配
   2. 根据名称自动装配：必须将目标bean 的名称和属性名设置的完全相同

3. 测试

   1. 创建两个实体类A和B

      ````java
      public class A {
      }
      ````

      ````java
      public class B {
      }
      ````

   2. 创建实体类C，属性为A,B

      ```java
      public class C {
          A a;
          B b;
      }
      ```

   3. 配置A和B

      ```xml
      <bean id="a" class="com.naclo.pojo.A"/>
      <bean id="b" class="com.naclo.pojo.B"/>
      ```

   4. 根据类型自动装配

      ````xml
      <bean id="c" class="com.naclo.pojo.C" autowire="byType"/>
      ````

   5. 根据名称自动装配

      ````xml
      <bean id="c" class="com.naclo.pojo.C" autowire="byName"/>
      ````

### 6. 使用注解注入

   #### 1. 开启注解

1. 在配置文件中引入context文件头

   ````xml
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
               http://www.springframework.org/schema/beans/spring-beans.xsd
               http://www.springframework.org/schema/context
               https://www.springframework.org/schema/context/spring-context.xsd">
   ````

2. 开启属性注解支持

   ````xml
   <context:annotation-config/>
   ````

#### 2. @Autowired

* 按类型自动装配，不支持按id匹配；

  ````java
  public class C {
      @Autowired
      A a;
      @Autowired
      B b;
  }
  ````

* `@Autowired(required=false)`
  * false：对象可以为null；
  * true：对象不能为null；

#### 3. @Qualifier

* @Autowired是根据类型自动装配的，加上@Qualifier则可以根据byName的方式自动装配；

* @Qualifier不能单独使用；

  ````java
  public class C {
      @Autowired
      @Qualifier(value = "a")
      A a;
      @Autowired
      @Qualifier(value = "b")
      B b;
  }
  ````

#### 4. @Resource

  * 先进行byName查找，再进行byType查找；

  * 如果允许对象为null，设置required = false,默认为true

    ````
    public class C {
        @Resource(name = "a")
        A a;
        @Resource
        B b;
    }
    ````

### 7. 其他

 #### 1. 别名alias

* 为bean设置别名，可以使用别名获取bean

  ````XML
  <alias name="student" alias="NaClO"/>
  ````

#### 2. 导入

* 可以导入外部的bean，实现分文件编写，方便团队合作

  ````xml
  <import resource="classpath:beans.xml"/>
  ````


## 4. 注解

### 1. 配置

1. 引入AOP包

   ````xml
   <dependency>
       <groupId>org.springframework</groupId>
       <artifactId>spring-aop</artifactId>
       <version>5.2.7.RELEASE</version>
   </dependency>
   ````

2. 在配置文件中引入context约束

   ````xml
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
               http://www.springframework.org/schema/beans/spring-beans.xsd
               http://www.springframework.org/schema/context
               https://www.springframework.org/schema/context/spring-context.xsd">
   </beans>
   ````

### 2. Bean

* 使用注解对bean进行注入

1. 配置扫描包

   ````xml
   <context:component-scan base-package="com.naclo"/>
   ````

2. 编写bean

   ````java
   @Component("student")
   public class Student {
       String name;
   }
   ````

   * 这里的`@Component("student")`相当于xml中的`<bean id="student" class="..."/>`

3. 编写测试类

   ````java
   @Test
   public void test() {
       ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
       Student student = (Student)context.getBean("student");
       System.out.println("student = " + student);
   }
   ````

   结果：`student = Student(name=null)`

### 3. 属性注入

1. 不用set方法，直接在属性上方添加`@value("...")`

   ````java
   @Component("student")
   public class Student {
       @Value("NaClO")
       String name;
   }
   ````

   * 这里的`@Value("NaClO")`相当于xml中的`<property name="name" value="NaClO"/>`

2. 使用set方法，直接在属性上方添加`@value("...")`

   ````java
   @Component("student")
   public class Student {
       String name;
   
       @Value("NaClO")
       public void setName(String name) {
           this.name = name;
       }
   }
   ````

### 4. 衍生注解

* `@Componen`有三个衍生注解，分别作用在持久层，业务层和控制层
* 这几个注解的功能是一模一样的，仅仅是为了区分所对应的组件功能不同。
  1. `@Repository`：作用在持久层；
  2. `@Service`：作用在业务层；
  3. `@Controller`：作用在控制层；

### 5. 作用域

* `@Scope`：作用域注解，相当于`<bean id="" class="" scope="">`
  * singleton：单例对象；
  * prototype：多例对象；
  * request：创建对象并放入request中；
  * session：创建对象并放入session中；

### 6. 配置注解

* `@Configuration`：用于指定当前类是一个spring配置类，beans.xml文件。

  ````java
  @Configuration
  public class SpringConfiguration {
  }
  ````

* `@Import`：用于导入其他配置类，相当于`<import resource="classpath:beans.xml"/>`

  * 参数为需要导入的其他配置文件类

  ````java
  @Configuration
  @Import(JdbcConfig.class)
  public class SpringConfiguration {
  }
  ````

* `@ComponentScan`：配置扫描包，相当于`<context:component-scan base-package="com.naclo"/>`

  ````java
  @Configuration
  @ComponentScan("com.naclo")
  public class SpringConfiguration {
  }
  ````

* `@PropertySource`：用于加载.properties文件中的配置。

  ````java
  @Configuration
  @PropertySource("classpath:student.properties")
  public class StudentConfig {
      @Value("${name}")
      private String name;
  }
  ````

* 通过注解获取容器

  ````java
  ApplicationContext context = new AnnotationConfigApplicationContext(SpringConfiguration.class);
  ````

## 5. AOP

### 1. 概述

1. 百度百科
   * 在软件业，AOP为Aspect Oriented Programming的缩写，意为：==面向切面编程==，通过预编译方式和运行期间动态代理实现程序功能的统一维护的一种技术。
   * AOP是OOP的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。
   * 利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

### 2. 环境搭建

* 导入aspectjweaver

  ````xml
  <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
      <version>1.9.5</version>
  </dependency>
  ````

### 3. 基于xml的AOP

1. 编写测试文件

   AOP.java

   ````java
   public class AOP {
       public void test(){
           System.out.println("test");
       }
   }
   ````

   Before.java

   ````java
   public class Before{
       public void beforeAOP(){
           System.out.println("beforeAOP");
       }
   }
   ````

   After.java

   ````java
   public class After{
       public void afterAOP() {
           System.out.println("afterAOP");
       }
   }
   ````

   Around.java

   ````
   public class Around {
       public void aroundAOP() {
           System.out.println("aroundAOP");
       }
   }
   ````

2. 注册bean

   ````xml
   <bean id="aop" class="com.naclo.AOP"/>
   <bean id="before" class="com.naclo.Before"/>
   <bean id="after" class="com.naclo.After"/>
   <bean id="around" class="com.naclo.Around"/>
   ````

3. 使用`aop:config`声明aop配置

   ````xml
   <aop:config>
   ....
   </aop:config>
   ````

4. 使用`aop:aspect`配置切面

   ````xml
   <aop:aspect id="" ref="">
   ...
   </aop:aspect>
   ````

   * id：切面的唯一标识；
   * ref：引用配置好的通知类bean的id。

5. 使用`aop:pointcut`配置切入点表达式

   ````xml
   <aop:pointcut id="pointcut" expression="execution(* com.naclo.AOP.*(..))"/>
   ````

   说明:

   * id：切入点的唯一标识；

   * expression：定义切入点表达式：

     * execution(表达式)

       * 语法：`execution([修饰符] 返回值类型 包名.类名.方法名(参数))`

       * 写法：

         * 全匹配：

           ````xml
           public void com.naclo.AOP.test()
           ````

         * 访问修饰符可以省略:

           ````xml
           void com.naclo.AOP.test()
           ````

         * 返回值可以使用*号，表示任意返回值

           ````xml
           * com.naclo.AOP.test()
           ````

         * 包名可以使用*号，表示任意包，但是有几级包，需要写几个

           ````xml
           * *.*.AOP.test()
           ````

         * 使用..来表示当前包，及其子包

           ````xml
           * com..AOP.test()
           ````

         * 类名可以使用*号，表示任意类

           ````xml
           * com..*.test()
           ````

         * 方法名可以使用*号，表示任意方法

           ````xml
           * com..*.*()
           ````

         * 参数列表可以使用*，表示参数可以是任意数据类型，但是必须有参数

           ````xml
           * com..*.*(*)
           ````

         * 参数列表可以使用..表示有无参数均可，有参数可以是任意类型

           ````xml
           * com..*.*(..)
           ````

         * 全通配方式

           ````xml
           * *..*.*(..)
           ````

6. 使用`aop:xxx`配置对应的通知类型

   ````xml
   <aop:xxx method="" pointcut-ref=""/>
   ````

   1. `aop:before`：用于配置前置通知；
   2. `aop:after`：用于配置最终通知；
   3. `aop:after-returning`：用于配置后置通知；
   4. `aop:after-throwing`：用于配置异常通知；
   5. `aop:around`：用于配置环绕通知；

   * 参数说明：

     * method：指定通知中方法的名称；

     * pointct：定义切入点表达式 ；

     * pointcut-ref：指定切入点表达式的引用；

7. ss

### 4. 使用aop:advisor实现AOP

1. 增强类实现Advice接口。

   1. 前置增强需要实现MethodBeforeAdvice，重写before方法

      ````java
      public class Before implements MethodBeforeAdvice {
          public void before(Method method, Object[] args, Object target) throws Throwable {
              System.out.println("before");
          }
      }
      ````

   2. 后置增强需要实现AfterReturningAdvice，重写afterReturning方法

      ````java
      public class After implements AfterReturningAdvice {
          public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
              System.out.println("after");
          }
      }
      ````

2. 配置aop

   ````xml
   <bean id="aop" class="com.naclo.AOP"/>
   <bean id="before" class="com.naclo.Before"/>
   <bean id="after" class="com.naclo.After"/>
   <aop:config>
       <aop:pointcut id="pointcut" expression="execution(* com.naclo.AOP.*(..))"/>
       <aop:advisor advice-ref="before" pointcut-ref="pointcut"/>
       <aop:advisor advice-ref="after" pointcut-ref="pointcut"/>
   </aop:config>
   ````

### 5. 基于注解的AOP

1. 开启spring对注解AOP的支持

   ````xml
   <aop:aspectj-autoproxy/>
   ````

2. 注解说明

   * `@Aspect`：把当前类声明为切面类；
   * `@Pointcut`：指定切入点表达式；
     * value：指定表达式的内容；
   * `@Before`：把当前方法看成是前置通知；
   * `@AfterReturning`：把当前方法看成是后置通知；
   * `AfterThrowing`：把当前方法看成是异常通知；
   * `@After`：把当前方法看成是最终通知；
   * `@Around`：把当前方法看成是环绕通知；
     * value：用于指定切入点表达式，还可以指定切入点表达式的引用；

### 6. 其他

1. 指定切面的优先级

   * 在同一个连接点上应用不止一个切面时，除非明确指定，否则它们的优先级是不确定的。

   * 切面的优先级可以通过实现Ordered 接口或利用@Order 注解指定。

   * 实现Ordered 接口，getOrder()方法的返回值越小，优先级越高。

   * 若使用@Order 注解，序号出现在注解中

     * 注解：

       ````java
       @Aspect
       @Order(1)
       public class Around {
       }
       ````

     * 接口：

       ````java
       public class Around implements Ordered {
           public int getOrder() {
               return 1;
           }
       }
       ````

## 6. JDBCTemplate

### 1. 说明

* 为了使JDBC 更加易于使用，Spring 在JDBC API 上定义了一个抽象层，以此建立一个JDBC
  存取框架。
* 作为Spring JDBC 框架的核心，JDBC 模板的设计目的是为不同类型的JDBC 操作提供模
  板方法，通过这种方式，可以在尽可能保留灵活性的情况下，将数据库存取的工作量降到最
  低。
* 可以将Spring 的JdbcTemplate 看作是一个小型的轻量级持久化层框架，相当于spring帮我们写好的DBUtils。

### 2. 环境配置

1. 导入jar包

   ````xml
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-webmvc</artifactId>
               <version>5.2.7.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-jdbc</artifactId>
               <version>5.2.7.RELEASE</version>
           </dependency>
           <dependency>
               <groupId>mysql</groupId>
               <artifactId>mysql-connector-java</artifactId>
               <version>8.0.20</version>
           </dependency>
           <dependency>
               <groupId>com.mchange</groupId>
               <artifactId>c3p0</artifactId>
               <version>0.9.5.5</version>
           </dependency>
           <dependency>
               <groupId>org.apache.commons</groupId>
               <artifactId>commons-dbcp2</artifactId>
               <version>2.7.0</version>
           </dependency>
   ````

2. 编写数据库配置文件db.properties

   ````properties
   driver=com.mysql.cj.jdbc.Driver
   url=jdbc:mysql://localhost:3306/jdbctemplate?serverTimezone=Asia/Shanghai&useSSL=true&useUnicode=true&characterEncoding=UTF-8
   username=root
   password=root
   ````

3. 引入配置文件

   ````xml
   <context:property-placeholder location="classpath:db.properties"/>
   ````

4. 配置c3p0数据源

   ```xml
   <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
       <property name="user" value="${user}"/>
       <property name="password" value="${password}"/>
       <property name="jdbcUrl" value="${jdbcUrl}"/>
       <property name="driverClass" value="${driverClass}"/>
   </bean>
   ```

5. 配置dbcp数据源

   ````xml
   <bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource">
       <property name="username" value="${user}"/>
       <property name="password" value="${password}"/>
       <property name="url" value="${jdbcUrl}"/>
       <property name="driverClassName" value="${driverClass}"/>
   </bean>
   ````

6. 创建JdbcTemplate 对象

   ````xml
   <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
       <property name="dataSource" ref="dataSource"/>
   </bean>
   ````

7. 获取JdbcTemplate 对象

   ````java
   ApplicationContext context = new ClassPathXmlApplicationContext("bean.xml");
   JdbcTemplate template = (JdbcTemplate) context.getBean("jdbcTemplate");
   ````

8. 创建数据库，并创建表

   ````sql
   create database jdbctemplate;
   create table user(
       id int,
       name varchar(30)
   )
   ````

9. 编写数据库映射对象

   ````java
   public class User {
       int id;
       String name;
   }
   ````

### 3. 操作数据库

1. 执行操作

   * `JdbcTemplate.update(String, Object...)`
   * 参数：（sql语句）

   ````JAVA
   template.execute("insert INTO user VALUES (1,'NaClO')");
   ````

2. 更新操作

   * `JdbcTemplate.update(String, Object...)`
   * （sql语句，参数列表）

   ````java
   template.update("insert INTO test VALUES (?,?)",1,"NaClO");
   template.update("delete from user where id=?",1);
   template.update("update user set name=? where id=?","666",1);
   ````

3. 查询操作

   1. 查询单行

      * `JdbcTemplate.queryForObject(String, RowMapper<Department>, Object...)`

      * 参数：（sql语句，自己编写的RowMapper，参数列表）

        UserRowMapper

        ````java
        public class UserRowMapper implements RowMapper<User> {
            @Override
            public User mapRow(ResultSet rs, int rowNum) throws SQLException {
                User user = new User();
                user.setId(rs.getInt("id"));
                user.setName(rs.getString("name"));
                return user;
            }
        }
        ````

        ````java
        User user = template.queryForObject("select * from user", new UserRowMapper());
        ````

   2. 查询多行

      * `JdbcTemplate.query(String, RowMapper<Department>, Object...)`

      * 参数：（sql语句，自己编写的RowMapper，参数列表）

        ````java
        List<User> userList = template.query("select * from user", new UserRowMapper());
        ````

   3. 查询单一值

      * `JdbcTemplate.queryForObject(String, Class, Object...)`

      * 参数：（sql语句，返回值的类，参数列表）

        ````java
        Integer id = template.queryForObject("select id from user", Integer.class);
        ````

## 7.事务

