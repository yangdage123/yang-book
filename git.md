# Git的常用操作

## 添加
```
	git add --all
	git add .
```

## 放弃工作区修改

```
	git checkout -- <file>
	git checkout .
```

## 放弃git的add跟踪

```
	git reset HEAD <file>
```

## 取消提交

```
	git reset <commit> --soft // 安全的回退 会恢复到指定的commit,之后的提交会缓存在工作区
	git reset <commit> --hard // 回退到 指定的commit,完全恢复。之前的提交会被回滚
```

## 代码误合并到master
> 在push到gitlab上的`master`分支前，要先关闭master的保护

* 先fetch，重新checkout`master`的代码
* 查看需要回滚的版本的commit`hash`，可以使用`git log`
* 回滚到代码，`git reset <commit> --hard`
* 重新push。可以使用`--force`来强制push,`git push --force origin master`

## 代码分支误删除
* 先查看git记录,`git log -g`,找到想要的commit
* 使用`使用git branch recover_branch[新分支] commit_id`命令用这个commit创建一个分支
* 切换到`recover_branch`分支,查看是否已经恢复

## 手动解决冲突(将GYLYF-1234Merge到sit)
* 首先`git fetch`
* 查看线上的分支名称`git branch -a`
* 将需要合并到的分支切到本地
* `git checkout -b 1234-sit remotes/origin/sit`,`git checkout -b 本地要checokout分支名 前面查看的线上的分支名称`
* 将`GYLYF-1234`merge到`1234-sit`分支
* `git merge GYLYF-1234`
* 将代码push到远程`git push origin 1234-sit`

## git更新远程库到本地
> webstorm里有一个`Update Project`选项可以进行更新,使用终端的话用`pull`

* `git pull origin master:master`第一个master是远程库的分支,第二个是本地的分支

## git`clone`代码到本地
> clone到本地的指定目录

* `git clone xxx.git 指定的目录`

## 远程版本库的操作

* 首先在页面上新建版本库
* 复制版本库的ssh路径
* 创建本地项目版本库`git init`
* 新建文件,并提交本地版本库`git add --all`,`git commit -m 'test'`
* 添加远程版本库`git remote add origin 版本库的路径`
* 上传本地的git项目`git push origin master`
* 输入账户密码
* 删除远程版本库`git remote remove orgin`

## 从远程版本库下载项目

* 找到项目在的页面
* 复制ssh路径
* 进入本地文件夹`git clone 项目ssh路径`
* 输入密码