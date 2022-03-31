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

```shell
# git log 详细用法
git log [<options>] [<since>..<until>] [[--] <path>...]

# 显示参数

-p：按补丁显示每个更新间的差异，比下一条- -stat命令信息更全
--stat：显示每次更新的修改文件的统计信息，每个提交都列出了修改过的文件，以及其中添加和移除的行数，并在最后列出所有增减行数小计
--shortstat：只显示--stat中最后的行数添加修改删除统计
--name-only：尽在已修改的提交信息后显示文件清单
--name-status：显示新增、修改和删除的文件清单
--abbrev-commit：仅显示SHA-1的前几个字符，而非所有的40个字符
--relative-date：使用较短的相对时间显示（例如："two weeks ago"）
--graph：显示ASCII图形表示的分支合并历史
—pretty＝：使用其他格式显示历史提交信息，可选项有：oneline,short,medium,full,fuller,email,raw以及format:<string>,默认为medium，如：
--pretty=oneline：一行显示，只显示哈希值和提交说明（--online本身也可以作为单独的属性）

--pretty=format:""：控制显示的记录格式，如：

    %H  提交对象（commit）的完整哈希字串
    %h  提交对象的简短哈希字串
    %T  树对象（tree）的完整哈希字串
    %t  树对象的简短哈希字串
    %P  父对象（parent）的完整哈希字串
    %p  父对象的简短哈希字串
    %an 作者（author）的名字
    %ae 作者的电子邮件地址
    %ad 作者修订日期（可以用 -date= 选项定制格式）
    %ar 作者修订日期，按多久以前的方式显示
    %cn 提交者(committer)的名字
    作者和提交者的区别不知道是啥？
    作者与提交者的关系：作者是程序的修改者，提交者是代码提交人（自己的修改不提交是怎么能让别人拉下来再提交的？）
    其实作者指的是实际作出修改的人，提交者指的是最后将此工作成果提交到仓库的人。所以，当你为某个项目发布补丁，然后某个核心成员将你的补丁并入项目时，你就是作者，而那个核心成员就是提交者（soga）
    %ce 提交者的电子邮件地址
    %cd 提交日期（可以用 -date= 选项定制格式）
    %cr 提交日期，按多久以前的方式显示
    %s  提交说明
带颜色的--pretty=format:""
以这句为例：%Cred%h%Creset -%C(yellow)%d%Cblue %s %Cgreen(%cd) %C(bold blue)<%an>

先断句：［%Cred%h］［%Creset   -］［%C(yellow)%d ］［%Cblue%s］［%Cgreen(%cd)］［%C(bold blue)<%an>］
然后就是很明显能得到的规律了
1.一个颜色＋一个内容
2.颜色以％C开头，后边接几种颜色，还可以设置字体，如果要设置字体的话，要一块加个括号
能设置的颜色值包括：reset（默认的灰色），normal, black, red, green, yellow, blue, magenta, cyan, white.
3.字体属性则有bold, dim, ul, blink, reverse.  
4.内容可以是占位元字符，也可以是直接显示的普通字符

--date= (relative|local|default|iso|rfc|short|raw)：定制后边如果出现%ad或%cd时的日期格式
有几个默认选项
--date=relative：shows dates relative to the current time, e.g. "2 hours ago".
--date=local：shows timestamps in user’s local timezone.
--date=iso (or --date=iso8601)：shows timestamps in ISO 8601 format.
--date=rfc (or --date=rfc2822)：shows timestamps in RFC 2822 format,often found in E-mail messages.
--date=short：shows only date but not time, in YYYY-MM-DD format.这个挺好用
--date=raw：shows the date in the internal raw git format %s %z format.
--date=default：shows timestamps in the original timezone (either committer’s or author’s).
也可以自定义格式（需要git版本2.6.0以上），比如--date=format:'%Y-%m-%d %H:%M:%S' 会格式化成：2016-01-13 11:32:13，其他的格式化占位符如下：
    %a：Abbreviated weekday name
    %A：Full weekday name
    %b：Abbreviated month name
    %B：Full month name
    %c：Date and time representation appropriate for locale
    %d：Day of month as decimal number (01 – 31)
    %H： Hour in 24-hour format (00 – 23)
    %I：Hour in 12-hour format (01 – 12)
    %j：Day of year as decimal number (001 – 366)
    %m：Month as decimal number (01 – 12)
    %M：Minute as decimal number (00 – 59)
    %p：Current locale's A.M./P.M. indicator for 12-hour clock
    %S：Second as decimal number (00 – 59)
    %U：Week of year as decimal number, with Sunday as first day of week (00 – 53)
    %w：Weekday as decimal number (0 – 6; Sunday is 0)
    %W：Week of year as decimal number, with Monday as first day of week (00 – 53)
    %x：Date representation for current locale
    %X：Time representation for current locale
    %y：Year without century, as decimal number (00 – 99)
    %Y：Year with century, as decimal number
    %z, %Z：Either the time-zone name or time zone abbreviation, depending on registry settings; no characters if time zone is unknown
    %%：Percent sign
 
```



`git reset HEAD filename`

将不小心执行了git add命令的内容移出暂存区

`git reset --hard commitID`

回退到某个版本

```shell
# 回退到上个版本
git reset --hard HEAD^

# 回退到前3次提交以前，以此类推，回退到n次提交之前
git reset --hard HEAD~3

# git reset 参数：
# 1. --soft:回退到某个版本，回退之前对工作区和暂存区的修改保存下来
# 2. --hard:回退到某个版本，但回退之前所有的修改都会被删除，比如你回退之前，对某个文件进行了修改，回退之后，意味着这些修改也会被抹除
# 3. --mixed(默认参数）：回退到某个版本但会保留工作区内容，清空暂存区

```



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

`git branch --merge`

查看已合并到当前分支的分支

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

