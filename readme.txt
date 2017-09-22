Git is a distributed version control system.
Git is free software distributed under the GPL.
I am learning.

1.Git基础概念：
	1.1.目前世界上最先进的分布式版本控制系统（没有之一）。（CVS，SVN及IBM的ClearCase,微软的VSS都是集中式）
	1.2.2005年Lunis用C语言写了第一个版本的Git,用于Lunix版本的控制管理。代替原先的集中式版本管理系统BitMover公司的BitKeeper.
2.Git安装初始设置
	2.1.建立账号：config --global user.name/email
		$ git config --global user.name "名字"
		$ git config --global email.name "邮箱" 
		****** --global参数为全局参数，表示这台机器上所有的Git仓库都会使用这个配置
3.创建版本库
	3.1.以英文在合适位置创建一个空目录
		$ mkdir learngit  //创建目录
		$ cd learngit     //进入该目录
		$ pwd             //显示目录路径
	结果：/users/michael/learngit
	3.2.用git init命令把这个目录变为Git可以管理的仓库,并在当前目录下生成一个.git目录
	3.3.如果.git隐藏，可以用ls -ah命令显示
	3.4.创建版本
		3.4.1.将要管理的文件放到版本库目录下 如readme.txt.
		3.4.2.用git add告知Git将什么文件添加入了临时仓库（缓存区）
			$ git add readme.txt
		3.4.3.用git commit -m ""命令让Git将缓冲区中的文件正式入库，形成一个版本。
			$ git commit -m "first version V1.0"
		3.4.4.git commit后面的 -m参数是该次提交版本的说明
		3.4.5.commit 一次可以提交多个文件，集中多次改动形成一个版本
4.版本管理
	4.1.版本修改过程
		4.1.1.修改文件并保存
		4.1.2.用git status命令查看什么文件有改动
		4.1.3.用git diff命令查看该文件被改动了什么内容
			git diff "文件名”
		4.1.4.确认被改动的内容后，用git add命令将其加入临时仓库（缓存区）
		4.1.5.所有文件的改动都确认后，用git commit命令让Git将一个或者多个已改动的文件正式入库并形成新版本。
	4.2.版本回退
		4.2.1.用git log命令查看所有的历史版本信息，可以用--pretty=oneline命令简化内容
			所看到的前面的长串十六进制字符就是该版本的commit ID,是一个SHA1计算出来的非常大的数字
		4.2.2.用git reset命令回到某个需要的版本
			git reset --hard HEAD^  //回到上个版本
			git reset --hard commit ID  //回到该ID指定的版本
		4.2.3.用git reflog可以查看命令历史。
5.管理修改
	5.1.Git跟踪并管理的是修改，而不是文件。
	5.2.修改过的文件如果没有add过，在commit时，其修改的内容不会加入新版本库中
6.撤销修改
	6.1.git checkout --file可以丢弃工作区的修改：把文件在工作区的修改全部撤销，两种情况
		1.修改的文件还没add,checkout命令将文件回到版本库中已经有的版本
		2.add后没有commit,但又做了修改,checkout命令将文件回到上一次add的版本
			git checkout --"文件名"
	6.2.git reset HEAD file 可以把已经add的，已经在缓存区中的文件撤销掉，重新放回工作区
			git reset HEAD "文件名"
7.删除文件
	7.1.用git rm 删除文件
	7.2.用commit命令确认为新版本
	7.3.用reset --hard commit ID（commit ID可以用reflog查找）命令恢复删除文件之前的版本，然后用checkout 文件名恢复误删除的文件。

8.远程仓库
	8.1.添加远程仓库
		8.1.1.注册GitHub账号
		8.1.2.创建SSH KEY,在用户主目录下，用以下命令创建SSH KEY
			$ ssh-keygen -t rsa -C "邮箱名"
			创建成功后可以在用户主目录下找到id_rsa（私钥）和id_rsa.pub（公钥）两个文件
		8.1.3.将id_rsa.pub内的钥匙密码拷贝到GitHub网站相应的对话框内完成钥匙添加
		8.1.4.在GitHub网站创建一个新仓库
9.关联推送
	9.1.1.用以下命令将本地仓库关联到GitHub上刚才创建的仓库
		$ git remote add origin https://github.com/logingcr/learngit
	9.1.2.在本地仓库目录I行啊，用以下命令将本地仓库的内容推送到Github上的仓库
		$ git push origin master
10.从远程克隆
	10.1.在Github上创建一个新的仓库
	10.2.用以下命令克隆一个本地仓库
		$ git clone https://github.com/logingcr/learngit.git

11.分支管理		
	11.1.创建并切换到分支
		git checkout -b dev
	11.2.用branch查看当前分支
	11.3.在分支上commit提交版本更改后，切换回master分支
	    git checkout master
	11.4.合并dev分支到master分支,这样所有在dev分支上的版本修改都合并到了master分支
		git merge dev
	11.5.删除分支
		git branch -d dev
		