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
**FreeMarker 是一款 模板引擎： 即一种基于模板和要改变的数据， 并用来生成输出文本(HTML网页，电子邮件，配置文件，源代码等)的通用工具。 它不是面向最终用户的，而是一个Java类库，是一款程序员可以嵌入他们所开发产品的组件。**

## 3.1 在pom.xml里增加dependency
    	<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-freemarker</artifactId>
        </dependency>

## 3.2 在application.properties里增加配置

    spring.freemarker.enabled=true
	spring.freemarker.template-loader-path=classpath:/templates/
	spring.freemarker.suffix=.ftl


## 3.3 增加用于网页显示的template，该文件位于resources文件夹下，存放网页显示模板
index.ftl 文件

    <!DOCTYPE html>
	<html lang="en">
	<head>
	    <meta charset="utf-8"/>
	    <title>FreeMarker</title>
	</head>
	<body>
	<h1>${name}</h1>
	你好，这是我的博客
	</body>
	</html>

## 3.4 创建用于访问上述网页模板的controller  

从下面的代码和上面的模板能够看出，模板中的${name}是从controller这里传过去的，目前只是类似写死的状况。
  
    package wpyk.blog.controller;

	import org.springframework.stereotype.Controller;
	import org.springframework.web.bind.annotation.RequestMapping;
	import org.springframework.web.servlet.ModelAndView;
	
	@Controller
	public class FreeMakerDemoController {
	    @RequestMapping("/")
	    public ModelAndView index() {
	        ModelAndView modelAndView = new ModelAndView("index");
	        modelAndView.addObject("name", "张三");
	        return modelAndView;
	    }
	}

# 4.引入静态文件
**在我们开发Web应用的时候，会用到大量的js、css、image、html等静态资源资源。第4部分就来讨论如何访问这些静态的文件**

## 4.1 在application.properties里进行相关的配置

我们将静态文件放置在resources文件夹下面的static文件夹中，并在application.properties里声明其路径：  
    spring.resources.static-locations=classpath:/static/

## 4.2 修改index.ftl
我们要将引入的静态文件在index.ftl里显示出来  
    <!DOCTYPE html>
	<html lang="zh">
	<head>
	    <meta charset="utf-8">
	    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
	    <meta name="description" content="">
	    <meta name="author" content="">
	
	    <title>${title!'全栈之路 - 摆码王子的个人博客'}</title>
	
	    <!-- Custom styles for this template -->
	    <link href="/css/full-slider/full-slider.css" rel="stylesheet">
	
	<#-- 自定义 样式 -->
	<#include "public/front_custom_css.ftl">
	
	<#-- CSS -->
	<#include "public/front_css.ftl">
	    
	</head>
	<body>
	<#assign page_index = 0>
	<#-- s-nav.ftl -->
	<#include "public/nav.ftl">
	<#-- e-nav.ftl -->
	
	<#-- s-slide-header-->
	<header>
	    <div id="slideIndicators" class="carousel slide" data-ride="carousel" data-interval="3000" data-pause="">
	        <ol class="carousel-indicators">
	            <li data-target="#slideIndicators" data-slide-to="0" class="active"></li>
	            <li data-target="#slideIndicators" data-slide-to="1"></li>
	            <li data-target="#slideIndicators" data-slide-to="2"></li>
	        </ol>
	        <div class="carousel-inner" role="listbox">
	            <!-- Slide One - Set the background image for this slide in the line below -->
	            <div class="carousel-item active"
	                 style="background-image: url('https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1515063491041&di=8767c9c3177b01c45db9cc3854b78e0f&imgtype=0&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F033edd5554c7e6d00000158fc7b2956.jpg')">
	                <div class="carousel-caption d-none d-md-block">
	                    <h3 class="txt_shadow">优秀的判断力来自经验，但经验来自错误的判断</h3>
	                    <p class="txt_shadow">Good judgment comes from experience, but experience comes from bad judgment.</p>
	                </div>
	            </div>
	            <!-- Slide Two - Set the background image for this slide in the line below -->
	            <div class="carousel-item"
	                 style="background-image: url('https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1515063190806&di=71bdda130cdedcd895e5a3d476a89081&imgtype=0&src=http%3A%2F%2Fimg.pconline.com.cn%2Fimages%2Fupload%2Fupc%2Ftx%2Fitbbs%2F1309%2F16%2Fc18%2F25748320_1379313651110.jpg')">
	                <div class="carousel-caption d-none d-md-block">
	                    <h3 class="txt_shadow">我不是一个伟大的程序员，我只是一个具有良好习惯的优秀程序员</h3>
	                    <p class="txt_shadow">I am not a great programmer, I am just a good programmer with good habits. </p>
	                </div>
	            </div>
	            <!-- Slide Three - Set the background image for this slide in the line below -->
	            <div class="carousel-item"
	                 style="background-image: url('https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1515063331413&di=de07b2eb50799360c9bf5c378da23bbf&imgtype=0&src=http%3A%2F%2Fpic.99wed.com%2Fattachment%2FMon_1107%2F98_736564_b419d830ab0564c.jpg')">
	                <div class="carousel-caption d-none d-md-block">
	                    <h3 class="txt_shadow">你们中大多数人都熟悉程序员的美德，有三种：那就是懒惰、急躁和傲慢</h3>
	                    <p class="txt_shadow">Most of you are familiar with the programmer's virtues, and there are three: laziness,
	                        impatience, and arrogance. </p>
	                </div>
	            </div>
	        </div>
	    <#-- <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-slide="prev">-->
	    <#-- <span class="carousel-control-prev-icon" aria-hidden="true"></span>-->
	    <#-- <span class="sr-only">Previous</span>-->
	    <#-- </a>-->
	    <#-- <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-slide="next">-->
	    <#-- <span class="carousel-control-next-icon" aria-hidden="true"></span>-->
	    <#-- <span class="sr-only">Next</span>-->
	    <#-- </a>-->
	    </div>
	</header>
	<#-- e-slide-header-->
	
	<!-- Page Content -->
	<section class="py-5">
	    <div class="container container-fluid">
	        <h1>全栈之路 —— 摆码王子的个人博客</h1>
	    </div>
	</section>
	
	<#-- s-footer -->
	<#include "public/footer.ftl">
	<#-- e-footer -->
	
	<#-- JS -->
	<#include "public/front_js.ftl">
	
	</body>
	</html>

接下来就能再访问localhost:8080/ 就能看到index.ftl的内容丰富了很多，包含了一些js，css

# 5. Dao层开发

这一部分主要总结了在创建user之后，如何创建Blog的增删改查。相比于User增加的地方：能够在浏览器网页页面实现增和查，并且通过css和js的渲染使文本更好看。

## 5.1 文件内容的修改
### 5.1.2 pom.xml 的修改
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

### 5.1.1 application.properties 的修改
     mybatis.type-aliases-package=wpyk.blog.entity

### 5.1.3 entity文件夹与Bean

在wpyk.blog下面创建entity文件夹，其本质和bean是一样的，用那种都行。  
**注意1** 一般任何一个entity，都留一个无参的构造器，这样框架想要new一个这样的对象的时候不会抱错。不然容易发生空指针错误。  
**注意2** 对于web架构中的对象，在view，controller端有可能不能以不变的形式出现，即从浏览器获取数据的bean和通过controller实现的bean，虽然都是为了传递一定的参数，但是其属性名称可能无法一一对应，并且在实际项目监理过程中也不能一一对应。这时就要建立这些bean之间的构造器，如下面的代码中的注意2，就通过BlogView构建出了blog.  


	package wpyk.blog.entity;
	
	import java.util.Date;
	
	import wpyk.blog.entity.vo.BlogView;
	
	public class Blog {
    private int id;

    private String title;
    
    private String summary;
    
    private Date releaseDate;
    
    private int clickHit;
    
    private int replyHit;
    
    private String content;
    
    private String keyword;
    
    // 注意1
    public Blog() {
        
    }
    
    //注意2
    public Blog(BlogView blogView) {
        this.title = blogView.getTitle();
        this.content = blogView.getHtmlMaterial();
    }
    
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getSummary() {
        return summary;
    }

    public void setSummary(String summary) {
        this.summary = summary;
    }

    public Date getReleaseDate() {
        return releaseDate;
    }

    public void setReleaseDate(Date releaseDate) {
        this.releaseDate = releaseDate;
    }

    public int getClickHit() {
        return clickHit;
    }

    public void setClickHit(int clickHit) {
        this.clickHit = clickHit;
    }

    public int getReplyHit() {
        return replyHit;
    }

    public void setReplyHit(int replyHit) {
        this.replyHit = replyHit;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }

    public String getKeyword() {
        return keyword;
    }

    public void setKeyword(String keyword) {
        this.keyword = keyword;
    } 
    
}



### 5.1.4 配置相关的 Service

*与上文中说到的相同。之前某个类访问数据库的时候我们给文件夹起的名字叫mapper，这里新建一个叫dao的文件夹，用于实现对数据库的访问。*  
与User.markdown文件中说到的业务流程相似，当通过controller访问某个连接的时候，服务器这边能够找打一个Service， Service会new一个同名的Dao对象，然后通过与该Dao对象映射的.xml文件来实现业务逻辑。这个**映射的实现方式是在.xml文件中的namespace**中指定其对应的Dao。下面是Service， Dao和.xml的代码：   
Service:

    package wpyk.blog.service;

	import java.util.List;
	
	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.stereotype.Service;
	
	import wpyk.blog.dao.BlogDao;
	import wpyk.blog.entity.Blog;
	import wpyk.blog.entity.vo.BlogView;
	
	@Service
	public class BlogService {
	
	@Autowired
	private BlogDao blogDao;
	
		public List<Blog> queryBlog(){
			List<Blog> list = blogDao.queryBlog();
			return list;
		}
		
		public BlogView queryById(int id) {
			return new BlogView(blogDao.queryById(id));
		}
		
		public void addBlog(Blog blog) {
			blogDao.addBlog(blog);
		}
		
		public void deleteBlog(int id) {
			blogDao.deleteBlog(id);
		}
		
		private void updateBlog(Blog blog) {
			blogDao.updateBlog(blog);
		}
	}

### 5.1.5  BlogDao 文件

    package wpyk.blog.dao;

	import java.util.List;
	
	import wpyk.blog.entity.Blog;
	import wpyk.blog.entity.vo.BlogView;
	
	public interface BlogDao {
		
		//增
		public void addBlog(Blog blog);
		//删
		public void deleteBlog(int id);
		//改
		public void updateBlog(Blog blog);
		//查
		public List<Blog> queryBlog();
		//query by id
		public Blog queryById(int id);
	}
### 5.1.6  Mapper.xml文件

    <?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE mapper
	PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
	"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
	<mapper namespace="wpyk.blog.dao.BlogDao">
		<select id="queryBlog" resultType="Blog">
			SELECT * FROM t_blog 
		</select>
		
		<select id="queryById" resultType="Blog">
			SELECT * FROM t_blog b WHERE b.id = #{id}
		</select>
	
		<insert id="addBlog">
			insert into t_blog(title, summary, releaseDate, clickHit, replyHit,content,keyword)
			values(#{title}, #{summary}, #{releaseDate}, #{clickHit}, #{replyHit},#{content},#{keyword})
		</insert>
		
		<delete id="deleteBlog">
			delete from t_blog b where b.id = #{id}
		</delete>
		
		<update id="updateBlog">
			update t_blog
			<set>
				<if test="title!=null and title!=''">
			 		title=#{title},
			 	</if>
			 	<if test="summary!=null and summary!=''">
			 		summary=#{summary},
			 	</if>
			 	<if test="content!=null and content!=''">
			 		content=#{content},
			 	</if>
				<if test="clickHit!=null">
					clickHit=#{clickHit},
				</if>
				<if test="replyHit!=null">
					replyHit=#{replyHit},
				</if>
				<if test="keyWord!=null and keyWord!=''">
			 		keyword=#{keyword},
			 	</if>
			</set>
			where id=#{id}
		</update>

	</mapper>



## 5.2 Controller 的编写

Controller的编写是这个Blog项目中最重要的东西，因此单独取出来作为一个部分。注意，下方代码目前和js，css整合了的方法是addBlog和queryById.

    package wpyk.blog.controller;

	import java.util.List;
	
	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.stereotype.Controller;
	import org.springframework.web.bind.annotation.PathVariable;
	import org.springframework.web.bind.annotation.RequestBody;
	import org.springframework.web.bind.annotation.RequestMapping;
	import org.springframework.web.bind.annotation.RestController;
	import org.springframework.web.servlet.ModelAndView;
	
	import wpyk.blog.entity.Blog;
	import wpyk.blog.entity.vo.BlogView;
	import wpyk.blog.service.BlogService;
	
	@Controller
	public class BlogController {
	
		@Autowired
		private BlogService blogService;
		
		@RequestMapping("/blogs/all")
		public List<Blog> queryBlog(){
			return blogService.queryBlog();
		}
		
		@RequestMapping("/blog/delete/{id}")
		public void deleteBlog(@PathVariable int id){
			blogService.deleteBlog(id);
		}
		
		@RequestMapping("/blog/{id}")
		public ModelAndView queryById(ModelAndView modelAndView, @PathVariable int id){
			BlogView blogView = blogService.queryById(id);
			modelAndView.addObject("article", blogView);
			modelAndView.setViewName("article");
			return modelAndView;
		}
		
		@RequestMapping("/blog/update")
		public void updateBlog(@RequestBody int id){
			blogService.deleteBlog(id);;
		}
		
		@RequestMapping("/admin/blog/add")
		public String addBlogPage(){
			return "admin/blogadd";
		}
		
		@RequestMapping("/admin/blogadd.f")
		public void addBlog(BlogView blogView){
			blogService.addBlog(new Blog(blogView));
		}
		
	}

### 5.2.1 addBlog()方法的实现

我们来简单想一下写一个blog的逻辑，当在浏览器中输入../blog/add的时候，应该出来一个能够写东西的框，就像markdown一样。展示在前端的是js文件，因此在下面的代码中，我们要做的是当用户访问../blog/add时，给他返回一个可编辑文本的页面，即项目中的blogadd.ftl

//根据框架的约束，返回是String的时候自动对应到application.properties里配置的ftl文件中。

   		
	//根据框架的约束，返回是String的时候自动对应到application.properties里配置的ftl文件中。
	@RequestMapping("/admin/blog/add")
    public String addBlogPage(){
			return "admin/blogadd";
	}

该ftl文件为：
   
    <!DOCTYPE html>
	<html lang="zh">
	<#-- 写博客 -->
	<head>

	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <meta name="viewport" content="width=device-width, initial-scale=1">
	    <meta name="description" content="">
	    <meta name="author" content="">
	
	    <title>Full-Stack 系统后台管理</title>
	
	    <!-- Bootstrap Core CSS -->
	    <link href="../../vendor/admin/bootstrap/css/bootstrap.min.css" rel="stylesheet">
	
	    <!-- MetisMenu CSS -->
	    <link href="../../vendor/admin/metisMenu/metisMenu.min.css" rel="stylesheet">
	
	    <!-- Custom CSS -->
	    <link href="../../dist/admin/css/sb-admin-2.css" rel="stylesheet">
	
	    <!-- Morris Charts CSS -->
	    <link href="../../vendor/admin/morrisjs/morris.css" rel="stylesheet">
	
	    <!-- Custom Fonts -->
	    <link href="../../vendor/admin/font-awesome/css/font-awesome.min.css" rel="stylesheet" type="text/css">
	
	    <!-- EditorMD -->
	    <link rel="stylesheet" href="../../vendor/editor/css/editormd.css"/>
	
	    <!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
	    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
	    <!--[if lt IE 9]>
	    <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
	    <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
	    <![endif]-->
	
	    <!-- 自定义样式 -->
	    <link rel="stylesheet" href="/css/public.css">
		</head>
	
	<body>
	
	<div id="wrapper">
	<#-- s 导航 -->
	<#include "public/nav.ftl">
	<#-- e 导航 -->
	
	<#-- s 页面内容 -->
	    <div id="page-wrapper">
	    <#-- s 页面内容 -->
	        <form>
	        <#-- s 隐藏字段 -->
	            <input name="mdMaterial" id="id_input_md" type="hidden">
	            <input name="htmlMaterial" id="id_input_html" type="hidden">
	            <input name="description" id="id_input_article_description" type="hidden">
	            <input name="rawTags" id="id_input_article_tags" type="hidden">
	        <#-- e 隐藏字段 -->
	        <#-- s 标题、标签等 -->
	            <div class="row">
	                <div class="col-sm-12">
	                    <div class="input-group">
	                        <div class="row">
	                            <div class="col-md-12"></div>
	                        </div>
	                    <#-- 文章标题 -->
	                        <input name="title" type="text" class="form-control" placeholder="标题">
	                        <div class="row">
	                            <div class="col-md-12"></div>
	                        </div>
	                        <span class="input-group-btn">
	                        <button id="id_btn_blog_submit" class="btn btn-primary" type="button">提交</button>
	                    </span>
	                    </div>
	                </div>
	            </div>
	        <#-- e 标题 -->
	        </form>
	        <div class="row">
	            <div class="col-sm-12">
	                <div id="test-editormd">
	                <#-- 文章内容 -->
	                    <textarea style="display:none;"></textarea>
	                </div>
	            </div>
	        </div>
	    <#-- e 页面内容 -->
	    </div>
	<#-- e 页面内容 -->
	
	</div>
	
	<#-- s 文章描述内容填写模态框 -->
	<div class="modal fade" tabindex="-1" role="dialog" id="id_modal_article_detail">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span>
                </button>
                <h4 class="modal-title">文章详情</h4>
            </div>
            <div class="modal-body">
            <#-- s 模态内容 -->
                <div class="form-group">
                    <label for="id_input_article_description_in_modal">对文章内容的描述</label>
                    <textarea type="text" class="form-control" id="id_input_article_description_in_modal" placeholder="Description"></textarea>
                </div>
                <div class="form-group">
                    <label for="id_input_article_tags_in_modal">为文章添加标签（以逗号分隔）</label>
                    <input type="text" class="form-control" id="id_input_article_tags_in_modal" placeholder="Tags">
                </div>
            <#-- e 模态内容 -->
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-default" data-dismiss="modal">取消</button>
                <button type="button" class="btn btn-primary" id="id_btn_release_in_modal">确认发布</button>
            </div>
        </div><!-- /.modal-content -->
    </div><!-- /.modal-dialog -->
	</div><!-- /.modal -->
	<#-- e 文章描述内容填写模态框 -->
	
	<!-- jQuery -->
	<script src="../../vendor/admin/jquery/jquery.min.js"></script>
	
	<!-- Bootstrap Core JavaScript -->
	<script src="../../vendor/admin/bootstrap/js/bootstrap.min.js"></script>
	
	<!-- Metis Menu Plugin JavaScript -->
	<script src="../../vendor/admin/metisMenu/metisMenu.min.js"></script>
	
	<!-- Morris Charts JavaScript -->
	<script src="../../vendor/admin/raphael/raphael.min.js"></script>
	<script src="../../vendor/admin/morrisjs/morris.min.js"></script>
	<script src="../../data/morris-data.js"></script>
	
	<!-- Custom Theme JavaScript -->
	<script src="../../dist/admin/js/sb-admin-2.js"></script>
	<script src="../../vendor/editor/editormd.min.js"></script>
	
	<#-- 自定义 js -->
	<script src="../../js/b_blogadd.js"></script>
	<script src="../../js/public.js"></script>
	</body>
	
	</html>

此时页面显示为：
![](https://i.loli.net/2020/01/14/P3Epz9KqZBsRbMc.png)
当我们完成编辑后，按下提交按钮的一瞬间，我们在View端输入的内容，会被赋值给vo中的类，即BlogView，然后传给下面的这个方法。
		
		  

		@RequestMapping("/admin/blogadd.f")    
		public void addBlog(BlogView blogView){    
			blogService.addBlog(new Blog(blogView));  
		}  


为什么提交后会到上面那个链接呢，这里需要仔细看一下js文件里面的内容： 
![](https://i.loli.net/2020/01/15/LS2jhw3aJUsPD9M.png)  
文本框中圈中的js文件是实现blog提交页面活起来，并且点击提交按钮后弹出模态框的功能。接下来我们解释一下html和js文件是如何联动，实现blog的添加功能的。

首先我们来看一下js文件，最开头加载的是页面显示类似markdown输入框的脚本，是edit md开源项目提供的。  
![3.png](https://i.loli.net/2020/01/15/OuYn1oUqVhjQ4vp.png)  

写完博客，点击提交之后出现了模态框。以模态框中出现的“确认提交”按钮为例，说一下html和js是如何协作将输入的内容传递回controller。
![4.png](https://i.loli.net/2020/01/15/naADJU2dmKeI6tW.png)  


模态框中有“对内容的描述” 和 “为文章添加标签”两个小的文本框，即有两个文本框的内容。当我们点击确认发表的时候，“确认发表”这个按钮的id："id_btn_release_in_modal",在js里，其同id的代码，如下图中红色框圈起来的，这个XXX.bind('click'，function（){method1，method2}，代表绑定一个click事件，当**点击**的时候，对这个绑定的id，执行后面的function


![5.png](https://i.loli.net/2020/01/15/QNicO9ur3Jxkmp8.png)  


接下来我们看一下这两个方法做了什么，在js里搜索saveDetailText方法，和 submitBlogAddForm方法，如下图：  

![6.png](https://i.loli.net/2020/01/15/5mKF86SpPENOjXC.png)  

标出的1和2就是两个被执行的方法。其中1是通过'val'方法将后面的内容赋值给"id_input_article_description"，而这个参数是存在于html文件的form表单中的input参数。
 

### 5.2.2 queryById（）方法的实现

**我们在创建Service的时候，queryById的返回值是个Blog，但是js在网页中显示的是blogView，上文中提到的POJO之间的相互转化不要忘记。**


    @RequestMapping("/blog/{id}")
	//modelAndView 是框架自动注入的，后面的@PathVariable是去url里的参数的
	public ModelAndView queryById(ModelAndView modelAndView, @PathVariable int id){
		BlogView blogView = blogService.queryById(id);
		modelAndView.addObject("article", blogView);
		modelAndView.setViewName("article");
		return modelAndView;
	}