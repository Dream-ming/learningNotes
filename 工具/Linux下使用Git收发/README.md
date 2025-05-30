# Git

## Linux下使用git

* git add code.txt
  * 修改文件后，添加文件
* git commit -m '描述'
  * 给本次修改写描述
* git commit -am '描述'
  * 合并 add 和 commit

* git reset --hard HEAD^
  * 回退一个版本
  * HEAD^^: 回退两个版本
  * HEAD~100: 回退100个版本
* git reflog
  * 查看每个版本的版本序号
  * git log --graph: 查看分支图
  * git log --pretty=online：简短的显示版本
* git reset --hard 版本序列号
  * 跳到某个版本
* git status
  * 查看工作区和暂存区的情况
* git reset HEAD code.txt
  * 丢弃暂存区的该文件的提交
* git checkout -- code.txt
  * 丢弃工作区的该文件的修改
* git diff HEAD -- code.txt
  * 对比工作区的code.txt和最新版本HEAD中的有什么不同
  * 第一行会返回暂时名字，按照顺序对应自己写的文件名，然后+xxx表示+++文件多的内容，-号反之
* git diff HEAD HEAD^ -- code.txt
  * 对比 HEAD 和 HEAD^ 中 code.txt 的不同
* git branch
  * 查看分支，*是当前分支
* git checkout -b dev
  * 创建并切换到 dev 分支
  * git checkout master: 切换回master分支
  * git b dev: 创建 dev 分支
* git merge dev
  * 快速合并 dev 到当前分支
  * 如果不能快速合并，手动解决冲突即可
* git branch -d dev
  * 删除 dev 分支
* git push origin dev
  * 将本地的 dev 分支推送到 github 上
* git pull origin smart
  * 将 github 上的 smart 分支拉取到本地
* git clone 仓库地址
  * 克隆仓库
  * git clone -b 分支名 仓库地址：指定分支克隆
* ssh-keygen -t rsa -C '邮箱'
  * 生成ssh密钥，创建在 ~/.ssh
* 更新子模块
  * 确认当前仓库的子模块是否需要更新，下面的命令会返回子模块当前的版本号
    * git submodule status

  * 进入子模块所在的目录
    * cd 子模块

  * 切换到子模块仓库对应的分支
    * git checkout dev

  * 拉取子模块的最新代码
    * git pull

  * 返回父仓库
    * cd ..

  * 更新子模块的引用
    * git submodule update --remote

* 回退子模块
  * 与更新子模块类似
  * 先进入子模块的文件目录
  * 回退版本
  * 回到父窗口
  * 更新子模块


## Gitkraken的图形化界面

这里是 git 的使用笔记

先用Gitkraken的图形化界面熟悉一下操作

下载完软件以后，clone没问题，push的时候一直跳失败，然后发现还要把SSH key放到github里，现在畅通使用了

Try Branch
