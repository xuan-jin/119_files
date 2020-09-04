# Git命令

```
在Linux上安装Git
$ sudo apt-get install git

$ git config --global user.name "Your Name"
$ git config --global user.name "email@example.com"


$ mkdir learngit		//选择合适的位置，创建一个空目录
$ cd learngit			//转到某目录
$ pwd					//显示当前目录
$ git init				// 把这个目录变成Git可以管理的仓库

$ git add readme.txt	// 添加到暂存区
$ git commit -m "wrote a readme file"	// 提交到仓库

$ git status			// 查看仓库当前状态
$ git diff readmen.txt	// 查看文件readme.txt具体的修改内容

$ git log					//  显示从最近到最远的提交日志
$ git log --pretty=oneline	  //   同上（显示较少的信息）

$ git reset --hard HEAD^		// 退回上一个版本
$ GIT reset --hard <commit_id>
// HEAD 表示当前版本
// HEAD^ 上一个版本
// HEAD^^ 上上一个版本
// HEAD~100 往上100个版本

// 回退到 commit_id 对应的版本，commid_id 为版本号，只需要前几位就行了
$ cat readme.txt		// 查看文件内容
$ git reflog  			// 记录你的每一次命令,找回曾经版本的commit_id

$ git diff HEAD -- readme.txt		// 查看工作区和版本库里面新版本的区别

$ git restore <file>  (建议使用) (如: git restore readme.txt)
$ git checkout -- <file>
// 命令中 -- 很重要，没有就变成 “切换到另一个分支” 的命令

// 第一步: 把暂存区的修改撤销掉(unstage)，重新放回工作区
$ git restore --staged <file>

// 第二步: 撤销工作区的修改
$ git restore <file>

$ rm readme.txt 			// 删除文件

// 确实要删除，从版本库中删除文件
$ git rm readme.txt
$ git commit -m "remove .txt"

// 删错了要恢复，
$ git checkout -- readme.txt

$ ssh-keygen -t rsa -C "youremail@example.com"

$ git add javaAndLife.md
$ git add MySQL.md
$ git commit -m "other notes"
$ git remote add origin git@github.com:xuan-jin/learngit.git
$ git push -u origin master

// 之后的简化命令（从现在起，只要本地作了提交，就可以通过命令，把本地master分支的最新修改推送至GitHub）
$ git push origin master

$ git clone git@github.com:xuan-jin/huangfu.git

$ git checkout -b dev			// 创建并切换到dev分支
$ git switch -c dev				// 同上

$ git branch dev				// 创建dev分支
$ git checkout dev				// 切换到dev分支

$ git branch					// 查看分支，当前分支前有*。

$ git checkout master			// 切换回master分支
$ git merge dev					//把dev分支的工作合并到master分支上
(合并某分支到当前分支)

$ git branch -d dev				 // 删除dev分支

$ git log --graph --pretty=oneline --abbrev-commit
// 查看分支合并情况（图）

$ git log --graph --pretty=oneline --abbrev-commit
// 查看分支合并情况（图）

$ git stash
// "储藏"当前工作现场

$ git stash list
// 查看已存储的工作区

$ git stash apply			// 恢复存储的工作区
$ git stash drop			// 删除存储的工作区
$ git stash pop				// 恢复的同时把stash也删了
$ git stash apply stash@{0}  多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash
# 通常在 dev 分支开发时,需要有紧急 bug 需要马上处理,保存现在修改的文件等,先修复 bug 后再回来继续工作的情况

$ git cherry-pick <commit> 
// 复制一个特定的提交到当前分支(当前分支的内容需要先 commit,然后冲突的文件需要解决冲突,然后 commit)
// 在master分支上修复bug后，对于之前从master分支出来的dev上也存在bug，简单的处理办法

$ git remote 			// 查看远程库的信息
$ git remote -v			// 查看远程库更详细的信息

$ git push origin master
$ git push origin dev		// 推送master或dev分支到远程库

// 当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的master分支。
// 要在dev分支上开发，就必须创建远程origin的dev分支到本地
$ git checkout -b dev origin/dev

// 两人对同一文件更改后，在提交时会发生冲突，解决：
$ git pull
// 如果git pull失败，原因是没有指定本地dev分支与远程origin/dev分支的链接
$ git branch --set-upstream-to=origin/dev dev
$ git pull

$ git rebase		// 把分叉的提交历史“整理”成一条直线

$ git branch		// 显示所有分支
$ git checkout master	// 切换到某分支
$ git tag v1.0		// 打上一个名为 v1.0 的标签，默认标签是打在最新提交的commit上的。
$ git tag			// 查看所有标签

$ git log --pretty=oneline --abbrev-commit 	// 找到历史提交的commit id
$ git tag v0.9 f52c633		// 为之前的commit id为f52c633的提交打上标签v0.9
// 注意，标签不是按时间顺序列出，而是按字母排序的。
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
// 还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字

$ git tag -d v1.0 		// 删除标签
$ git push origin v1.0   // 推送v1.0标签到远程
$ git push origin --tags // 一次性推送所有尚未推送到远程的标签

// 如果标签已经推送到远程,先从本地删除,然后，从远程删除
$ git tag -d v1.0					// 删除本地
$ git push origin :refs/tags/v1.0	  // 删除远程
```

Git代码更新到本地

正规流程

1. git status（查看本地分支文件信息，确保更新时不产生冲突）
2. git checkout – [file name] （若文件有修改，可以还原到最初状态; 若文件需要更新到服务器上，应该先merge到服务器，再更新到本地）
3. git branch（查看当前分支情况）
4. git checkout remote branch(若分支为本地分支，则需切换到服务器的远程分支)
5. git pull

若命令执行成功，则更新代码成功！

快速流程

上面是比较安全的做法，如果你可以确定什么都没有改过只是更新本地代码

1. git pull (一句命令搞定)

git branch 看看分支
git chechout aaa 切换分支aaa
git branck aaa 创建aaa分支
git chechout -b aaa 本地创建 aaa分支，同时切换到aaa分支。只有提交的时候才会在服务端上创建一个分支