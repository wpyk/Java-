# JDK相关知识与操作
## 1. JDK是什么
Java Development Kit，是java开发工具包，给程序员使用java语言编写java程序提供所需的开发工具包。其包含JRE，同时还包含了编译java源码的编译器javac，还包含了很多java程序调试和分析的工具：jconsole，jvisualvm等工具软件，还包含了java程序编写所需的文档和demo例子程序。jdk可以编译与运行java代码。

*与jre的区别*  
jre 是java运行时环境，包含了java虚拟机，java基础类库。是使用java语言编写的程序运行所需要的软件环境，是提供给想运行java程序的用户使用的。但是只有jre环境是无法做java开发的。

## 下载与安装
下载路径： https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html  
推荐使用临时邮箱从甲骨文下载内容。

安装：随便找网上安装教程就行，记得自己装在哪里了。     
有一点需要注意的是，安装jdk的时候是先安装了jdk后安装了jre，要注意这两个安装的文件不能再同一个文件夹，即不能把jre安装到jdk文件夹，否则jdk的安装文件会被删除。但是可以在java文件夹下分别创建jdk和jre的文件夹，这样没问题。    
https://www.jianshu.com/p/f4b4c6177046 这一篇说的挺好的，包括了环境配置。
https://www.cnblogs.com/cnwutianhao/p/5487758.html   
环境变量配置： 找网上教程就行了，配多了自己就会了。可以参见maven的环境变量配置。

安装好之后通过： java，javac 和 java -version三个指令检查自己安装的是否成功。

## 重要的组件
### javac编译器

javac命令是将源代码编程成class字节码文件，因为我们的JVM虚拟机是执行class字节码文件的，不是执行源代码，JVM虚拟机是不认识源代码的。javac能将java文件便以为字节码的.class文件，这个文件能够瓯北JVM虚拟机执行。  
当java文件中有了结构包，javac指令会有所不同，如：  javac -d之类的，具体的根据项目中包结构的不同而不同。 


### java指令

java xxx.class是发出了执行class文件的指令。即：java指令时运行字节码的时候使用的。
