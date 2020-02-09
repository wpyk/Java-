# 1. Maven 的安装配置

1. Marven 的安装过程
	1. 先从Google进行下载： https://maven.apache.org/download.cgi, 选择Binary zip archive.
	2. 解压，配置环境变量 参考https://www.cnblogs.com/liuhongfeng/p/5057827.html
	3. 检验是否安装成功 cmd: mvn -version

2.给工程配置 Marven
	1. 在eclipse中Java程序上右击-configure-convert to maven project. 此时在project中出现pom.xml文件
	2. 打开pom.xml文件，在</build > 后加入：
		<dependencies>
			<!-- https://mvnrepository.com/artifact/javax.servlet/servlet-api -->
			<dependency>
				<groupId>javax.servlet</groupId>
				<artifactId>servlet-api</artifactId>
				<version>2.5</version>
				<scope>provided</scope>
			</dependency>
		</dependencies>
	    eclipse会自动下载相应版本的文件包，并名为“servlet-api.jar”文件包导入到该工程中。
		添加指令在Google中搜索需要的jar包和maven，如“servlet maven”，选择使用人数多的版本
	3.  下载的jar包出现在C:\Users\lenovo\.m2\repository位置
	
# 2. Maven 相关知识	  
**Maven 是一个项目管理工具，可以对 Java 项目进行构建、依赖管理。**  
Maven 能够帮助开发者完成以下工作：
构建  
文档生成    
报告  
依赖  
SCMs  
发布  
分发  
邮件列表  

注意：  
1. 创建项目的时候，项目结构要按照maven约定的格式来，这样Maven才能更好的管理项目。
2. mvn dependency:sources 下载依赖包的源码，