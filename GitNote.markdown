# GitNote
## 1.什么是Git
Git是一个开源的分布式版本管理系统，由Linus通过C语言实现。其特点有：分布式（所有电脑上都有完整的版本库，不需要联网也能工作。同时由于没有中央版本库，增大了安全性，便捷性）、存储元数据，有分支功能，使用SHA-1哈希算法进行内容存储。

## 2.Git的常用操作
## 创建
首先在网页端创建一个Git的仓库，用来管理后续的文档版本。
按照创建和使用的流程，将常用git指令总结如下：  
### git clone [git URL]
通过上述指令将远程仓库克隆到本地
创建文档  
注意：（这段引用自廖雪峰老师的网站，网址：https://www.liaoxuefeng.com/wiki/896043488029600/896827951938304）
首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。  
不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的，前面我们举的例子只是为了演示，如果要真正使用版本控制系统，就要以纯文本方式编写文件。  

因为文本是有编码的，比如中文有常用的GBK编码，日文有Shift_JIS编码，如果没有历史遗留问题，强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。

创建了名为master.txt的文档（后续还要进行分支操作，为了能够清楚的看到merge操作的效果，文档的名称和将要push去的远程分支名是一样的。实际起名时并无这种要求）  

## add相关
## 查
创建了文档，或修改了文档，可以检查：
### git status     查看当前版本状态，是否有更改  
![git status.png](https://i.loli.net/2020/01/01/njBOeAvxodpPRY5.png)  
可以看到这里显示列新添加的文档，这些文档其实是untracked file 
## 增
接下来我们把它放置到index（缓存区）中：  
### git add [file name]  OR  git add .
前者是只添加单个文件，后者是所有改动了的文档都会被一起add 
![1.png](https://i.loli.net/2020/01/01/FxBqb1QHlzJ7Wtc.png)   
## 删改
如果想要撤销本次add的操作，分为以下两种情况，（1）单纯的想要撤销本次操作：   
### git reset HEAD [file name]  OR git rm --cached [file name]
注意：在索引中删除后，该文件在工作目录中依然存在。 此时如果使用 git rm [file name]，则在缓存区的文件和在工作目录中的文件将会被删除，并且不可恢复。
（2）已经add了的文件，在本地又做了修改。查看add之后文件修改内容的命令：  
### git diff       显示所有未添加至index的变量   
但是又不想要这个修改了，此时应选择用：  
### git checkout -- [file name]  
执行后，本地文件会被更新成之前缓存区的版本。  

注意：我遇到过一个问题，有两个本地文件，执行add操作后，从本地删除了其中一个文件。这个时候，再次执行以下add，之前的那次add就会被覆盖。


## commit

## 增
commit命令时将位于暂存区/缓存区/index/目录区 的文件添加到本地分支上去。
### git commit -m "message" 
打包，最好在message那里写一些针对本次提交的有说明性的文字，在日后想要寻找版本的时候会方便一些。当然，有些重要的提交可以通过打标签的方式进行强调和记忆。  

##查  
### git log  
查看commit的历史记录，在这里能看到单个commit的MD5值
### git show md5 
查看该md5对应的commit的改动明细
### git reflog
查看所有的commit操作，包括被git reset --hard了的命令。  
举例来说，加入现在处于developer分支上，进行了commit c4，但是这个commit被reset回了commit c3。这个时候使用git log是无法看到commit c4的，但是reflog可以，差别见下图：  
![git log git reflog.png](https://i.loli.net/2020/01/02/DHymxgVCWvTKQbr.png)  
此时的source tree的状态为：  
![source tree1.png](https://i.loli.net/2020/01/02/6dbW3RpuwTQCieN.png)  
如果找到commit c4的id， 并且执行git reset，再查看git log就能看到commit c4的信息了。 
![git log git reflog2.png](https://i.loli.net/2020/01/02/tD86bvsxgPwSQ7T.png)  
![source tree2.png](https://i.loli.net/2020/01/02/5B4yIROP62heLsH.png)


## 改
**修改commit的message**
###git commit --amend

**撤销commit**
假设现在有一个交master2.markdown 的文件，创建后commit了一次；    
![2.png](https://i.loli.net/2020/01/01/SMK5Qxsmr1ZoIfV.png)
然后再未push的情况下，进行了修改，然后又commit了一次：  
![3.png](https://i.loli.net/2020/01/01/hzYPnZduiykl9F8.png)  
继续修改，并再一次commit：    
![1.png](https://i.loli.net/2020/01/01/fJ7lxMv9HuTegmS.png)

记三次提交分别为1,2,3，则目前的提交记录可以表示为：  
1->2->3,此时head指向3。  
现在通过对上述几次提交进行修改来说明revert，reset和rebase的简单应用


### revert
### reset   
如果想要head从3的位置移动到1，执行：  
### $ git reset --soft eef9590fcacf42d4f767f82c812be34bf84b0577
后面那一长串就是commit 1 的id。执行前后都查了git log的记录。可以看出，在执行上面命令之前，git log 显示的是，当前head领先远端的origin master三个commit。执行完后，只领先一个，因此我们能够判断出head回到了1的位置。并且查询git status，能够看到2,3的修改被恢复到了缓存区。
![1.png](https://i.loli.net/2020/01/01/2eDsGymSudHoAjV.png)  
这个时候如果直接调用git commit ，可以生成一个新的提交包含2、3两次提 交的修改。  
在commit 1 那里，是第一次创建master2.markdown，文档的内容为：  
![1.png](https://i.loli.net/2020/01/01/HDq4tZsNgn13UzG.png)  
当我执行完reset命令后，commit2 和commit3包含的修改，被退回到了暂存区，然后又执行了commit命令，相当于将commit2和commit3的修改合并在一起再次提交了。push后的文档在远程仓库展示出来的内容是：  
![1.png](https://i.loli.net/2020/01/01/NTGsf1MILybluJZ.png)  


另一种情况，当commit2和commit3回滚到缓存区，把他们从缓存区移除之后push，则远端仓库的文档内容为：  
![1.png](https://i.loli.net/2020/01/01/g9LcFCyxmW8E43b.png)  
本地文档内容为：  
![2.png](https://i.loli.net/2020/01/01/8cF6YfpHnvQmr4X.png)  
远端和本地的内容是不一样的。  
上面的命令中，soft可以替换为mixed和hard：

 *mixed*： 本地文档中，2,3所做的修改还存在，但是已经不存在于缓存区了。其效果和上面这个退回到缓存区再从缓存区删除是一样的效果。
 *hard*：2,3两次所做的修改都不复存在。

### rebase


注意： 以上讨论的内容都是针对多次commit的情况下，commit记录之间的切换。commit之后是无法退回暂存区的，因为commit之后，再次查询git status，显示为：
![1.png](https://i.loli.net/2020/01/01/KAFy8ao4mvudM3J.png)  
暂存区是干净的。


## 将创建好的文档push到远端的过程：  
### git push origin master  
上述是最简单的push指令，后续创建了更多分支的时候，就能够将文件push到别的分支去。


## branch 与 merge
**branch**
### $ git branch developer1
创建名为developer1的分支
### $ git branch
列出所有branch
### $ git checkout developer1
切换到developer1 分支
### $ git branch -d [branch name]  
删除某一分支
### $ git checkout -b [branch name]
创建新分支并切换到该分支

现在除了master分支，还创建了developer1和developer2两个分支，并且每个分支下有一个和分支同名的文件，分别为developer1.markdown和developer2.markdown。现在要尝试把developer1中的文件merge到master中。
**merge**
在master分支中简历名为master4.markdown的文档，最初的内容为：“这个文档用于和developer1合并”
### $ git merge master developer1
在developer1分支中，将master分支合并，此时developer1中也出现master4.markdown文件。  
接下来，分别在master分支中和developer1分支中修改master4.markdown文件。如下图所示：  
![2.png](https://i.loli.net/2020/01/01/UhnqNBpClvoKxRz.png)  
![1.png](https://i.loli.net/2020/01/01/qOpIFXSWvUJPQYn.png)
再次在developer分支中merge master分支，看看情况：  
![merge conflict.png](https://i.loli.net/2020/01/01/iRVsOcLT4l8baEZ.png)  
处理的是时候，先打开文档，文档中通过<<<<<<< ======== >>>>>>>区分出了两个文档中不同的东西，v修改后，add，然后commit，就解决了冲突。  
![conflict management.png](https://i.loli.net/2020/01/01/vlxJoQpYAcNP38i.png)


上面提到的merge是快速合并，全合并。假设我developer分支上有文档1、2、3,master分支上有文档1、6，我只想要指定文档，而不是全合并，应该怎么做？
如果是用目标文件覆盖本地文件，则直接merge过来就好
![merge a certain file to overwrite the file with same name.png](https://i.loli.net/2020/01/01/xh7rj3IHimQFAgb.png)  
在远端master分支的master4.markdown文档本来是：
![before rewrite.png](https://i.loli.net/2020/01/01/ejLwKHNG7XQl8hz.png)  
被覆盖之后与developer中的master4.markdown一样了：  
![after rewrite.png](https://i.loli.net/2020/01/01/rMdFzNmqSYu6UVD.png)  
本地没有的文件也能通过这种方式选择性merge
![merge a certain file from another branch.png](https://i.loli.net/2020/01/01/Z6XYHK8WdvqIROu.png)


**fast forward merge 和 --no-ff 的区别**

假设我们现在处于developer分支上的commit c4，从commit c4时分出去一个t1的分支，然后做了commit c5和commit c6.  
![t1 before merge.png](https://i.loli.net/2020/01/02/834hceToG5iYJxj.png)  
这时我们想把t1合并到developer上，有两种操作，这两种操作分别会使得source tree有不同的效果：  
### git merge t1
![developer fast forward merge with t1.png](https://i.loli.net/2020/01/02/hVbePmXLvzsqW5B.png)
### git merge --no-ff t1  
![developer no fast forward merge with t1.png](https://i.loli.net/2020/01/02/RweElvt15fzdpq8.png)
显然，后一种做法能够更明确的表现出项目在推进过程中的每一次修改变化

假设从developer 位于commit c4时分出了两个分支t1和t2，并且t1进行了commit c5和commit c6.通过git merge --no-ff t1  将t1合并到developer了。随后分出t3，进行commit c8并且也同样合并了。  
t2进行的修改commit c7这时该如何做呢？
![before rebase.png](https://i.loli.net/2020/01/02/pu2MF4sJKfLA5q1.png) 
此时为了使t2能够将内容更新的与developer分支一样，我们使用rebase（变基）操作：  
![git rebase.png](https://i.loli.net/2020/01/02/u8OzsdBI7iHEqTr.png)  
此时打开t2位置的commit的文档，里面会出现t2位置与developer位置文档中的变化，根据需要进行更新，然后执行：  
![git rebase2.png](https://i.loli.net/2020/01/02/uhJ3PeDoiR7IQCc.png)  
此时，再打开source tree，变化为：  
![after rebase.png](https://i.loli.net/2020/01/02/JTnL6ji8eybfPFS.png)  
然后我们再checkout到developer，合并t2：    
![merge t2](https://s2.ax1x.com/2020/01/02/lNym0U.png))
