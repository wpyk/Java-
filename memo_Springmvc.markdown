[![l03BNt.md.png](https://s2.ax1x.com/2020/01/04/l03BNt.md.png)](https://imgchr.com/i/l03BNt)


# 配置好环境后，创建java bean文件 Greeting.java，创建controller文件GreetingController.java 以及入口文件Application.java.  
*这三个文件中，controller是通过url匹配接收80端口传入的参数信息，并将这个参数传递至bean文件创建新的java对象，而application的main函数是springbootapplication，整个项目的入口。*  
# 在文件所在目录shift+右键打开powershell，运行mvn spring-boot:run,跑起来后通过localhost：http://8080/greeting 来访问默认设置，在greeting后加上?name=wpyk来改变默认参数。

参考教程：  
https://spring.io/guides/gs/rest-service/

# 如何从0创建一个SpringMVC，SpringBoot，Mybatis架构

# 1.创建一个跑得起来的mvc工程

## 1.1 创建maven工程并配置相应的.xml文件

1. 新建一个dynamic web project-> config to maven project 
2. pom.xml 配置
build tag 里加上：


		<sourceDirectory>src</sourceDirectory>
	
		<parent>  
	        <groupId>org.springframework.boot</groupId>  
	        <artifactId>spring-boot-starter-parent</artifactId>  
	        <version>2.2.1.RELEASE</version>  
	    </parent>  

		<dependencies>
	
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-web</artifactId>
	        </dependency>
	
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-test</artifactId>
	            <scope>test</scope>
	        </dependency>
	
	        <dependency>
	            <groupId>com.jayway.jsonpath</groupId>
	            <artifactId>json-path</artifactId>
	            <scope>test</scope>
	        </dependency>
	
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-tomcat</artifactId>
	            <scope>provided</scope>
	        </dependency>
	 
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-configuration-processor</artifactId>
	            <optional>true</optional>
	        </dependency>
	 
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-jdbc</artifactId>
	        </dependency>
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-aop</artifactId>
	        </dependency>
	 
	        <dependency>
	            <groupId>mysql</groupId>
	            <artifactId>mysql-connector-java</artifactId>
	        </dependency>
	        <!--mybatis -->
	        <dependency>
	            <groupId>org.mybatis.spring.boot</groupId>
	            <artifactId>mybatis-spring-boot-starter</artifactId>
	            <version>1.2.0</version>
	        </dependency>
	        <dependency>
	            <groupId>com.alibaba</groupId>
	            <artifactId>druid</artifactId>
	            <version>1.0.11</version>
	        </dependency>
	 
	        <!-- spring boot tomcat jsp 支持开启 -->
	        <dependency>
	            <groupId>org.apache.tomcat.embed</groupId>
	            <artifactId>tomcat-embed-jasper</artifactId>
	        </dependency>
	        <!-- servlet支持开启 -->
	        <dependency>
	            <groupId>javax.servlet</groupId>
	            <artifactId>javax.servlet-api</artifactId>
	        </dependency>
	        <!-- jstl 支持开启 -->
	        <dependency>
	            <groupId>javax.servlet</groupId>
	            <artifactId>jstl</artifactId>
	        </dependency>
	        <dependency>
	            <groupId>org.springframework.boot</groupId>
	            <artifactId>spring-boot-starter-freemarker</artifactId>
	        </dependency>
	        <!-- Map工具类 -->
			<dependency>
				<groupId>commons-collections</groupId>
				<artifactId>commons-collections</artifactId>
				<version>3.2</version>
			</dependency>
			<!-- Jackson JSON Mapper -->
			<dependency>
				<groupId>com.fasterxml.jackson.core</groupId>
				<artifactId>jackson-core</artifactId>
				<version>2.9.6</version>
			</dependency>
			<dependency>
				<groupId>com.fasterxml.jackson.core</groupId>
				<artifactId>jackson-databind</artifactId>
				<version>2.9.6</version>
			</dependency>
			<dependency>
				<groupId>com.fasterxml.jackson.core</groupId>
				<artifactId>jackson-annotations</artifactId>
				<version>2.9.6</version>
			</dependency>
			<!-- apache common -->
			<dependency>
				<groupId>org.apache.commons</groupId>
				<artifactId>commons-lang3</artifactId>
				<version>3.7</version>
			</dependency>
	
			<dependency>
				<groupId>commons-beanutils</groupId>
				<artifactId>commons-beanutils</artifactId>
				<version>1.8.3</version>
			</dependency>
			<dependency>
				<groupId>commons-collections</groupId>
				<artifactId>commons-collections</artifactId>
				<version>3.2.2</version>
			</dependency>
	        
	    </dependencies>`

3.   mvn clean eclipse:clean eclipse:eclipse-> mvn install

*如果想修改maven的默认源路径，例如，想要将<sourceDirectory>src</sourceDirectory>修改为<sourceDirectory>src/main</sourceDirectory>*，可以自己手动先在src下面建一个main文件夹，再去mvn clean eclipse:clean eclipse:eclipse。不然可能会遇到右击src无法创建package的情况。其原因在于创建的项目里缺少一些文件，eclipse不完整，经过上述三个命令，会使需要的配置文件齐全。每个项目都是自己的文件夹，即使在别的项目里文件齐全，也无法给当前的项目使用。

*mvn clean :This command deletes target directory and then builds all you code and installs artifacts into local repository.*  
*eclipse:clean eclipse:eclipse : First, it deletes previously generated Eclipse files (like .project and .classpath and .settings) and then generates new ones, thus, effectively updating them. It may be useful if you introduced some changes in pom.xml (like new dependencies or plugins) and want Eclipse to be aware of them.*

## 1.2使程序跑起来

**现在我们要使用之前建立好的框架，创建一个能够跑的起来的工程**

### 1.2.1 创建application.properties
### 1.2.2 创建接口类
本质上就是提供一个main函数，使程序能够跑

    package wpyk.blog;

	import org.springframework.boot.SpringApplication;
	import org.springframework.boot.autoconfigure.SpringBootApplication;
	
	@SpringBootApplication
	public class Application {

  	public static void main(String[] args) {
    	SpringApplication.run(Application.class, args);
 	 }
	}

### 1.2.3 创建bean

    package wpyk.blog.bean;

	public class Greeting {
	
	  private final long id;
	  private final String content;
	
	  public Greeting(long id, String content) {
	    this.id = id;
	    this.content = content;
	  }
	
	  public long getId() {
	    return id;
	  }
	
	  public String getContent() {
	    return content;
	  }
	}
### 1.2.4 创建controller

    package wpyk.blog.controller;

	import java.util.concurrent.atomic.AtomicLong;
	import org.springframework.web.bind.annotation.RequestMapping;
	import org.springframework.web.bind.annotation.RequestParam;
	import org.springframework.web.bind.annotation.RestController;
	
	import wpyk.blog.bean.Greeting;
	
	@RestController
	public class GreetingController {
	
	  private static final String template = "Hello, %s!";
	  private final AtomicLong counter = new AtomicLong();
	
	  @RequestMapping("/greeting")
	  public Greeting greeting(@RequestParam(value="name", defaultValue="World") String name) {
	    return new Greeting(counter.incrementAndGet(),
	              String.format(template, name));
	  }
	}

# 2. Spring 与 Mybatis 的整合
## 2.1 pom 文件相关配置

    <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
 
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <optional>true</optional>
        </dependency>
 
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-aop</artifactId>
        </dependency>
 
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
        <!--mybatis -->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>1.2.0</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.0.11</version>
        </dependency>
 
        <!-- spring boot tomcat jsp 支持开启 -->
        <dependency>
            <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-jasper</artifactId>
        </dependency>
        <!-- servlet支持开启 -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
        </dependency>
        <!-- jstl 支持开启 -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
        </dependency>


    	<resources>
			<!-- 在spring-boot:run 的时候，maven项目中src源代码下的xml等资源文件编译进classes文件夹， 注意：如果没有这个，它会自动搜索resources下是否有mapper.xml文件， 
				如果没有就会报org.apache.ibatis.binding.BindingException: Invalid bound statement 
				(not found): com.pet.mapper.PetMapper.selectByPrimaryKey -->
			<resource>
				<directory>src/main/java</directory>
				<includes>
					<include>**/*.xml</include>
				</includes>
			</resource>

			<!--如果上面的resources找不到，则执行下面这个。将resources目录下的配置文件编译进classes文件 -->
			<resource>
				<directory>src/main/resources</directory>
			</resource>
		</resources>


## 2.2 application.properties 文件
**Spring Boot使用了一个全局的配置文件application.properties，放在src/main/resources目录下或者类路径的/config下。Sping Boot的全局配置文件的作用是对一些默认配置的配置值进行修改。**

*有时候配置的jdbc没问题也会报错，这个时候试一下在最后增加 “&serverTimezone=UTC”*



    //jdbc.ds是和DataSourceConfiguration中的@ConfigurationProperties(prefix = "jdbc.ds")是保持一致的。
	jdbc.ds.jdbc-url=jdbc:mysql://localhost/ssm_wpyk?autoReconnect=true&useUnicode=true&characterEncoding=utf-8&zeroDateTimeBehavior=convertToNull&serverTimezone=UTC
	jdbc.ds.username=root
	jdbc.ds.password=asdfg12345
	jdbc.ds.driver-class-name=com.mysql.jdbc.Driver
	 
	mybatis.type-aliases-package=com.sam.project.*.model
	//mapper文件的位置，在run的时候需要将其放到classes里面，所以在这里的classpath指的就是pom文件中resource的路径。
	mybatis.mapper-locations=classpath:mapper/*.xml
	 
	 //这个端口号可以自己改
	server.port=8080
	server.contextPath=/spring_boot
	
	//传统的web项目开发，如使用ssm框架时，我们需要在web.xml中配置统一的字符集，以防输入和输出的乱码；使用SpringBoot时也需要配置字符集。
	spring.http.encoding.charset=UTF-8
	spring.http.encoding.enabled=true
	spring.http.encoding.force=true
	 
	 
	logging.file=/export/log
	logging.level.root=INFO
	logging.level.org.springframework.web=INFO
	logging.level.sample.mybatis.mapper=TRACE
	 
	spring.main.banner-mode=off

## 2.3 创建database
在resources文件夹下面创建init.sql文件，将创建数据库的指令放在里面，将来有什么错误可以在这里检查。

    CREATE DATABASE ssm_wpyk;

	CREATE TABLE `t_user` (
	  `id` int(11) NOT NULL AUTO_INCREMENT,
	  `username` varchar(255) default NULL,
	  `password` varchar(255) default NULL,
	  `email` varchar(255) default NULL,
	  `useable` int(20) default NULL,
	  `addtime` datetime default NULL,
	  `logintime` datetime default NULL,
	  `loginip` varchar(255) default NULL,
	  PRIMARY KEY  (`id`)
	) ENGINE=InnoDB auto_increment=1001 DEFAULT CHARSET=utf8;

    insert into t_user (username,password,email) values ('wpyk','aaa','wpyk1992@gmail.com');
	insert into t_user  values (null,'kw','bbb','lkwangwenmail@gmail.com',null,null,null,null);


## 2.4  controller文件，Service文件，Mapper文件，.xml 文件之间的分工合作
**当我们访问一个页面的时候从url开始，url在controller中进行匹配。在controller中匹配好了之后，会调相应的service执行url的指令。但是service本身并不与数据库相连，没有对数据库实际操作的功能。可以看做service是controller和真正的后端之间的独立的一层。那真正的执行者是谁呢，是一个interface类型的Mapper.java 文件，这个文件有一个同名的.xml文件，而这个xml文件才能真正对数据库进行操作。**

**但是一个合格的后端程序员，是要从后往前写的！哈哈哈哈**


### 2.4.1 UserMapper.xml文件
*xml文件是对数据库直接进行操作的，当我们创建完数据库之后，就该知道当前数据库可以有怎样的操作。在上面我们的sql创建了一个user的表，那么对于这个表，我们能够实现的功能有增删改查*

    <?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" 
		"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
	<!--在mybatis中，映射文件中的namespace是用于绑定Dao接口的，即面向接口编程。当你的namespace绑定接口后，你可以不用写接口实现类，mybatis会通过该绑定自动帮你找到对应要执行的SQL语句。在本例中，创建了interface类UserMapper.java，其功能是操作数据库。当这两个文件同名，即UserMapper.java 和 UserMapper.xml，mybatis执行到UserMapper.java时会自动找到xml里的语句，并执行。指的注意的点是，两个文件中的SQL语句ID一一对应-->
	<mapper namespace="wpyk.blog.mapper.UserMapper">
		<select id="queryList" resultType="wpyk.blog.bean.User">
			SELECT u.id, u.username, u.password, u.email, u.useable, u.addtime, u.logintime, u.loginip FROM t_user u
		</select>
		
		<select id="queryById" resultType="wpyk.blog.bean.User">
			SELECT u.id, u.username, u.password, u.email, u.useable, u.addtime, u.logintime, u.loginip FROM t_user u where u.id = #{id}
		</select>
		
		<insert id="save">
			insert into t_user(username, password, email, useable, addtime)
			values(#{username}, #{password}, #{email}, #{useable}, now())
		</insert>
		
		<update id="update">
			update t_user set password = #{password}, email = #{email}, useable = #{useable} where id = #{id}
		</update>
		
		<delete id="batchDelete">
			delete from t_user where id in
			<foreach collection="array" item="item" open="(" separator="," close=")">
				#{item}
			</foreach>
		</delete>
		
		<!-- <delete id="delUsers">
			delete from t_user where id in
			<foreach collection="list" item="item" open="(" separator="," close=")">
				#{item}
			</foreach>
		</delete> -->
	</mapper>


### 2.4.2 UserMapper.java 文件
    package wpyk.blog.mapper;


	import java.util.List;
	
	import wpyk.blog.bean.User;
	  
	/**
	 * @ClassName: UserMapper 
	 * @Description: mybites数据查询接口
	 */
	public interface UserMapper {
	 
		List<User> queryList();
		
		User queryById(int id);
	 
		void save(User user);
	 
		void batchDelete(Integer[] ids);
	 
		void update(User user);
	 
	}

### 2.4.3 Bean文件 User.java 文件

    package wpyk.blog.bean;
	/**
	 * @ClassName: User
	 * @Description: 实体模型
	 */
	public class User {
		private Integer id;
	 
		private String username;
	 
		private String password;
	 
		private String email;
	 
		/**
		 * 是否可用(0禁用,1可用)
		 */
		private Integer useable;
	 
		/**
		 * 创建时间
		 */
		private String addtime;
	 
		/**
		 * 登陆时间
		 */
		private String logintime;
	 
		/**
		 * 登陆IP
		 */
		private String loginip;
	 
		/**
		 * @return id
		 */
		public Integer getId() {
			return id;
		}
	 
		/**
		 * @param id
		 */
		public void setId(Integer id) {
			this.id = id;
		}
	 
		/**
		 * @return username
		 */
		public String getUsername() {
			return username;
		}
	 
		/**
		 * @param username
		 */
		public void setUsername(String username) {
			this.username = username;
		}
	 
		/**
		 * @return password
		 */
		public String getPassword() {
			return password;
		}
	 
		/**
		 * @param password
		 */
		public void setPassword(String password) {
			this.password = password;
		}
	 
		/**
		 * @return email
		 */
		public String getEmail() {
			return email;
		}
	 
		/**
		 * @param email
		 */
		public void setEmail(String email) {
			this.email = email;
		}
	 
		/**
		 * 获取是否可用(0禁用,1可用)
		 *
		 * @return useable - 是否可用(0禁用,1可用)
		 */
		public Integer getUseable() {
			return useable;
		}
	 
		/**
		 * 设置是否可用(0禁用,1可用)
		 *
		 * @param useable
		 *            是否可用(0禁用,1可用)
		 */
		public void setUseable(Integer useable) {
			this.useable = useable;
		}
	 
		/**
		 * 获取创建时间
		 *
		 * @return addtime - 创建时间
		 */
		public String getAddtime() {
			return addtime;
		}
	 
		/**
		 * 设置创建时间
		 *
		 * @param addtime
		 *            创建时间
		 */
		public void setAddtime(String addtime) {
			this.addtime = addtime;
		}
	 
		/**
		 * 获取登陆时间
		 *
		 * @return logintime - 登陆时间
		 */
		public String getLogintime() {
			return logintime;
		}
	 
		/**
		 * 设置登陆时间
		 *
		 * @param logintime
		 *            登陆时间
		 */
		public void setLogintime(String logintime) {
			this.logintime = logintime;
		}
	 
		/**
		 * 获取登陆IP
		 *
		 * @return loginip - 登陆IP
		 */
		public String getLoginip() {
			return loginip;
		}
	 
		/**
		 * 设置登陆IP
		 *
		 * @param loginip
		 *            登陆IP
		 */
		public void setLoginip(String loginip) {
			this.loginip = loginip;
		}
	}

### 2.4.4 UserService.java 文件
*UserService 文件是controller和mapper文件之间的连接桥梁*

    package wpyk.blog.service;

	import java.util.List;
	
	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.stereotype.Service;
	
	import wpyk.blog.bean.User;
	import wpyk.blog.mapper.UserMapper;
	
	@Service
	public class UserService {
	
		@Autowired
		private UserMapper userMapper;
	
		public List<User> queryList() {
			List<User> list = userMapper.queryList();
			return list;
		}
		
		public User queryById(int id) {
			User user = userMapper.queryById(id);
			return user;
		}
	
		public User save(User user) {
			user.setUsername("user" + System.currentTimeMillis());
			user.setPassword("123456");
			user.setEmail("user" + System.currentTimeMillis() + "@test.com");
			user.setUseable(1);
			userMapper.save(user);
			return user;
		}
	
		public User save(String username, String password) {
			User user = new User();
			user.setUsername(username);
			user.setPassword(password);
			user.setEmail("user" + System.currentTimeMillis() + "@test.com");
			user.setUseable(1);
		    userMapper.save(user);
		    return user;
		}
	
		public void batchDelete(Integer[] ids) {
			userMapper.batchDelete(ids);
		}
	
		public void update(User user) {
			userMapper.update(user);
		}
	
	}


### 2.4.5 UserController.java 文件
*Controller文件实际上就是url的匹配文件*

    package wpyk.blog.controller;


	import java.util.List;
	
	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.web.bind.annotation.PathVariable;
	import org.springframework.web.bind.annotation.RequestMapping;
	import org.springframework.web.bind.annotation.RequestParam;
	import org.springframework.web.bind.annotation.RestController;
	
	import wpyk.blog.bean.User;
	import wpyk.blog.service.UserService;
	  
	/**
	 * @ClassName: UserController 
	 * @Description: 用户Controller
	 */
	@RestController
	public class UserController {
	 
		@Autowired
		private UserService userService;
		
		@RequestMapping("/users")
		public List<User> queryList(){
			return userService.queryList();
		}
		
		@RequestMapping("/users/{id}")
		public User queryById(@PathVariable int id){
			return userService.queryById(id);
		}
	 
		@RequestMapping("/add/user")
		
		public User addUser(@RequestParam(value="username") String username,@RequestParam(value="password") String password){
			return userService.save(username,password);
		}
		
		@RequestMapping("/delete/user")	
		public Integer[] delUser(Integer[] ids){
			userService.batchDelete(ids);
			return ids;
		}
		
		@RequestMapping("/update/user")
		public User updateUser(User user){
			userService.update(user);
			return user;
		}
	 
	}


# 3. SpringBoot整合FreeMarker