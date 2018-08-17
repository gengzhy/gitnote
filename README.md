#	第一部分：Git本地操作
1	初始化Git版本库：
git init
(这样就会在指定的文件夹中增加了一个 .git 的文件夹，
	默认是隐藏的，需要显示隐藏文件惨能看见)
	
2	新建文件：touch README.md，加该文件添加到暂存区：
	git add README.md
	接着使用 git status 可以查看当前的git 版本库的状态

3	接着使用：
	git commit -m "提交的备注"
	就可以将文件提交到Git版本库的提交区，这样就可以实现了文件的管理

4	使用：
	git log
	可以查看提交的记录日志：
		包含：提交ID、提交作者、提交日期和提交的备注
	
5	回退到上一个版本的命令：
	git reset --hard HEAD^
	(注：在Git中，使用 HEAD 作为当前所在的版本，
	上一个版本则是 HEAD^，上上一个版本 HEAD^^)
	
6	回退到指定的版本：
		使用 git reflog 打印出所有的提交记录日志表，查处需要回退的版本ID号
	使用命令：
		git reset --hard 版本ID号
		即可时间回退到指定的版本库
	
7	打印精简版(只打印版本ID和提交备注)的log日志：
	git log --pretty-online
	
-------------
8	有时候，当在工作区中修改了文件，但不准备 add 到暂存区，
	可以使用 git checkout -- 文件名：
	例： git checkout -- h.txt

	则会清空当前工作区的内容，并撤销当前工作空间中的全部修改

-------------

9	对于已经 git add 到暂存区的文件，发现有问题，不想 git commit 
	到提交区，想撤回到工作区修改之前的状态，需要两步：

	git reset HEAD 文件名  (把暂存区的状态撤销掉，让文件回到工作区)
	git checkout -- 文件名 (撤销工作区的文件修改，回到修改之前的状态)


10	当修改了一个文件之后，可以使用 
		git diff 文件名
	来查看当前文件所做的改动

------------

11	断工作区文件与版本库里面最新版本的区别
	git diff HEAD -- 文件名


---------
12	当不小心在本地项目删除了文件，想恢复：
	git checkout -- 已删除的文件名 【必须记住文件名，不然没法恢复】

--------
13	如果确实要删除本地文件：
	git rm 要删除的文件名
	git commit '备注'

# 第二部分：Git本地与远程操作
1	在GitHub上创建一个仓库，如 gitnote

2	查看GitHub是否配置了当前操作计算机的ssh-key
	(1)查看本地计算机：用户/.ssh ，没有，则创建：
		ssh-keygen -t rsa -C "本地计算机设定的git邮箱"
	(2)创建完成后，将id_rsa.pub文件的内容添加到GitHub中
	
3	使用下面的Git命令将本地Git版本库与GitHub仓库关联起来：
	git remote add origin https://github.com/Lissonor/gitnote.git
	
4	推送本地代码到GitHub的gitnote库：
	git push -u origin master【origin指远程库、master指本地库】
	
5	首次推送本地仓库代码到远程仓库时，需要两个步骤：
	(1)建立与远程库的联系：git remote add origin https://github.com/Lissonor/gitnote.git
	(2)将代码推送到远程库：git push -u origin master
	注意：如果在与远程库建立联系后，可以直接使用一下命令即可到达到推送目的。
		  原因是本地项目已经和远程项目关联上了，无序重复操作。
		git push origin master
	
