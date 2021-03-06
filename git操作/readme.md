# Git操作

> 以前对 Git 只是简单使用，今天开始深入学习。

- 参考文章
    - [廖雪峰老师git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

## Git 简介

- 开源
    - Linus 创建了 Linux，后来 Linux 成为最大的开源服务器系统软件
    - Linux代码库日益壮大，无法手工管理，所以 Linus 花两周时间用 C 写了 Git。

- 分布式版本控制系统 Git
    - 每个人的电脑上都有一份完整的版本库
    - 不需要联网
    - 强大的分支管理
    - 个人库和中央仓库一样，服务器挂了可以从任一个个人库拷过去，重新搭建版本库

- 集中式版本控制系统 SVN、CVS
    - 版本库存放在中央服务器
    - 必须联网
    - 每次提交的是 commit
    - 如果服务器挂了，没法恢复，因为个人库没有历史版本库

## Git 安装

- [Git官网下载](https://git-scm.com/downloads)

- 可以选择 Mac、Windows、Linux版本，下载后解压运行即可

配置全局用户名、邮箱，这是你以后提交以及拉取代码的身份信息

``` git
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

## 创建版本库

- 版本库是代码仓库，仓库可以被 Git 管理起来，以后每个人的提交记录都会被记录。

``` git
mkdir git-test & cd git-test
git init
```


- 提示 'Initialized empty Git repository in D:/_my/git-test/.git/' 表示创建成功

## git 命令

### git stash

stash命令可用于跨分支临时的保存和恢复本地修改

> stash 命令只能保存git add 保存在暂存区的修改记录

> 应用场景：比如在开发分支 develop 上进行某个需求的开发，但是临时有个紧急的线上问题需要修改。
> - 第一种办法：本地新拉 hotfix 分支，这样就 develop 修改的内容将不会被影响。但是实际开发中 我们从新拉分到安装依赖，在到启动项目将耗费大量时间。
> - 第二种办法：使用 git stash 将 develop 分支的修改记录保存下来，切换至hotfix分支，完成线上问题的修改。然后回到 develop 分恢复保存的记录。

- git stash [save message]
    - git stash
    默认保存
    - git stash save 'message'
    带注释
- git stash list
    查看所有保存记录
- git stash apply [stash@{index}]
    可恢复多次 恢复后记录保存在git stash list 中
    - git stash apply
    恢复第一个记录
    - git stash apply 'stash@{1}'
    恢复第二记录
- git stash pop [stash@{index}]
    只能恢复一次 恢复后删除暂存记录
    - git stash pop
    - git stash pop 'stash@{1}'
- git stash drop [stash@{index}]
    删除某个记录
- git stash clear
    删除所有

## 新建代码库
```git
# 在当前目录新建一个Git代码库
git init 

# 新建一个目录，将其初始化为Git代码库
git init [project-name]

#克隆项目和整个history
git clone [url]
```

## 配置
```git
# 查看当前项目配置
git config --list

# 设置提交代码时的用户信息
git config [--global] user.name "[name]"  // 用户名
git config [--global] user.email "[email address]"  // 邮箱
```

## 添加暂存文件
```git
# git add之前最好执行git status
#查看当前项目更改状态
# git status

# 暂存所有已更改文件
git add *

# 暂存指定文件
git add [文件名]
git add [文件1] [文件2] ...
 
# 添加当前目录的所有文件到暂存区
$ git add .
```

## 分支
```git
# 列出所有本地分支
git branch

# 列出所有远端分支
git branch -r

# 新建一个分支，但依然停留在当前分支
git branch [分支名]

# 新建一个分支，并切换到该分支
git checkout -b [分支名]

# 新建切换到该分支，并创建远程分支建立连接
git checkout -b [分支名]
git push origin [分支名]

# 本地分支与远端分支同步并建立关联，没有则新建
git push origin [本地分支名]:[远端分支名]

# 合并目标分支到当前分支
git merge [目标分支名]

# 删除分支
$ git branch -d [分支名]

# 删除远端分支
$ git push origin --delete [分支名]
$ git push origin : [分支名]
```

## 添加远程仓库
```git
# 为目标远程仓库建立指引(取别名 )
git remote add [别名] [远端仓库url] // git remote add dfv [远端url]  (注：dfv 为别名 表示这个远端地址) 
```

## 更新代码
```git
# 实际开发中最好每次提交代码前更新代码

# 更新与提交代码前,注意切换分支

# 拉取远端仓库代码，与本地合并
# mater 分支
git pull origin master  // 此处 origin 表示远程仓库地址
# 其他分支
git pull [远端地址\别名] [分支名]  // git pull dfv br_feature
```

## 代码提交
```git
# 提交暂存区的代码到仓库
git commit -m [注释]

# 提交暂存区的指定文件到仓库区
git commit [文件1] [文件2] ... -m [注释]

# 建议：git commit 后执行 git pull 对比，解决冲突后 git push 推送到远端

# git push
# master分支
git push origin master
# 其他分支
git push dfv br_feature
git push [远程仓库url] [分支名]
```