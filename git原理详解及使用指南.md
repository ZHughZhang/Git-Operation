###git命令说明

**git clone 地址** 将远程的项目克隆到本地
	
**git log** 查看提交日志

**git commit** 提交

**git status** 查看当前目录的状态

	描述状态：
		位于master分支上
		当前branch没有落后于origin/master
		你当前有untracked files（未追踪的文件），文件名字为xxxx或者有待提交的文件（Changes to be commited），（unstaged）文件已经放在了暂存区（staging area）
		你可以使用git add来追踪文件

**git add** 追踪文件 将文件添加至缓存区

**git push** 将本地仓库的代码提交打远程仓库

 * **git push --set-upstream origin branch-name**设置本地分支追踪远程分支
 * **git push origin branch-name** 将本地的分支提交到远程服务器
 * **git push origin --delete branch-name**删除远程服务器上的分支
 * **git branch -d branch-name** 删除本地分支


####总结：
	
* 从GitHub把中央仓库clone到本地（==git clone==）
* 撸完代码提交（先 ==git add==  文件名 把文件添加到缓存区，在用==git commit== 提交）
	* 这个过程可以通过==git status==随时查看工作目录的状态
	* 每个文件有"changed/ubstaged(已修改)"，"staged（已修改并暂存）"，"commited(已提交)"三种状态，以及一种特殊状态"untracked（为跟踪）"
* 提交一次或者多次之后，把本地提交==push== 到中央仓库(==git push==)


**git pull** 将中央仓库的最新代码拉取下来
	
	当多人合作时每次提交代码或者工作任务之前，需要先pull 然后在进行push

###git branch
* **git branch branch-name** 创建一个叫branch-name 的分支
* **git branch**创建本地分支
* **git branch -a** 查看所有分支列表，包括本地和远程* **git branch -r** 查看远程版本库分支列表
* **git branch -d branch-name**删除本地分支
* **git branch -vv**可以查看本地分支对应的远程分支
* **git branch -m oldName newName** 给分支重命名

###git checkout
1. 操作文件 
 * **git checkout filename**放弃单个文件修改
 * **git checkout .**放弃当前目录下的修改  
2. 操作分支

* **git checkout branch-name** 将分支切换到branch-name下
* **git checkout -b master**
如果分支存在则只切换分支，若不存在则创建并切换到master分支，repo start是对git checkout -b这个命令的封装，将所有仓库的分支都切换到master，master是分支名。


