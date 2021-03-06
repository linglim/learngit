#学习地址
> [http://blog.just4fun.site/open-edx-dev-skill-and-resource.html](http://blog.just4fun.site/open-edx-dev-skill-and-resource.html "学习git网址")
#learn git
##安装与配置
   ` git config --global user.name "name"`
    
   `git config --global user.email "emailadd"`
##创建版本库(不要存在中文)
###先创建空目录（工作区）
    mkdir learngit
    cd learngit
    pwd
###将目录变为仓库

    git init

当前目录下多了一个.git的目录出现 .git的目录（暂存区），ls -ah查看隐藏文件

##*****工作原理
![工作原理图](http://www.liaoxuefeng.com/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)
>把文件往Git版本库里添加的时候，是分两步执行的：
	


>	-  第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；



>	-  第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

>因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。


>每次修改，如果不add到暂存区，那就不会加入到commit中。

##把文件添加到版本库
创建文件（不要用txt和word）后存在工作区目录 learngit

    git add readme.txt//把文件添加到仓库，加入到缓存区
    
    git commit -m"注释"//把文件提交到仓库，提交到master分支

可多次添加，一次进行提交

##穿越小节（commit到本地分支的可用）
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。

穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。


##查看当前状态（告诉你，什么被修改啦）

    $ git status

##****状态解释
###

- 工作区下提示信息

>    `# On branch master`

>    `# Changes not staged for commit:`
    
>表示：在工作区有修改，还没放在缓存区

>####撤销工作区的修改
` $ git checkout -- readme.txt`

//git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

----------

###
- 缓存区下提示信息

>`# On branch master`

>  ` # Changes to be committed:`
 

>表示：添加到了暂存区，还没有提交：

>####撤销缓存区的修改
    $ git reset HEAD readme.txt

----------


###
- 本地分支master下

>###已经提交到本地master分支的可用版本回退撤销提交
>`$ git log --pretty=oneline`//找到回退的版本id
>`$ git reset --hard 3628164`//回退到过去某个版本



----------
文件：已跟踪、未跟踪、变化的，暂存的

把跟踪的文件放入暂存区，add 命令
		
    Changes not staged for commit：（跟踪文件内容发生了变化，但还没放入暂存区）
	change to be committed:(文件被修改了，并放入暂存的)

On branch master(在分支的)
>
	 Changes not staged for commit:（改动啦，还没提交的）
	 modified:   readme.txt（此文件已经被改动啦，但还没被提交commit）
Untracked files:（在learngit的目录下，但还没被add文件）


nothing to commit (working directory clean)：工作区是空的



##查看更修改内容（在还没commit之前，告诉你修改的内容）

    $ git diff readme.txt：（/查看尚未暂存的文件有哪些修改更新，用来看暂存前后的变化）
    $git diff --cached/staged:(暂存文件的改变)
##查看状态
	$git status
	M :被修改、暂存
	 M:被修改
	 A:新入暂存的
	？？：未跟踪的文件

##回退历史版本

当前是HEAD,前一个是HEAD^

    $ git reset --hard HEAD^

只要记住git log下 历史版本的commit id前几位就可回到任意时间（穿越过去-未来）

##移除文件
    
    $git rm (文件已修改，但未入暂存)
    $git rm -f(文件已经在暂存区里)
    $git rm --cached <> (从git仓库删除，但要保留到本地硬盘)
##移动文件（重命名）
    $git mv <> <new>
##删除
    $ rm test.txt

##查看命令日志，有几个历史版本（查看提交历史纪录）

    $ git log
    
    $ git log --pretty=oneline//显示好看

##远程

###1


1.  获得key
 ` ssh-keygen -t rsa -C "email"`
- 自选保存key地址(写到.ssh)
 ` /c/Users/lenovo/learngit/key/.ssh`
- “Add SSH Key”，在Key文本框里粘贴id_rsa.pub文件的内容
- 创建远程仓库Create repository，填上仓库名字

###2
1. 关联本地
    git remote add origin git@gitlab.com:linglim/learn-git.git

>若提示出错信息：fatal: remote origin already exists.

>    解决办法如下：

>    1、先输入$ git remote rm origin

>    2、再输入$ git remote add origin git@github.com:djqiang/gitdemo.git 就不会报错了！



##分支

>创建与合并分支


   
>小结
Git鼓励大量使用分支：

> 查看分支：git branch
> 查看每个分支最后一次提交：git branch -v
> 查看已经合并到当前的：git branch --merged
> 创建分支：git branch <name>
> 
> 切换分支：git checkout <name>
> 
> 创建+切换分支：git checkout -b <name>
> 
> 合并某分支到当前分支：git merge <name>
> 
> 删除分支：git branch -d <name分支名>
> 查看分支合并图：git log --graph

##远程分支
> 没添加远程分支时master就是本地分支
> 
>添加远程仓库时：
>分支种类：远程master、本地master（跟踪分支）、origin/master(远程跟踪分支：不能移动的本地分支)
>
>git clone <url><本地仓库名：不写默认为origin>，此时分支有两个：本地master、origin/master，你在master工作，当有人推送到远端后，你再推送，先git fetch origin,然后推送：git push (remote)(branch)/git push origin(branch本地)（branch远端）
>
>git merge orgin/branch: 合并到当前分支

>git checkout _b branchname:新建并切到自己的分支，工作起点是origin/branch
>
>
>git fetch origin:本地不会组成一个可编辑的副本，从服务器抓取数据，并不修改工作目录内容
>
>git pull:=git fetch+git merge ：修改合并入本地分支，生成本地可修改的副本
##查看远端的分支
    git ls -remote//查看远端目录列表
    git remote show(remote)//查看更多远端信息


##合并


- >git merge <name>
>Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。





- >git merge --no-ff -m "merge with no-ff" dev

>强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。




#注意：
*
##每次更改，都要add，然后commit
*
死机时：ctrl+c

#命令
![](https://camo.githubusercontent.com/e12dfd770f44b37c8a81e0339d3ef6d1aee035dc/687474703a2f2f7777312e73696e61696d672e636e2f6d773639302f3434383934636262677731657569676339397a38776a323065343062706a736d2e6a7067)

#Command line instructions

    
    Git global setup
    
    git config --global user.name "linglim"
    git config --global user.email "359128244@qq.com"
    
    Create a new repository
    
    git clone git@gitlab.com:linglim/shiyanshi.git
    cd shiyanshi
    touch README.md
    git add README.md
    git commit -m "add README"
    git push -u origin master
    
    Existing folder or Git repository
    
    cd existing_folder
    git init
    git remote add origin git@gitlab.com:linglim/shiyanshi.git
    git add .
    git commit
    
    git push -u origin master






##猴子都能懂得git
-创建分支

    $ git branch issue1
-切换到分支issue1

    $ git checkout issue1
-查看分支

    $ git branch
--b选项可以创建分支并切换

    $ git checkout -b <branch>

-合并分支

--先切回到master，然后合并issue1

    $ git checkout master
    $ git merge issue1

--删除

    $ git branch -d issue1

--并行

    $ git branch issue2
    $ git branch issue3
    $ git checkout issue2


