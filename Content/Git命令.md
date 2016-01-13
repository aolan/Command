#Git日常使用场景

##Git配置

***

1.生成密钥对

	ssh-keygen -t rsa -C "你的邮箱"

2.去~/.ssh目录下找id_rsa.pub文件

	 pbcopy < id_rsa.pub

3.把拷贝到剪切版的公钥粘贴到公司gitlab网站

4.测试是否可用  
  
	ssh -T git@"你的gitlab服务器地址"


##上传本地代码到github

	1、先到github上创建一个仓库
	2、cd到工程目录下
	3、git init
	4、git remote add origin https://github.com/aolan/{Project}.git
	5、git add .
	6、git commit -m 'first commit'
	7、git push origin master

##创建新分支

	git checkout master							//切换到master分支
	git pull									//更新最新的master分支
	git branch <new-local-branch-name>			//以master分支为基点创建本地分支
	git checkout <new-local-branch-name>		//切换到本地新分支
	git push origin <new-local-branch-name>		//推送到远程
	
	
	
##合并个人开发分支到主开发分支

	git branch -D beta                            //删除本地分支
	git fetch                                     //同步远程分支       
	git checkout -b beta origin/beta              //重新创建本地分支
	git pull origin beta					
	git merge orgin/lawn_dev                      //将远程lawn_dev分支合并到本地beta分支
	git push


##日常提交代码

	1、git add .
	2、git status
	3、git commit --verbose
	4、git fetch
	5、git rebase origin/master    【git rebase -i origin/master 可以合并之前的多次提交】
	6、git push origin dev    ﻿    ﻿【git push --force origin dev】这是因为使用rebase以后，分支历史改变了，跟远程分支不一定兼容，有可能需要强行推送


##其他

	git push origin :beta				//删除远程分支beta
	git push -f <SHA> beta				//回滚代码到某个(SHA)提交，慎用
	git commit --amend				//修改上次提交的描述

