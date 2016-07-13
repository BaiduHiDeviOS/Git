## 参考资料

### Git教程

[廖雪峰Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000): 入门和快速上手

[Pro Git](https://git-scm.com/book/en/v2)：适合有一定基础的同学。

[merging vs rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing/)


### Git Workflow

[Workflows with git-flow](https://www.git-tower.com/learn/git/ebook/en/mac/advanced-topics/git-flow)

[A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)

[Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows/)

[git workflow tutorial](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)


### Git 命令快速查询


#### git config
```bash
$ git config --global alias.co checkout 
$ git config --global alias.br branch 
$ git config --global alias.ci commit 
$ git config --global alias.st status
$ git config --global alias.last 'log -1 HEAD'
$ git config --global alias.unstage 'reset HEAD --'
$ git config user.name "donganyuan"
$ git config user.email "donganyuan@baidu.com"
$ git config --global core.editor "atom --wait"
```

#### git commit
```bash
$ git commit -a -m "comment" //添加并提交
$ git commit --amend //修改上次commit, do not amend your last commit if you have already pushed it

```

#### git merge
```bash

$ git merge [branch name]

禁用fast forward merge
$ git merge --no-ff -m "comment" branch_name
```


#### git log
```bash
$ git log -p -2 //查看每次提交的diff
$ git log --since=2.weeks
$ git log --author=AnYuan
$ git log --grep=keywords
$ git log --oneline --decorate // show you where the branch pointers are pointing.


//this command shows you any commits in your current branch that are not in
//the master branch on your origin remote.
$ git log origin/master..HEAD
```


#### git remote
```bash
查看远程仓库信息：
$ git remote -v
$ git remote add dev https://github.com/ddd/git
$ git remote show origin //inspecting a remote
```

#### git stash
```bash
$ git stash --保存未提交修改
$ git stash list --查看当前stash

$ git stash apply stash@{0}
$ git stash drop
等价于
$ git stash pop
```

#### git branch
```bash
分支管理：

$ git checkout -b dev //-b 表示创建并切换分支
等价于
$ git branch dev
$ git checkout dev


git branch //查看当前分支 *表示当前分支

$ git branch -d dev //删除dev分支
$ git branch -D dev //强制删除未merge分支

$ git branch -vv //to see what tracking branches you have set up

禁用fast forward merge
$ git merge --no-ff -m "comment" branch_name

//share branch
$ git push origin branch_name
//delete remote branch
$ git push origin --delete [branchname]
```

#### undo

```bash
1.未add 修改文件时（工作区），撤销可以：
$ git checkout -- [filename] 把文件在工作区的修改全部撤销， 把这个文件会退到最近一次commit或add状态
这个操作很危险，checkout后无法恢复了

2.add修改文件后(修改进入暂存区)，撤销可以：
$ git reset HEAD [filename]

3.commit后，撤销：
$ git reset --hard HEAD^
```


#### git reflog
```bash
$ git reflog 记录每次命令
```

#### git diff
```bash
$ git diff //to see what you have changed but not yet staged
$ git diff --staged or cache // compares your staged changes to your last commit.
```

#### git reset
```bash
$ git reset --hard HEAD^ 回退到上一次commit
$ git reset --hard 3628164
//HEAD^^ 回退到上两个版本
//HEAD~100 回退到上100个版本

$ git reset --soft //update HEAD pointer
$ git reset --soft HEAD~ 等价于git commit --amend
$ git reset --mixed //default 参数，将commit的修改，放到stage区
$ git reset --hard //update working copy

//squashing
$ git reset --soft HEAD~2
```


#### git rm
```bash
$ git rm [filename]

//keep the file in your working tree but remove it from your staging area.
$ git rm --cached filename
```

#### git tag
```bash
打标签,tag默认在本地，必须显示的push到服务器
$ git tag v1.0
$ git tag v0.9 commit-id
$ git tag -a v0.1 -m "version 0.1 released" commit-id
$ git push origin v1.0 //推送标签到远程服务器
$ git push origin --tags //一次性推送全部尚未推送到远程的本地标签

//删除标签
//1.删除本地
$ git tag -d v0.9
//2.推送到远程
$ git push origin :refs/tags/v0.9
```
