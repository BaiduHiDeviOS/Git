## 参考资料

### [Open Source Guides](https://opensource.guide/)



### Git教程

[廖雪峰Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000): 入门和快速上手

[Pro Git](https://git-scm.com/book/en/v2)：适合有一定基础的同学。

[merging vs rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing/)

[git recipes](https://github.com/geeeeeeeeek/git-recipes): :octocat: Git recipes in Chinese. 高质量的Git中文教程.

[some git summary](http://hujiaweibujidao.github.io/blog/2016/08/02/some-git-summary/)

### Git Workflow

[Workflows with git-flow](https://www.git-tower.com/learn/git/ebook/en/mac/advanced-topics/git-flow)

[A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)

[Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows/)

[git workflow tutorial](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)

### Git and Xcode

[Versioning with Xcode and git](https://fuller.li/posts/versioning-with-xcode-and-git/): Using a script in your build phase, you can run a shell to determine the version number and inject this into the Info.plist of a build. It will never modify your local project, just the created build.

[Xcode Git ignore](https://github.com/github/gitignore/blob/master/Global/Xcode.gitignore)

[gitignore](https://www.gitignore.io/): 生成各种gitignore

[gitignore](https://github.com/github/gitignore): A collection of useful .gitignore templates


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

#### [git grep](https://git-scm.com/docs/git-grep)

```git grep``` will look through the files in your working directory.
you can search through any tree in Git, not just the working directory.


```bash
// print out the line numbers where Git has found matches.
$ git grep -n/--line-number

// summarize the output by showing you only which files contained 
// the search string and how many matches there were in each file
$ git grep -c/--count

// display the enclosing method or function for each matching
// string with either of the -p or --show-function options
$ git grep -p self.window

// ensures that multiple matches must occur in the same linie of text.
$ git grep --break --heading \
-n -e '#define' --and \( -e LINK -e BUF_MAX\) v1.8.0
```


#### [git bisect](https://git-scm.com/docs/git-bisect)

```git bisect``` use binary search to find the commit that introduced a bug.

```bash
$ git bisect start
// Current version is bad
git bisect bad

// v2.6.13-rc2 is known to be good
$ git bisect good v2.6.13-rc2
```

Once you have specified at least one bad and one good commit, ```git bisect``` selects a commit in the middle
of that range of history, checks it out.

You sholud now compile the checked-out version and test it. If that version works correctly, type
```bash
$ git bisect good
```

If that version is broken type
```bash
$ git bisect bad
```

reset
```bash
$ git bisect reset
```
