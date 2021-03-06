# Git日常使用场景

## Git配置


1. 生成密钥对

	```ssh-keygen -t rsa -C "你的邮箱"```

2. 去~/.ssh目录下找id_rsa.pub文件

	 ```pbcopy < id_rsa.pub```

3. 把拷贝到剪切版的公钥粘贴到公司gitlab网站

4. 在~/.ssh目录下执行，将专用密钥添加到 ssh-agent 的高速缓存中
	
	```ssh-add id_rsa```

5. 测试是否可用  
  
	``` ssh -T git@"你的gitlab服务器地址" ```


## 上传本地代码到github

	1、先到github上创建一个仓库
	2、cd到工程目录下
	3、git init
	4、git remote add origin https://github.com/aolan/{Project}.git
	5、git add .
	6、git commit -m 'first commit'
	7、git push origin master

## 创建新分支

	git checkout master				// 切换到master分支
	git pull					// 更新最新的master分支
	git branch <new-local-branch-name>		// 以master分支为基点创建本地分支
	git checkout <new-local-branch-name>		// 切换到本地新分支
	git push origin <new-local-branch-name>		// 推送到远程
	
	
	
## 合并个人开发分支到主开发分支

	git branch -D beta                            // 删除本地分支
	git fetch                                     // 同步远程分支       
	git checkout -b beta origin/beta              // 重新创建本地分支
	git pull origin beta					
	git merge orgin/lawn_dev                      // 将远程lawn_dev分支合并到本地beta分支
	git push


## 日常提交代码

	1、git add .
	2、git status
	3、git commit --verbose
	4、git fetch
	5、git rebase origin/master    【git rebase -i origin/master 可以合并之前的多次提交】
	6、git push origin dev         【git push --force origin dev】这是因为使用rebase以后，分支历史改变了，跟远程分支不一定兼容，有可能需要强行推送

## Git标签使用

	git tag -a v1.0.0 -m 'Release Version 1.0.0'    // 打标签
	git tag 					// 查看标签
	git push origin --tags				// 推送标签到远程仓库
	git tag -d v1.0.0				// 删除标签
	git push origin :refs/tags/v1.0.0		// 删除远程仓库标签

## 远程代码回滚

	git checkout the_branch
	git pull origin the_branch
	git branch -b the_branch_backup 		// 备份一下当前的分支
	git reset --head the_commit_id 
	git branch the_branch_backup 			// 备份一下这个分支当前的情况
	git push origin :the_branch 			// 删除远程分支the_branch
	git push origin the_branch 			// 用回滚后的本地分支重新建立远程分支
	git branch -d the_branch_backup			// 删除本地备份分支［如果前面的操作都成功的话］
	
## 创建分支发起merge request

	git checkout dev
	git checkout -b fix_bug
	
	// 修改代码后
	git add .
	git commit -m 'fix bug'
	git push origin fix_bug
	
	// 服务端merge之后，删除本地分支
	git branch -D fix_bug
	git branch -d -r origin/fix_bug

## 迁移仓库
	
	git clone --bare git://github.com/username/project.git	// 从原地址克隆一份裸版本库，比如原本托管于 GitHub。

	cd project.git
	
	git push --mirror git@gitcafe.com/username/newproject.git // 以镜像推送的方式上传代码到 GitCafe 服务器上。

## 其他
	git push origin :beta				// 删除远程分支beta
	
	git push -f <SHA> beta				// 回滚代码到某个(SHA)提交，慎用
	
	git commit --amend			       	// 修改上次提交的描述
	
	git rebase -i HEAD~2				// 合并最近两次提交，然后把需要合并到另一个commit中的commit前的pick改为s或者squash
	
	git log -n 1 -p 				// 查看最近一次提交所有更改的细节
	
	git log -n 1 --stat				// 查看最近一次提交所有更改过的文件
	
	git pull --rebase origin dev		  	// 多人在dev分支开发时，拉代码最好使用git pull --rebase，这样就不会出现merge记录


## 文件太大

   如果文件太大，导致git push 不上去，显示出 git push error: RPC failed; result=56, HTTP code = 0 [closed] 错误，建议修改Git's HTTP Buffer 
   
   ``` git config --global http.postBuffer 2M ```

