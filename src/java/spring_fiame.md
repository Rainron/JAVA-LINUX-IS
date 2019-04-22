# spring_frame
- [Spirng](#Spirng)
    - [Spring-IOC](#Spring-IOC)
    - [Spring-AOP](#Spring-AOP)
- [MyBatis](#MyBatis)
    - [MyBatis-核心组件](#MyBatis-核心组件)
    - [MyBatis-相关配置](#MyBatis-相关配置)
- [SpringMvc](#SpringMvc)









### Spirng
### Spring-IOC
### Spring-AOP















### MyBatis
### MyBatis-核心组件
* **SqlSsessionFactoryBuilder构造器** 根据配置或者代码来生成SqlSessionFactory 采用建造者模式分布构建。
* **SqlSessionFactory** 依靠它来产生SqlSession 采用工厂模式。
* **SqlSession会话**，一个可以发生sql执行返回结果，也可以获取mapper的接口。
* **SqlMapper** 映射器MyBatis新设计存在的组件，它由一个Java接口和XML文件或注解构成需要给出对应的SQL和映射规则它负责发送SQL去执行并返回结果。
<br/>
**1.SqlSessionFactory工厂接口**
* MyBatis提了构造器 SqlSessionFactoryBuilder,它提供了一个类.org.apache.ibatis.session.Configuration 作为引导，采用的是Builder模式,具体的分步则是在Configuration类里面完成的。你可以使用xml或者代码的方式配置生成SqlSessionFactory.

  * **xml配置SqlSessionFactory**，MyBatis会读取xml配置文件，通过 Configuration 类对象构建整个MyBatis的上下文。SqlSessionFactory是一个接口，在MyBatis中它存在两个实现类：SqlSessionManager和DefaultSqlSessionFactory。 一般而言，具体是由DefaultSqlSessionFactory去实现的，而 SqlSessionManager 使用在多线程的环境中，而且每个基于MyBatis 的应用都是以一个SqlSessionFactory的实例为中心的，而SqlSessionFactory唯一的作用就是生产 MyBatis的核心接口对象SqlSession。

  



### MyBatis-相关配置











### SpringMvc

