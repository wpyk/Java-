# 任务一：确定项目的git url -> 克隆到本地 -> 任务二  
# 任务二：file->import->existing projects into workspace -> 要导入的文件

# 报错

点击File菜单，分别选择Import->General->Existing Projects into Workspace，然后在Select root directory中Browse你想要加入的工程。但是怎么点击Refresh都没有显示可用的Projects文件。  
这是为什么呢？因为用eclipse创建的工程有一个.project文件，而有时候我们下载来的项目是没有这个文件的。  
解决办法：选择File--New--XXX Project，在弹出的窗口中，去掉Use default location前面的勾，点击Browse，然后选择你想要打开的工程目录，还是选择你要引入的项目所在文件夹，在Poject name中输入工程的名字，接着next、finish。在目录下就会生成.project,.classpath以及.setting文件。 