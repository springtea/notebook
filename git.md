`git init`

初始化，将该目录作为git管理的目录

`git status`

查看当前目录下的文件情况

-s: 简洁查看文件情况

`git add`

将文件添加到暂存区，即跟踪文件

`git diff`

比较跟踪的文件，在工作目录和暂存区的不同

`git diff --staged`

比较跟踪的文件，在暂存区和最近一次commit的不同

`git commit -m  `

是记录当前项目的一次快照，之后可以恢复到这个状态

`git commit -a -m`

加上`-a`参数，git会把所有跟踪过的文件一起提交，而跳过`git add`这个步骤

`git  rm  <file>`

在工作目录中手动删除文件后，使用该命令删除暂存区中的该文件

`git rm --cached`

当打算移除跟踪但不删除文件，可以使用这个命令。通常使用在你想稍后将该文件移到`.gitigonre`目录下

`git commit --amend`

当提交之后想更改提交信息，使用该命令，可以修改提交信息，或者可以将忘记add的内容add，再使用该命令，它们将记入最近一次的提交

`git log`

查看commit历史。当你在提交了若干更新之后，又或者克隆了某个项目，想回顾下提交历史，可以使用该命令。

+ 图形化工具gitk相当于git log的可视化工具

`git reset HEAD filename`

将不小心执行了git add命令的内容移出暂存区

`git checkout --  filename`

暂存区里的文件内容被修改之后，如果想撤销该修改，可以使用该命令

`git restore --staged filename`

将文件移出暂存区

`git restore filename`

撤销工作区里对已跟踪文件的修改

eg. 比如我对工作区的文件进行了修改，我想撤销这个修改，可以使用这个命令

`git config --global alias.co checkout`

起别名

`git remote`

命令可以列出当前配置有哪些远程仓库

`git remote -v`

'verbose',显示对应的克隆地址

`git remote add [remotename] [url]`

要添加一个新的远程仓库，可以指定一个简单的名字，以便将来引用

```shell
# git remote add origin git@gitee.com:meandmylittlecat/notebook.git
```

`git fetch [remotename]`，可简写为`git fetch`

从远程仓库抓取数据到本地,默认情况下取回所有分支的更新。如果只想取回特定分支的更新，可以指定分支名



`git fetch <remotename> <branchname>`

```shell
# 取回origin主机的master分支
git fetch origin master
```

**fetch 命令只是将远端的数据拉到本地仓库，并不自动合并到当前工作分支，只有当你确实准备好了，才能手工合并。**

```shell
# 例如：
macos@MacOSdeMacBook-Pro notebook % git branch -a
* master
  remotes/origin/master
macos@MacOSdeMacBook-Pro notebook % git merge origin/master
Updating ceb5668..66f050f
Fast-forward
 test.md | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 test.md
```



`git push [remotename] [branchname]`

推送本地数据到远程仓库

例如：

 ```shell
# git push origin master
 ```

`git remote show [remotename]`

查看某个远程仓库的详细信息

```shell
# git remote show origin
```

`git remote rename origin origin2`

修改某个远程仓库在本地的简称，例如将`origin`修改为`origin2`

`git remote rm origin`

碰到远端仓库服务器迁移，或者原来的克隆镜像不再使用，又或者某个参与者不再贡献代码，那么需要移除对应的远端仓库。

`git config --global alias.co checkout`

设置别名，该语句含义为输入`git co`，则等同于输入`git checkout`

```shell
git config --global alias.unstage 'reset HEAD --'

# 这样以来，下面这两行命令等价
git unstage fileA
git reset HEAD fileA

# 常用别名
git config --global alias.last 'log -1 HEAD'
```

`git branch testing`

创建新的分支testing

`git branch -d testing`

删除testing分支

`git branch -D testing`

删除没有被合并的分支

`git branch -v`

查看各个分支最后一个提交对象的信息

`git branch -r`

查看远程分支

`git branch -a`

查看所有分支

```shell
$ git branch -r
origin/master

$ git branch -a
* master
  remotes/origin/master
```



`git branch`

如果不加任何参数，它会给出当前所有分支的清单.*表示当前所在分支

```shell
# git branch
#    iss53
#    * master
#    testing
```

`git branch --no-merged`

查看尚未合并的工作

**它会显示还未合并进来的分支。由于这些分支中还包含着尚未合并进来的工作成果，所以简单地用 `git branch -d` 删除该分支会提示错误，因为那样做会丢失数据**

`git checkout testing`

切换到分支testing

`git -b checkout testing`

创建并切换到分支testing

```shell
git checkout master
git merge hotfix
```

切换到master，合并分支hotfix

`git stash`

将当前工作现场储藏起来，等以后恢复现场后继续工作

`git stash list`

查看所有stash

`git stash pop`

恢复现场（`git stash apply`)

同时删除stash内容(`git stash drop`)

`git cherry-pick 4c805e2`

复制另一条分支上的commit

