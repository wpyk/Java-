# 1. Tomcat
# 2. Tomcat的安装
## 2.1 下载
地址： https://tomcat.apache.org/index.html
选择binary的core的zip 

## 2.2 安装
解压 -> bin->startup.bat->双击运行，就跑起来了。

# 3. Tomcat的文档结构
进入tomcat安装目录下：

|-- **bin  该目录下存放的是二进制可执行文件**  
|   |-- bootstrap.jar		tomcat启动时所依赖的一个类，在启动tomcat时会发现Using CLASSPATH: 是加载的这个类    
|   |-- catalina-tasks.xml		定义tomcat载入的库文件，类文件  
|   |-- catalina.bat  
|   |-- catalina.sh		                 tomcat单个实例在Linux平台上的启动脚本  
|   |-- commons-daemon-native.tar.gz	           jsvc工具，可以使tomcat已守护进程方式运行，需单独编译安装  
|   |-- commons-daemon.jar		           jsvc工具所依赖的java类  
|   |-- configtest.bat  
|   |-- configtest.sh	        tomcat检查配置文件语法是否正确的Linux平台脚本 
|   |-- cpappend.bat  
|   |-- daemon.sh		tomcat已守护进程方式运行时的，启动，停止脚本  
|   |-- digest.bat  
|   |-- digest.sh  
|   |-- setclasspath.bat    
|   |-- setclasspath.sh    
|   |-- shutdown.bat    tomcat服务器在window平台下关闭  
|   |-- shutdown.sh		tomcat服务在Linux平台下关闭脚本  
|   |-- startup.bat              tomcat服务在windows平台下启动脚本 
|   |-- startup.sh		         tomcat服务在Linux平台下启动脚本  
|   |-- tomcat-juli.jar   
|   |-- tomcat-native.tar.gz	 使tomcat可以使用apache的apr运行库，以增强tomcat的性能需单独编译安装    
|   |-- tool-wrapper.bat  
|   |-- tool-wrapper.sh  
|   |-- version.bat  
|   |-- version.sh		查看tomcat以及JVM的版本信息  
|-- **conf			配置文件目录**  
|   |-- catalina.policy		配置tomcat对文件系统中目录或文件的读、写执行等权限，及对一些内存，session等的管理权限  
|   |-- catalina.properties		配置tomcat的classpath等  
|   |-- **context.xml**			tomcat的默认context容器,对所有应用的统一配置，通常我们不会去配置它。  
|   |-- logging.properties		配置tomcat的日志输出方式  
|   |-- **server.xml**			    配置整个服务器信息。例如修改端口号，添加虚拟主机等    
|   |-- **tomcat-users.xml**	       存储tomcat用户的文件，这里保存的是tomcat的用户名及密码，以及用户的角色信息。可以按着该文件中的注释信息添加tomcat用户，然后就可以在Tomcat主页中进入Tomcat Manager页面了  
|   |-- **web.xml**				tomcat的应用程序的部署描述符文件.这个文件中注册了很多MIME类型，即文档类型。这些MIME类型是客户端与服务器之间说明文档类型的，如用户请求一个html网页，那么服务器还会告诉客户端浏览器响应的文档是text/html类型的，这就是一个MIME类型。客户端浏览器通过这个MIME类型就知道如何处理它了。当然是在浏览器中显示这个html文件了。但如果服务器响应的是一个exe文件，那么浏览器就不可能显示它，而是应该弹出下载窗口才对。MIME就是用来说明文档的内容是什么类型的！  
|-- **lib     Tomcat的类库，里面是一大堆jar文件。**  
|-- **logs		日志文件默认存放目录**  
|-- **temp    存放Tomcat的临时文件，这个目录下的东西可以在停止Tomcat后删除**  
|   |-- safeToDelete.tmp  
|-- **webapps		          tomcat默认存放应用程序的目录**  
|   |-- docs	tomcat文档  
|   |-- examples                  tomcat自带的一个独立的web应用程序例子  
|   |-- host-manager              tomcat的主机管理应用程序  
|	|   |-- META-INF	          整个应用程序的入口，用来描述jar文件的信息    
|	|   |   |-- context.xml    当前应用程序的context容器配置，它会覆盖tomcat/conf/context.xml中的配置      
|	|   |-- WEB-INF		 用于存放当前应用程序的私有资源  
|	|   |   |-- classes		 用于存放当前应用程序所需要的class文件   
|       |   |	|-- lib		         用于存放当前应用程序锁需要的jar文件    
|	|   |   |-- web.xml		当前应用程序的部署描述符文件，定义应用程序所要加载的serverlet类，以及该程序是如何部署的  
|   |-- manager              tomcat的管理应用程序  
|   |-- ROOT	             一个特殊的项目，在地址栏中没有给出项目目录时，对应的就是ROOT项目。    
`-- work	用于存放JSP应用程序在部署时编译后产生的class文件  

# 4. 安装Jenkins
下载Jenkins的war包放在webapp文件夹下面然后启动tomcat，就可以了