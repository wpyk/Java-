[![l03BNt.md.png](https://s2.ax1x.com/2020/01/04/l03BNt.md.png)](https://imgchr.com/i/l03BNt)

# 新建一个dynamic web project-> config to maven project -> pom.xml 配置,build tag 里加上<sourceDirectory>src</sourceDirectory>> -> mvn clean eclipse:clean eclipse:eclipse-> mvn install  
# 配置好环境后，创建java bean文件 Greeting.java，创建controller文件GreetingController.java 以及入口文件Application.java.  
*这三个文件中，controller是通过url匹配接收80端口传入的参数信息，并将这个参数传递至bean文件创建新的java对象，而application的main函数是springbootapplication，整个项目的入口。*  
# 在文件所在目录shift+右键打开powershell，运行mvn spring-boot:run,跑起来后通过localhost：http://8080/greeting 来访问默认设置，在greeting后加上?name=wpyk来改变默认参数。