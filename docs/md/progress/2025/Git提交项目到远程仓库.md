```
createtime: 2025-11-25
```

问题：e-commerce-system: Everything is up-to-date inventory-service: Push to origin/master was rejected order-service: Push to origin/master was rejected
提交子项目的时候报错，解决办法是给每个子项目建立一个独立的git仓库



设置远端仓库地址：

```
git remote set-url origin https://gitee.com/flying_shrimp/order-service.git
```

当需要重新设置仓库地址时可以用



问题：拉取项目报错`choose upstream branch`


原因是本地仓库和远端仓库的分支没有关联

解决：关联远端仓库

1. 查看远端仓库 `git remote -v`

2. 使用`git fetch`命令更新本地对远程仓库的认知，然后使用`git branch -r`命令查看所有远程分支。
3. 设置本地仓库和远端仓库的关联关系 `git branch --set-upstream-to=origin/master master`



问题：refusing to merge unrelated histories
原因：本地和远端内容有冲突
解决： git pull origin master --allow-unrelated-histories（允许拉取不相关的历史）



本地无项目，关联远端仓库的步骤

```
创建 git 仓库:
mkdir order-service
cd order-service
git init
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin https://gitee.com/flying_shrimp/order-service.git
git push -u origin "master"
```



已有仓库，关联远端仓库的步骤

```
cd existing_git_repo
git remote add origin https://gitee.com/flying_shrimp/order-service.git
git push -u origin "master"
```



**总结**

本地项目，先要设置远端仓库的地址，然后要同步本地和远端的历史，分支也要关联上，这样才能拉取成功。

如果是父子项目，分为两种情况，父子项目强关联、父子项目单独一个仓库。如果是强关联，一般是单独一个团队开发。单独仓库更适合不同的团队负责不同的项目，单独仓库可以保证每个项目都有各自的历史，父项目只要管理好每个子项目的版本就可以了。

> 实操记录：子项目创建为maven项目，git记录是在父项目的仓库中的，子项目为springboot项目，git记录会单独一个仓库。这是因为IDEA设置了**Create Git repository**，创建新项目就会自动创建一个单独的仓库。