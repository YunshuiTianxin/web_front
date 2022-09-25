# Spring(5)

## 1.[为什么](https://spring.io/why-spring)要使用Spring

> Spring makes programming Java quicker, easier, and safer for everybody. Spring’s focus on speed, simplicity, and productivity has made it the [world's most popular](https://snyk.io/blog/jvm-ecosystem-report-2018-platform-application/) Java framework.

- 解决企业应用开发的复杂性

## 2.什么是Spring

- Spring是一个**轻量级**的开源的JavaEE的框架
- 由[Rod Johnson](https://baike.baidu.com/item/Rod Johnson/1423612)发起，是针对bean的生命周期进行管理的轻量级容器（lightweight container）
- Spring框架的组成
- ![image-20210111224535111](https://jayoss.oss-cn-beijing.aliyuncs.com/images/image-20210111224535111.png)
- Spring中的两个核心技术：**IOC**、**AOP**
  - 控制反转(IoC：Inversion of Control ) /依赖注入(DI：Dependency Injection )
  - 面向切面编程(AOP：Aspect Oriented Programming)
- 优点：
  - 1、低侵入式设计：非入侵式设计，基于Spring开发的应用一般不依赖于Spring的类
  - 2、独立于各种应用服务器，真正实现：一次编写，到处运行。
  - 3、Spring的依赖注入特性使Bean与Bean之间的依赖关系变的完全透明，降低了耦合度：使用IOC容器，将对象之间的依赖关系交给Spring，降低组件之间的耦合性，让我们更专注于应用逻辑
  - 4、面向切面编程特性允许将一些通用任务如安全、事务、日志等进行集中式处理
  - 5、提供了与第三方持久层框架的良好整合，并简化了底层数据库访问
  - 6、高度的开放性（可以和Struts2、Hibernate、MyBatis、CXF等很多主流第三方框架无缝整合）

## 3.如何使用
maven配置上课已经演示 不再赘述


4. 定义普通类

   ```java
   public class Person {
       public void speak(){
           System.out.println("xxx说话。。。。");
       }
   ```

5. 创建Spring配置文件，在配置文件中创建对象

![image-20210111232221759](https://jayoss.oss-cn-beijing.aliyuncs.com/images/image-20210111232221759.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--配置一个创建Person对象的bean-->
    <bean id="person" class="com.iweb.spring5.Person"></bean>
</beans>
```

6. 编写测试代码（单元测试）

   ```java
   public class TestSpring5 {
       @Test
       public void testPserson(){
           // 1.加载配置文件
           ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
           // 2.获取配置文件中的对象
           Person person = context.getBean("person", Person.class);
           person.speak();
       }
   }
   ```

7. 报错

   ```
   java.lang.NoClassDefFoundError: org/apache/commons/logging/LogFactory
   ```

8. [下载](https://mvnrepository.com/)并导入日志的依赖包commons-logging, 然后再次运行：

   ![image-20210111234216789](https://jayoss.oss-cn-beijing.aliyuncs.com/images/image-20210111234216789.png)



## 4.IOC/DI**控制反转** **/** 依赖注入

- 控制反转（Inversion of Control，缩写为IoC），是面向对象编程中的一种**设计原则**，可以用来降低计算机代码之间的耦合度。
- 其中最常见的方式叫做依赖注入（Dependency Injection，简称DI）
- 在传统的程序设计过程中，通常由调用者来**创建被调用者**的实例。但是在spring里，创建被调用者的工作**不再**由调用者来完成。创建被调用者实例的工作通常由spring容器来完成，然后注入给调用者，称为控制反转，也称为依赖注入。这样给程序带来很大的灵活性，这样也实现了我们的接口和实现的分离。

    - 将组件对象的控制权从代码本身转移到外部容器
    - 组件化的思想：分离关注点，使用接口，不再关注实现

 IOC底层原理：

- xml解析
- 简单工厂
- 反射

演示示例：传统方式下的对象与对象之间的紧耦合：

```java
public class Person {
    private Cat cat;
    public Cat getCat() {return cat;}
    public void setCat(Cat cat) {
        this.cat = cat;
    }
    /**
     * 撸猫
     */
    public void luCat() {
        System.out.println("终于下班到家了，好累，撸撸猫减压。。");
        cat.purr();
    }
    public void speak() {
        System.out.println("speak....");
    }
}
```

```java
public class Cat {
    private String name;
    private String type;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public void miaow(){
        System.out.println("喵喵喵");
    }
    public void purr(){
        System.out.println("咕噜咕噜。。。。。");
    }
}
```

```java
// 测试代码
Person person = new Person();
Cat cat = new Cat();
// person对象与cat对象之间是紧耦合关系
person.setCat(cat);
person.luCat();
```



IOC底层分析：

- IOC思想基于IOC容器实现，IOC容器底层使用了对象工厂
- IOC容器的实现有两种方式：
    - **BeanFactory**  是IOC容器的基本实现，是Spring内部使用的接口，不提供给开发人员使用，该容器加载配置文件时，不会创建对象，在获取（使用）对象时，才去创建对象。
    - ApplicationContext，BeanFactory的子接口，提供更多强大的功能，一般由开发人员使用。该容器在加载配置文件时，就会创建配置的对象。
- 使用Application获取Bean的结果：

![image-20210112152951529](https://jayoss.oss-cn-beijing.aliyuncs.com/imagesimage-20210112152951529.png)

​	PS: 如果是多实例模式，ApplicationContext则会在在获取（使用）对象时，才去创建对象。

```java
@Test
public void testPerson() {
    //BeanFactory context = new ClassPathXmlApplicationContext("bean1.xml");
    BeanFactory context = new XmlBeanFactory(new ClassPathResource("bean1.xml"));
    Person person = context.getBean("person", Person.class);
    Person person2 = context.getBean("person", Person.class);
    System.out.println(person);
    System.out.println(person2);
    person.speak();
}
```

- 使用BeanFactory获取bean的结果:

![image-20210112154235295](https://jayoss.oss-cn-beijing.aliyuncs.com/imagesimage-20210112154235295.png)

## 5.Spring的Bean管理

Spring的Bean管理，主要管理bean的两种操作

- bean的创建
- 属性值的注入

操作方式：

- 基于xml配置方式
- 基于注解操作方式

### 5.1 基于xml配置方式创建bean

```xml
<bean id="person" class="com.iweb.spring5.Person"></bean>
```

id属性：对象的唯一标示，通过标示获取对象的实例

class属性：对象所对应的类的完全限定名

scope属性：取值prototype/singleton

**PS:使用上述方式创建对象时，要保证类中有无参构造方法。**

### 5.2 基于xml配置方式注入属性值

- DI，依赖注入，即 注入属性，主要分为设值注入与构造注入。

#### 5.2.1 设值注入

```java
public class Cat {
    public Cat() {}
    // 构造注入name值
    public Cat(String name) {
        this.name = name;
    }
    private String name;
    private String type;
    public String getName() {
        return name;
    }
    // set注入name值
    public void setName(String name) {
        this.name = name;
    }
    public String getType() {
        return type;
    }
    public void setType(String type) {
        this.type = type;
    }
    public void miaow(){
        System.out.println(this.name + ":喵喵喵~~~");
    }
    public void purr(){
        System.out.println(this.name + ":咕噜咕噜~~~");
    }
}
```

```xml
<bean id="cat" class="com.iweb.spring5.Cat">
    <property name="name" value="tom"/>
    <property name="type" value="加菲"/>
</bean>
```

```java
@Test
public void testCat(){
    // 1.加载配置文件
    ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
    // 2.获取配置文件中的对象
    Cat cat = context.getBean("cat", Cat.class);
    System.out.println(cat);
}
```

![image-20210113110645529](https://jayoss.oss-cn-beijing.aliyuncs.com/imagesimage-20210113110645529.png)

#### 5.2.2 构造注入

```xml
<bean id="cat" class="com.iweb.spring5.Cat">
    <constructor-arg name="name" value="tom" />
</bean>
```

其他代码不变，运行结果：

![image-20210113111952437](https://jayoss.oss-cn-beijing.aliyuncs.com/imagesimage-20210113111952437.png)

#### 5.2.3 p名称空间注入（简化写法）

1. 添加p名称空间的约束

    ```xml
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:p="http://www.springframework.org/schema/p"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    ```

2. 在bean中直接使用p属性

    ```xml
    <bean id="cat" class="com.iweb.spring5.Cat" p:name="tom" p:type="加菲"></bean>
    ```

#### 5.2.4 注入空值

```xml
<bean id="cat" class="com.iweb.spring5.Cat">
    <property name="name">
        <null/>
    </property>
</bean>
```

#### 5.2.5 注入特殊符号

```xml
<bean id="cat" class="com.iweb.spring5.Cat">
    <property name="name">
        <value><![CDATA[>-_-<]]></value>
    </property>
</bean>
```

```json
Cat{name='>-_-<', type='null'}
```

#### 5.2.6 注入外部bean

```xml
<bean id="person" class="com.iweb.spring5.Person">
    <property name="cat" ref="cat"/>
</bean>
<bean id="cat" class="com.iweb.spring5.Cat">
    <property name="name">
        <value><![CDATA[>-_-<]]></value>
    </property>
</bean>
```

```java
@Test
public void testPserson(){
    // 1.加载配置文件
    ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
    // 2.获取配置文件中的对象
    Person person = context.getBean("person", Person.class);
    person.luCat();
}
```

运行结果：

```
终于下班到家了，好累，撸撸猫减压。。
>-_-<:咕噜咕噜。。。。。
```

#### 5.2.7 注入内部bean

内部bean只在某个bean的内部可以访问，外部的其他bean无法访问它。

```xml
<bean id="person" class="com.iweb.spring5.Person">
    <property name="cat">
        <bean class="com.iweb.spring5.Cat">
            <property name="name">
                <value><![CDATA[>-_-<]]></value>
            </property>
        </bean>
    </property>
</bean>
```

```java
@Test
/**
  * 测试注入内部bean
  */
public void testPserson1(){
    // 1.加载配置文件
    ApplicationContext context = new ClassPathXmlApplicationContext("bean2.xml");
    // 2.获取配置文件中的对象
    Person person = context.getBean("person", Person.class);
    person.luCat();
}
```

#### 5.2.8 级联赋值

```xml
<bean id="person" class="com.iweb.spring5.Person">
    <property name="cat" ref="cat"/>
    <property name="cat.type" value="波斯猫"/>
</bean>
<bean id="cat" class="com.iweb.spring5.Cat">
    <property name="name">
        <value><![CDATA[>-_-<]]></value>
    </property>
</bean>
```

PS: 级联赋值要保证对应的属性有setter

#### 5.2.9 注入集合

```java
// Person类的部分属性
private String[] catNameArray;
private List<String> catNameList;
private Map<String, String> catNameMap;
private Set<String> catNameSet;
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--   级联赋值-->
    <bean id="person" class="com.iweb.spring5.Person">
        <property name="cat" ref="cat"/>
        <property name="cat.type" value="波斯猫"/>
        <!--        注入数组-->
        <property name="catNameArray">
            <array>
                <value>tom</value>
                <value>jerry</value>
                <value>kitty</value>
            </array>
        </property>
        <!--        注入List-->
        <property name="catNameList">
            <list>
                <value>tom</value>
                <value>jerry</value>
                <value>kitty</value>
            </list>
        </property>
        <!--        注入map-->
        <property name="catNameMap">
            <map>
                <entry key="tom" value="汤姆"/>
                <entry key="jerry" value="杰瑞"/>
                <entry key="kitty" value="凯蒂"/>
            </map>
        </property>
        <property name="catNameSet">
            <set>
                <value>tom</value>
                <value>jerry</value>
                <value>kitty</value>
            </set>
        </property>
    </bean>
    <bean id="cat" class="com.iweb.spring5.Cat">
        <property name="name">
            <value><![CDATA[>-_-<]]></value>
        </property>
        <property name="age" value="2"/>
    </bean>
</beans>
```

```java
@Test
/**
     * 测试注入集合
     */
public void testPserson4() {
    // 1.加载配置文件
    ApplicationContext context = new ClassPathXmlApplicationContext("bean4.xml");
    // 2.获取配置文件中的对象
    Person person = context.getBean("person", Person.class);
    person.luCat();
    for (int i = 0; i < person.getCatNameArray().length; i++) {
        System.out.println(person.getCatNameArray()[i]);
    }
    System.out.println(person.getCatNameList());
    for (Map.Entry<String, String> entry : person.getCatNameMap().entrySet()) {
        System.out.println(entry.getKey() + ":" + entry.getValue());
    }
    // java8 lambda的写法
    person.getCatNameMap().entrySet().forEach(item -> {
        System.out.println(item.getKey() + ":" + item.getValue());
    });
}
```

#### 5.2.10 注入外部集合

1. 添加util名称空间

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:util="http://www.springframework.org/schema/util"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd">
   ```

2. 配置并注入外部集合

   ```xml
   <!--注入外部集合-->
   <bean id="person" class="com.iweb.spring5.Person">
       <property name="catNameList" ref="catNameList"/>
   </bean>
   <!--配置独立外部集合-->
   <util:list id="catNameList">
       <value>tom</value>
       <value>jerry</value>
       <value>kitty</value>
   </util:list>
   ```

3. 测试

   ```java
   @Test
   /**
        * 测试注入外部集合
        */
   public void testPerson5(){
       ApplicationContext context = new ClassPathXmlApplicationContext("bean5.xml");
       Person person = context.getBean("person", Person.class);
       System.out.println(person.getCatNameList());
   }
   ```

   运行结果：

   ```
   [tom, jerry, kitty]
   ```







## 10.加载外部配置文件

本小节以配置**德鲁伊druid**连接池为例，演示如何加载外部配置文件

操作步骤：

1. 导入druid的jar包

2. 在xml文件中配置druid对应的bean

   ```xml
   <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
       <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"></property>
       <property name="url" value="jdbc:mysql://192.168.200.6:3306/littlemall?useUnicode=true&amp;characterEncoding=utf-8&amp;serverTimezone=UTC"></property>
       <property name="username" value="root"></property>
       <property name="password" value="123456"></property>
   </bean>
   ```

3. 使用外部配置文件改进bean的配置

   - 创建db.properties保存连接数据库的配置信息

     ```
     jdbc.url=jdbc:mysql://192.168.200.6:3306/littlemall?useUnicode=true&amp;characterEncoding=utf-8&amp;serverTimezone=UTC
     jdbc.driver=com.mysql.cj.jdbc.Driver
     jdbc.username=com.mysql.cj.jdbc.Driver
     jdbc.password=123456
     ```

   - 在xml文件中配置context上下文名称空间，以加载外部配置文件

     ```xml
     <beans xmlns="http://www.springframework.org/schema/beans"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:context="http://www.springframework.org/schema/context"
            xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                                http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
     ```

   - 在xml文件中加载外部配置文件

     ``` xml
     <context:property-placeholder location="classpath:db.properties" />
     ```

   - 使用表达式占位符获取外部配置文件中的值

     ```xml
     <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
         <property name="driverClassName" value="${jdbc.driver}"></property>
         <property name="url" value="${jdbc.url}"></property>
         <property name="username" value="${jdbc.username}"></property>
         <property name="password" value="${jdbc.password}"></property>
     </bean>
     ```

   PS: 完整配置文件如下：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
       <!--    导入外部配置文件-->
       <context:property-placeholder location="classpath:db.properties" />
       <!--    配置druid连接池-->
       <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
           <property name="driverClassName" value="${jdbc.driver}"></property>
           <property name="url" value="${jdbc.url}"></property>
           <property name="username" value="${jdbc.username}"></property>
           <property name="password" value="${jdbc.password}"></property>
       </bean>
   </beans>
   ```

## 11.基于注解方式创建Bean

- 目的：简化配置的操作

- 定义：是代码的一种特殊标记，语法格式为

  ```java
  @注解名称(属性名=属性值,属性名=属性值)
  ```

- 使用场景：用于类上、方法上、属性上

Spring容器对于管理的Bean提供了四种注解, 这四种注解功能一致，都可以创建Bean：

- @Component    普通注解，可以创建Bean
- @Service    Service注解，一般用于Service层的bean
- @Controller    Controller注解，一般用于控制器层的Bean
- @Repository    Repository注解，一般用于Dao层

**使用步骤：**

1. 导入aop依赖包--spring-aop-5.3.2.jar

2. 配置xml文件的上下文名称空间context，以便Spring容器扫描要管理的的Bean

    ```xml
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:context="http://www.springframework.org/schema/context"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                               http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    
    </beans>
    ```

3. 开启组件(包)的扫描，以便Spring容器扫描到管理的的Bean

   PS: 多个包之间用英文逗号隔开，也可以配置扫描父包

   ```xml
   <context:component-scan base-package="com.iweb.spring5.dao,com.iweb.spring5.service"/>
   ```

   ```xml
   <!--    配置父包-->
   <context:component-scan base-package="com.iweb.spring5"/>
   ```

4. 在需要被Spring管理的类上配置注解

    ```java
    @Service(value="userService")
    // 以上等同于 <bean id="userService" class="com.iweb.spring5.service.impl.UserServiceImpl" />
    public class UserServiceImpl implements UserService {
        @Override
        public int add() {
            return 0;
        }
    }
    ```

5. 若希望不扫描某些包，可以进行自定义配置(use-default-filters="false")

    比如, 只扫描@Service注解

    ```xml
    <context:component-scan base-package="com.iweb.spring5"
                            use-default-filters="false">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Service"/>
    </context:component-scan>
    ```

    比如，排除@Repository注解

    ```xml
    <context:component-scan base-package="com.iweb.spring5">
        <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Repository"/>
    </context:component-scan>
    ```
    
    PS: 不要随便排除@Component注解，一旦排除，所有相关的@Service, @Controller，@Repository都将失效

## 12.基于注解方式注入属性的值

- @AutoWired	根据属性类型自动注入(装配)
- @Qualifier	根据属性名称自动注入
- @Resource    根据属性名称或类型自动注入
- @Value    注入普通值

### 12.1 AutoWired

**根据类型自动注入示例：**

```java
@Service(value="userService")
// <bean id="userService" class="com.iweb.spring5.service.impl.UserServiceImpl" />
public class UserServiceImpl implements UserService {
    @Autowired
    private UserDao userDao;
    @Override
    public int add() {
        System.out.println(userDao);
        return 0;
    }
}
```

```java
@Repository
public class UserDaoImpl implements UserDao {
    @Override
    public int add() {
        return 0;
    }
}
```

```java
@Test
public void testUserService() {
    ApplicationContext context =
        new ClassPathXmlApplicationContext("bean7.xml");
    UserService userService = context.getBean("userService", UserService.class);
    System.out.println(userService);
    userService.add();
}
```

运行结果：

```
com.iweb.spring5.service.impl.UserServiceImpl@358ee631
com.iweb.spring5.dao.impl.UserDaoImpl@ec756bd
```

### 12.2 Qualifier

当实现类有多个时，可以**根据名称指定自动注入哪个子类实例**

```java
@Service(value="userService")
public class UserServiceImpl implements UserService {
    @AutoWired
    @Qualifier(value="userDao")
    private UserDao userDao;
    @Override
    public int add() {
        System.out.println(userDao);
        return 0;
    }
}
```

```java
@Repository(value = "userDao")  // 指定名称
public class UserDaoImpl implements UserDao {
    @Override
    public int add() {
        return 0;
    }
}
```

运行结果：

```
com.iweb.spring5.service.impl.UserServiceImpl@3d121db3
com.iweb.spring5.dao.impl.UserDaoImpl@3b07a0d6
```

### 12.3 @Resource

**根据@Resource注解自动注入属性：**

根据类型注入

```java
@Service(value="userService")
public class UserServiceImpl implements UserService {
    @Resource
    private UserDao userDao;
    @Override
    public int add() {
        System.out.println(userDao);
        return 0;
    }
}

@Repository
public class UserDaoImpl implements UserDao {
    @Override
    public int add() {
        return 0;
    }
}
```

根据名称注入：

```java
@Service(value="userService")
public class UserServiceImpl implements UserService {
    @Resource(name="userDao")
    private UserDao userDao;
    @Override
    public int add() {
        System.out.println(userDao);
        return 0;
    }
}

@Repository(value="userDao")
public class UserDaoImpl implements UserDao {
    @Override
    public int add() {
        return 0;
    }
}
```

### 12.4 @Value

直接注入值

```java
@Repository(value = "userDao")
public class UserDaoImpl implements UserDao {
    @Value(value = "tom")
    private String name;
    @Value("20")
    private int age;

    @Override
    public int add() {
        System.out.println("name:" + name + ",age:" + age);
        return 0;
    }
}
```

配置的值写在外部配置文件中：

1. 编写外部配置文件 data.properties

    ```
    name=tom
    age=20
    ```

2. xml文件中导入配置文件

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:context="http://www.springframework.org/schema/context"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                               http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    
        <context:property-placeholder location="classpath:data.properties" />
        <context:component-scan base-package="com.iweb.spring5" />
    </beans>
    ```

3. 使用表达式注入值

    ```java
    @Repository(value = "userDao")
    public class UserDaoImpl implements UserDao {
        @Value(value = "${name}")
        private String name;
        @Value("${age}")
        private int age;
    
        @Override
        public int add() {
            System.out.println("name:" + name + ",age:" + age);
            return 0;
        }
    }
    ```

## 13.完全注解式开发

在Spring中，可以实现不基于XML配置（SpringBoot推荐的方式），进行完全注解式的开发

实现步骤：

1. 定义配置类, 并标示配置类（添加@Configuration注解，开启组件扫描）

    ```java
    @Configuration
    @ComponentScan(basePackages={"com.iweb.spring5"})
    public class SpringConfig {
        
    }
    ```

    ```java
    @Component
    public class User {
        private Integer id;
        private String name;
    
        public Integer getId() {
            return id;
        }
        public void setId(Integer id) {
            this.id = id;
        }
        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
    }
    ```

2. 测试

    ```java
    @Test
    public void testConfig(){
        ApplicationContext context =
            new AnnotationConfigApplicationContext(SpringConfig.class);
        User user = context.getBean("user", User.class);
        System.out.println(user);
    }
    ```

    ```
    com.iweb.spring5.User@72a7c7e0
    ```

## 14.Spring AOP

### 14.1 基本概念
名词解释和逻辑图上课已经讲了 自行汇总到md中

面向切面编程（方面），利用 AOP 可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率。

### 14.2 底层原理

AOP 底层使用动态代理 ，动态代理有两种情况：

- 第一种 有接口情况，使用 JDK 动态代理 (创建**接口实现类代理对象**，增强类的方法)
- 第二种 没有接口情况，使用 CGLIB 动态代理(创建**子类的代理对象**，增强类的方法）

PS: 具体实现过程，详见java代理模式文档。

### 1.4.3 AOP术语

- 连接点：可能需要被增强的方法，这些方法被称为连接点

- 切入点：实际真正被增强的方法

- 通知(增强)：实际增强的逻辑部分，称为通知，且分为5种类型：

    ​					前置通知、后置通知、环绕通知、异常通知、最终通知

- 切面：把通知应用到切入点的过程

### 14.4 AOP操作

Spring框架一般基于AspectJ实现AOP操作，AspectJ不是Spring组成部分，独立于AOP框架，一般把AspectJ和Spring框架一起使用，进行AOP的操作。

基于AspectJ实现AOP操作的方式：

- 基于xml配置文件方式实现
- 基于注解方式实现(推荐方式)

PS: 本小结以UserDao的add方法为例进行演示。

#### 14.4.4 基于xml配置文件方式

1. 导入相关依赖包

    <img src="https://jayoss.oss-cn-beijing.aliyuncs.com/imagesimage-20210122161434113.png" alt="image-20210122161434113" style="zoom: 80%;" />

2. 创建增强类(代理类)，并定义增强方法

    ```java
    /**
     * @autor g
     * @data 2021/1/22
     * @desc UserDao的增强类
     */
    public class UserDaoProxy {
        /**
         * 定义前置增强方法
         */
        public void before(JoinPoint joinPoint) {
            System.out.println("执行前置增强1111。。。。");
            System.out.println("准备执行" + joinPoint.getTarget() + "的方法：" + joinPoint.getSignature().getName());
        }
    }
    ```

2. 在Spring配置文件中对目标类和增强类进行配置

    ```xml
    <!--    配置目标Bean-->
    <bean id="userDao" class="com.iweb.spring5.dao.impl.UserDaoImpl"></bean>
    <!--    配置增强(代理)Bean-->
    <bean id="userDaoProxy" class="com.iweb.spring5.dao.UserDaoProxy"></bean>
    ```

3. 在Spring配置文件中，配置AOP增强

    - 切入点    定义对哪个类里面的哪个方法进行增强 

        ```
        语法结构： execution([权限修饰符] [返回类型] [类全路径] [方法名称]([参数列表]) )
        示例：
        对 com.iweb.dao.UserDao 类里面的 add 进行增强
        	execution(* com.iweb.dao.UserDao.add(..))
        对 com.iweb.dao.UserDao 类里面的所有的方法进行增强
        	execution(* com.iweb.dao.UserDao.* (..))
        对 com.iweb.dao 包里面所有类，类里面所有方法进行增强
        	execution(* com.iweb.dao.*.* (..))
        ```

    - 切面   把增强操作切入到切入点中

        ```xml
        <!--    配置AOP增强-->
        <aop:config>
            <!--        配置切入点-->
            <aop:pointcut id="pointcut" expression="execution(* com.iweb.spring5.dao.UserDao.add(..))"/>
            <!--        配置切面-->
            <aop:aspect ref="userDaoProxy">
                <!--            配置具体增强操作,并作用到哪个切入点中-->
                <aop:before method="before" pointcut-ref="pointcut"/>
            </aop:aspect>
        </aop:config>
        ```

4. 测试执行

    ```java
    @Test
    public void test9(){
        ApplicationContext context =
            new ClassPathXmlApplicationContext("bean9.xml");
        UserDao userDao = context.getBean("userDao", UserDao.class);
        int ret = userDao.add();
        System.out.println(ret);
    }
    ```

    运行结果：

    ```
    执行前置增强。。。。
    name:null,age:0
    0
    ```

#### 14.4.2 基于注解方式

##### 前置增强

在目标方法前织入增强处理

1. 导入相关依赖包

2. 创建增强类(代理类)，并定义增强方法, 并配置AOP增强

    ```java
    @Component
    @Aspect // 生成代理对象
    public class UserDaoProxy {
        /**
         * 定义前置增强方法
         */
        @Before(value = "execution(* com.iweb.spring5.dao.UserDao.add())")
        public void before(JoinPoint joinPoint) {
            System.out.println("执行前置增强1111。。。。");
            System.out.println("准备执行" + joinPoint.getTarget() + "的方法：" + joinPoint.getSignature().getName());
        }
    }
    ```

3. 开启注解扫描

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:aop="http://www.springframework.org/schema/aop"
           xmlns:context="http://www.springframework.org/schema/context"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd
           http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    <!--    演示基于注解式的AOP操作-->
    <!--开启扫描-->
        <context:component-scan base-package="com.iweb.spring5"></context:component-scan>
    <!--开启aop 注解扫描-->
        <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
    </beans>
    ```

4. 进行测试

    ```java
    @Test
    /**
      * 测试基于注解的aop操作
      */
    public void testAop1() {
        ApplicationContext context =
            new ClassPathXmlApplicationContext("myBean23.xml");
        UserDao userDao = context.getBean("userDaoImpl", UserDao.class);
        int ret = userDao.add();
        System.out.println("执行结果ret:" + ret);
    }
    ```

    

##### 后置增强

在目标方法正常执行（不出现异常）后织入增强处理

UserDao中的方法:

```java
@Override
public int add() {
    System.out.println("执行UserDaoImpl:add()方法。。。。。");
    return 0;
}
```

代理中的方法：

```java
/**
  * 后置增强
  */
@AfterReturning(value = "execution(* com.iweb.spring5.dao.UserDao.add())",returning = "returnValue")
public void afterReturning(JoinPoint joinPoint, Object returnValue) {
    System.out.println("执行后置增强。。。。");
    System.out.println(joinPoint.getTarget() +
                       "的方法" + joinPoint.getSignature().getName()
                       + "的返回值为：" + returnValue);
}
```

测试代码：

```java
@Test
public void test12() {
    ApplicationContext context =
        new ClassPathXmlApplicationContext("bean10.xml");
    UserDao userDao = context.getBean("userDao", UserDao.class);
    int ret = userDao.add();
    System.out.println("打印方法返回值ret:" + ret);
}
```

运行结果：

```
执行UserDaoImpl:add()方法。。。。。
执行后置增强。。。。
com.iweb.spring5.dao.impl.UserDaoImpl@5d534f5d的方法add的返回值为：0
打印方法返回值ret:0
```

PS: 给目标对象中的方法，加入可能发生异常的代码，然后观察执行情况：

```java
@Override
public int add() {
    System.out.println("执行UserDaoImpl:add()方法。。。。。");
    // 异常代码
    int a = 10/0;
    return 0;
}
```



##### **异常抛出增强**

- 在目标方法抛出异常时织入增强处理
- 可拔插的异常处理方案

UserDao中的方法：

```java
@Override
public int add() throws Exception {
    try {
        System.out.println("执行UserDaoImpl:add()方法。。。。。");
        int a=10/0;
        return 0;
    } catch (Exception e) {
        throw new Exception(e);
    }
}
```
代理中的方法：

```java
/**
     * 异常增强
     */
@AfterThrowing(value = "execution(* com.iweb.spring5.dao.UserDao.add())", throwing = "ex")
public void afterThrowing(JoinPoint joinPoint, Exception ex) {
    System.out.println("执行异常抛出增强。。。");
    System.out.println("调用" + joinPoint.getSignature().getName() + "方法发生异常：" + ex.getMessage());
}
```

测试代码：

```java
@Test
public void test11() {
    ApplicationContext context =
        new ClassPathXmlApplicationContext("bean10.xml");
    UserDao userDao = context.getBean("userDao", UserDao.class);
    int ret = 0;
    try {
        ret = userDao.add();
    } catch (Exception e) {
        e.printStackTrace();
    }
    System.out.println("打印方法返回值ret:" + ret);
}
```

运行结果：

```
执行UserDaoImpl:add()方法。。。。。
执行异常抛出增强。。。
调用add方法发生异常：java.lang.ArithmeticException: / by zero
java.lang.Exception: java.lang.ArithmeticException: / by zero
```



##### **最终增强**

- 无论方法是否抛出异常，都会在目标方法最后织入增强处理，即：该增强都会得到执行
- 类似于异常处理机制中finally块的作用，一般用于释放资源
- 可以为各功能模块提供统一的，可拔插的处理方案

UserDao中的方法：

```java
@Override
public int add() {
    System.out.println("执行UserDaoImpl:add()方法。。。。。");
    int a = 10/0;
    return 0;
}
```

代理类中的方法：

```java
/**
  * 定义最终增强方法
  */
@After(value="execution(* com.iweb.spring5.dao.UserDao.add())")
public void after(JoinPoint joinPoint){
    System.out.println("执行最终增强。。。。");
    System.out.println("调用" + joinPoint.getSignature().getName() + "方法结束了");
}
```

运行结果：

```
执行UserDaoImpl:add()方法。。。。。
执行最终增强。。。。
调用add方法结束了

java.lang.ArithmeticException: / by zero
```

##### **环绕增强**

- 目标方法前后都可织入增强处理
- 功能最强大的增强处理
- 可获取或修改目标方法的参数、返回值，可对它进行异常处理，甚至可以决定目标方法是否执行

UserDao中的代码：

```java
@Override
public int add() {
    System.out.println("执行UserDaoImpl:add()方法。。。。。");
    return 0;
}
```

代理中的方法:

```java
/**
     * 环绕增强
     */
@Around(value = "execution(* com.iweb.spring5.dao.UserDao.add())")
public Object around(ProceedingJoinPoint jointPont) {
    System.out.println("执行环绕增强1111。。。。");
    try {
        System.out.println("准备执行" + jointPont.getTarget() + "的方法：" + jointPont.getSignature().getName());
        Object ret = jointPont.proceed();
        System.out.println("方法返回值：" + ret);
        return ret;
    } catch (Throwable throwable) {
        throwable.printStackTrace();
        return null;
    }
}
```

测试代码：

```java
/**
  * 测试环绕增强
  */
@Test
public void test12() {
    ApplicationContext context =
        new ClassPathXmlApplicationContext("bean10.xml");
    UserDao userDao = context.getBean("userDao", UserDao.class);
    int ret = userDao.add();
    System.out.println("打印方法返回值ret:" + ret);
}
```

运行结果：

```
执行环绕增强1111。。。。
准备执行com.iweb.spring5.dao.impl.UserDaoImpl@3527942a的方法：add
执行UserDaoImpl:add()方法。。。。。
方法返回值：0
打印方法返回值ret:0
```



##### 小结

| 增强处理类型   | 特 点                                                        |
| -------------- | ------------------------------------------------------------ |
| Before         | 前置增强处理，在目标方法前织入增强处理                       |
| AfterReturning | 后置增强处理，在目标方法正常执行（不出现异常）后织入增强处理 |
| AfterThrowing  | 异常抛出增强处理，在目标方法抛出异常后织入增强处理           |
| After          | 最终增强处理，不论方法是否抛出异常，都会在目标方法最后织入增强处理 |
| Around         | 环绕增强处理，在目标方法的前后都可以织入增强处理             |












