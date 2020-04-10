### Git学习笔记

- git是一种分布式版本控制系统，与CVS和SVN集中式版本控制系统不一样的是每个用户都有一个完整的库，只有需要交换修改的时候才会用到互联网(两者的差别就好比client-server模式和P2P模式的区别)。

- Git安装：

  ​	Linux环境下直接sudo apt-get install git即可。

  ​	Windows环境下下载安装程序，按照默认选项勾选即可。

  ​	最后一步还需要设置用户名和邮箱地址

  ​	 **git config --global user.name "Your Name"**

  ​	 **git config --global user.email "email@example.com"**

  ​	(因为我之前有注册过git但是忘记了用户名和密码，这里使用

  ​	**git config user.name**和**git config user.email**即可分别查看原来自己注册用户名和邮箱信息) 

### Git建立仓库

​	通过```git init```命令来建立仓库。，在当前目录下会多出来一个```.git```目录用于管理仓库。

​	**PS**:所有文件都是以纯文本文件来跟踪的，WORD文件无法跟踪，并且要使用notepad++来编辑文件。

​	(说到这里，这里出来了一系列问题，我想试着用linux shell的方法来打卡文件并且编辑，结果notepad

​	命令弹出来的是windows自带的记事本，想使用notepad++得键入notepad++所在路径，然后这时候又

​	出现了permission denied,关于怎么调整默认编辑方式的问题以后再说)

###Git添加和提交文件

​	这里主要用的就是**git add filename**和**git commit -m "changed information"**这两个命令。

​	你可以add很多次不同的文件(**注意应该是修改文件之后再git add才会显示准备提交**)，然后一次提交上去。

###时光机穿梭(关于仓库的版本回溯问题)

​	**git diff  <filename>**表示查看文件发生了什么改动

​	**git status**查看工作区是否发生文件改动

​	**git reset <HEAD^ / commit id>**表示重新设置版本

​	如果忘记版本号可以用**git reflog**查看以前输入过的命令以查到版本号。

​	**git log**可以查看提交历史，嫌信息太多的可以加--pretty=oneline参数

​	HEAD永远指向当前版本号。

​	**使用git回退版本的命令```git reset --hard <版本号>```其中版本号既可以是SHA的那些数字，也可以使用HEAD^之类的指针**

* 工作区和暂存区域

工作区：在电脑里面可以看到的目录，工作区中有一个隐藏文件.git，称作git的版本库

暂存区：.git里面存了很多东西，最重要的就是stage(暂存区)，就是我们每次git add的时候就会将文件存入暂存区，git commit就会在当前分支(master)上面进行修改。

* 管理修改

这里的意思就是说文件有修改之后必须git add才能加入暂存区以备与在后面被commit上去，简而言之就是被add的changes才能commit到分支

* 撤销修改

当我们不小心改动了文件，但是还没有提交到暂存区，可以用git checkout --<文件名>来返回改动之前的文件状态

如果不小心提交到了暂存区，就使用```git reset HEAD<文件名>```所以说git reset既可以重置版本，也可以取消暂存区的提交，使用reset取消暂存区的添加之后，在使用```git checkout -- <filename>```来撤销修改。

另外如果不小心提交的话，只要没有推送到远程库，就可以使用reset回退版本库。

* 删除文件

其实这个和之前的差不多，就是将删除也变成一个文件操作，git checkout实质上是从版本库中返回修改，这里的版本共库包括了暂存区和分支，如果暂存区有对应文件，就用暂存区的文件替代，如果没有就用分支（master）中的文件替代。

还有就是如果真的要删除，并且删除之后我们肯定不能加add一个已删除的改动，而是使用git rm <文件名>l来在暂存区中添加修改，之后再提交就可以删除所选文件。

**```git reset version<filename>```在我感觉像是用某一个版本号的的文件来代替当前的暂存区域**





​	
