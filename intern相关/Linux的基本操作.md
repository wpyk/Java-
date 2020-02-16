# 1. putty
PuTTY是一款开源(Open Source Software)的连接软件，主要由Simon Tatham维护，使用MIT许可证授权。包含的组件有：PuTTY, PuTTYgen,PSFTP, PuTTYtel, Plink, PSCP, Pageant,默认登录协议是SSH，默认的端口为22。Putty是用来远程连接服务器的，支持SSH、Telnet、Serial等协议的连接。其中最常用的是SSH。用它来远程管理Linux十分好用，其主要优点如下：

◆ 完全免费;

◆ 在Windows 9x/NT/2000下运行的都非常好;

◆ 全面支持SSH1和SSH2；

◆绿色软件，无需安装，下载后在桌面建个快捷方式即可使用；

◆ 体积很小，不到1M；

◆ 操作简单，所有的操作都在一个控制面板中实现。

## 1.1 下载
下载地址： https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html  
安装 64-bit: putty-64bit-0.73-installer.msi

## 1.2 生成秘钥对
在申请完AWS的EC2电脑时， 有一个服务叫密钥对，create后可以生成一个.pem的密钥文件。
在windows启动PuTTYgen -> load -> all files -> *.pem -> save private key -> 存储成同名的 .ppk文件。

## 1.3 远程登录
在PuTTY里面登录，需要做以下几步：  
1. Host name or IP  
   这里的输入方式是用户名@ip，首次登录EC2的时候，默认的用户是centos，是权限非常高的用户。ip地址在aws ec2登陆后，“正在运行的实例”中能够看到。  
2. 新建一个属于这个hostname的session  
   选中default，在上方空栏里输入session的名字，然后单击save。  
3. 密钥配对  
   为了连接到远程服务器，我们需要携带有远程服务器的密钥。在之前我们生成了.ppk的文件，要将这个文件绑定在PuTTY上，发送连接申请的时候一起发过去。connetction -> SSH -> auth,选定.ppk文件，然后点open就好了。

# 2. Linux基本操作指令

## 2.1 查
知道自己在哪里，有什么文件是很重要的。登陆进去之后，在当前账户的根目录下面。  
1. 切换到服务器的根目录：   
	`cd /`  
2. 切换回当前用户的根目录：  
	`cd ~`  
3. 进入*** 文件：  
	`cd ***`  
4. 查看某路径下的文档：  
	`ls` 或 `ls -a`  
后者能够将隐藏的文档也列出来。

## 2.2 增
可以通过命令直接创建新的文件夹或者文档
1. 创建新的文件夹， 通过下述指令就能传建一个名为temp的文件夹：   
	`mkdir temp`  
2. 创建新的.txt文件  
	`touch 1.txt`  
3. 修改文件内容  
	3.1 `vim 1.txt`  
	3.2 `i`  插入模式  
    3.3 `esc` 结束编辑  
	3.4 `:wq` 退出vim模式  
## 2.3 删
**删除文件**  
	`rm [options] name `  
	`-i 删除前逐一询问确认。   `   
	`-f 即使原档案属性设为唯读，亦直接删除，无需逐一确认。`    
	`-r 将目录及以下之档案亦逐一删除。`  
	`rm -f  /opt/test.txt   #将会强制删除/opt/test.txt这个文件`  
**删除文件夹**  
	`rm -rf /opt/svn #将会删除/opt/svn/目录以及其下所有文件夹，包括文件`  
通过以上两个实例能够看出，-r是一个向下兼容的命令，当-rf的时候，是目录下所有子文件，-f的时候，只是强行删除某一个。  

## 2.4 改
对文件的修改可以通过上面说到的vim命令实现。  
这里说一下对于文档的拷贝： cp， rcp和scp。cp是实现同一个服务器的复制操作的，rcp和scp是远程服务器的复制操作，区别在于scp加密，而rcp不加密。

cp [options] source... directory
参数说明：

-a：此选项通常在复制目录时使用，它保留链接、文件属性，并复制目录下的所有内容。其作用等于dpR参数组合。  
-d：复制时保留链接。这里所说的链接相当于Windows系统中的快捷方式。  
-f：覆盖已经存在的目标文件而不给出提示。  
-i：与-f选项相反，在覆盖目标文件之前给出提示，要求用户确认是否覆盖，回答"y"时目标文件将被覆盖。  
-p：除复制文件的内容外，还把修改时间和访问权限也复制到新文件中。   
-r：若给出的源文件是一个目录文件，此时将复制该目录下所有的子目录和文件。  
-l：不复制文件，只是生成链接文件。 

eg：  
使用指令"cp"将当前目录"test/"下的所有文件复制到新目录"newtest"下，输入如下命令：   

`$ cp –r test/ newtest   `

rcp [-pr][源文件或目录][目标文件或目录]

scp [options] source dest

scp常用的命令选项:

`-P`:数据传输默认端口，默认是22
`-r`:递归拷贝整个目录
`-i`:指定密钥文件，参数直接传递给ssh使用
`-l`:限定网速，以Kbit/s为单位
`-C`:允许压缩
`-1,-2`:强制scp命令使用ssh1或者ssh2协议
`-4,-6`:使用ipv4或者ipv6寻址
下面是比较常用的scp命令使用的例子。

本地文件传输到远程服务器
命令格式:

scp test.txt root@192.168.1.1:/home/

将test.txt文件复制到目标服务器（192.168.1.1）下的home文件夹下。

本地文件夹传输到远程服务器
命令格式:

scp -r test root@192.168.1.1:/home/

将test整个文件夹复制到目标服务器下的home文件夹下。

远程服务器文件传输到本地
命令格式:

scp root@192.168.1.1:/home/test.txt test

将远程服务中home目录下的test.txt文件，复制到本地的test目录下

远程服务器文件夹复制到本地

scp -r root@192.168.1.1:/home/test /Users/jjz

将远程服务器中home目录下的test整个目录复制到本地的jjz目录下

scp命令指定密钥文件

scp test.txt root@192.168.1.1:/home/ -i ~/.ssh/id_rsa.1

这里指定了密钥文件id_rsa.1做为ssh的连接参数，不使用默认的密钥文件。


链接：https://www.jianshu.com/p/d21a5d4818a5

https://blog.csdn.net/u011794238/article/details/50351354

https://lbb4511.gitbooks.io/linux-command/content/cmd/08.html