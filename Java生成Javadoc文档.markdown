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
在实际开发过程中，工程项目包含大量的类，同时由多人团队参与开发。javadoc就像一份说明性文档，即使自己不是某个环节的实际开发者，也能够文档中的类了解并使用。这就是api文档，通过文档能够知道每个类有什么样的方法，如何使用，并且在不需要明确知道该类的具体实现的情况下实现对这个类的使用。即通过api编程。
