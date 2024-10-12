---
title: SpringBoot 学习笔记
date: '2020-08-01 00:00:00 +0800'
updated: '2020-08-01 00:00:00 +0800'
categories:
  - 博客
  - 后端
tags:
  - 学习
  - 后端
  - java
  - Spring
author: NaClO
abbrlink: 374670429
---

## SpringBoot基础

### 修改banner

在线制作网站：https://www.bootschool.net/ascii/

生成banner.txt并放在resources目录下

````


                        _ooOoo_
                       o8888888o
                       88" . "88
                       (| ^_^ |)
                       O\  =  /O
                    ____/`---'\____
                  .'  \\|     |//  `.
                 /  \\|||  :  |||//  \
                /  _||||| -:- |||||-  \
                |   | \\\  -  /// |   |
                | \_|  ''\---/''  |   |
                \  .-\__  `-`  ___/-. /
              ___`. .'  /--.--\  `. . ___
            ."" '<  `.___\_<|>_/___.'  >'"".
          | | :  `- \`.;`\ _ /`;.`/ - ` : | |
          \  \ `-.   \_ __\ /__ _/   .-` /  /
    ========`-.____`-.___\_____/___.-`____.-'========
                         `=---='
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    ^        佛祖保佑       永不宕机       永无BUG      ^
    ^        SpringBoot: ${spring-boot.version}              ^
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
````



## SpringBoot整合thymeleaf

### 搭建thymeleaf环境并跑起来

1. 添加maven依赖

   ````xml
   <!--thymeleaf依赖-->
   <!-- thymeleaf-spring5 -->
   <dependency>
       <groupId>org.thymeleaf</groupId>
       <artifactId>thymeleaf-spring5</artifactId>
       <version>3.0.11.RELEASE</version>
   </dependency>
   <!-- thymeleaf-extras-java8time -->
   <dependency>
       <groupId>org.thymeleaf.extras</groupId>
       <artifactId>thymeleaf-extras-java8time</artifactId>
       <version>3.0.4.RELEASE</version>
   </dependency>
   ````

2. 在html中添加

   ````html
   <html xmlns:th="http://www.thymeleaf.org">
   ````

3. 创建controller

   ````java
   @Controller
   public class HelloController {
       @RequestMapping({"/", "/index", "/index.html"})
       public String toIndex(Model model) {
           model.addAttribute("msg", "hello,springboot");
           return "index";
       }
   }
   ````

4. 创建主页index.html

   ````html
   <!DOCTYPE html>
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   </head>
   <body>
   <h1>这是主页</h1>
   <p th:text="${msg}"></p>
   </body>
   </html>
   ````

5. 运行


## SpringBoot整合mybatis

### 搭建环境并测试成功

1. 创建数据库并添加数据

   ````sq
   DROP TABLE IF EXISTS user;
   CREATE TABLE user  (
     id int(10) PRIMARY KEY,
     username varchar(255),
     password varchar(255),
     role varchar(255),
   ) ;
   
   INSERT INTO user VALUES (1, 'naclo', '123456', 'admin');
   INSERT INTO user VALUES (2, 'root', 'root', 'admin');
   INSERT INTO user VALUES (3, 'admin', 'admin', 'admin');
   INSERT INTO user VALUES (4, 'guest', 'guest', 'guest');
   INSERT INTO user VALUES (5, '张三', '123456', 'user');
   INSERT INTO user VALUES (6, '李四', '123456', 'user');
   ````

2. 添加maven依赖

   ```xml
   <!-- mybatis依赖 -->
   <!-- mysql-connector-java -->
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
       <version>8.0.19</version>
   </dependency>
   <!-- mybatis-spring-boot-starter -->
   <dependency>
       <groupId>org.mybatis.spring.boot</groupId>
       <artifactId>mybatis-spring-boot-starter</artifactId>
       <version>2.1.2</version>
   </dependency>
   <!-- lombok -->
   <dependency>
       <groupId>org.projectlombok</groupId>
       <artifactId>lombok</artifactId>
       <version>1.18.12</version>
   </dependency>
   ```

3. 在application.yml里添加

   ````yaml
   mybatis:
     type-aliases-package: com.naclo.pojo
     mapper-locations: classpath:mapper/*.xml
   spring:
     datasource:
       username: root
       password: root
       url: jdbc:mysql://localhost:3306/springbootstudy?useSSL=true&useUnicode=true&characterEncoding=UTF-8&serverTimezone=UTC
   ````

4. 在pom.xml里添加

   ````xml
   <build>
       <!-- 如果不添加此节点mybatis的mapper.xml文件都会被漏掉。 -->
       <resources>
           <resource>
               <directory>src/main/java</directory>
               <includes>
                   <include>**/*.yml</include>
                   <include>**/*.properties</include>
                   <include>**/*.xml</include>
               </includes>
               <filtering>false</filtering>
           </resource>
           <resource>
               <directory>src/main/resources</directory>
               <includes>
                   <include>**/*.yml</include>
                   <include>**/*.properties</include>
                   <include>**/*.xml</include>
                   <include>**/*.html</include>
                   <include>**/*.css</include>
                   <include>**/*.js</include>
                   <include>**/*.txt</include>
               </includes>
               <filtering>false</filtering>
           </resource>
       </resources>
   </build>
   ````

5. 编写实体类

   ````java
   @Data
   @AllArgsConstructor
   @NoArgsConstructor
   public class User {
       private int id;
       private String username;
       private String password;
       private String role;
   }
   ````

6. 编写mapper接口

   ```java
   @Repository
   @Mapper
   public interface UserMapper {
       public List<User> queryAllUser();
   }
   ```

7. 编写mapper

   ````xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.naclo.mapper.UserMapper">
       <select id="queryAllUser" resultType="User">
           select *
           from user
       </select>
   </mapper>
   ````

8. 编写测试类

   ````java
   @SpringBootTest
   public class UserMapperTest {
       @Autowired
       UserMapper userMapper;
   
       @Test
       public void queryAllUserTest() {
           userMapper.queryAllUser().forEach(System.out::println);
       }
   }
   ````

   

9. 



## SpringBoot整合druid

### 添加maven依赖

````xml
<!-- druid -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.22</version>
</dependency>
````

修改application添加数据源

````yaml

````

创建DruidConfig

````java
@Configuration
public class DruidConfig {

    @ConfigurationProperties(prefix = "spring.datasource")
    @Bean
    public DataSource druidDataSource() {
        return new DruidDataSource();
    }

    //配置 Druid 监控管理后台的 Servlet；
    @Bean
    public ServletRegistrationBean<StatViewServlet> statViewServlet() {
        ServletRegistrationBean<StatViewServlet> bean = new ServletRegistrationBean<StatViewServlet>(new StatViewServlet(), "/druid/*");

        //后台需要有人登陆，账号密码配置
        Map<String, String> initParams = new HashMap<>();
        initParams.put("loginUsername", "admin"); //后台管理界面的登录账号
        initParams.put("loginPassword", "123456"); //后台管理界面的登录密码

        //后台允许谁可以访问
        initParams.put("allow", "");

        //设置初始化参数
        bean.setInitParameters(initParams);
        return bean;
    }

    //配置 Druid 监控管理后台的 filter
    @Bean
    public FilterRegistrationBean<WebStatFilter> webStatFilter() {
        FilterRegistrationBean<WebStatFilter> bean = new FilterRegistrationBean<WebStatFilter>();
        bean.setFilter(new WebStatFilter());

        //exclusions：设置哪些请求进行过滤排除掉，从而不进行统计
        Map<String, String> initParams = new HashMap<>();
        initParams.put("exclusions", "*.js,*.css,/druid/*");
        bean.setInitParameters(initParams);

        //"/*" 表示过滤所有请求
        bean.setUrlPatterns(Arrays.asList("/*"));
        return bean;
    }
}
````




## SpringBoot整合shiro

### 添加maven依赖

````java
<!-- shiro-spring -->
<dependency>
    <groupId>org.apache.shiro</groupId>
    <artifactId>shiro-spring</artifactId>
    <version>1.5.2</version>
</dependency>
````

### 编写UserService，查询用户名

### 创建UserRealm

````java
//自定义Realm
public class UserRealm extends AuthorizingRealm {
    @Autowired
    UserService userService;
    //授权
    @Override
    protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principals) {
        System.out.println("执行了=>授权doGetAuthorizationInfo");
        SimpleAuthorizationInfo info = new SimpleAuthorizationInfo();

        Subject subject = SecurityUtils.getSubject();
        User currentUser = (User) subject.getPrincipal();

        //设置角色
        Set<String> roleSet = new HashSet<>();
        roleSet.add(currentUser.getRole());
        info.setRoles(roleSet);

        //设置权限
        //info.setStringPermissions();

        return info;
    }

    //认证
    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
        System.out.println("执行了=>认证doGetAuthenticationInfo");

        UsernamePasswordToken userToken = (UsernamePasswordToken) token;
        User user = userService.queryUserByName(userToken.getUsername());

        if(user==null){
            return null;
        }

        return new SimpleAuthenticationInfo(user,user.getPassword(),"");
    }
}

````

### 创建ShiroConfig

```java
@Configuration
public class ShiroConfig {

    @Bean
    public ShiroFilterFactoryBean getsShiroFilterFactoryBean(@Qualifier("securityManager") DefaultWebSecurityManager defaultWebSecurityManager) {
        ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
        //设置安全管理器
        bean.setSecurityManager(defaultWebSecurityManager);

        //添加shiro的内置过滤器
        Map<String, String> filterMap = new LinkedHashMap<>();

        //权限拦截
        //filterMap.put("/user/add","perms[]");
        //拦截
        //filterMap.put("/user/*", "authc");
        //角色拦截
        filterMap.put("/user/*", "roles[user]");
        filterMap.put("/admin/*", "roles[admin]");
        filterMap.put("/guest/*", "roles[guest]");


        //拦截登出请求
        filterMap.put("/logout", "logout");

        //开放登陆接口
        filterMap.put("/login", "anon");
        filterMap.put("/toLogin", "anon");
        filterMap.put("/", "anon");
        filterMap.put("/index", "anon");
        //其余接口一律拦截,必须放在所有权限设置的最后，不然会导致所有 url 都被拦截
        filterMap.put("/**", "authc");
        bean.setFilterChainDefinitionMap(filterMap);

        //设置登陆的请求
        bean.setLoginUrl("/toLogin");
        bean.setUnauthorizedUrl("/noauth");

        return bean;
    }

    @Bean(name = "securityManager")
    public DefaultWebSecurityManager getDefaultWebSecurityManager(@Qualifier("userRealm") UserRealm userRealm) {
        DefaultWebSecurityManager securityManager = new DefaultWebSecurityManager();
        //关联Realm
        securityManager.setRealm(userRealm);
        return securityManager;
    }

    @Bean
    public UserRealm userRealm() {
        return new UserRealm();
    }

    @Bean
    public ShiroDialect getShiroDialect(){
        return new ShiroDialect();
    }
}
```

常用拦截器

| **Filter**   | 解释                       |
| ------------ | -------------------------- |
| anon         | 无需认证                   |
| auathc       | 需要认证                   |
| logout       | 登出                       |
| user         | 需要记住我才有用           |
| perms[user]  | 需要某个或某些权限才能通过 |
| roles[admin] | 是某个或某些角色才能通过   |

创建controller跳转

````java
@Controller
public class HelloController {
    @RequestMapping({"/", "/index"})
    public String toIndex(Model model) {
        model.addAttribute("msg", "hello,springboot");
        return "index";
    }

    @RequestMapping("/admin/adminIndex")
    public String toAdminIndex() {
        return "adminIndex";
    }

    @RequestMapping("/guest/guestIndex")
    public String toGuestIndex() {
        return "guestIndex";
    }

    @RequestMapping("user/userIndex")
    public String toUserIndex() {
        return "userIndex";
    }
    @RequestMapping("toLogin")
    public String toLogin() {
        return "login";
    }

    @RequestMapping("/login")
    public String login(String username, String password, Model model) {
        //获取当前用户
        Subject subject = SecurityUtils.getSubject();
        //封装用户的登陆数据
        UsernamePasswordToken token = new UsernamePasswordToken(username, password);

        try {
            subject.login(token);//执行登陆方法
            return "guest/guestIndex";
            return "index";
        } catch (UnknownAccountException e) {
            //用户名不存在
            model.addAttribute("msg", "用户名错误");
            return "login";
        } catch (IncorrectCredentialsException e) {
            //密码错误
            model.addAttribute("msg", "密码错误");
            return "login";
        } catch (LockedAccountException e) {
            //用户被锁定
            model.addAttribute("msg", "用户被锁定");
            return "login";
        }
    }

    @RequestMapping("/noauth")
    @ResponseBody
    public String unauthorized(){
        return "未经授权";
    }
}
````

index.html

````html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org"
      xmlns:shiro="http://www.pollix.at/thymeleaf/shiro">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>这是主页</h1>
<p th:text="${msg}"></p>
<hr/>
    <a th:href="@{/toLogin}">login</a>
    <a th:href="@{/logout}">logout</a>
    <a th:href="@{/user/userIndex}">user</a>
    <a th:href="@{/admin/adminIndex}">admin</a>
    <a th:href="@{/guest/guestIndex}">guest</a>
</body>
</html>
````

login.html

````html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>登陆</h1>
<hr/>
<p th:text="${msg}" style="color: red"></p>
<form th:action="@{/login}">
    <p>用户名: <input type="text" name="username"></p>
    <p>密码: <input type="text" name="password"></p>
    <p><input type="submit"></p>
</form>
</body>
</html>
````



### 设置登陆后按照不同角色跳转不同页面

在controller里，登陆成功之后判断角色，并进行跳转，添加代码

````java
if(subject.hasRole("admin"))
    return "admin/adminIndex";
if(subject.hasRole("user"))
    return "user/userIndex";
if(subject.hasRole("guest"))
````



### shiro整合thymeleaf

1. 添加maven依赖

   ````xml
   <!-- thymeleaf-extras-shiro -->
   <dependency>
       <groupId>com.github.theborakompanioni</groupId>
       <artifactId>thymeleaf-extras-shiro</artifactId>
       <version>2.0.0</version>
   </dependency>
   ````

2. html添加命名空间

   ````html
   <html lang="en" xmlns:shiro="http://www.pollix.at/thymeleaf/shiro">
   ````

3. 在ShiroConfig添加Bean

   ````java
   @Bean
   public ShiroDialect getShiroDialect(){
       return new ShiroDialect();
   }
   ````

4. 不同用户显示不同的按钮

   ````html
   <div shiro:hasAnyRoles="user">
       <a th:href="@{/user/userIndex}">user</a>
   </div>
   <div shiro:hasAnyRoles="admin">
       <a th:href="@{/admin/adminIndex}">admin</a>
   </div>
   <div shiro:hasAnyRoles="guest">
       <a th:href="@{/guest/guestIndex}">guest</a>
   </div>
   ````

5. 已有用户登陆不显示登陆按钮，未有用户登陆不显示登出按钮

   登陆成功，添加session

   ````java
   Session session = subject.getSession();
   session.setAttribute("loginUser",username);
   ````

   页面上添加

   ````html
   <div th:if="${session.loginUser}==null">
       <a th:href="@{/toLogin}">login</a>
   </div>
   <div th:if="${session.loginUser}!=null">
       <a th:href="@{/logout}">logout</a>
   </div>
   ````

6. sss

## SpringBoot整合poi

### 添加maven依赖

````java

````



## SpringBoot整合easyexcel

### 添加maven依赖

````java

````



## SpringBoot整合zookeeper+dubbo

## SpringBoot整合swagger

