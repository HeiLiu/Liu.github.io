
---
title: git 操作常用命令
date: 2018-4-21
tags: 'git'
categories: Skill
---


git所有的命令都是以git开头 后面为所要做的操作 再后面即为参数
- 初始化 git init 初始化后会生成.git文件
- git clone URL 将URL地址下的资源clone到本地  
- git add . 将当前目录下面的文件提交到暂存区
- git commit -m '你所做的修改，利于以后维护和回退' 会得到一个指针
- git push origin master 上传代码到github `master`分支
- git branch 查看所有分支
- git branch hexo 新建名为hexo的分支
- git checkout hexo 切换到hexo分支
- git merge <branch> 合并指定分支到当前分支


##git合并分支
&nbsp;git支持很多种工作流程，在进行合作开发时一般是这样，远程创建一个主分支，本地每人创建功能分支，日常工作流程如下：
1. 去自己的工作分支
    >   git checkout work

2. 工作
....

3. 提交工作分支的修改
    > git commit -a

4.回到主分支  
> git checkout master

5.获取远程最新的修改，此时不会产生冲突  
> git pull

6.回到工作分支  
> git checkout work

7.用rebase合并主干的修改，如果有冲突在此时解决  
> git rebase master

8.回到主分支  
> git checkout master

9.合并工作分支的修改，此时不会产生冲突。  
> git merge work

10.提交到远程主干  
> git push origin master

这样做的好处是，远程主干上的历史永远是线性的。每个人在本地分支解决冲突，不会在主干上产生冲突.

可以在一条分支上一起开发，你有变更的时候，在提交前，使用
> git stash

这样将本地的修改全部缓存在一个堆栈中了，然后把别人的修改同步过来

> git pull --rebase

下一步是将自己的变更恢复到最新的节点上

> git stash pop

然后再使用git commit提交，这样就会让一个分支的版本按顺序继续发展





