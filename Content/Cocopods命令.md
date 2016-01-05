#Cocoapods日常使用
1.安装Cocoapods工具

	gem install cocoapods
	
2.生成Podfile文件

	pod init
	
3.更新本地Cocopods配置文件，这些文件在 */Users/lawn/.cocoapods/* 目录下

	pod setup
	
4.查找第三方pod库

	pod search jsonkit
	
5.下载第三方库源码，并配置依赖关系等等。在没有修改Podfile的前提下，即使第三方库有更高的版本，再次执行该命令，还是安装之前的版本，这和 *Podfile.lock* 文件有关

	pod install
	
6.下载第三方库源码，并配置依赖关系等等。这个方法会更新 *Podfile.lock* 文件，所以当Podfile里面的配置第三方库没有指定版本的时候，会安装最新的第三方库

	pod update
	
7.执行命令的时候不更新spec仓库，这样会快很多

	pod install --verbose --no-repo-update
	pod update --verbose --no-repo-update