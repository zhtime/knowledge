# Spring

### 简介

分层的Java SE/EE应用 full - stack轻量级开源框架。

核心:**IOC(Inverse Of Control 控制反转)**和**AOP(Aspect Oriented Programming  面向切面编程)**



###  优势

- 方便解耦，简化开发
- AOP编程的支持
- 声明式事务的支持
- 方便程序的测试
- 方便集成各种优秀框架
- 降低JAVAEE API的使用难度
- Java源码经典学习范例



### **体系结构**

![Spring的体系结构](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//5-1Z606104H1294.gif)



**1. Data Access/Integration（数据访问／集成）**

数据访问/集成层包括 JDBC、ORM、OXM、JMS 和 Transactions 模块，具体介绍如下。

- JDBC 模块：提供了一个 JDBC 的抽象层，大幅度减少了在开发过程中对数据库操作的编码。
- ORM 模块：对流行的对象关系映射 API，包括 JPA、JDO、[Hibernate](http://c.biancheng.net/hibernate/) 和 iBatis 提供了的集成层。
- OXM 模块：提供了一个支持对象/XML 映射的抽象层实现，如 JAXB、Castor、XMLBeans、JiBX 和 XStream。
- JMS 模块：指 [Java](http://c.biancheng.net/java/) 消息服务，包含的功能为生产和消费的信息。
- Transactions 事务模块：支持编程和声明式事务管理实现特殊接口类，并为所有的 POJO。

**2. Web 模块**

Spring 的 Web 层包括 Web、[Servlet](http://c.biancheng.net/servlet/)、Struts 和 Portlet 组件，具体介绍如下。

- Web 模块：提供了基本的 Web 开发集成特性，例如多文件上传功能、使用的 Servlet 监听器的 IoC 容器初始化以及 Web 应用上下文。
- Servlet模块：包括 Spring 模型—视图—控制器（MVC）实现 Web 应用程序。
- Struts 模块：包含支持类内的 Spring 应用程序，集成了经典的 Struts Web 层。
- Portlet 模块：提供了在 Portlet 环境中使用 MV C实现，类似 Web-Servlet 模块的功能。

**3. Core Container（核心容器）**

Spring 的核心容器是其他模块建立的基础，由 Beans 模块、Core 核心模块、Context 上下文模块和 Expression Language 表达式语言模块组成，具体介绍如下。

- Beans 模块：提供了 BeanFactory，是工厂模式的经典实现，Spring 将管理对象称为 Bean。
- Core 核心模块：提供了 Spring 框架的基本组成部分，包括 IoC 和 DI 功能。
- Context 上下文模块：建立在核心和 Beans 模块的基础之上，它是访问定义和配置任何对象的媒介。ApplicationContext 接口是上下文模块的焦点。
- Expression Language 模块：是运行时查询和操作对象图的强大的表达式语言。



## Spring程序开发步骤

![image-20210727165139658](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210727165139658.png)

1. 导入Spring开发的基本包坐标(Maven)
2. 编写Dao接口和实现类
3. 创建配置文件
4. 在配置文件中配置实现类
5. 使用Spring中API获取Bean实例



创建Maven项目

1. **在pom.xml导入Spring开发的基本包坐标（导入坐标）**

   ```xml
   <!--导入spring的context坐标，context依赖core、beans、expression-->
   <dependency>
     <groupId>org.springframework</groupId>
     <artifactId>spring-context</artifactId>
     <version>5.0.5.RELEASE</version>
   </dependency>
   ```

2. **编写Dao接口和实现类**

   <img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210728153640652.png" alt="image-20210728153640652" style="zoom:50%;" />

   ```java
   public interface UserDao {
   
       public void save();
   }
   
   public class UserDaoImpl implements UserDao {
       public void save() {
           System.out.println("Hello");
       }
   }
   ```

3. **在类路径下(resources)创建`applocationContext.xml`配置**

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
        //配置对应userDao的实现类
       <bean id="userDao" class="dao.impl.UserDaoImpl"></bean>
   </beans>
   ```

4. **测试**

   ```java
   public class UserDaoDemo {
   
       public static void main(String[] args) {
           //创建ApplicationContext对象
           ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
           //通过getBean方法获取配置文件中Bean(指定的对象)
           UserDao userDao = (UserDao) app.getBean("userDao");
           userDao.save();
       }
   }
   //结果:Hello
   ```



## Spring配置文件

#### Bean标签基本配置

默认情况下它调用的是类中的**无参构造函数**，如果没有无参构造函数则不能创建成功

##### bean

- 类型：**标签**
- 归属：beans标签
- 作用：定义spring中的资源，受此标签定义的资源将受到spring控制
- 格式：

```xml
<beans>
	<bean id="beanId" name="beanName1,beanName2" class="ClassName"></bean>
</beans>
```

- 基本属性：

```xml
<bean id="beanId" name="beanName1,beanName2" class="ClassName"></bean>

/*
id：bean的名称，通过id值获取bean(对象),唯一性标识
class：Bean的全限定名称
name：bean的名称，可以通过name值获取bean，用于多人配合时给bean起别名
*/
```



#### Bean标签范围配置

##### scope

- 类型:**属性**

- 归属：bean标签

- 作用：定义bean的作用范围

- 格式：

  ```xml
      <bean id="userDao" class="dao.impl.UserDaoImpl" scope="singleton"></bean>
  ```

- 取值：

  - singleton：

    实例化个数：1

    **实例化时机：Spring容器被创建，加载配置文件时创建对象。**

    **销毁：**应用卸载，销毁容器时

  - prototype：设定创建出的对象保存在spring容器中，

    实例化个数：多个

    **实例化时机：在调用getBean方法时创建对象**

    **销毁：**创建的对象长时间不用时(**不可达判定二次标记**)，被GC回收了

  - request、session、application、 websocket ：设定创建出的对象放置在web容器对应的位置

  

#### Bean生命周期配置



##### init-method：

**指定类中的初始化方法名称**

##### destroy-method：

**指定类中的销毁方法名称**

- 归属：bean标签

- 作用：定义bean对象在初始化或销毁时完成的工作

- 格式

  ```xml
      <bean id="userDao" class="dao.impl.UserDaoImpl" init-method="init" destroy-method="destroy"></bean>
  ```

- 注意事项：

  当scope=“singleton”时，spring容器中有且仅有一个对象，init方法在创建容器时仅执行一次

  当scope=“prototype”时，spring容器要创建同一类型的多个对象，init方法在每个对象创建时均执行一次

  当scope=“singleton”时，关闭容器会导致bean实例的销毁，调用destroy方法一次

  当scope=“prototype”时，对象的销毁由垃圾回收机制gc()控制，destroy方法将不会被执行



#### Bean实例化三种方式

- **无参构造方法实例化**(重要)

  ```xml
  <!--    无参构造创建对象--><bean id="userDao" class="com.itheima.dao.impl.UserDaoImpl" </bean>
  ```

- 工厂静态方法实例化(了解)

  ```java
  /**
   * 定义工厂静态方法实例化
   */
  public class StaticFactory {
  
      public static UserDao getUserDao(){
          return new UserDaoImpl();
      }
  }
  ```

  ```xml
  <!--        工厂静态方法实例化配置-->
          <bean id="userDao" class="factory.StaticFactory" factory-method="getUserDao"></bean>
  ```

- 工厂实例方法实例化(了解)

  ```java
      //工厂实例方法实例化
      public  UserDao getUserDao1(){
          return new UserDaoImpl();
      }
  ```

  ```xml
  <!--    工厂实例方法实例化配置-->
  <!--    先获取StaticFactory对象-->
      <bean id="factory" class="factory.StaticFactory"></bean>
  <!--    再去调用实例方法实例化-->
      <bean id="userDao" factory-bean="factory" factory-method="getUserDao1"></bean>
  ```



#### Bean依赖的注入

 ![image-20210728165623600](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210728165623600.png)

![image-20210728165706555](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210728165706555.png)

##### **依赖注入概念**

- **DI（Dependency Injection）依赖注入**，应用程序运行依赖的资源由Spring为其提供，资源进入应用程序的方式称为**注入**。Spring框架核心IOC的具体实现
- 在编写程序时，通过**控制反转，把对象的创建交给了 Spring**，但是代码中不可能出现没有依赖的情况。IOC 解耦只是降低他们的依赖关系，但不会消除。例如：业务层(Service)仍会调用持久层(Dao)的方法。
- 简单的说，就是坐等框架把持久层(Dao)对象传入业务层(Service)，而不用我们自己去获取。



##### 依赖注入方式

- 构造方法
- set方法

###### **set方法注入**

- 名称：**property**

- 类型：**标签**

- 归属：bean标签

- 作用：使用set方法的形式为bean提供资源

- 格式：

  ```xml
  <bean>	<property /></bean>
  ```

```xml
<bean id="userDao" class="dao.impl.UserDaoImpl"></bean><bean id="userService" class="service.impl.UserServiceImpl">    <!--    set方法注入 -->    <!--       name对应set方法，例如 setUserDao方法去掉set,之后首字母小写-userDao-->    <!--        ref 将bean 中 id为userDao引入-->    <property name="userDao" ref="userDao" ></property></bean>
```

`name`：对应bean中的属性名，要求该属性**必须提供可访问的set方法**（严格规范为此名称是set方法对应名称）

 `value`：设定**非引用类型**属性对应的值，不能与ref同时使用

 `ref`：设定**引用类型**属性对应bean的id ，不能与value同时使用



###### 使用p命名空间简化配置（了解）

使用p命令空间需要先开启spring对p命令空间的的支持，在beans标签中添加对应空间支持

```xml
 xmlns:p="http://www.springframework.org/schema/p" 
```

例子

```xml
<bean id="userService" class="service.impl.UserServiceImpl" p:userDao-ref="userDao"/>
```

和上面使用property相对比，变得简介了。



###### 构造方式注入

- 名称：**constructor-arg**

- 类型：**标签**

- 归属：bean标签

- 作用：使用构造方法的形式为bean提供资源，兼容早期遗留系统的升级工作

- 格式：

  ```xml
  <bean>	<constructor-arg /></bean>
  ```

例子

```xml
<!--    构造方法注入-->    <bean id="userService" class="service.impl.UserServiceImpl"><!--        name指的是构造函数中的参数名userDao--><!--        public UserServiceImpl(UserDao userDao) {--><!--        this.userDao = userDao;--><!--        }--><!--        ref指bean 中 id为userDao引入-->        <constructor-arg name="userDao" ref="userDao"></constructor-arg>    </bean>
```

`name`：对应bean中的构造方法所携带的参数名

`ref`：设定**引用类型（对象）**构造方法参数对应bean的id ，不能与value同时使用



```xml
<constructor-arg index="arg-index" type="arg-type" ref="beanId" value=""/>
```

 `value`：设定**非引用类型(基本数据类型)**构造方法参数对应的值，不能与ref同时使用

`type` ：设定构造方法参数的类型，用于按类型匹配参数或进行类型校验

 `index` ：设定构造方法参数的位置，用于按位置匹配参数，参数index值从0开始计数

**注意**：一个bean可以有多个constructor-arg标签



##### 依赖注入数据类型

**之前都是对象数据的引入，接下来介绍基本数据类型的引用**

对于**集合数据类型**注入：

- 名称：array，list，set，map，props
- 归属：**property**标签 或 **constructor-arg**标签
- 作用：注入集合数据类型属性




- **普通数据注入**

```java
public class User {

    private String name ;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

对应xml文件中的配置

```xml
    <bean id="user" class="entity.User">
     <!--        name是属性名,也就是setUsername方法去掉set,之后首字母小写-->
     <!--        name是属性名,也就是setAge方法去掉set,之后首字母小写-->
     <!--        普通值的注入,用value-->
        <property name="name" value="汤姆猫"></property>
        <property name="age" value="12"></property>
    </bean>
    <bean id="user1" class="entity.User">
        <property name="name" value="杰瑞"></property>
        <property name="age" value="8"></property>
    </bean>
```



- **List类型注入**

```java
//集合
    private List<String> strList;
    public void setStrList(List<String> strList) {
        this.strList = strList;
    }
```

对应xml文件中的配置

```xml
    <bean id="baseDataDao" class="dao.impl.BaseDataImpl">
        <property name="strList">
<!--            list类型-->
            <list>
<!--                value对应非引用数据类型，ref对应引用数据类型-->
                <value>赵信</value>
                <value>卡莎</value>
                <value>薇恩</value>
            </list>
        </property>
     </bean>

```

- **Map类型注入**

```java
    private Map<String, User> userMap;    public void setUserMap(Map<String, User> userMap) {        this.userMap = userMap;    }
```

对应xml文件中的配置

```xml
    <bean id="baseDataDao" class="dao.impl.BaseDataImpl">        <property name="userMap">            <!--        map类型-->            <map>                <entry key="key1" value-ref="user"></entry>                <entry key="key2" value-ref="user1"></entry>            </map>        </property>     </bean>
```

- **Properties注入**

```java
    private Properties properties;    public void setProperties(Properties properties) {        this.properties = properties;    }
```

对应xml文件中的配置

```xml
    <bean id="baseDataDao" class="dao.impl.BaseDataImpl">        <property name="properties">            <props>                <prop key="p1">北京</prop>                <prop key="p2">南京</prop>            </props>        </property>     </bean>
```



##### 团队开发

import 一般用于团队开发使用，可以将多个 beans.xml 配置文件，导入合并为一个。

- 类型：**标签**

- 归属：beans标签

- 作用：在当前配置文件中导入其他配置文件中的项

- 格式：

  ```xml
  <beans>    <import /></beans>
  ```

- 基本属性：

  ```xml
  <import resource=“config.xml"/>
  ```

 resource：加载的配置文件名

- Spring容器加载多个配置文件

  ```java
  new ClassPathXmlApplicationContext("config1.xml","config2.xml");
  ```

- Spring容器中的bean定义冲突问题

  - 同id的bean，后定义的覆盖先定义的
  - 导入配置文件可以理解为将导入的配置文件复制粘贴到对应位置
  - 导入配置文件的顺序与位置不同可能会导致最终程序运行结果不同



#### Spring相关API

**applicationContext接口**

**applicationContext** ：接口类型，代表应用上下文，可以通过其实例获得Spring容器中的Bean对象



**applicationContext实现类**

**ClassPathXmlApplicationContext** : 它是从类的根路径下加载配置文件，推荐使用这种

**FileSystemXmlApplicationContext** : 它是从磁盘路径上加载配置文件，配置文件可以在磁盘的任意位置

**AnnotationConfigApplicationContext** : 当使用注解配置容器对象时，需要使用此类来创建 spring 容器。它用来读取注解



**getBean()方法**

getBean("id") : 当参数的数据类型是字符串时，表示根据 Bean 的 id 从容器中获得Bean实例，返回是Object，需要强转。

getBean(Class) ：当参数的数据类型是Class字节码类型时，表示根据类型从容器中匹配Bean实例，当容器中相同类型的Bean有多个时，

则此方法会报错。



## Spring配置数据源

**使用连接池来配置数据源**

#### 数据源(连接池)的作用

- 数据源就是连接池
- 事先实例化数据源，初始化部分连接资源
- 使用连接资源时从数据源中获取
- 使用完毕后将连接资源归还给数据源
- 常见的数据源(连接池)：DBCP、C3P0、Druid等



#### 数据源的开发步骤

1. 导入数据源的坐标和数据库驱动坐标

   ```xml
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
       <version>5.1.47</version>
   </dependency>
   <dependency>
       <groupId>c3p0</groupId>
       <artifactId>c3p0</artifactId>
       <version>0.9.1.2</version>
   </dependency>
   <dependency>
       <groupId>com.alibaba</groupId>
       <artifactId>druid</artifactId>
       <version>1.1.10</version>
   </dependency>
   <dependency>
       <groupId>junit</groupId>
       <artifactId>junit</artifactId>
       <version>4.11</version>
   </dependency>
   <dependency>
       <groupId>org.springframework</groupId>
       <artifactId>spring-context</artifactId>
       <version>5.0.5.RELEASE</version>
   </dependency>
   ```

   

2. 在资源resources目录下新建`jdbc.properties`

   ```java
   jdbc.driver=com.mysql.jdbc.Driver
   jdbc.url=jdbc:mysql://localhost:3306/test
   jdbc.username=root
   jdbc.password=root
   ```

3. applicationContext.xml加载jdbc.properties配置文件获得连接信息

   - 首先引入context命名空间和约束路径

   - 命名空间()

     ```xml
     xmlns:context="http://www.springframework.org/schema/context"
     ```

   - 约束路径

     ```xml
     http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
     ```

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
   
   <!--    加载外部的properties文件-->
   <context:property-placeholder location="classpath:jdbc.properties"/>
   
   <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
       <property name="driverClass" value="${jdbc.driver}"></property>
       <property name="jdbcUrl" value="${jdbc.url}"></property>
       <property name="user" value="${jdbc.username}"></property>
       <property name="password" value="${jdbc.password}"></property>
   </bean>
   
   </beans>
   ```

4. 测试

```java
        @Test
        //Spring容器产生数据源对象 .xml文件配置bean
        public void test3() throws SQLException {
                ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
                DataSource dataSource = (DataSource) context.getBean("dataSource");
                Connection connection = dataSource.getConnection();
                connection.close();
        }
```



## Spring注解开发

Spring是轻代码而重配置的框架，配置比较繁重，影响开发效率，所以注解开发是一种趋势，注解代替xml配置文件可以简化配置，提高开发效率。

#### Spring原始注解

Spring原始注解主要是**替代Bean的配置**

```xml
<!--   使用Spring注解开发时让Spring知道使用了注解开发  配置组件扫描-->
    <context:component-scan base-package="service"/>
    <context:component-scan base-package="dao"/>
```

- 说明
  - 在进行包所扫描时，会对配置的包及其子包中所有文件进行扫描
  - 扫描过程是以文件夹递归迭代的形式进行的
  - 扫描过程仅读取合法的java文件
  - 扫描时仅读取spring可识别的注解
  - 扫描结束后会将可识别的有效注解转化为spring对应的资源加入IoC容器

- 注意
  - 无论是注解格式还是XML配置格式，最终都是将资源加载到IoC容器中，差别仅仅是数据读取方式不同
  - 从加载效率上来说注解优于XML配置文件

- 我们也可以开启属性注解支持，这样所有注解都可生效

```xml
<!--开启属性注解支持-->
<context: annotation-config/>
```



**原始注解**

| 注解           | 说明                                            |
| -------------- | ----------------------------------------------- |
| @Component     | 使用在类上个用于实例化Bean                      |
| @Controller    | 使用在web层类上用于实例化Bean                   |
| @Service       | 使用在service层类上用于实例化Bean               |
| @Repository    | 使用在dao层类上用于实例化Bean                   |
| @Autowired     | 使用在字段上上用于根据类型依赖注入              |
| @Qualifier     | 结合@Autowired一起使用用于根据名称进行依赖注入  |
| @Resource      | 相当于@Autowired + @Qualifier，按照名称进行注入 |
| @Value         | 注入普通属性                                    |
| @Scope         | 标注Bean的作用范围                              |
| @PostConstruct | 使用在方法上标注方法是Bean的初始化方法          |
| @PreDestroy    | 使用在方法上标注该方法是Bean的销毁方法          |

**注意：**

- 使用注解进行开发时，需要在applicationContext.xml中配置组件扫描，作用是指定哪个包及其子包下的Bean需要进行扫描以便识别使用注解配置的类、字段和方法

实际开发中，都会使用注解开发

##### Bean定义

- 名称：@Component 
- 类型：**类注解**
- 位置：**类定义上方**
- 作用：设置该类为spring管理的bean

```java
@Component
public class ClassName{}
```

- - @Controller、@Service 、@Repository是@Component的衍生注解，功能同@Component,在 web 开发中，会按照mvc三层架构分层！
    - dao层： `@Repository`
    - service层： `@Service`
    - controller层：`@Controller`

```
@Repository
public class ClassName{}

@Service
public class ClassName{}

@Controller
public class ClassName{}
```



**作用域注解**

使用`@Scope`标注Bean的范围

- 名称：`@Scope`

- 类型：**类注解**

- 位置：**类定义上方**

- 作用：设置该类作为bean对应的scope属性

- 范例：

  ```java
  //@Scope("prototype")
  //@Scope("singleton")
  public class ClassName{}
  ```

- 范围：prototype、singleton



**bean的生命周期**

- 名称：`@PostConstruct`(初始化方法)、`@PreDestroy(销毁方法)`
- 类型：**方法注解**
- 位置：**方法定义上方**
- 作用：设置该类作为bean对应的生命周期方法



**bean的非引用类型属性注入**

- 名称：`@Value`
- 类型：**属性注解、方法注解**
- 位置：**属性定义上方，方法定义上方**

- 作用：设置对应属性的值或对方法进行传参
- 说明：
  - value值仅支持非引用类型数据，赋值时对方法的所有参数全部赋值
  - value值支持读取properties文件中的属性值，通过类属性将properties中数据传入类中
  - @value注解如果添加在属性上方，可以省略set方法（set方法的目的是为属性赋值）

```java
@Component("userDao")
public class UserDaoImpl implements UserDao {
    @Value("注入普通数据")
    private String str;
    @Value("${jdbc.driver}")
    private String driver;
    
    @Override
    public void save() {
        System.out.println("save running...");
    }
}
```



**bean的引用类型属性注入（依赖注入(对象注入)）**

- 名称：`@Autowired`、`@Qualifier`
- 类型：**属性注解、方法注解**
- 位置：**属性定义上方，方法定义上方**

- 作用：设置对应属性的对象或对方法进行引用类型传参

- 范例：

  ```java
  	@Autowired
      //只使用@Autowired作为依赖注入
      //按照数据类型从Spring容器中进行匹配
  	@Qualifier("userDao")
      //结合@Autowired一起使用用于根据名称进行依赖注入
      @Resource(name = "userDao")
      //相当于@Autowired+@Qualifier结合
  private UserDao userDao;
  ```

- 说明：
  - @Autowired默认按类型装配，指定@Qualifier后可以指定自动装配的bean的id



##### Bean自动装配

1. Spring满足bean依赖的一种方式
2. Spring会在上下文中自动寻找，并自动给bean装配属性



在Spirng中由三种装配方式

1. 在xml中显示的配置(**手动装配**)
2. 在java中显示配置(**注解**)
3. 隐士的自动装配备案(**自动装配**)



**测试环境搭配**

1. 定义两个动物类cat 和dog以及一个people类

   ```xml
    <bean id="cat" class="com.kuang.pojo.Cat" />
       <bean id="dog" class="com.kuang.pojo.Dog" />
       
       <bean id="people" class="com.kuang.pojo.People" >
           <property name="cat" ref="cat" />
           <property name="dog" ref="dog" />
       </bean>
   ```

   这种是手动装配的过程

2. 通过**byName**来编写配置文件

   ```xml
   <!--    自动装配-->
       <bean id="cat" class="pojo.cat"></bean>
       <bean id="dog" class="pojo.dog"></bean>
   
   <!--    byName:会自动在容器上下文中查找，和要查找的对象中set方法后面的值对应的bean的id-->
       <bean id="people" clasxmls="pojo.people" autowire="byName">
       </bean>
   ```

    弊端:若bean中的id的名称和对应set方法后名字不同,就会找不到.

   **需要保证所有的 bean 的 id 唯一，并且这个 bean 需要和自动注入的属性的 set 方法的值一致！**

3. 通过**byType**来编写配置文件

   ```xml
     <bean id="cat" class="pojo.cat"></bean>
     <bean id="dog" class="pojo.dog"></bean>
     
    <!--    byType:会自动在容器上下文中查找，和要查找的对象中类型相同的bean-->
       <bean id="people" class="pojo.people" autowire="byType">
       </bean>
   ```

   弊端:若由多个同类型的bean,就无法找到

   **需要保证所有的 bean 的 class 唯一，并且这个 bean 需要和自动注入的属性的类型一致！**



**使用注解进行自动装配**

@**Autowired(required)**

- 按照类型自动注入依赖
- 能够在属性中使用,也可以使用在set方法上(使用了@**Autowired**后就可以省略set方法了)

@Autowired注解中有一个属性:**required属性**

required

- true:表明不可以为null
- false:表明可以为null

@**Qualifier(value)**

- 不能单独使用
- 一般配合@Autowired一起使用,可以根据**名称**方式自动装配



@**Resource(name)**

相当于@Autowired单独使用+@Autowired和@Qualifier联合使用.

先是根据名称(**byName**)查找,再根据类型(**byType**)查找,若都不成功则报异常



#### Spring新注解

使用上面的注解还不能全部替代xml配置文件，还需要使用注解替代的配置如下：

- 非自定义的Bean的配置：`<bean>`
- 加载properties文件的配置：`context:property-placeholder`
- 组件扫描的配置：`<context:component-scan>`
- 引入其他文件：`<import>`

| 注解            | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| @Configuration  | 用于指定当前类是一个Spring配置类，当创建容器时会从该类上加载注解 |
| @ComponentScan  | 用于指定Spring在初始化容器时要扫描的包。等价于`<context:component-scan base-package="com.itheima"/>` |
| @Bean           | 使用在方法上，标注将该方法的返回值存储到Spring               |
| @PropertySource | 用于加载.properties文件中的配置                              |
| @Import         | 用于导入其他配置类                                           |



**加载properties文件**

- 名称：`@PropertySource`
- 类型：**类注解**
- 位置：**类定义上方**
- 作用：加载properties文件中的属性值

```java
@PropertySource(value = "classpath:jdbc.properties")
public class SpringConfiguration {
    @Value("${jdbc.driver}")
    private String driver;

    @Value("${jdbc.url}")
    private String url;
}
```

**纯注解格式**

- 名称：@Configuration、@ComponentScan
- 类型：**类注解**
- 位置：**类定义上方**
- 作用：设置当前类为spring核心配置加载类

```java
//标志该类是Spring的核心配置
//使用类来替代xml配置
//使用注解替代Bean配置
@Configuration
//包扫描
@ComponentScan({"service","dao"})
public class SpringConfiguration {
}
```

- 说明：
  - 核心配合类用于替换spring核心配置文件，此类可以设置空的，不设置变量与属性
  - bean扫描工作使用注解@ComponentScan替代

**AnnotationConfigApplicationContext**

- 加载纯注解格式上下文对象，需要使用AnnotationConfigApplicationContext

```java
                ApplicationContext applicationContext = new AnnotationConfigApplicationContext(SpringConfiguration.class);
```



**第三方bean配置与管理**

- 名称：`@Import`
- 类型：**类注解**
- 位置：**类定义上方**
- 作用：导入第三方bean作为spring控制的资源

```java
//引入其他配置
@Import(dataSourceConfiguration.class)
public class SpringConfiguration {
}
```

- 说明：
  - @Import注解在同一个类上，仅允许添加一次，如果需要导入多个，使用数组的形式进行设定
  - 在被导入的类中可以继续使用@Import导入其他资源（了解）
  - @Bean所在的类可以使用导入的形式进入spring容器，无需声明为bean



将之前使用Bean配置的xml用纯注解替代

**配置类**

```java
package config;


import com.mchange.v2.c3p0.ComboPooledDataSource;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.*;

import javax.sql.DataSource;
import java.beans.PropertyVetoException;
import java.sql.Connection;

//标志该类是Spring的核心配置
//使用类来替代xml配置
//使用注解替代Bean配置
@Configuration
//包扫描
@ComponentScan({"service","dao"})
//<!--    加载外部的properties文件-->
//<context:property-placeholder location="classpath:jdbc.properties"/>
@PropertySource(value = "classpath:jdbc.properties")
//引入其他配置
@Import(dataSourceConfiguration.class)
public class SpringConfiguration {

    @Value("${jdbc.driver}")
    private String driver;

    @Value("${jdbc.url}")
    private String url;

    @Value("${jdbc.username}")
    private String username;

    @Value("${jdbc.password}")
    private String password;

    //以指定名称该方法的返回值存入Spring容器中
    @Bean("dataSource")
    public DataSource getDataSource() throws PropertyVetoException {
        //创建数据源
        ComboPooledDataSource dataSource = new ComboPooledDataSource();
        //设置连接参数
        dataSource.setDriverClass(driver);
        dataSource.setJdbcUrl(url);
        dataSource.setUser(username);
        dataSource.setPassword(password);
        return dataSource;
    }
}
```

**测试类**

```java
        //使用新注解(纯注解)来替代xml配置文件
        @Test
        public void test4() throws SQLException {
                ApplicationContext applicationContext = new AnnotationConfigApplicationContext(SpringConfiguration.class);
                DataSource dataSource = (DataSource) applicationContext.getBean("dataSource");
                Connection connection = dataSource.getConnection();
                connection.close();

                UserService userService = applicationContext.getBean(UserService.class);
                userService.save();
        }
```



#### Spring集成Junit

##### 原始Junit测试Spring问题

在测试类中，每个测试方法都有以下两行代码：

```java
ApplicationContext app = new ClasspathXmlApplicationContext("xml文件");
app.getBean("id");
```

比较繁琐，并且如果忽略会报空指针异常

**解决思路**：

- 让 SpringJunit 负责创建Spring容器，但是需要将配置文件的名称告诉它
- 将需要进行测试Bean直接在测试类中进行注入



##### 步骤

- 导入spring集成junit的坐标

```xml
<!--此处需要注意的是，spring5 及以上版本要求 junit 的版本必须是 4.12 及以上-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>5.0.2.RELEASE</version>
</dependency>
```



使用`@RunWith`注解替换原来的运行期

```java
@RunWith(SpringJUnit4ClassRunner.class)
public class SpringJunitTest {
    
}

```

使用`@ContextConfiguration`指定配置文件或配置类

```java
@RunWith(SpringJUnit4ClassRunner.class)
//加载spring核心配置文件
//@ContextConfiguration(value = {"classpath:applicationContext.xml"})
//加载spring核心配置类
@ContextConfiguration(classes = {SpringConfiguration.class})
public class SpringJunitTest {
    
}
```

使用`@Autowired`注入需要测试的对象

```java
@RunWith(SpringJUnit4ClassRunner.class)
//加载spring核心配置类
@ContextConfiguration(classes = {SpringConfiguration.class})
public class SpringJunitTest {
    @Autowired
    private UserService userService;
}
```





## Spirng AOP

##### AOP概念

AOP(Aspect Oriented Programming)  **面向切面编程**

通过**预编译方式**和**运行期动态代理**实现程序功能的统一维护的一种技术

AOP是**OOP**的延续，是软件开发中的一个热点，也是Spring框架中的一个重要内容，是函数式编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的**耦合度降低**，提高程序的可重用性，同时提高了开发的效率。


##### AOP的作用及其优势

- 在程序运行期间，在不修改源码的情况下对方法进行功能增强
- 减少重复代码，提高开发效率，并且便于维护

例如：

代码执行过程中，需要进行当前状态的记录并且打印出来。

日志记录、打印功能为一个单独模块

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210811155333084.png" alt="image-20210811155333084" style="zoom:50%;" />

业务代码功能为一个单独模块

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210811155428811.png" alt="image-20210811155428811" style="zoom:50%;" />

通过配置文件将两个模块关联到一起，单独看它们都是独立的存在，互不影响。

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210811155638418.png" alt="image-20210811155638418" style="zoom:50%;" />

<img src="https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210811155938687.png" alt="image-20210811155938687" style="zoom:50%;" />

##### AOP底层实现

实际上，AOP的底层是通过Spring提供的的**动态代理技术**实现的。在**运行期间**，Spring通过动态代理技术动态的生成**代理对象**，**代理对象方法执行时进行增强功能的介入**，在去**调用目标对象的方法**，从而完成功能的增强。



##### AOP动态代理技术

常用动态代理技术

- JKD代理：基于**接口**的动态代理技术
- Cglib代理：基于**父类**的动态代理技术

![image-20210811160958882](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210811160958882.png)



**JDK动态代理**

下面是实现过程，这里是需要做一个了解，因为AOP对应的底层已经完成了。

```java
public class Enhance {

    public void before(){
        System.out.println("前置增强模拟");
    }

    public void after(){
        System.out.println("后置增强模拟");
    }
}
//模拟：增强方法
```

```java
//基于接口
public interface Target {

   void save();
}

public class TargetImpl  implements Target {
    @Override
    public void save() {
        System.out.println("基于接口的JDK代理技术动态生成代理对象，由代理对象调用save方法");
    }
}
```

```java
    //实现
    public static void main(String[] args) {

        final Enhance enhance = new Enhance();
        final TargetImpl target = new TargetImpl();

        // 返回值 动态生成的代理对象
        //基于JDK代理技术:基于接口，因此动态生成的代理对象使用接口来对接
        Target  proxyInstance= (Target) Proxy.newProxyInstance(
                //目标类加载器
                target.getClass().getClassLoader(),
                //目标对象相同的接口字节码对象数组
                target.getClass().getInterfaces(),
                new InvocationHandler() {
                    /**
                     * 调用代理对象的任何方法 实质上执行的都是invoke方法
                     * @param proxy 代理对象
                     * @param method 目标方法
                     * @param args
                     * @return
                     * @throws Throwable
                     */
                    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                        //方法增强
                        enhance.before();
                        //执行目标方法,这里invoke不是上面代理对象的invoke方法，而是反射中的方法
                        method.invoke(target,args);
                        enhance.after();
                        return null;
                    }
                }
        );

        //调用代理对象的方法，实质调用invoke方法
        proxyInstance.save();

    }
/*
前置增强模拟
基于接口的JDK代理技术动态生成代理对象，由代理对象调用save方法
后置增强模拟
*/
```



**cglib的动态代理**

```java
    public static void main(final String[] args) {
         final Enhance enhance = new Enhance();
        final TargetImpl target = new TargetImpl();

        // 返回值 动态生成的代理对象
        //基于cglib代理

        //1.创建增强器
        Enhancer enhancer = new Enhancer();

        //2.设置父类(目标)
        enhancer.setSuperclass(TargetImpl.class);


        //3.设置回调
        enhancer.setCallback(new MethodInterceptor() {
            @Override
            public Object intercept(Object proxy, Method method, Object[] objects, MethodProxy methodProxy) throws Throwable {
                //执行前置
                enhance.before();

                //执行目标
                method.invoke(target,args);

                //执行后置
                enhance.after();
                return null;
            }
        });

        //4.创建代理对象
        TargetImpl target1 = (TargetImpl) enhancer.create();

        target1.save();

    }

/*
前置增强模拟
基于接口的cglib代理技术动态生成代理对象，由代理对象调用save方法
后置增强模拟
*/
```

上面都是一个理解，Spring AOP模式下都已经封装完成，需要做的只是在配置文件中做配置即可。



##### AOP相关概念

Spring的AOP实现底层就是对上面的动态代理的代码进行了封装，封装后我们只需要对需要关注的部分进行代码编写，并通过配置的方式完成指定目标的方法增强。

在正式讲解AOP的操作之前，我们必须理解AOP的相关术语，常用的术语如下:

- **Target (目标对象)** :代理的目标对象

- **Proxy (代理)** : 一个类被AOP织入增强后，就产生一个结果代理类

- **Joinpoint (连接点)** :所谓连接点是指那些被拦截到的点(**方法**)。在spring中,这些点指的是方法,因为spring只支持方法类型的连接点。**能够被增强的方法就叫做连接点**(每个公民都可以成为人大代表)

- **Pointcut(切入点)**：**对于连接点进行拦截的定义**（被选择成为人大代表的公民）

- **Advice(通知/增强)**：拦截到连接点之后要做的事情

- **Aspect(切面)**：切点+增强(通知) == 目标方法 + 增强

- **Weaving(织入)**:  把增强应用到目标对象来创建新的代理对象的过程。**切点 和通知 结合到一起的过程。**



##### AOP开发明确的事项

1. **需要编写的内容**

   - 编写核心业务代码(目标类的目标方法)
   - **编写切面类，**切面类中通知(增强功能方法)
   - 在配置文件中，配置织入关系，即将哪些通知与哪些连接点进行结合

2. **AOP技术实现的内容**

   Spring框架监控切入点方法的执行。一旦监控到切入点方法被运行，使用代理机制，动态创建目标对象的代理对象，根据通知类别，在代理对象的对应位置，将通知对应的功能织入，完成完整的代码逻辑运行。

3. **AOP底层中的代理方式**

   在Spring中，框架会根据目标类是否实现了接口来决定采用哪种动态代理的方式





#### 基于XML的AOP的开发

**快速入门**

①导入AOP相关坐标

```xml
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.0.5.RELEASE</version>
        </dependency>
        
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.8.10</version>
        </dependency>
```

②创建目标接口和目标类(内部有切点)

```java
public interface Target {

   void save();
}
public class TargetImpl implements Target {
    @Override
    public void save() {
        System.out.println("基于XML配置文件实现AOP");
    }
}
```

③创建切面类(内部有增强方法)

```java
public class Aspect {

    //前置增强
    public void before(){
        System.out.println("前置增强");
    }
}
```

④将目标类和切面类的对象创建权交给spring

```xml
<!--    目标对象:切点-->
<bean class="AOP.impl.TargetImpl"></bean>
<!--    切面对象:通知-->
    <bean id="aspect" class="AOP.impl.Aspect"></bean>
```

⑤在applicationC ontext.xml中配置织入关系

```xml
<!--    配置织入:告诉Spring框架哪些方法(切点)需要进行增强(通知)-->
    <aop:config>
<!--        声明切面-->
        <aop:aspect ref="aspect">
<!--            对应方法(切点)的前置增强-->
            <aop:before method="before" pointcut="execution(public void AOP.impl.TargetImpl.save())"/>
        </aop:aspect>
    </aop:config>
```

⑥测试代码

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class test2 {

    @Autowired
    private Target target;

    @Test
    public void test1(){
        target.save();
    }
}
```





1. **切点表达式的写法**

   ```xml
               <aop:before method="before" pointcut="execution(public void AOP.impl.TargetImpl.save())"/>
   ```

   表达式语法:
   **execution**([修饰符] 返回值类型 包名.类名.方法名(参数))

   - 访问修饰符可以省略
   - 返回值类型、包名、类名、方法名可以使用星号*****代表任意
   - 包名与类名之间**一个点 .**代表当前包下的类，**两个点..**表示当前包及其子包下的类
   - 参数列表可以使用**两个点..**表示任意个数，任意类型的参数列表

   ```java
   //例如:
   execut ion (public void com.ithema.aop.Target.method())
   execution(void com.itheima.aop.Target.*(..))
   //Target类下的 void类型的任意方法任意参数
   execution(* com. itheima.aop.*.*(..))
   //aop包下的任意类中任意方法任意参数都是切点
   execution(* com.itheima.aop..*.*(..))
    //aop包以及子包下的任意类中任意方法任意参数都是切点
   execution(* *..*.*(..))
   //所有
   ```

2.  **通知类型**

   通知的配置语法:

   ```
   <aop:通知类型 method=“切面类中方法名” pointcut= “切点表达式"> </aop:通知类型>
   ```

   ![image-20210813153444293](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210813153444293.png)

   ```xml
   <!--    配置织入:告诉Spring框架哪些方法(切点)需要进行增强(通知)-->
       <aop:config>
   <!--        声明切面-->
           <aop:aspect ref="aspect">
   <!--            对应方法(切点)的前置增强-->
   <!--            <aop:before method="before" pointcut="execution(public void AOP.impl.TargetImpl.save())"/>-->
                   <aop:around method="around" pointcut="execution(* AOP.impl.*.*(..))"></aop:around>
               <aop:after-throwing method="afterThrowing" pointcut="execution(* AOP.impl.*.*(..))"></aop:after-throwing>
               <aop:after method="after" pointcut="execution(* AOP.impl.*.*(..))"></aop:after>
           </aop:aspect>
       </aop:config>
   ```

3. **切点表达的抽取**

   ```xml
   <!--            抽取表达式-->
               <aop:pointcut id="pointCut" expression="execution(* AOP.impl.*.*(..))"/>
               <aop:around method="around" pointcut-ref="pointCut"></aop:around>
               <aop:after-throwing method="afterThrowing" pointcut-ref="pointCut"></aop:after-throwing>
               <aop:after method="after"  pointcut-ref="pointCut"></aop:after>
   ```



#### 基于注解的AOP开发

①创建目标接口和目标类(内部有切点)

②创建切面类(内部有增强方法)

③将目标类和切面类的对象创建权交给spring

```java
@Component
public class TargetImpl implements Target {
    @Override
    public void save()  {
        System.out.println("基于XML配置文件实现AOP");
        int i = 6;
//        if (i > 5){
//             i = i /0;
//        }
    }
}
```

④在切面类中使用注解配置织入关系

```java
@Component("aspect")
//标注当前类是一个通知类
@Aspect
public class MyAspect {

    //前置增强
    @Before("execution(* annoation.TargetImpl.*(..))")
    public void before(){
        System.out.println("前置增强");
    }


    //后置增强
    @AfterReturning("execution(* annoation.TargetImpl.*(..))")
    public void afterReturning(){
        System.out.println("后置通知");
    }

    //ProceedingJoinPoint： 正在执行的连接点===切点
    @Around("execution(* annoation.TargetImpl.*(..))")
    public void around(ProceedingJoinPoint joinPoint) throws Throwable {
        System.out.println("环绕前");
        Object object = joinPoint.proceed();
        System.out.println("环绕后");
    }

    @AfterThrowing("execution(* annoation.TargetImpl.*(..))")
    public void afterThrowing(){
        System.out.println("抛出异常");

    }


    //最终通知
    @After("execution(* annoation.TargetImpl.*(..))")
    public void after(){
        System.out.println("最终通知");
    }

}

```

⑤在配置文件中开启组件扫描和AOP的自动代理

```jxml
<!--    组件扫描-->
        <context:component-scan base-package="annoation"/>
<!--        AOP自动代理-->
        <aop:aspectj-autoproxy/>

```

⑥测试

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class annoationTest {

    @Autowired
    private Target target;

    @Test
    public void test() {
        target.save();
    }
}
```



**注解通知类型**

![image-20210813164044865](https://gitee.com/zhanghui2233/image-storage-warehouse/raw/master/img//image-20210813164044865.png)



**注解切点表达式的抽取**

同xml配置AOP一样，注解也可以将表达式进行抽取。

使用**@Pointcut注解进行抽取**

```java
 //定义切点表达
    @Pointcut("execution(* annoation.TargetImpl.*(..))")
    public void  pointCut(){

    }

    //前置增强
    @Before("pointCut()")
    public void before(){
        System.out.println("前置增强");
    }


    //后置增强
    @AfterReturning("pointCut()")
    public void afterReturning(){
        System.out.println("后置通知");
    }

    //ProceedingJoinPoint： 正在执行的连接点===切点
    @Around("pointCut()")
    public void around(ProceedingJoinPoint joinPoint) throws Throwable {
        System.out.println("环绕前");
        Object object = joinPoint.proceed();
        System.out.println("环绕后");
    }

    @AfterThrowing("pointCut()")
    public void afterThrowing(){
        System.out.println("抛出异常");

    }


    //最终通知
    @After("pointCut()")
    public void after(){
        System.out.println("最终通知");
    }
```



