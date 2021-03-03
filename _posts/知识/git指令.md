---
date: 2015-06-13 19:11
status: public
tags: git
title: git指令
---
获取github上的项目

    git clone 项目地址

切换分支
    
    git checkout 'branchName'
从远程更新代码到本地
    
    git pull
添加代码到索引

    git add .
提交

    git commit -m 'update'
更新至远程

    git push origin master    
查看提交纪录
    
    git log
    git log -p xxxxxxxxxxxxxxxxx
回退更改
    
    git reset xxxxxxxxxxxxxxxxx


删除Git仓库所有提交历史记录，成为一个干净的新仓库

Checkout

    git checkout --orphan latest_branch
   Add all the files

    git add -A
Commit the changes

    git commit -am "commit message"
    
Delete the branch

    git branch -D master

Rename the current branch to master

    git branch -m master
Finally, force update your repository

    git push -f origin master

参考地址:
>https://stackoverflow.com/questions/13716658/how-to-delete-all-commit-history-in-github

git add -A 和 git add . 的区别

Git Version 1.x: 

![](/git指令/git1.jpg)

Git Version 2.x: 

![](/git指令/git2.jpg)
