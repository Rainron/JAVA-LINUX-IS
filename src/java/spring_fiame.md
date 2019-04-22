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





### MyBatis-相关配置











### SpringMvc

