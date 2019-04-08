#git命令说明
====

**git clone 地址** 将远程的项目克隆到本地
	


### git commit

* **git commit -m "the commit message"** 提交添加到缓存仓库的文件 并添加说明
* **git commit -a**会先把所有已经track的文件的改动`git add`进来，然后提交(有点像svn的一次提交,不用先暂存)。对于没有track的文件,还是需要执行`git add <file>` 命令。
* **git commit --amend**  增补提交，会使用与当前提交节点相同的父节点进行一次新的提交，旧的提交将会被取消。

	>"amend" 是「修正」的意思。在提交时，如果加上 --amend 参数，Git 不会在当前 commit 上增加 commit，而是会把当前 commit 里的内容和暂存区（stageing area）里的内容合并起来后创建一个新的 commit，用这个新的 commit 把当前 commit 替换掉。所以 commit --amend 做的事就是它的字面意思：对最新一条 commit 进行修正。




**git status** 查看当前目录的状态

	描述状态：
		位于master分支上
		当前branch没有落后于origin/master
		你当前有untracked files（未追踪的文件），文件名字为xxxx或者有待提交的文件（Changes to be commited），（unstaged）文件已经放在了暂存区（staging area）
		你可以使用git add来追踪文件
		
		
### git add

* **git add \<path\>** 追踪文件 将文件添加至缓存区
* **git add .**  将所有修改添加到暂存区
* **git add -i** 查看被修改过或已删除文件但没有提交的文件，并通过其revert子命令可以查看<path>中所有未跟踪的文件，同时进入一个子命令系统。
* **git add -A** 表示把中所有跟踪文件中被修改过或已删除文件和所有未跟踪的文件信息添加到索引库
* **git add \*Controller**   将以Controller结尾的文件的所有修改添加到暂存区
* **git add Hello\***  将所有以Hello开头的文件的修改添加到暂存区 例如:HelloWorld.txt,Hello.java,HelloGit.txt ...
* **git add Hello?**  将以Hello开头后面只有一位的文件的修改提交到暂存区 例如:Hello1.txt,HelloA.java 如果是HelloGit.txt或者Hello.java是不会被添加的
* **git add -u [\<path>]** 把<path>中所有跟踪文件中被修改过或已删除文件的信息添加到索引库。它不会处理那些不被跟踪的文件。省略<path>表示 . ,即当前目录。

### git push
* **git push** 将本地仓库的代码提交打远程仓库
* **git push --set-upstream origin branch-name**设置本地分支追踪远程分支
* **git push origin branch-name** 将本地分支提交到远程服务器
* **git push origin --delete branch-name**删除远程服务器上的分支
* **git branch -d branch-name** 删除本地分支

#### 总结：
	
* 从GitHub把中央仓库clone到本地（==git clone==）
* 撸完代码提交（先 ==git add==  文件名 把文件添加到缓存区，在用==git commit== 提交）
	* 这个过程可以通过==git status==随时查看工作目录的状态
	* 每个文件有"changed/ubstaged(已修改)"，"staged（已修改并暂存）"，"commited(已提交)"三种状态，以及一种特殊状态"untracked（为跟踪）"
* 提交一次或者多次之后，把本地提交==push== 到中央仓库(==git push==)


**git pull** 将中央仓库的最新代码拉取下来
	
>当多人合作时每次提交代码或者工作任务之前，需要先pull 然后在进行push

### git branch
* **git branch branch-name** 创建一个叫branch-name 的分支
* **git branch**创建本地分支
* **git branch -a** 查看所有分支列表，包括本地和远程* **git branch -r** 查看远程版本库分支列表
* **git branch -d branch-name**删除本地分支
* **git branch -vv**可以查看本地分支对应的远程分支
* **git branch -m oldName newName** 给分支重命名

### git checkout
1. 操作文件 
 * **git checkout filename**放弃单个文件修改
 * **git checkout .**放弃当前目录下的修改  
2. 操作分支

* **git checkout branch-name** 将分支切换到branch-name下
* **git checkout -b master**
如果分支存在则只切换分支，若不存在则创建并切换到master分支，repo start是对git checkout -b这个命令的封装，将所有仓库的分支都切换到master，master是分支名。


### merge

merge含义：
 
 marge的意思是合并，从目标commit和当前commit（即HEAD所指向的commit）分叉位置起，把目标commit的路径上所有commit的内容一并用到当前commit，然后自动生成一个新的commit。
 
合并分支： **git merge branch1**

适用场景：

* 合并分支

	 当一个branch开发完成需要把内容合并回去时，用mergehebing
* pull的内部操作

	pull 的实际操作是把远端仓库的没用fetch取下来，用merge来合并

特殊场景：

* 特殊场景1
	
	情景1：当一个分支修改了A文件，另外一个分支改了B文件，合并后即改A也改B，自动完成合并
	
	情景2：两个分支同时都修改了A，但是分支1修改了第一行，分支2修改了第二行，合并后第一行和第二行都改，也是自动完成。
	
	情景3：两个分支修改了同一部分的内容，merge的自动算法就会失效，这样的情况称之为冲突[Conflict]
	
	### 冲突
	
	1. 解决冲突
		
		Git虽然没有帮完成自动merge，但它对文件做了一些处理，把两个分支的冲突内容放在一起，并用符号标出了他们的边界以及出处。格式：<<<<<<<<\<HEAD  ======\>>>>>>>branch_name
		假设你决定保留 HEAD 的修改，那么只要删除掉 branch_name 的修改，再把 Git 添加的那三行 <<< === >>> 辅助文字也删掉，保存文件退出，所谓的「解决掉冲突」就完成了或者使用merge工具来解决冲突
		
	2. 手动commit一下
	
	>放弃解决冲突，取消merge ：git merge --abort
* 特殊情况2  HEAD领先于目标commit:Git 什么也不做，空操作

* 特殊情况3：HEAD落后于目标commit:fast-forward。


## Feature Branching


> 简介:
> 这种工作流的核心内容可以总结为两点；
> 
> 1.任何新的功能（feature）或者bug修复全都新建一个branch来写
> 
> 2.branch写完后，合并到master，然后删掉这个branch



## 查看修改了什么

### git log

* **git log** 查看提交日志
* **git log -p（--patch）** 查看详细历史
* **git log stat** 查看简要统计

### 查看已提交的内容git show

* **git show**查看当前commit
* **git show xxxx\[在 show 后面加上这个 commit 的引用（branch 或 HEAD 标记）或它的 SHA-1 码]**查看任意一个commit
* **git show 5e68b0d8 filename**看指定 commit 中的指定文件

### 查看未提交的内容 git diff

* **git diff --staged/--cached**比对暂存区和上一条提交
* **git diff**比对工作目录和暂存区
* **git HEAD**比对工作目录和上一条提交


### git rebase（重新设置基础点）


写错的不是最新提交的，而是倒数第二个？

**git reabse-i**

* 第一步查看**git log** 找到需要修改的commit
* 第二步使用**git rebase -i HEAD^^ 或者 ~ **向前或者向后移动commit
* 第三步 将你需要修改的commit的**pick** 修改成**edit**，修完完成后退出编辑
* 第四步修改写错的**commit git add 文件名**，使用**git commit --amend** 完成修改
* 第五步使在修复完成之后，就可以用**git rebase --continue** 来继续 rebase 过程，把后面的 commit 直接应用上去。

### reset --hard 丢弃最新的提交

**git reset --hard 目标commit**
>但是这并不是真正意义上的撤销，只是再也找不到它了。如果你还记得撤销的
SHA-1码，那么你还可以通过SHA-1来找到它。


### 想丢弃的也不是最新的提交？

方法一：

使用**git rebase -i HEADE^^来**找到你需要移除的commit，探后将**pick** 修改成**drop**

方法二：

使用**git rebase --noto** 来撤销提交

>方法有两种，理念是一样的：在 rebase 的过程中去掉想撤销的 commit，让他它消失在历史中。

### 代码已经 push 上去了才发现写错？

1. 出现的内容在自己的branch
 **git push origin branch_name -f**   -f 是--force的缩写，意为[忽略冲突，强制push]，需要注意的是这里不能先`pull`一下再去`push`，而是要选择**强行**`push`
2. 出错的内容已经合并带master

**git revert HEAD^**

上面这行代码就会增加一条新的 `commit`，它的内容和倒数第二个 `commit` 是相反的，从而和倒数第二个 `commit`相互抵消，达到撤销的效果。

在 `revert` 完成之后，把新的 `commit`再 `push` 上去，这个 `commit` 的内容就被撤销了。它和前面所介绍的撤销方式相比，最主要的区别是，这次改动只是被「反转」了，并没有在历史中消失掉，你的历史中会存在两条 `commit` ：一个原始 `commit` ，一个对它的反转 `commit`。

### rest的本质，不止可以撤销提交

```
git reset --hard HEAD^^  
撤销当前commit
```
### reset 的本质:移动HEAD以及它所指向的branch**














	





 
 

