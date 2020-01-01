# Java 自动生成文档

eclipse能够将java项目自动生成带有注释的文档javadoc，用于从Java源代码生成HTML格式的API文档，HTML格式用于增加将相关文档链接在一起的便利性。

## 生成步骤

首先点击file--> export
![1.png](https://i.loli.net/2020/01/01/G3yNOfEhPUz9QRK.png)  
选择生成javadoc文件：  
![2.png](https://i.loli.net/2020/01/01/rUMjfN8IFXV6KYt.png)  
然后配置好相应的javadoc command，选择生成文件的存放路径以及public/private 等属性，如下图：  
![3.png](https://i.loli.net/2020/01/01/LKf1ybmkzHYXx9A.png)  
在之前选定的路径的文件处，会出现doc文件，如下图：  
![4.png](https://i.loli.net/2020/01/01/aTcBPM6bnpViFWj.png)  
点进去後有一个名为index.html的文件，单机并在浏览器中点开：  
![5.png](https://i.loli.net/2020/01/01/Sgb3MJQXNwLqho5.png)  
![6.png](https://i.loli.net/2020/01/01/w2lAUzfsXeHYxTP.png)  
就能够看到自己创建的java文档的信息了。  

## 好处  
生成的文档很好的显示了工程中不同类之间的api关系，对于理解工程很有帮助。
同时对于每一个类，文档能够识别出使用到的方法、构造器、继承等等关于文档的细节，提高了程序和工程的可读性。