# Git的使用教程
## 1. 下载
下载地址 ： https://git-scm.com/download/win  
下载后一路默认安装就行。

## 2. GitHub（GitLab）的仓库
从网页端新建就行，复制clone的url

## 3. 设置ssh

### 3.1 SSH 和 HTTPS(S) 的区别

在讨论SSH或者HTTPS之前，先要了解一下*数字签名*和*数字证书*，有一个非常好的文章讲解，链接如下：

中文 http://www.ruanyifeng.com/blog/2011/08/what_is_a_digital_signature.html  
英文 http://www.youdzone.com/signature.html


SSH ： SSH以非对称加密实现身份验证。身份验证有多种途径，例如其中一种方法是使用自动生成的公钥-私钥对来简单地加密网络连接，随后使用密码认证进行登录；另一种方法是人工生成一对公钥和私钥，通过生成的密钥进行认证，这样就可以在不输入密码的情况下登录。任何人都可以自行生成密钥。公钥需要放在待访问的电脑之中，而对应的私钥需要由用户自行保管。认证过程基于生成出来的私钥，但整个认证过程中私钥本身不会传输到网络中。在类Unix系统中，已许可登录的公钥通常保存在用户 /home 目录的 '~/.ssh/authorized_keys' 文件中，该文件只由SSH使用。

当远程机器持有公钥，而本地持有对应私钥时，登录过程不再需要手动输入密码。另外为了额外的安全性，私钥本身也能用密码保护。 私钥会保存在固定位置，也可以通过命令行参数指定（例如ssh命令的“-i”选项）。ssh-keygen是生成密钥的工具之一。SSH也支持基于密码的身份验证，此时密钥是自动生成的。若客户端和服务端从未进行过身份验证，SSH未记录服务器端所使用的密钥，那么攻击者可以模仿服务器端请求并获取密码，即中间人攻击。但是密码认证可以禁用，而且SSH客户端在发现新密钥或未知服务器时会向用户发出警告。（来自维基百科 ： https://zh.wikipedia.org/wiki/Secure_Shell）

  
优缺点：  
	1. 架设git服务器时通常使用SSH协议作为传输协议。其方便架设，并且经过验证授权，安全且方便。  
	2. 缺点： 无法通过SSH协议实现匿名访问。在访问服务器之前已经将公钥放在了要访问的服务器那边。另外，SSH服务端一般使用22端口，企业防火墙有可能没有打开该端口。


HTTP(S): 是一种通过计算机网络进行安全通信的传输协议。HTTPS经由HTTP进行通信，但利用SSL/TLS来加密数据包。HTTPS开发的主要目的，是提供对网站服务器的身份认证，保护交换数据的隐私与完整性。

优缺点：
	1. HTTPS使用用户名／密码授权，下载时只要知道http url，可以随意克隆git项目。使用频率不高的情况下，能够免去生成和配置SSH密钥的麻烦。
	2. 企业防火墙一般会打开 80 和 443 这两个常见的http和https协议的端口，使用没有什么安全限制。
	3. 缺点非常明显，push的时候需要每次输入口令，麻烦。

综上，在安装git的时候，选择SSH传输协议。


### 3.2 如何生成自己的SSH 

**首先查看自己是否已经有SSH KEY**  
$ cd ~/.ssh
$ ls  
如果已经存在id_rsa.pub 或 id_dsa.pub 文件，说明已经有了，没有的话要创建：  
$ ssh-keygen -t rsa -C "your_email@example.com"  
-t 指定密钥类型，默认是 rsa ，可以省略。  
-C 设置注释文字，比如邮箱。  
-f 指定密钥文件存储文件名。  
其中上面的引号里内容是任意的，类似于commit最后的message，不一定要是邮箱名。我在创建的时候这条message写的是创建这个密钥的电脑名称。  
接下来会提示输入密码，这个密码是push时候用到的， 可以选择输入，或者不输入直接回车跳过。其实在电脑是安全的情况下，这个密码并不是非常的必须，可以跳过。  

**创建成功后，会有如下提示信息：**  

*Your identification has been saved in /c/Users/you/.ssh/id_rsa.  
 Your public key has been saved in /c/Users/you/.ssh/id_rsa.pub.  
 The key fingerprint is:  
 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com*

**将创建后的SSH KEY放到github/gitlab中**  
复制： 
$ clip < ~/.ssh/id_rsa.pub  
登录账号，进入setting，添加SSH，然后给这个钥匙起个名字。  
*注意*：使用上述命令复制的时候出现过一次汉字的乱码，可以用notepad++打开SSH所在文件中的.pub
自己手动复制。  

**测试SSH key**  
$ ssh -T git@github.com   

*出现警告代码*  
*The authenticity of host 'github.com (207.97.227.239)' can't be established.  
 RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.  
 Are you sure you want to continue connecting (yes/no)?*

输入yes  
如果在创建ssh的时候自己设定了密码，那再上面yes后回车需要输入密码。输入密码/回车 后会看到：  
*Hi username! You've successfully authenticated, but GitHub does not
provide shell access.*  
说明SSH密钥已经成功设置了。

参考文档： https://www.cnblogs.com/ayseeing/p/3572582.html