##新建一个project的流程
 
 - 建的工程类别叫 dynamic web project

 - 转成maven工程，详细操作参见MavenNote

 - 用maven导入servlet 包，详细操作参见MavenNote

 - 将工程转化成 UTF-8

 - 创建servlet

 - 在web.xml中配置servlet  
配置xml时指定class要指定其包名，eg: com.wpyk.Login

```xml
<servlet>
<servlet-name>login</servlet-name>
<servlet-class>com.wpyk.Login</servlet-class>
</servlet>
```