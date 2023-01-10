#  SpringMVC

![在这里插入图片描述](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/9af0bb1f70be4e18a61bed179c8bb204.png)

## Spring与Web环境集成

[springboot 添加webapp目录-百度经验 (baidu.com)](https://jingyan.baidu.com/article/9f7e7ec062de112f28155490.html)

**ApplicationContext应用上下文获取方式**

应用上下文对象是通过new ClasspathXmlApplicationContext(spring配置文件)方式获取的，但是每次从容器中获得Bean时都要编写new ClasspathXmlApplicationContext(spring配置文件) ，这样的弊端是配置文件加载多次，应用上下文对象创建多次，影响性能。

```java
ClassPathXmlApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
```

**创建监听器**

在Web项目中使用**ServletContextListener**监听Web应用的启动，当Web应用启动时，就加载Spring的配置文件，创建应用上下文对象ApplicationContext，将其存储到**最大的域servletContext域**中，这样就可以在任意位置从域中获得应用上下文ApplicationContext对象了。



**Spring提供获取应用上下文的工具**

上面的分析不用手动实现，Spring提供了一个监听器**ContextLoaderListener**就是对上述功能的封装，该监听器内部加载Spring配置文件，创建应用上下文对象，并存储到ServletContext域中，提供了一个客户端工具WebApplicationContextUtils供使用者获得应用上下文对象。



所以我们需要做的只有两件事：

①在web.xml中配置ContextLoaderListener监听器（导入spring-web坐标）

```xml
导入Spring集成web的坐标
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-web</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
```

```xml
<!--全局参数-->
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:applicationContext.xml</param-value>
</context-param>
<!--Spring的监听器-->
<listener>
	<listener-class>
      org.springframework.web.context.ContextLoaderListener
   </listener-class>
 </listener>
```

②使用WebApplicationContextUtils获得应用上下文对象ApplicationContext

```java
ApplicationContext applicationContext =    
    WebApplicationContextUtils.getWebApplicationContext(servletContext);
    Object obj = applicationContext.getBean("id");
```





## SpringMVC简介

##### 概述

MVC(Model View Controller) 模型,视图,控制器

SpringMVC 是一种基于 Java 的实现 MVC 设计模型的请求驱动类型的轻量级 Web 框架，属于SpringFrameWork 的后续产品，已经融合在 Spring Web Flow 中。

SpringMVC 已经成为目前最主流的MVC框架之一，并且随着Spring3.0 的发布，全面超越 Struts2，成为最优秀的 MVC 框架。它通过一套注解，让一个简单的 Java 类成为处理请求的控制器，而无须实现任何接口。同时它还支持 RESTful 编程风格的请求。



##### 快速入门

需求：客户端发起请求，服务器端接收请求，执行逻辑并进行视图跳转。

##### 开发步骤

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210815170227082.png" alt="image-20210815170227082" style="zoom:80%;" />

①导入SpringMVC相关坐标

②配置SpringMVC核心控制器DispathcerServlet

③创建Controller类和视图页面

④使用注解配置Controller类中业务方法的映射地址

⑤配置SpringMVC核心文件 spring-mvc.xml

⑥客户端发起请求测试



**代码实现**

①导入Spring和SpringMVC的坐标、导入Servlet和Jsp的坐标

```xml
 <!--Spring坐标-->
 <dependency>
     <groupId>org.springframework</groupId>
     <artifactId>spring-context</artifactId>
     <version>5.0.5.RELEASE</version>
 </dependency>
 <!--SpringMVC坐标-->
 <dependency>
     <groupId>org.springframework</groupId>
     <artifactId>spring-webmvc</artifactId>
     <version>5.0.5.RELEASE</version>
 </dependency>
 <!--Springweb坐标-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-web</artifactId>
    <version>5.0.5.RELEASE</version>
</dependency>
<!--Servlet坐标-->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>servlet-api</artifactId>
    <version>2.5</version>
</dependency>
<!--Jsp坐标-->
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>jsp-api</artifactId>
    <version>2.0</version>
</dependency>
```

②在web.xml配置SpringMVC的核心控制器 **DispatcherServlet**

```xml
<!--  SpringMVC的前端控制器 -->
<servlet>
    <servlet-name>DispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
    <!--
            为DispatcherServlet提供初始化参数的
            设置springmvc配置文件的路径
                name是固定的，必须是contextConfigLocation
                value指的是SpringMVC配置文件的位置
         -->
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:spring-mvc.xml</param-value>
    </init-param>
    <!--
            指定项目启动就初始化DispatcherServlet
     -->
	<load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>   
    <servlet-name>DispatcherServlet</servlet-name>
     <!--
             /           表示当前servlet映射除jsp之外的所有请求（包含静态资源）
             *.do        表示.do结尾的请求路径才能被SpringMVC处理(老项目会出现)
             /*          表示当前servlet映射所有请求（包含静态资源,jsp），不应该使用其配置DispatcherServlet
         -->
    <url-pattern>/</url-pattern>
</servlet-mapping>

```



③创建Controller和业务方法和配置映射地址和注解

```java
@Controller
public class UserController {

    /**
     * //请求映射
     * @return
     */
    @RequestMapping("/quick")
    public String save(){
        System.out.println("Controller save running");
        return "success.jsp";
    }
}
```

③创建视图页面success.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<h1>Success</h1>
</body>
</html>
```

④创建spring-mvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 开始扫描Controller包
SpringMVC基于Spring容器，所以在进行SpringMVC操作时，需要将Controller存储到Spring容器中，如果使用@Controller注解标注的话 	-->
    <context:component-scan base-package="controller"></context:component-scan>

</beans>
```

⑤访问测试地址

```
http://localhost:8081/SpringMVC1_war_exploded/quick
```

![image-20210815170313730](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210815170313730.png)

遇到tomact无法启动的原因

[(12条消息) 找到多个名为spring_web的片段。这是不合法的相对排序。有关详细信息，请参阅Servlet规范的第8.2.2 2c节，解决办法：项目lib中有重复的Spring框架_LeBronJJJ的博客-CSDN博客](https://blog.csdn.net/LeBronJJJ/article/details/114490544)

[(12条消息) Tomcat启动报错：一个或多个筛选器启动失败。由于之前的错误，Context[\]启动失败_xzl的博客-CSDN博客_一个或多个筛选器启动失败](https://blog.csdn.net/qq_42957436/article/details/107531826)



##### SpringMVC流程视图

![image-20210815170406489](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210815170406489.png)

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210806151232413.png" alt="image-20210806151232413" style="zoom:67%;" />

1. 服务器启动

   1.  加载web.xml中DispatcherServlet
   2. 读取spring-mvc.xml中的配置，加载所有com.itheima包中所有标记为bean的类
   3. 读取bean中方法上方标注@RequestMapping的内容

   

2. 处理请求

   1. DispatcherServlet配置拦截所有请求 /
   2. 使用请求路径与所有加载的@RequestMapping的内容进行比对执行对应的方法
   3. 根据方法的返回值在webapp目录中查找对应的页面并展示

   

## SpringMVC组件解析

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210806152037059.png" alt="image-20210806152037059" style="zoom:67%;" />

1. **前端控制器：DispatcherServlet**

    用户请求到达前端控制器，它就相当于 MVC 模式中的 C，DispatcherServlet 是整个流程控制的中心，由它调用其它组件处理用户的请求，DispatcherServlet 的存在降低了组件之间的耦合性。

2. **处理器映射器：HandlerMapping**

    HandlerMapping 负责根据用户请求找到 Handler 即处理器，SpringMVC 提供了不同的映射器实现不同的映射方式，例如：配置文件方式，实现接口方式，注解方式等。

3. **处理器适配器：HandlerAdapter**

    通过 HandlerAdapter 对处理器进行执行，这是适配器模式的应用，通过扩展适配器可以对更多类型的处理器进行执行。

4. **处理器：Handler**

    它就是我们开发中要编写的具体业务控制器。由 DispatcherServlet 把用户请求转发到 Handler。由Handler 对具体的用户请求进行处理。

5. **视图解析器：View Resolver**

 View Resolver 负责将处理结果生成 View 视图，View Resolver 首先根据逻辑视图名解析成物理视图名，即具体的页面地址，再生成 View 视图对象，最后对 View 进行渲染将处理结果通过页面展示给用户。

​	6.**视图：View**

 视图，最终产出结果， 常用视图如jsp、 html



## SpringMVC注解解析

##### @RequestMapping

设置请求映射规则

作用：用于建立请求 URL 和处理请求方法之间的对应关系

位置：方法上或者是类上

- 类上，请求URL 的第一级访问目录。此处不写的话，就相当于应用的根目录
- 方法上，请求 URL 的第二级访问目录，与类上的使用@ReqquestMapping标注的一级目录一起组成访问虚拟路径

属性：

- value：只写单个属性时可以省略

  ```java
  @Controller
  @RequestMapping(value = "user")
  //@RequestMapping("user")
  public class UserController {
  
      /**
       * 请求映射
       * @return
       */
      @RequestMapping(value = "quick")
      @RequestMapping("quick")
      public String save(){
          System.out.println("Controller save running");
          return "/success.jsp";
      }
  }
  ```

- method：可以用来指定可处理的请求方式。

   注意：我们可以也可以运用如下注解来进行替换

   @PostMapping 等价于 @RequestMapping(method = RequestMethod.POST)

   @GetMapping 等价于 @RequestMapping(method = RequestMethod.GET)

   @PutMapping 等价于 @RequestMapping(method = RequestMethod.PUT)

   @DeleteMapping 等价于 @RequestMapping(method = RequestMethod.DELETE)


- params: 指定请求参数,对请求参数进行一些限制

  例如：

  - `params = {"username"}`，表示请求参数必须有username
  - `params = {"moeny!100"}`，表示请求参数中money不能是100
  - `params = {"!username"}`, 表示不能有username这个参数







##  SpringMVC的数据响应

##### 页面跳转

- **直接返回字符串**

在进行请求地址映射后，返回一个静态页面的路径如下

```java
@Controller
@RequestMapping(value = "user")
public class UserController {

    /**
     * 请求映射
     * @return
     */
//    @RequestMapping(value = "quick",method = RequestMethod.GET)
    @GetMapping(value = "quick",params = "name")
    public String save(){
        System.out.println("Controller save running");
        return "/success.jsp";
    }
}
```

- 默认的跳转其实是转发的方式跳转的。
- 可以在路径前加上**forwar：**，这样SpringMVC也会帮我们进行请求转发。

```java
        return "forward:/success.jsp";
```

- 如果想实现重定向跳转则可以在跳转路径前加上`redirect:` 进行标识。
- 这样SpringMVC就会帮我们进行重定向跳转

```java
        return "redirect:/success.jsp";
```

![image-20210807142144661](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210807142144661.png)

地址发生了改变，但是跳转的还是原来的界面。

下面进行一些优化，把跳转地址的前缀和后缀省略(**放入到配置文件中**)；

- 配置spring-mvc.xml如下

  ```xml
  <!--    配置内部资源视图解释器：映射地址跳转对应静态页面  return "/success.jsp";-->
      <bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
  <!--        对这个路径进行优化 "/success.jsp";-->
          <!--        前缀-->
          <property name="prefix" value="/"></property>
  <!--        后缀-->
          <property name="suffix" value=".jsp"></property>
      </bean>
  ```

  ```java
      @GetMapping(value = "quick",params = "name")
      public String save(){
          System.out.println("Controller save running");
          return "success";
      }
  ```

- 测试

![image-20210807142634814](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210807142634814.png)

- **通过ModelAndView对象返回**

  1. 方式一

     ```java
         @GetMapping(value = "quick2")
         public ModelAndView save2(){
             /*
             Model:模型 封装数据
             View：视图  展示数据
              */
             ModelAndView modelAndView = new ModelAndView();
             //设置模型数据
             modelAndView.addObject("username","dema");
     
             //设置视图,跳转到对应的success jsp页面
             modelAndView.setViewName("success");
             return modelAndView;
         }
     ```

     最标准方式

  2. 方式二

     ```java
         @GetMapping(value = "quick3")
         public String save3(Model model){
             //Model类型的引用，调用save3方法的是SpringMVC框架
             //在映射地址调用方法时容器已经帮忙创建好Model类型的对象
             model.addAttribute("username","地错");
     		//success前面配置了视图解析器，将完整地址拼接起来
             return "success";
         }
     ```

  3. 方式三

     ```java
         //这种方式使用很少
     	@GetMapping(value = "quick4")
         public String save3(HttpServletRequest request){
             request.setAttribute("username","没道理");
     
             return "success";
         }
     ```

##### 回写数据

- 直接返回字符串

  - 方式一

    通过SpringMVC框架注入的response对象，使用response.getWriter.print()回写数据，此时不需要视图跳转，业务方法返回值为void。

    ```java
    //不再跳转页面，而是通过字符串回写
    @GetMapping(value = "quick5")
    public void save4(HttpServletResponse response) throws IOException {
        response.getWriter().print("Hello Boy");
    }
    ```

  - 方式二

    注解：@ResponseBody

    ```java
        @ResponseBody
        @RequestMapping("quick6")
        public String save5()  {
    
           return "不进行页面条件，这里进行数据回写通过@ResponseBody注解来标识告知框架";
        }
    ```

- 返回对象或集合

  ```java
      @RequestMapping(value = "quick7")
      @ResponseBody
      public User save6()  {
          //通过SpringMVC能够将数据以json格式返回，MVC框架帮助转换
          User user = new User();
          user.setAge(20);
          user.setName("name1");
  
  		//json的格式返回
          return user;
      }
  ```

  ![image-20210807181000771](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210807181000771.png)

- **导入依赖**

  ```xml
   <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-annotations</artifactId>
          <version>2.12.4</version>
      </dependency>
      <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-core</artifactId>
          <version>2.12.4</version>
      </dependency>
      <dependency>
          <groupId>com.fasterxml.jackson.core</groupId>
          <artifactId>jackson-databind</artifactId>
          <version>2.12.4</version>
      </dependency>
  ```

- **配置文件**

  ```java
  <!--    配置映射处理器，把集合或对象以json格式返回-->
      <bean  class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter">
          <property name="messageConverters">
              <list>
                  <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter"/>
              </list>
          </property>
      </bean>
  ```

**注意：**这里遇到了使用@Response注解无法回写数据的问题。

[(12条消息) Java Web——tokenize(Ljava/lang/String；)Ljava/util/List；报错解决_肺叶回收站的博客-CSDN博客](https://blog.csdn.net/weixin_47954807/article/details/115535725)

作为一个参考，我这里确实也是jar包重复问题，在创建SpringMVC时会创建一个lib的目录，我在配置tomact服务器启动时会创建out文件夹，当中的jar都重复了，我这里把lib目录删除之后，接解决了问题。

![image-20210807181407825](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210807181407825.png)

![image-20210807181423754](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210807181423754.png)



上面通过@ResponseBody注解返回json格式字符串，配置比较繁琐。

**这里使用注解替代上述配置**

在SpringMVC的各个组件中，**处理器映射器、处理器适配器、视图解析器**称为SpringMVC的三大组件。

```xml
<mvc:annotation-driven/>
```

自动加载RequestMappingHandlerMapping (处理映射器）和
RequestMappingHandlerAdapter(处理适配器），可用在Spring-xml.xml配置文件中使用上述注解处理器和适配器的配置。同时默认底层就会集成jackson进行对象或集合的son格式字符串的转换。



## SpringMVC获得请求数据

##### 获得请求参数

参数值自动映射匹配前提：Controller中业务方法的参数名与请求参数的name一致。

- **基本类型参数**

  

  ```
  http://localhost:8081/user/quick8?name=zhanghui&age=22
  ```

  ```java
      @RequestMapping(value = "quick8")
      @ResponseBody
      public User save7(String name , int age)  {
          User user = new User();
          user.setName(name);
          user.setAge(age);
          return user;
      }
  
  ```

  ![image-20210809154155084](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210809154155084.png)

  

- **POJO类型参数**

  ```
  http://localhost:8081/user/quick9?name=zhang&age=12
  ```

  ```java
      @RequestMapping(value = "quick9")
      @ResponseBody
      public User save8(User user)  {
          return user;
      }
  ```

  ![image-20210809154738921](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210809154738921.png)

- **数组类型参数**

  ```
  http://localhost:8081/user/quick10?list=123&list=5869
  ```

  ```java
      @RequestMapping(value = "quick10")
      @ResponseBody
      public String[] save9(String[] list)  {
          return list;
      }
  ```

  ![image-20210809155008520](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210809155008520.png)

- **集合类型参数**

  获取集合参数时，将集合参数包装到一个POJO中才可以。

  创建一个VO对象，用来存放User类型的集合

  ```java
  public class vo {
  
      public List<User> userList;
  
      public List<User> getUserList() {
          return userList;
      }
  
      public void setUserList(List<User> userList) {
          this.userList = userList;
      }
  
      @Override
      public String toString() {
          return "vo{" +
                  "userList=" + userList +
                  '}';
      }
  }
  ```

  来到Controller层,使用VO来接收User类型的对象集合

  ```java
      @RequestMapping(value = "quick11")
      @ResponseBody
      public void save10(vo vo)  {
          System.out.println(vo);
      }
  ```

  写一个简单的jsp页面，表单输入

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
  <head>
      <title>Title</title>
  </head>
  <body>
  <form action="${pageContext.request.contextPath}/user/quick11" method="post">
  <%--    表明是第几个User对象的username和age--%>
      <input type="text" name="userList[0].userName">
      <input type="text" name="userList[0].age">
      <input type="text" name="userList[1].userName">
      <input type="text" name="userList[1].age">
      <input type="submit" value="提交">
  </form>
  </body>
  </html>
  ```

  页面

  ![image-20210809160501342](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210809160501342.png)

  ![image-20210809163400715](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210809163400715.png)

   

  另一种形式

  通过指定contentType为json形式，在方法参数位置使用@RequestBody可以直接接收集合数据而无需使用POJO进行包装。

   

  开启静态资源访问配置

  ```xml
  <mvc:default-servlet-handler/>
  ```



##### 请求数据乱码问题

使用post请求时，数据出现乱码

![image-20210809163425037](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210809163425037.png)

配置过滤器进行编码的过滤

```xml
<!--    配置全局过滤的filter-->
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```



##### 参数绑定注解@requestParam

Controller中业务方法的参数名与请求参数名称不一致，通过该注解显示绑定。

```java
    @RequestMapping(value = "quick12")
    @ResponseBody
    /*request中name的值映射到userName中*/
    public void save11(@RequestParam(value = "name") String userName)  {
        System.out.println(userName);
    }
```

参数

- **value**:请求的参数名称
- **required:**默认为true，表示请求参数中包含value中的参数，若为fasle，表示请求参数中没有该参数名
- **defaultValue:** 当参数中没有指定值，提供一个默认的值

```java
    @RequestMapping(value = "quick12")
    @ResponseBody
    /*request中name的值映射到userName中*/
    public void save11(@RequestParam(value = "name",required = false,defaultValue = "zhang") String userName)  {
        System.out.println(userName);
    }
```



##### 获取Restful风格的参数

Restful是一种**软件风格，设计风格**，不是标准，提供了一组设计原则和约束条件。

主要用于客户端和服务器交互类的软件，基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存机制等。

Restful风格的请求是使用“**url+**请求方式”表示一次请求目的的，HTTP协议里面四个表示操作方式的动词如下:
**GET**:用于获取资源

**POST**:用于新建资源

**PUT**:用于更新资源

**DELETE**:用于删除资源

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210815170600206.png" alt="image-20210815170600206" style="zoom:67%;" />

![image-20210815170620745](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210815170620745.png)

```java
    @RequestMapping(value = "quick13/{userName}")
    @ResponseBody
    /*request中name的值映射到userName中*/
    public void save12( @PathVariable(value = "userName") String userName)  {
        System.out.println(userName);
    }
```

```
http://localhost:8081/user/quick13/name
```



##### 自定义类型转换器

SpringMVC默认已经提供了一些常用的类型转换器，例如客户端提交的字符串转换成int型进行参数设置。但是不是所有的数据类型都提供了转换器，没有提供的就需要自定义转换器，例如:日期类型的数据就需要自定义转换器。


**自定义类型转换器的开发步骤：**

1. 定义转换器类实现Converter接口
2. 在配置文件中声明转换器
3. 在<annotation-driven>中引用转换器



实现Converter接口

```java
/**
 * 自定义类型转换器
 * 日期类型转换
 */
public class DateConverter implements Converter<String,Date> {
    public Date convert(String dateStr) {
        //将日期字符串转换成日期对象
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd");
        Date date = null;
        try {
            date = format.parse(dateStr);
        } catch (ParseException e) {
            e.printStackTrace();
        }
        return date;
    }
}
```

配置文件

```xml
<!--   优化: 使用注解来替代json格式配置-->
    <mvc:annotation-driven conversion-service="conversionService"/>
    
<!--    声明自定类型转换器-->
    <bean id="conversionService" class="org.springframework.context.support.ConversionServiceFactoryBean">
        <property name="converters">
            <list>
                <bean class="util.DateConverter"></bean>
            </list>
        </property>
    </bean>
```

测试

```java
    @RequestMapping(value = "quick14")
    @ResponseBody
    public void save13(Date date)  {
        System.out.println(date);
    }
```



##### 获取Servlet相关API

SpringMVC支持原始ServletAPI对象作为控制器方法的参数进行注入，

- HttpServletRequest
- HttpServletResponse
- HttpSession

```java
@RequestMapping(value = "quick15")
@ResponseBody
public void save13(HttpServletResponse response, HttpServletRequest request, HttpSession session){
    System.out.println(request);
    System.out.println(response);
    System.out.println(session);
}
```



##### 获取请求头

**@RequestHeader**

使用@RequestHeader可以获得请求头信息，相当于web阶段学习的

request.getHeader(name)@RequestHeader注解的属性如下:

- value:请求头的名称
- required:是否必须携带此请求头



**@CookieValue**
使用@CookieValue可以获得指定Cookie的值

@CookieValue注解的属性如下:

- value: 指定cookie的名称
- required: 是否必须携带此cookie



```java
    @RequestMapping(value = "quick16")
    @ResponseBody
    public void save14(@RequestHeader(value = "User-Agent")  String userAgentStr,@CookieValue("JSESSIONID") String cookie)  {
        System.out.println(userAgentStr);
        System.out.println(cookie);
    }
```

![image-20210810160311852](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210810160311852.png)

```java
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.131 Safari/537.36
DCC434A6D72FDDC5204686834566FAB6
```



##### 文件上传

**文件上传客户端三要素**

1. 表单项type= "file"
2. 表单的提交方式是post
3. 表单的enctype属性是多部分表单形式，及enctype=“multipart/form-data"

**文件上传原理**

- 当form表 单修改为多部分表单时，request.getParameter()将失效。

- enctype= "application/x-www-form-urlencoded" 时, form表单的正文内容格式是:

  **key= value&key= value&key=value**

- 当form表 单的enctype取值为Mutilpart/form-data时,请求正文内容就变成多部分形式:

![image-20210810161436324](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210810161436324.png)



##### 单文件上传步骤

1. 导入**fileupload和io**坐标
2. 配置文件上传解析器
3. 编写文件上传代码



导入坐标

```xml
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.6</version>
</dependency>
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.3.2</version>
</dependency>
```



配置文件

```xml
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
<!--        上传文件总大小:5*1024*1024=5MB-->
        <property name="maxUploadSize" value="5242880" />
        <!--        单个文件大小:5*1024*1024=5MB-->
        <property name="maxUploadSizePerFile" value="5242880" />
<!--        文件编码类型-->
        <property name="defaultEncoding" value="UTF-8"/>
    </bean>
```

编写代码

jsp页面

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>文件上传</title>
</head>
<body>
    <form action="${pageContext.request.contextPath}/user/quick17" method="post" enctype="multipart/form-data">
<%--        名称--%>
    <input type="text" name="username"><br/>
    <input type="file" name="loadFile"><br/>
        <input type="submit" name="load"/>
    </form>
</body>
</html>
```

controller层

```java
public void save15(@RequestParam("username")String name ,@RequestParam("loadFile") MultipartFile file) throws IOException {
        System.out.println(name);
        //获取文件上传名称
        String uploadFileName = file.getOriginalFilename();
        System.out.println(uploadFileName);
        //将文件存储下来
        file.transferTo(new File("C:\\Users\\25246\\Desktop\\打印"+"存储下来的文件.txt"));
    }
```

![image-20210810170222572](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210810170222572.png)

![image-20210810171528527](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210810171528527.png)



这里遇到保存问题

1.   	java.lang.ClassNotFoundException: org.apache.commons.fileupload.FileItemFactory
2. nested exception is java.lang.NoClassDefFoundError: org/apache/commons/io/IOUtils

这两问题都是导入IO包和fileupload包没有导入导致。

解决：

![image-20210815170706416](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210815170706416.png)

![image-20210815170722197](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210815170722197.png)



## Spring JDBCTemplate基本使用

##### JDBCTemplate概述

它是spring框架中提供的一个对象，是对原始繁琐的JdbcAPI对象的简单封装。spring框架为我们提供了很多的操作模板类。例如:操作关系型数据的JdbcTemplate和HibernateTemplate，操作nosql数据库的RedisTemplate，操作消息队列的JmsTemplate等等。



##### JDBCTemplate开发步骤

- 导入spring-jdbc和spring-tx(事务)坐标

  ```xml
    <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-jdbc</artifactId>
              <version>5.0.5.RELEASE</version>
          </dependency>
  
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-tx</artifactId>
              <version>5.0.5.RELEASE</version>
    </dependency>
          <!--        数据库驱动-->
          <dependency>
              <groupId>mysql</groupId>
              <artifactId>mysql-connector-java</artifactId>
              <version>5.1.49</version>
          </dependency>
  
          <dependency>
              <groupId>c3p0</groupId>
              <artifactId>c3p0</artifactId>
              <version>0.9.1.2</version>
          </dependency>
  
          <dependency>
              <groupId>com.alibaba</groupId>
              <artifactId>druid</artifactId>
              <version>1.2.1</version>
          </dependency>
  ```

- 创建数据库表和实体

  ![image-20210816152034848](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210816152034848.png)

  ```java
  public class Account {
  
      private String name;
      private double money;
  }
  ```

- 创建JdbcTemplate对象

  ```java
    //创建数据源
          ComboPooledDataSource dataSource = new ComboPooledDataSource();
          dataSource.setDriverClass("com.mysql.jdbc.Driver");
          dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/test2");
          dataSource.setUser("root");
          dataSource.setPassword("root");
      JdbcTemplate jdbcTemplate = new JdbcTemplate();
          //连接数据库，设置数据源
          jdbcTemplate.setDataSource(dataSource);
  ```

- 执行数据库操作

  ```java
   //操作执行
          jdbcTemplate.update("insert into account values (?,?)","Tom","3000");
  ```



##### Spring产生JdbcTemplate对象

xml配置文件

```xml
<!--    数据源对象配置-->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="com.mysql.jdbc.Driver"></property>
        <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/test2"></property>
        <property name="user" value="root"></property>
        <property name="password" value="root"></property>
    </bean>

    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource"></property>
    </bean>
```

测试

```java
@Test
    public void Test1()   {
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
        JdbcTemplate jdbcTemplate = applicationContext.getBean(JdbcTemplate.class);
        jdbcTemplate.update("insert into account values (?,?)","Jack","7000");
    }
```

复习一下：优化

jdbc.properties文件

```properties
jdbc.driver = com.mysql.jdbc.Driver
jdbc.url =jdbc:mysql://localhost:3306/test2
jdbc.user = root
jdbc.password = root
```

```xml
<!--    加载jdbc.properties-->
        <context:property-placeholder location="jdbc.properties"/>

<!--    数据源对象配置-->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="driverClass" value="${jdbc.driver}"></property>
        <property name="jdbcUrl" value="${jdbc.url}"></property>
        <property name="user" value="${jdbc.user}"></property>
        <property name="password" value="${jdbc.password}"></property>
    </bean>
```



##### JDBC基本操作

CRUD（增删改查）

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class jdbcTemplateCRUDTest {

    @Autowired
    private JdbcTemplate jdbcTemplate;


    @Test
    public void insertTest(){
        jdbcTemplate.update("insert into account values (?,?)","T1",1111);
    }

    @Test
    public void updateTest(){
        jdbcTemplate.update("update account set money=? where name=?",6000,"Tom");
    }

    @Test
    public void selectTest(){
        List<Account> list = jdbcTemplate.query("select * from account ", new BeanPropertyRowMapper<Account>(Account.class));
        
       Account list = jdbcTemplate.queryForObject("select * from account where name = ?  ", new BeanPropertyRowMapper<Account>(Account.class),"Tom");
        
        Long list = jdbcTemplate.queryForObject("select count(*) from account where ", Long.class);
        System.out.println(list);
    }

}
```



## SpringMVC拦截器

##### 拦截器(interceptor)的作用

Spring MVC的**拦截器**类似于Servlet开发中的过滤器Filter，用于对处理器进行**预处理**和**后处理**.

将拦截器按一定的顺序联结成一条链，这条链称为**拦截器链(Interceptor Chain)**。在访问被拦截的方法或字段时，拦截器链中的拦截器就会按其之前定义的顺序被调用。拦截器也是AOP思想的具体实现。



##### 拦截器和过滤器区别

![image-20210816163512883](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210816163512883.png)



##### 拦截器快速入门

自定义拦截器三步骤：

1. **创建拦截器类实现HandlerInterceptor接口**

   ```java
   public class MyInterceptor implements HandlerInterceptor {
   
       //在目标方法执行之前执行
       public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
           System.out.println("preHandle....");
           //false:表示到此拦截,后面方法都被拦截了
           return true;
       }
   
       //在目标方法执行之后 视图对象返回之前执行
       public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
           System.out.println("postHandle....");
   
       }
   
       //整个流程都执行完毕后 视图对象已经返回执行
       public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
           System.out.println("afterCompletion....");
   
       }
   }
   ```

    

   ![image-20210817154519313](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210817154519313.png)

   

   

2. **配置拦截器**

   ```xml
   <!--    配置拦截器-->
   
    <mvc:interceptors>
           <mvc:interceptor>
   <!--            对哪些资源执行拦截操作
               /**:表示对所有目标方法都进行拦截
                /xx/**:表示xx目录下所有的目标方法   -->
               <mvc:mapping path="/**"/>
               <bean class="interceptor.MyInterceptor"/>
           </mvc:interceptor>
   </mvc:interceptors>
   ```

3. **测试拦截器效果**

```java
@Controller
public class TargetController {
	//目标方法
    @GetMapping(value = "quick2")
    public ModelAndView save2(){
        System.out.println("目标方法执行....");
        /*
        Model:模型 封装数据
        View：视图  展示数据
         */
        ModelAndView modelAndView = new ModelAndView();
        //设置模型数据
        modelAndView.addObject("username","DeMA");

        //设置视图,跳转到对应的success jsp页面
        modelAndView.setViewName("success");
        return modelAndView;
    }
}
```

若自定义方法中的**preHandle()**返回的false，就会出现以下的情况。

![image-20210816165549186](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210816165549186.png)

![image-20210816165600914](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210816165600914.png)





若返回改为**true**

![image-20210816165653976](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210816165653976.png)

![image-20210816165722185](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210816165722185.png)





小拓展

```java
public class MyInterceptor implements HandlerInterceptor {

    //在目标方法执行之前执行
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("preHandle....");

        //规定请求资源中需要一个request参数
        String param = request.getParameter("request");
        if ("111".equals(param)){
            return true;
        }else{

            //进行拦截,重定向资源
            request.getRequestDispatcher("/index.jsp").forward(request,response);
            return false;
        }

        //false:表示到此拦截,后面方法都被拦截了,开启拦截
        //true: 关闭拦截
//        return true;
    }

    //在目标方法执行之后 视图对象返回之前执行
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        //对视图进行变动
        modelAndView.addObject("username","资源发生改变");
        System.out.println("postHandle....");
    }

    //整个流程都执行完毕后 视图对象已经返回执行
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("afterCompletion....");

    }
}
```

![image-20210816170905524](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210816170905524.png)

![image-20210816170915734](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210816170915734.png)



**应用场景**

用户登录拦截

```java
/**
 * 模拟一个用户登录拦截的业务
 */
public class UserLoginInterceptor implements HandlerInterceptor {

    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //判断用户是否登录过，没有登录进行地址重定向
       HttpSession session = request.getSession();
       //模拟用户：1 表示已经登录，2表示没有登录跳转页面
        User user = (User) session.getAttribute("user");

        if (user == null){
            response.sendRedirect(request.getContextPath()+"/userLogin.jsp");
            return false;
        }

        return true;
    }
}
//别忘了xml中拦截器的配置
```

```xml
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <!--            对于login路径请求不进行拦截-->
            <mvc:exclude-mapping path="/login"/>
            <bean class="interceptor.UserLoginInterceptor"/>
        </mvc:interceptor>
```





## SpringMVC异常处理机制

##### 异常处理的思路

系统中异常包括两类∶**预期异常**和**运行时异常**RuntimeException，前者通过捕获异常从而

获取异常信息，后者主要通过规范代码开发、测试等手段减少运行时异常的发生。



系统的**Dao、Service、Controller**出现都通过throws Exception向上抛出，最后由

SpringMVC**前端控制器**交由异常处理器进行异常处理，如下图:

![image-20210817163522545](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210817163522545.png)



##### 异常处理的两种方式

1. 使用Spring MVC提供的简单异常处理器**SimpleMappingExceptionResolver**实现

    spring-mvc.xml 配置文件

   ```xml
   <!--    配置映射异常处理器-->
       <bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
   <!--        多种异常类型配置-->
           <property name="exceptionMappings" >
   <!--            map形式-->
               <map>
   <!--                键值对-->
   <!--                key对应异常类型，value对应条状的自定义页面，实际开发对应响应的自定义异常页面提高用户体验感-->
                   <entry key="java.lang.ClassCastException" value="error1"/>
                   <entry key="java.lang.NullPointerException" value="error3"/>
                   <entry key="java.lang.ArithmeticException" value="error2"/>
               </map>
           </property>
       </bean>
   ```

   配置了三种最常见的简单异常类型空指针、算术错误、类不匹配跳转到对应页面。

   

   

   测试

   ```java
   @Controller
   @RequestMapping("test")
   public class DemoController {
   
       @Autowired
       private DemoService demoService;
   
       @GetMapping("/exp")
       public String test(){
           System.out.println("Running....");
           //类型转换异常页面
   //        demoService.show1();
           //除数异常页面
   //        demoService.show2();
           //空指针异常页面
           demoService.show3();
           return "index";
       }
   }
   
   @Component
   public class DemoServiceImpl implements DemoService{
       public void show1() {
           System.out.println("抛出类型转换异常。。。。");
           Object str = "zhang";
           Integer num = (Integer) str;
       }
   
       public void show2() {
           System.out.println("抛出除数为0的异常。。。。");
           int i = 1 / 0;
       }
   
       public void show3() {
           String str = null ;
           str.length();
           System.out.println("空指针异常。。。。");
       }
   
   
   }
   ```

   ![image-20210825161109146](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210825161109146.png)  

   ![image-20210825161311363](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210825161311363.png) 

   ![image-20210825161425549](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210825161425549.png) 

2. Spring的异常处理接口**HandlerExceptionResolver**自定义自己的异常处理器
   公

   - 创建异常处理类实现HandlerExceptionResolver
   - 配置异常处理器
   - 编写异常页面
   - 测试异常跳转

   ```java
       /**
        *
        * @param request 请求
        * @param response 响应
        * @param handler 处理
        * @param ex 异常对象
        * @return 跳转到对应错误的视图信息
        */
       public ModelAndView resolveException(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) {
           ModelAndView modelAndView = new ModelAndView();
   
           //模拟对异常类型进行判断
           if (ex instanceof  MyExceptionResolver){
               modelAndView.addObject("info","自定义异常");
           }else  if (ex instanceof ClassCastException){
               modelAndView.addObject("info","类转换异常");
           }
   
           return modelAndView;
       }
   ```

   

 
