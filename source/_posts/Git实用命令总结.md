---
title: Git实用命令总结
date: 2020-05-22 11:52:12
tags:
---

#### 从一个分支拷贝提交到当前分支

- 将ID为commit_id 的提交应用到当前分支
``` bash
git cherry-pick <commit-id>  
```

- 将从A到B的提交应用到当前分支 (A比B先提交)
``` bash
git cherry-pick A^..B  # 包含A
git cherry-pick A..B  # 不包含A
```

- `git fetch --all` 仅fetch当前分支
可以通过命令
```
$ git config --get remote.origin.fetch
+refs/heads/master:refs/remotes/origin/master
```
检查fetch设置，可以看到以上例子中，我们设置了只fetch远端master分支，可以通过修改这个配置参数来将追踪远端所有分支
```
$ git config remote.origin.fetch "+refs/heads/*:refs/remotes/origin/*"
$ git config --get remote.origin.fetch
+refs/heads/*:refs/remotes/origin/*
```
