# spring_frame
- ##  [Spirng](#Spirng)
- ##     [Spring-IOC](#Spring-IOC)
- ##     [Spring-AOP](#Spring-AOP)
- ##  [MyBatis](#MyBatis)
- ##     [MyBatis-核心组件](#MyBatis-核心组件)
- ##     [MyBatis-相关配置](#MyBatis-相关配置)
- ##  [SpringMvc](#SpringMvc)









### Spirng
### Spring-IOC
### Spring-AOP















### MyBatis
### MyBatis-核心组件
* **SqlSsessionFactoryBuilder构造器** 根据配置或者代码来生成SqlSessionFactory 采用建造者模式分布构建。
* **SqlSessionFactory** 依靠它来产生SqlSession 采用工厂模式。
* **SqlSession会话**，一个可以发生sql执行返回结果，也可以获取mapper的接口。
* **SqlMapper** 映射器MyBatis新设计存在的组件，它由一个Java接口和XML文件或注解构成需要给出对应的SQL和映射规则它负责发送SQL去执行并返回结果。

#### 1.SqlSessionFactory工厂接口 
- MyBatis提了构造器 SqlSessionFactoryBuilder,它提供了一个类.org.apache.ibatis.session.Configuration 作为引导，采用的是Builder模式,具体的分步则是在Configuration类里面完成的。你可以使用xml或者代码的方式配置生成SqlSessionFactory.
- xml配置SqlSessionFactory，MyBatis会读取xml配置文件，通过 Configuration 类对象构建整个MyBatis的上下文。SqlSessionFactory是一个接口，在MyBatis中它存在两个实现类：SqlSessionManager和DefaultSqlSessionFactory。 一般而言，具体是由DefaultSqlSessionFactory去实现的，而 SqlSessionManager 使用在多线程的环境中，而且每个基于MyBatis 的应用都是以一个SqlSessionFactory的实例为中心的，而SqlSessionFactory唯一的作用就是生产 MyBatis的核心接口对象SqlSession。
- xml的配置都可以在MyBatis SQL mapper framework for Java http://mybatis.github.io/mybatis-3/ 网站中获取。
```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE configuration PUBLIC "-//ibatis.apache.org//DTD Config 3.0//EN" 
	"http://ibatis.apache.org/dtd/ibatis-3-config.dtd">
<configuration>
	<!-- 别名 -->
	<typeAliases>
	<typeAlias alias="rainron" type="mybatis.test.Rainron"/> 
	</typeAliases>
	<!-- 数据库环境 -->
	<environments default="environment">
		<environment id="environment">
			<transactionManager type="JDBC" />
			<!-- MyBatis自带的连接池 -->
			<dataSource type="POOLED">
				<property name="driver" value="com.mysql.jdbc.Driver" />
				<property name="url"
					value="jdbc:mysql://localhost:3306/test" />
				<property name="username" value="root" />
				<property name="password" value="root" />
			</dataSource>
		</environment>
	</environments>
	<!-- 配置映射文件的位置 -->
	<mappers>
		<mapper resource="mybatis/mapper/RainMapper.xml" />
	</mappers>
	<mapper>
		<class=" 
	</mapper>
</configuration>
```
#### 2.SqlSession
-  SqlSession的作用类似于一个JDBC中的Connection对象，代表着一个连接资源的启用，其实是一个接口，MyBatis中实际使用的是执行器Executor。
 * 获取Mapper 接口。
 * 发送 SQL 给数据库。
 * 控制数据库事务。 
```java
private SqlSession session;
@Before
public void init(){

	SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
	SqlSessionFactory ssf = builder.build(TestCase.class.getClassLoader().getResourceAsStream("mybatis-config.xml"));
	session = ssf.openSession();
}
@Test
public void test1(){
	Rainron a = new Rainron();
	a.setId(1);
	a.setName("rainron1");
	a.setAge(10);
	//SqlSession发送sql
	session.insert("mybatis.mapper.RainronMapper.save", a);
	session.commit();
	session.close();
}
@Test
public void test4(){
	RainronMapper rm = session.getMapper(RainronMapper.class);
	//mapper发送sql
	Rainron a = rm.getId(1);
	System.out.println(a);
	session.close();
}
使用Mapper接口编程可以消除SqlSession 带来的功能性代码，提高可读性,而且使用mapper一般ide会校验类型。

```

#### 3.SqlMapper映射器
- 它由一个接口和对应的 XML 文件（或 注解〉组成。它可以配置以下内容：
 * 描述映射规则。
 * 提供SQL语旬，并可以配置SQL参数类型、返回类型、缓存刷新等信息。 
 * 配置缓存。 
 * 提供动态SQL。 
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="mybatis.test.mapper.RainronMapper">
	<!-- 插入 -->
	<insert id="insertRain" parameterType="Rainron">
		insert into rainron values(#{id},#{name},#{age})
	</insert>	
	<delete id="deleteRain" parameterType="int">
		delete from rainron where id = #{id}
	</delete>
	<update id="updateRain" parameterType="Rainron">
		update rainron set name = #{name},age = #{age} where id = #{id}
	</update>
	<select id="getId" parameterType="int" resultType="Rainron">
		select id , name ,age from rainron where id = #{id}	
	</select>
	<select id="findRains" parameterType="String" resultType="Rainron">
		select * from rainron where name concat('%',#{name},'%')	
	</select>
</mapper>
```
```java
package mybatis.test.mapper;
import java.util.List;
import mybatis.test.pojo.Rainron;
public interface RainronMapper {
	
	public int insertRain(Rainron a);
	public int deleteRain(int id);
	public int updateRain(Rainron a);
	public Rainron getId(int id);
	public List<Rainron> findRains(String rainname);
	
}
除XML方式定义映射器外，还可以采用注解方式定义映射器，它只需要一个接口就可以通过MyBatis的注解来注入SQL
public interface RainronMapper {
	@Insert("insert into rainron values(#{id},#{name},#{age})")
	public int insertRain(Rainron a);
	
}
如两种方式存在xml优先覆盖注解	
```
#### 4.生命周期
- SqlSessionFactoryBuilde 的作用在于创建 SqlSessionFactory ，创建成功后 SqlSessionFactoryBuilder就失去了作用，所以它只能存在于创建 SqlSessionFactory的方法中。
- Sq!SessionFactory可以被认为是一个数据库连接池，它的作用是创建SqlSession接口对象。所有其生命周期应该存在于整个MyBatis工程中，一旦创建，应该长期保存，并且是以单例的方式存在，工程中公用，不然多个数据库连接池会导致数据库连接资源耗尽。
- 如果说 SqlSessionFactory相当于数据库连接池，那么SqlSession就相当于一个数据库连接（ Connection对象），你可以在一个事务里面执行多条SQL，然后通过它的commit、rollback 等方法，提交或者回滚事务。所以它应该存活在一个业务请求中，处理完整个请求后，应该关闭这条连接，让它归还给SqlSessionFactory。
- Mapper是一个接口，它由SqlSession 所创建，所以它的最大生命周期至多和SqlSession保持一致，尽管它很好用，但是由于SqlSession的关闭，它的数据库连接资源也会消失，所以它的生命周期应该小于等于SqlSession的生命周期。

### MyBatis-相关配置
```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE configuration PUBLIC "-//ibatis.apache.org//DTD Config 3.0//EN" 
	"http://ibatis.apache.org/dtd/ibatis-3-config.dtd">
<configuration>

	<!-- 属性配置 给系统配置一些运行参数 比如数据库连接配置  可以使用properties文件resource引入
		 也可以使用resource对象读取配置文件 properties读取标志位
	 -->
	<properties/>
	<properties resource="*.properties"/>
	<!-- settings是MyBatis中最复杂的配置，它能深刻影响 MyBatis底层的运行 
		 所以在大部分情况下不需要大量配置它，
		 只需要修改一 些常用的规则即可， 比如自动映射、驼峰命名映射、级联规则、 是否启动缓存、执行器 CExecutor）类型等。 
	-->
	<settings>
		<!-- 开启驼峰自动映射 -->
		<setting name="mapUnderscoreToCamelCase" value="true" />
		<!-- 二级缓存的总开关 -->
		<setting name="cacheEnabled" value="false" />
	</settings>
	
	<!-- 类的全限定名很长一般使用别名来代替  MyBatis中有系统定义别名及自定义别名 
		 自定义别名需要通过Configuration获取TypeAliasRegis类对象的registerAlias方法注册别名
	-->
	<typeAliases>
		<typeAlias alias="rainron" type="mybatis.test.pojo.Rainron"/> 
		<!-- 支持包扫描 -->
		<package name="mybatis.test.pojo"/> 
	</typeAliases>
	
	<!-- pojo的javatype与数据库的类型jdbctype如何进行映射呢
		 就是使用类型转换器
		 系 统提供的 typeHandler能覆盖大部分场景的要求，但是有些情况下是不够的，枚举类就是要自定义类型转换器。
	 -->
	<typeHandlers/>
	<!-- 对象工厂当
	创建结果集时， MyBatis会使用一个对象工厂来完成创建这个结果集实例。在默认 的情况下，
	 MyBatis 会使用其定义的对象工厂DefaultObjectFactory来完成对应的工作。也可以自定义对象工厂 -->
	<objectFactory type=""/>
	<!-- 插件  最灵活同时也是最复杂难以使用的组件 需要熟悉MyBatis底层原理 -->
	<plugins/>
	<!-- 行环境主要的作用是配置数据库信息，它可以配置多个数据库，一般配置一个可以
		 下面又可以配置事务管理器及数据源
	 -->
	<environments default="environment">
		<environment id="environment">
		<transactionManager type="JDBC"></transactionManager>
		<dataSource type="POOLED">
			
		</dataSource>
	</environments>
	<!-- 数据库厂商标识 支持不同类型数据库 -->
	<databaseidProvider/>
	<!-- 定义映射器 -->
	<mappers>
		<!-- 使用这个方案，可以单独指定Mapper的位置 -->
		<!-- <mapper resource="mybatis/mappings/RainMapper.xml"/>
		<mapper resource="mybatis/mappings/UserMapper.xml"/> -->
		
		<!-- 使用下面两个个方法，Mapper.xml 文件位置必须在和其内部 <mapper namespace="">的类在一起，当然，
		使用注解模式的话，Mapper.xml文件就没有必要存在了 -->
		
		<!-- 直接指定一个包去扫描-内保包含多个Mapper配置- -->
		<!-- <package name="mybatis.test.mapper"/> -->
		
		<!-- class 级别的指定 -->
		<mapper class="mybatis.test.mapper.RainMapper"/>
	</mappers>
</configuration>
```











### SpringMvc

