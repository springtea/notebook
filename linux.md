# linux基础命令

常见的执行linux命令的格式如下：

> 命令名称  [命令参数]  [命令对象]

+ Linux系统中的命令、参数、对象都是严格区分大小写的。



## man

man命令中常用按键以及作用

| 按键      | 作用                               |
| --------- | ---------------------------------- |
| 空格键    | 向下翻一页                         |
| PaGe down | 向下翻一页                         |
| PaGe up   | 向上翻一页                         |
| home      | 直接前往首页                       |
| end       | 直接前往尾页                       |
| /         | 从上至下搜索某个关键词，如“/linux” |
| ?         | 从下至上搜索某个关键词，如“?linux” |
| n         | 定位到下一个搜索到的关键词         |
| N         | 定位到上一个搜索到的关键词         |
| q         | 退出帮助文档                       |

快捷键：

+ Ctrl + d:当同时按下键盘上的Ctrl和字母d的时候，表示键盘输入结束。
+ Ctrl + l:当同时按下键盘上的Ctrl和字母l的时候，会清空当前终端中已有的内容（相当于清屏操作）。
+ Tab:实现对命令、参数或文件的内容补全
+ Ctrl + c: 当同时按下键盘上的Ctrl和字母c的时候，意味着终止当前进程的运行。
+ Ctrl + u/Ctrl + k: 分别是从光标处向前删除指令串或向后删除指令串
+ Ctrl + a/Ctrl + e:分别是让光标移动到整个指令串的最前面 ([ctrl]+a) 或最后面 ([ctrl]+e)。

## echo

输出字符串或提取Shell变量的值。

常用参数：

| -n       | 不输出结尾的换行符               |
| -------- | -------------------------------- |
| -e “\a”  | 发出警告音                       |
| -e “\b”  | 删除前面的一个字符               |
| -e “\c”  | 结尾不加换行符                   |
| -e “\f”  | 换行，光标扔停留在原来的坐标位置 |
| -e “\n”  | 换行，光标移至行首               |
| -e “\r”  | 光标移至行首，但不换行           |
| -E       | 禁止反斜杠转移，与-e参数功能相反 |
| —version | 查看版本信息                     |
| --help   | 查看帮助信息                     |

```shell
echo $PATH
# /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin

# 常用的环境变量
# 1. PATH 决定了shell将到哪些目录中寻找命令或程序 
# 2. HOME 当前用户主目录 
# 3.HISTSIZE　历史记录数 
# 4.LOGNAME 当前用户的登录名 
# 5.HOSTNAME　指主机的名称 
# 6.SHELL 当前用户Shell类型 
# 7.LANGUGE 　语言相关的环境变量，多语言可以修改此环境变量 
# 8.MAIL　当前用户的邮件存放目录 

echo PATH
# PATH

# 结合输出重定向符，将字符串信息导入文件中：
 echo "hello world" > hello.txt
 
 # 使用-b参数
 echo -e "123\b456" 
 # 12456
```

+ date

date命令用于显示或设置系统的时间与日期，语法格式为“date [+指定的格式]”。

  date命令中的参数及其作用

| 参数 | 作用                             |
| ---- | -------------------------------- |
| %S   | 秒（00～59）                     |
| %M   | 分钟（00～59）                   |
| %H   | 小时（00～23）                   |
| %I   | 小时（00～12）                   |
| %m   | 月份（1~12）                     |
| %p   | 显示出AM或PM                     |
| %a   | 缩写的工作日名称（例如：Sun）    |
| %A   | 完整的工作日名称（例如：Sunday） |
| %b   | 缩写的月份名称（例如：Jan）      |
| %B   | 完整的月份名称（例如：January）  |
| %q   | 季度（1~4）                      |
| %y   | 简写年份（例如：20）             |
| %Y   | 完整年份（例如：2020）           |
| %d   | 本月中的第几天                   |
| %j   | 今年中的第几天                   |
| %n   | 换行符（相当于按下回车键）       |
| %t   | 跳格（相当于按下Tab键）          |

例如：

```shell
 date "+%Y-%m-%d %H:%M:%S"
 # 2022-04-09 16:11:00
```

+ reboot

reboot命令用于重启系统，输入该命令后按回车键执行即可。

由于重启计算机这种操作会涉及硬件资源的管理权限，因此最好是以root管理员的身份来重启，

```shell
sudo reboot
```

+ top

top命令用于动态地监视进程活动及系统负载等信息，输入该命令后按回车键执行即可。

+ ifconfig

ifconfig命令用于获取网卡配置与网络状态等信息，英文全称为“interface config”，语法格式为“ifconfig [参数] [网络设备]”。

+ uname

Uname命令用于查看系统内核版本与系统架构等信息，英文全称为“unix name”，语法格式为“uname [-a]”。

+ uptime

uptime命令真的很棒，它可以显示当前系统时间、系统已运行时间、启用终端数量以及平均负载值等信息。

+ who 

who命令用于查看当前登入主机的用户终端信息，输入该命令后按回车键执行即可。

+ ping

ping命令用于测试主机之间的网络连通性，语法格式为“ping [参数] 主机地址”。

+ netstat

netstat命令用于显示如网络连接、路由表、接口状态等的网络相关信息，英文全称为“network status”，语法格式为“netstat [参数]”。

# Bash

## 查看当前的shell

shell不止一种，常见的shell有sh(Bourne Shell),csh(C Shell),ksh,tcsh,zsh,bash

查看当前使用的shell

```shell
echo $0
# -zsh
# mac默认的shell就是zsh
# zsh的配置文件目录为 ~/.zshrc,这个文件需要自己创建
# bash的配置文件目录为 ~/.bash_profile
```

如果对~/.zshrc或~/.bash_profile文件进行了修改，需要使用对应命令生效：

```shell
source ~/.zshrc
source ~/.bash_profile
```

Mac系统的环境变量，加载顺序为：

```SHELL
# /etc/profile 
# /etc/paths 
# ~/.bash_profile 
# ~/.bash_login 
# ~/.profile 
# ~/.bashrc
```

当然/etc/profile和/etc/paths是系统级别的，系统启动就会加载

```shell
# 查看/etc/paths中的内容

vim /etc/paths
# /usr/local/bin
# /usr/bin
# /bin
# /usr/sbin
# /sbin
```

上面的目录`usr`指的是'Unix System Source'。

通常：

`/usr/bin`下面的都是系统预装的可执行程序，会随着系统升级而改变。

`/usr/local/bin`目录是给用户放置自己的可执行程序的地方，推荐放在这里，不会被系统升级而覆盖同名文件。

查看系统有哪些shell可用

```shell
cat /etc/shells

/bin/bash
/bin/csh
/bin/dash
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```



+ `history`

  在命令行窗口种使用history命令会显示最近使用过的命令。这些历史被记录在～.zsh_history文件中。若使用bash，则记录在.bash_history中。

  ```shell
  # 要清空当前用户在本机上执行的Linux命令历史记录信息，可执行如下命令：
  history -c
  ```

  

## 查询指令是否为内置命令

bash包含内置命令和外部命令（其他非bash提供的指令），使用type指令可以观察是否为内置命令

```SHELL
type cd
# cd is a shell builtin
type ls
# ls is /bin/ls
```

## 变量

### 变量的取用

```shell
macos@MacOSdeMacBook-Pro local % echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
macos@MacOSdeMacBook-Pro local % echo ${PATH}
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
macos@MacOSdeMacBook-Pro local % echo name
name
macos@MacOSdeMacBook-Pro local % echo $name
Elaine

```

如上所示，利用echo能够读出变量，不过需要在变量名称前加上\$, 或者是以${变量名}的方式来取用

+ 变量的设置规则：

  + 双引号内的特殊字符，如$等，可以保有原本的特性

    ```shell
    macos@MacOSdeMacBook-Pro local % str1="my name is $name"
    macos@MacOSdeMacBook-Pro local % echo $str1
    my name is Elaine
    macos@MacOSdeMacBook-Pro local % str2='my name is $name'
    macos@MacOSdeMacBook-Pro local % echo str2
    str2
    macos@MacOSdeMacBook-Pro local % echo $str2
    my name is $name
    ```

  + 若该变量为扩增变量内容时，则可用 "\$变量名称" 或 \${变量} 累加内容，如下所示: 

    ```shell
    PATH="$PATH":/home/bin
    PATH=${PATH}:/home/bin
    
    # 场景：我需要在将变量name的内容后多出一个world
    name=hello
    name=${name}world
    # 注意：这里的花括号不能省
    
    # 场景：我经常使用目录~/study/web，怎样能每次能快捷访问这个目录呢
    # 方案：由于我使用的是zsh，我可以在~/.zshrc文件中配置一个变量：
    #      work=~/stydy/web
    # 		 这样，我下次使用cd $work 就能直接进入这个目录了！
    
    ```

  + 使用`unset`取消刚刚设置的变量内容

    ```shell
    name=elaine
    unset name
    ```

### 环境变量

问一下，目前我的 shell 环境中， 有多少默认的环境变量啊?我们可以利用两个指令来查阅，分别是 env 与 export !

```shell
# 示例，列出目前的shell环境下的所有环境变量与其内容
macos@MacOSdeMacBook-Pro linux % env
TMPDIR=/var/folders/b1/7szn11v96kgfyd5tbq38db440000gn/T/
XPC_FLAGS=0x0
TERM_PROGRAM_VERSION=433
LANG=zh_CN.UTF-8
TERM_PROGRAM=Apple_Terminal
XPC_SERVICE_NAME=0
TERM_SESSION_ID=7742BCAE-856B-41D6-A446-94EC90C4D171
TERM=xterm-256color
SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.UCXwmV0lAG/Listeners
SHELL=/bin/zsh # 目前这个环境下，使用的shell是哪一个程序
HOME=/Users/macos  # 这个使用者的主文件夹，也就是使用cd ~ 命令去到的主文件夹
LOGNAME=macos # 登陆者用来登录的账号名称
USER=macos # 使用者的名称
PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
SHLVL=1
PWD=/Users/macos/study/web/linux
OLDPWD=/Users/macos/study/web
_=/usr/bin/env

```

BASH中不仅有环境变量，还有一些与bash操作由关的变量，以及使用者自己定义的变量存在。这些变量可以使用

用 **set** 观察所有变量 (含环境变量与自订变量)

```shell
set
'!'=0
'#'=0
'$'=11687
'*'=(  )
-=569XZilms
0=-zsh
'?'=0
...
```

+ 想要知道我们的 shell 的 PID ，就可以用:“ echo $$ ”即可!出现的数字就是你的 PID (process id)号码,即线程代号。

+ bash里`?`也是一个特殊的变量，这个变量值是“上一个执行的指令所回传的值”。当我们执行某些指令时，这些指令都会回传一个执行后的代码。一般来说，如果成功的执行该指令，则会回传一个0值。如果执行过程发生错误，就会回传错误代码

  ```shell
  macos@MacOSdeMacBook-Pro linux % echo $SHELL
  /bin/zsh # 可顺利显示!没有错误!
  macos@MacOSdeMacBook-Pro linux % echo $?
  0  # 因为没问题，所以回传值为 0
  macos@MacOSdeMacBook-Pro linux % 12name=hello
  zsh: command not found: 12name=hello # 发生错误了!bash回报有问题
  macos@MacOSdeMacBook-Pro linux % echo $?
  127 # 因为有问题，回传错误代码(非为0)
  ```

  

谈了 env 与 set 现在知道有所谓的环境变量与自订变量，那么这两者之间有啥差异呢?其实这两者的差异在于“ 该变量是否会被子程序所继续引用”!那么啥是父程序?子程序? 这就得要了解一下指令的下达行为了。

当你登陆 Linux 并取得一个 bash 之后，你的 bash 就是一个独立的程序，这个程序的识别使用的是一个称为程序识别码，被称为 PID 的 就是。 接下来你在这个 bash 下面所下达的任何指令都是由这个 bash 所衍生出来的，那些被下达的指令就被称为子程序了。

+ 子程序仅会继承父程序的环境变量， 子程序不会继承父程序的自订变量!
+ 所以在原本 bash 的自订变量在进入了子程序后就会消失不见， 一直到你离开子程序并回到原本的父程序后，这个变量才会又出现!

如你想要让该变量内容继续的在子程序中使用:

```SHELL
export  变量名称
```

如果仅下达 export 而没有接变 量时，那么此时将会把所有的“环境变量”列出来

```shell
macos@MacOSdeMacBook-Pro linux % export
HOME=/Users/macos
LANG=zh_CN.UTF-8
LOGNAME=macos
OLDPWD=/Users/macos/study/web
PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
PWD=/Users/macos/study/web/linux
SHELL=/bin/zsh
SHLVL=1
SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.UCXwmV0lAG/Listeners
TERM=xterm-256color
TERM_PROGRAM=Apple_Terminal
TERM_PROGRAM_VERSION=433
TERM_SESSION_ID=7742BCAE-856B-41D6-A446-94EC90C4D171
TMPDIR=/var/folders/b1/7szn11v96kgfyd5tbq38db440000gn/T/
USER=macos
XPC_FLAGS=0x0
XPC_SERVICE_NAME=0
macos@MacOSdeMacBook-Pro linux % export
HOME=/Users/macos
LANG=zh_CN.UTF-8
LOGNAME=macos
OLDPWD=/Users/macos/study/web
PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
PWD=/Users/macos/study/web/linux
SHELL=/bin/zsh
SHLVL=1
SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.UCXwmV0lAG/Listeners
TERM=xterm-256color
TERM_PROGRAM=Apple_Terminal
TERM_PROGRAM_VERSION=433
TERM_SESSION_ID=7742BCAE-856B-41D6-A446-94EC90C4D171
TMPDIR=/var/folders/b1/7szn11v96kgfyd5tbq38db440000gn/T/
USER=macos
XPC_FLAGS=0x0
XPC_SERVICE_NAME=0

```



### 键盘读取变量

要读取来自键盘输入的变量，就要 read 这个指令了。

```shell
[dmtsai@study ~]$ read atest
This is a test <==此时光标会等待你输入!请输入左侧文字看看 
[dmtsai@study ~]$ echo ${atest}
This is a test <==你刚刚输入的数据已经变成一个变量内容!

```

### 声明变量

declare 或 typeset 是一样的功能，就是在“宣告变量的类型”。如果使用 declare 后面并没有接任何参数，那么 bash 就会主动的将所有的 变量名称与内容通通叫出来，就好像使用 set 一样!

显示已定义的变量

```shell
declare 
```

delare参数含义：

```shell
declare [-aixr] variable
选项与参数:
-a :将后面名为 variable 的变量定义成为阵列 (array) 类型
-i :将后面名为 variable 的变量定义成为整数数字 (integer) 类型
-x :用法与 export 一样，就是将后面的 variable 变成环境变量;
-r :将变量设置成为 readonly 类型，该变量不可被更改内容，也不能 unset

```

由于在默认的情况下面， bash 对于变量有几个基本的定义:

+ 变量类型默认为“字串”，所以若不指定变量类型，则 1+2 为一个“字串”而不是“计算式”。 
+  bash 环境中的数值运算，默认最多仅能到达整数形态，所以 1/3 结果是 0;

```shell
# 让sum变成只读变量，不可更改
macos@MacOSdeMacBook-Pro linux % declare -r sum=2
macos@MacOSdeMacBook-Pro linux % echo $sum
2
macos@MacOSdeMacBook-Pro linux % sum=3
zsh: read-only variable: sum
macos@MacOSdeMacBook-Pro linux % unset sum   
zsh: read-only variable: sum

# 让count变量进行1+1+1的累加
macos@MacOSdeMacBook-Pro linux % declare -i count=1+1+1
macos@MacOSdeMacBook-Pro linux % echo $count
3
macos@MacOSdeMacBook-Pro linux % declare count2=1+1+1
macos@MacOSdeMacBook-Pro linux % echo $count2
1+1+1

# 让变量变成环境变量
macos@MacOSdeMacBook-Pro linux % declare cat=hanhan
macos@MacOSdeMacBook-Pro linux % export | grep cat
macos@MacOSdeMacBook-Pro linux % declare -x cat=hanhan
macos@MacOSdeMacBook-Pro linux % export | grep cat
cat=hanhan

# 定义数组变量
macos@MacOSdeMacBook-Pro linux % arr[1]='small'
macos@MacOSdeMacBook-Pro linux % arr[2]='big'
macos@MacOSdeMacBook-Pro linux % arr[3]='huge'
macos@MacOSdeMacBook-Pro linux % echo "${arr[1]},${arr[2]},${arr[3]}"
small,big,huge
```

使用-p显示变量定义

```shell
macos@MacOSdeMacBook-Pro linux % declare -p sum
export -ir sum=2 # 上面的例子设置了sum为只读，且为整数的环境变量，所以显示了-ir，export
macos@MacOSdeMacBook-Pro linux % declare +x sum 
macos@MacOSdeMacBook-Pro linux % export | grep sum # 用+取消掉设置的x参数赋予的环境变量的特性
macos@MacOSdeMacBook-Pro linux % declare -p sum 
typeset -ir sum=2
```

显示所有的环境变量

```shell
declare -x
```

显示所有的整数变量

```shell
delcare -i
```

显示所有的只读变量

```shell
declare -r
```

### 变量内容的删除，取代，替换

我们先看几个例子：

```shell
# 场景：如果我们有一个很长的字符串，想从开头删除到某个指定的字符/字符串，而不是一个一个字				符删除，应该怎么做呢

macos@Maclinux % content=helloworldhelloworldhelloworldhanhan
macos@Mac linux % echo ${content##*world} #从开头开始删除，直到匹配到最后一个字符串‘world’
hanhan   
macos@Mac linux % echo $content
helloworldhelloworldhelloworldhanhan
macos@Mac linux % echo ${content#*world} #从开头开始删除，直到匹配到第一个字符串'world'
helloworldhelloworldhanhan 

# 总结：
# ${变量#关键字}：若变量内容从头开始的数据符合“关键字”，则将符合的最短数据删除
# ${变量##关键字}：若变量内容从头开始的数据符合“关键字”，则将符合的最长数据删除
# 注意：*匹配大于等于0的任意字符
```

上面谈到的是“从前面开始删除变量内容”，那么如果想要“从后面向前删除变量内容”呢? 这个时候就得使用百分比 (%) 符号了：

```shell
# 例如：我想删除目录“/user/study/python/study/note"末尾的“/study/note"，该怎么做呢

macos@MacOSdeMacBook-Pro linux % dir=/user/study/python/study/note
macos@MacOSdeMacBook-Pro linux % echo ${dir%/study*}
/user/study/python

# 又如：我想删除目录“/user/study/python/study/note"中的部分，使结果为“/user”，该怎么做呢

macos@MacOSdeMacBook-Pro linux % echo ${dir%%/study*}
/user

# 总结：
# 1.${变量%关键字}：若变量内容从尾向前的数据符合“关键字”，则将符合的最短数据删除
# 2.${变量%%关键字}：若变量内容从尾向前的数据符合“关键字”，则将符合的最长数据删除
```

场景：将 p 的变量内容内的 sbin 取代成大写 SBIN:

```SHELL
macos@MacOSdeMacBook-Pro linux % p=/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/dmtsai/.local/bin:/home/dmtsai/bin
macos@MacOSdeMacBook-Pro linux % echo ${p//sbin/SBIN}
/usr/local/bin:/usr/bin:/usr/local/SBIN:/usr/SBIN:/home/dmtsai/.local/bin:/home/dmtsai/bin
macos@MacOSdeMacBook-Pro linux % echo ${p/sbin/SBIN}
/usr/local/bin:/usr/bin:/usr/local/SBIN:/usr/sbin:/home/dmtsai/.local/bin:/home/dmtsai/bin
# 总结：
# 1.${变量/旧字串/新字串}：若变量内容符合“旧字串”则“第一个旧字串会被新字串取代”
# 2.${变量//旧字串/新字串}：若变量内容符合“旧字串”则“全部的旧字串会被新字串取代”
```

### 命令别名

为命令设置别名：

```shell
macos@MacOSdeMacBook-Pro linux % alias lm='ls -al | more'
macos@MacOSdeMacBook-Pro linux % lm # 这时lm就相当于 ls -al | more了
# 取消别名
unalias lm
```

### history

显示最近的n条命令记录

```shell
history -n

macos@MacOSdeMacBook-Pro linux % history -3
 1154  history 10
 1155  history -3
 1156  history -10
```

利用histroy指令执行命令

```shell
macos@MacOSdeMacBook-Pro linux % history -3
 1157  history -3
 1158  history -3
 1159  history -3
 
 # 使用感叹号+history为我们展示的前面的数字，可以执行相应命令
 # 使用方法为 !n
 # !! :就是执行上一个指令(相当于按↑按键后，按 Enter)
 
macos@MacOSdeMacBook-Pro linux % !1159 
history -3
 1158  history -3
 1159  history -3
 1160  history -3
 
macos@MacOSdeMacBook-Pro linux % !!
history -3  # 执行的上一条命令
 1159  history -3
 1160  history -3
 1161  history -3

```

### 数据流重导向

standard output与standard error output:

简单的说，标准输出指的是“指令执行所回传的正确的讯息”，而标准错误输出可理解为“ 指令执行失败后，所回传的错误讯息”。		

1. 标准输入  (stdin,Standard input) :代码为 0 ，使用 < 或 << 
2. 标准输出  (stdout,standard output):代码为 1 ，使用 > 或 >> ; 
3. 标准错误输出(stderr,standard error output):代码为 2 ，使用 2> 或 2>> ;	 

```SHELL
# 我们执行命令返回的结果通常是输出在终端窗口中，如果我们想让它的结果返回到指定的文件中，就可以使用标准输出
echo 'hello world\nthis is a wonderful day' > hello.txt

#  打开hello.txt，我们就能看到我们刚刚输入的内容了
#  注意：
#  1. 1> :以覆盖的方法将“正确的数据”输出到指定的文件或设备上; 
#  2. 1>>:以累加的方法将“正确的数据”输出到指定的文件或设备上;

# 有时我们输入错误命令或者其他情况导致返回错误的结果，我们可以把它返回到指定的文件中：

macos@MacOSdeMacBook-Pro test % ccat hello.txt 2>> hello.txt
macos@MacOSdeMacBook-Pro test % vim hello.txt 

# 再打开刚刚的文件，发现下面追加了一行错误提示
# 这便是我们执行错误命令返回的错误
# 注意：
# 1. 2> :以覆盖的方法将“错误的数据”输出到指定的文件或设备上; 
# 2. 2>>:以累加的方法将“错误的数据”输出到指定的文件或设备上;
# 要注意，“ 1>> ”以及“ 2>> ”中间是没有空格的!

hello world
this is a wonderful day
zsh: command not found: ccat
                          
                         
# 如果无论执行错误或者正确，我都想把返回结果返回到指定文件中，应该用什么指令呢
macos@MacOSdeMacBook-Pro test % ls -al &> hello.txt # 覆盖
macos@MacOSdeMacBook-Pro test % ls -al &>> hello.txt  # 追加
macos@MacOSdeMacBook-Pro test % caat hello.txt &>> hello.txt 
macos@MacOSdeMacBook-Pro test % ccat hello.txt >> hello.txt 2>&1 # 追加
macos@MacOSdeMacBook-Pro test % ccat hello.txt > hello.txt 2>&1 # 覆盖

```

使用cat创建文件

```SHELL
# 如果test文件不存在，会自动创建。
# 执行cat > test,输入内容将保存在test文件中
# ctrl+d 结束输入

macos@MacOSdeMacBook-Pro test % cat > test
hello world
my cat's name is hanhan
ha
macos@MacOSdeMacBook-Pro test % cat test
hello world
my cat's name is hanhan
ha

# 如果我们不想手动输入，而是想用某个文件的内容代替输入，就可以使用下面这种方式

macos@MacOSdeMacBook-Pro test % cat > hanhan.txt < test
macos@MacOSdeMacBook-Pro test % cat hanhan.txt 
hello world
my cat's name is hanhan
ha
# 此时，我们刚刚存入test文件中的内容就作为输入输出到hanhan.txt中了

# 看下面这个例子。<< 这个连续两个小于的符号，代表的是“结束的输入字符”的意思
macos@MacOSdeMacBook-Pro test % cat > catfile << 'eof'
heredoc> this is a test
heredoc> ok now stop
heredoc> eof # 输入'eof'再按下回车键即结束输入
macos@MacOSdeMacBook-Pro test % cat > catfile << 'h'
heredoc> this is also a test
heredoc> ok
heredoc> now 
heredoc> stop
heredoc> h # 输入'h'再按下回车键即结束输入.这个字符取决于上面<<后的字符
```

**/dev/null** 垃圾桶黑洞设备与特殊写法

如果我知道错误讯息会发生，所以要将错误讯息忽略掉而不显示或储存呢? 这个时候黑洞设备 /dev/null 就很重要了!

```SHELL
# 将错误的数据丢弃，屏幕上显示正确的数据
macos@MacOSdeMacBook-Pro test % ccat hello.txt 2> /dev/null

```

### 命令执行的判断依据

在某些时候，我们希望可以一次执行多个指令。

**cmd ; cmd** (不考虑指令相关性的连续指令下达)

在指令与指令中间利用分号 (;) 来隔开，这样一来，分号前的指令执行完后就会立刻接着执行后面的指令了。

```shell
ls -al;cat hello.txt
```

想象这样一个场景：我想要在某个目录下面创建一个文件，也就是说，如果该目录存在的话， 那我才创建这个文件，如果不存在，那就算了。 也就是说这两个指令彼此之间是有相关性的， 前一个指令是否成功的执行与后一个指令是否要执行有关!那就得动用到 && 或 || 。

+ `cmd1 && cmd2`

1. 若 cmd1 执行完毕且正确执行(\$?=0)，则开始执行 cmd2。 
2. 若 cmd1 执行完毕且为错误 ($?≠0)，则 cmd2 不执行。

+ `cmd1 || cmd2`

1. 若 cmd1 执行完毕且正确执行(\$?=0)，则 cmd2 不执行。 
2.  若 cmd1 执行完毕且为错误 ($?≠0)，则开始执行 cmd2。

再复习一次，''若前一个指令执行的结果为正确，在 Linux 下面会回传 一个 $? = 0 的值"

### 管线命令（pipe）

管线命令“ | ”仅能处理经由前面一个指令传来的正确信息，也就是 standard output 的信 息，对于 stdandard error 并没有直接处理的能力。

+ 管线命令仅会处理 standard output，对于 standard error output 会予以忽略 
+ 管线命令必须要能够接受来自前一个指令的数据成为 standard input 继续处理才行。

### 撷取命令: **cut,** **grep**

```shell
[dmtsai@study ~]$ cut -d'分隔字符' -f fields <==用于有特定分隔字符 
[dmtsai@study ~]$ cut -c 字符区间 <==用于排列整齐的讯息 选项与参数:
-d :后面接分隔字符。与 -f 一起使用;
-f :依据 -d 的分隔字符将一段讯息分区成为数段，用 -f 取出第几段的意思;
-c :以字符 (characters) 的单位取出固定字符区间;

```

范例一:将 PATH 变量取出，我要找出第3,4,5个路径。

```SHELL
macos@MacOSdeMacBook-Pro test % echo ${PATH}
/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin
macos@MacOSdeMacBook-Pro test % echo ${PATH} | cut -d ':' -f 3,4,5
/bin:/usr/sbin:/sbin
```

范例二：新创建一个文件，读出这个文件每行第6个字符之后的内容

```shell
macos@MacOSdeMacBook-Pro test % cat > practice.txt
hello this is the first line
hello this is the second line
hello this is the third line
hello this is thie last line
hello I'm just kidding
hello this is not the last line
hello hahaha
macos@MacOSdeMacBook-Pro test % cat practice.txt | cut -c 6-
 this is the first line
 this is the second line
 this is the third line
 this is thie last line
 I'm just kidding
 this is not the last line
 hahaha
```

grep

刚刚的 cut 是将一行讯息当中，取出某部分我们想要的，而 grep 则是分析一行讯息， 若当中有我们所需要的信息，就将该行拿出来~ 简单的语法是这样的:

```SHELL
[dmtsai@study ~]$ grep [-acinv] [--color=auto] '搜寻字串' filename 选项与参数:
-a :将 binary 文件以 text 文件的方式搜寻数据
-c :计算找到 '搜寻字串' 的次数
-i :忽略大小写的不同，所以大小写视为相同
-n :顺便输出行号
-v :反向选择，亦即显示出没有 '搜寻字串' 内容的那一行!
--color=auto :可以将找到的关键字部分加上颜色的显示喔!
范例一:将 last 当中，有出现 root 的那一行就取出来; 
[dmtsai@study ~]$ last | grep 'root'

范例二:与范例一相反，只要没有 root 的就取出! 
[dmtsai@study ~]$ last | grep -v 'root'

范例三:在 last 的输出讯息中，只要有 root 就取出，并且仅取第一栏 [dmtsai@study ~]$ last | grep 'root' |cut -d ' ' -f1
# 在取出 root 之后，利用上个指令 cut 的处理，就能够仅取得第一栏啰!

范例四:取出 /etc/man_db.conf 内含 MANPATH 的那几行
[dmtsai@study ~]$ grep --color=auto 'MANPATH' /etc/man_db.conf ....(前面省略)....
MANPATH_MAP /usr/games
MANPATH_MAP /opt/bin
MANPATH_MAP /opt/sbin
# 神奇的是，如果加上 --color=auto 的选项，找到的关键字部分会用特殊颜色显示喔!
```

下面是grep用法的例子

1.  搜寻特定字符串"the"，并忽略大小写。

```shell
macos@MacOSdeMacBook-Pro test % grep --color=auto -ni the reg.txt
3:i think the weather is good
5:the wheather is not good
11:the weather is good
12:The apple tastes good
```

2. 利用中括号 **[]** 来搜寻集合字符。

   如果我想要搜寻 test 或 taste 这两个单字时，可以发现到，其实她们有共通的 't?st' 存在~这个时候，我可以这样来搜寻:

```shell
macos@MacOSdeMacBook-Pro test % grep --color=auto -ni 't[ae]st' reg.txt 
1:this is a file for reg test
12:The apple tastes good
13:tasttest
#  [] 里面不论有几个字符，他都仅代表某“一个”字符
#  所以如果是teest，则不能匹配

# 如果我想搜寻'oo'，但是希望前面不是字母，则可以这样写：
macos@MacOSdeMacBook-Pro test % grep --color=auto -ni '[^a-z]oo' reg.txt 
9:1oo
10:2oo
```

3. 行首与行尾字符 **^ $**

```SHELL
# 搜寻行首以the开头的
macos@MacOSdeMacBook-Pro test % grep -n '^the' reg.txt 
5:the wheather is not good
11:the weather is good

# 搜寻不以字母开头的行
macos@MacOSdeMacBook-Pro test % grep -n '^[^a-zA-Z]' reg.txt
9:1oo
10:2oo
#  注意：^ 符号，在字符集合符号(括号[])之内与之外是不同的! 在 [] 内代表“反向选择”，在 [] 之外则代表定位在行首的意 义

# 搜寻以.结束的行
# 注意： 由于.是特殊字符，前面需要加上跳脱符号\
macos@MacOSdeMacBook-Pro test % grep -n '\.$' reg.txt
8:oo.
9:1oo.

```

4. 任意一个字符 **.** 与重复字符 *

+ . (小数点):代表“一定有一个任意字符”的意思;

* (星星号):代表“重复前一个字符， 0 到无穷多次”的意思，为组合形态



#  正则表达式

## sed



```shell
[dmtsai@study ~]$ sed [-nefr] [动作]
选项与参数:
-n :使用安静(silent)模式。在一般 sed 的用法中，所有来自 STDIN 的数据一般都会被列出到屏幕上。
但如果加上 -n 参数后，则只有经过 sed 特殊处理的那一行(或者动作)才会被列出来。
-e :直接在指令列模式上进行 sed 的动作编辑;
-f :直接将 sed 的动作写在一个文件内， -f filename 则可以执行 filename 内的 sed 动作;
-r :sed 的动作支持的是延伸型正则表达式的语法。(默认是基础正则表达式语法)
-i :直接修改读取的文件内容，而不是由屏幕输出。
动作说明: [n1[,n2]]function
n1, n2 :不见得会存在，一般代表“选择进行动作的行数”，举例来说，如果我的动作
是需要在 10 到 20 行之间进行的，则“ 10,20[动作行为] ”
function 有下面这些咚咚:
a :新增， a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)~
c :取代， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行!
d :删除，因为是删除啊，所以 d 后面通常不接任何咚咚;
i :插入， i 的后面可以接字串，而这些字串会在新的一行出现(目前的上一行);
p :打印，亦即将某个选择的数据印出。通常 p 会与参数 sed -n 一起运行~
s :取代，可以直接进行取代的工作哩!通常这个 s 的动作可以搭配正则表达式!
例如 1,20s/old/new/g 就是啦!
```



```shell
# 展示的内容中删除2到10行
macos@MacOSdeMacBook-Pro test % nl reg.txt | sed '2,10d'
     1	this is a file for reg test
    11	the weather is good;
    12	The apple tastes good
    13	tasttest
    
# 如果是从第5行删除到最后一行，则如下：
# 这里的$代表最后一行
macos@MacOSdeMacBook-Pro test % nl reg.txt | sed '5,$d' 
     1	this is a file for reg test
     2	i have some food
     3	i think the weather is good
     4	i want to google 
     
# 删除空白行
sed '/^$/d' file

# 删除最后一行
sed '$d' file

# 在第二行至第五行的每行末尾添加内容
macos@MacOSdeMacBook-Pro test % nl reg.txt | sed '2,5a hello'
     1	this is a file for reg test
     2	i have some food
hello
     3	i think the weather is good
hello
     4	i want to google 
hello
     5	the wheather is not good
hello

# 将第二行至第五行的内容替换
macos@MacOSdeMacBook-Pro test % cat -n reg.txt | sed '2,5c hello'
     1	this is a file for reg test
hello
     6	that man is fool
     7	i am going to school
     8	oo.
   

```

MAC中sed用法和linux不同，如果想使用linux的sed，可以安装一个gsed

```shell
brew install gnu-sed
alias sed=gsed
```

部分数据的搜寻并取代的功能

```SHELL
# 使用方法： sed 's/要被取代的字串/新的字串/g'
macos@MacOSdeMacBook-Pro test % nl reg.txt | grep --color=auto 'the'
     3	i think the weather is good
     5	the wheather is not good
    11	the weather is good;
macos@MacOSdeMacBook-Pro test % nl reg.txt | grep --color=auto 'the' | sed 's/the/123/g'
     3	i think 123 wea123r is good
     5	123 whea123r is not good
    11	123 wea123r is good;
```

直接修改文件内容(危险动作)

```SHELL
# sed 的“ -i ”选项可以直接修改文件内容
macos@MacOSdeMacBook-Pro test % sed -i 's/the/123/g' reg.txt
macos@MacOSdeMacBook-Pro test % cat reg.txt 
this is a file for reg test
i have some food
i think 123 wea123r is good
i want to google 
123 whea123r is not good
```

# 文件权限和目录配置

在我们Linux系统当中，默认的情况下，所有的系统上的帐号与一般身份使用者，还有那个root的相关信息， 都是记录在/etc/passwd这 个文件内的。至于个人的密码则是记录在/etc/shadow这个文件下。 此外，Linux所有的群组名称都纪录在/etc/group内!

MAC下查看所有用户和组

```shell
dscacheutil -q group
```

mac下查看当前用户和组

```shell
groups # 查看当前用户所属组（注意：用户所属组可能有多个）
groups user_name # 查看指定用户所属组
id -a user_name # 查看指定用户所属组的详细信息
whoami # 当前用户的用户名

```

mac下用户切换

```shell
sudo -i # 切换到root超级用户 ---- 需要输入密码
su - macos # - 要切换到的用户名 // 切换到某一个普通用户 注意:横杠两边都有一个空格
```

## 改变文件权限

### 改变文件所属组

改变一个文件的群组真是很简单的，直接以chgrp来改变即可，这个指令就是change group的缩写嘛!这样就很好记了吧! 。不过，请记得，要被改变的群组名称必须要在/etc/group文件内存在才行，否则就会显示错误!

```shell
# 用法：root@study ~]# chgrp [-R] dirname/filename ...

MacOSdeMacBook-Pro:test root# ls -al
-rw-r--r--   1 macos  staff  220 Apr 12 21:59 reg.txt
MacOSdeMacBook-Pro:test root# chgrp wheel reg.txt
-rw-r--r--   1 macos  wheel  220 Apr 12 21:59 reg.txt
```

### 改变文件拥有者

如何改变一个文件的拥有者呢?很简单呀!既然改变群组是change group，那么改变拥有者就是change owner!那就是 chown这个指令的用途，要注意的是， 使用者必须是已经存在系统中的帐号，也就是在/etc/passwd 这个文件中有纪录的使用者名称才能改变。

chown的用途还满多的，他还可以顺便直接修改群组的名称呢!此外，如果要连目录下的所有次目录或文件同时更改文件拥有者的话， 直接加上 -R 的选项即可!

```shell
# 用法：
# [root@study ~] chown [-R] 帐号名称 文件或目录
# [root@study ~] chown [-R] 帐号名称:群组名称 文件或目录
MacOSdeMacBook-Pro:test root# chown root:staff reg.txt 
```

### 改变权限

文件权限的改变使用的是chmod这个指令，但是，权限的设置方法有两种， 分别可以使用数字或者是符号来进行权限的变更。

1. 数字类型改变文件权限

   Linux文件的基本权限就有九个，分别是owner/group/others三种身份各有自己的read/write/execute权限， 先复习一下刚刚上面提到的数据文件的权限字符为:“-rwxrwxrwx”， 这九个权限是三个三个一组的!其中，我们可以使用数字来代表各个权限，各权限的分数对照表 如下:

   **r:4 w:2 x:1**

   每种身份(owner/group/others)各自的三个权限(r/w/x)分数是需要累加的，例如当权限为: [-rwxrwx---] 分数则是:

   owner=rwx=4+2+1=7 

   group=rwx=4+2+1=7 

   others= --- = 0+0+0 = 0

   ```SHELL
   MacOSdeMacBook-Pro:test root# ls -al
   -rw-r--r--   1 root   staff  220 Apr 12 21:59 reg.txt
   MacOSdeMacBook-Pro:test root# chmod 764 reg.txt 
   -rwxrw-r--   1 root   staff  220 Apr 12 21:59 reg.txt
   ```

2. 符号类型改变文件权限

   还有一个改变权限的方法呦!从之前的介绍中我们可以发现，基本上就九个权限分别是(1)user (2)group (3)others三种身份! 那么我们就可以借由**u, g, o**来代表三种身份的权限!此外， **a** 则代表 all 亦即全部的身份!那么读写的权限就可以写成r, w, x!

   ```shell
   # 1. 假如我们要“设置”一个文件的权限成为“-rwxr-xr-x”
   chomod u=rwx,go=rx reg.txt
   -rwxr-xr-x   1 root   staff  220 Apr 12 21:59 reg.txt
   
   # 2. 假如是“ -rwxr-xr-- ”这样的权限呢
   chmod u=rwx,g=rx,o=r file
   
   # 3. 如果我不知道原先的文件属性，而我只想要增加.bashrc这个文件的每个人均可写入的权限
   chmod a+w .bashrc
   
   # 4. 而如果是要将权限去掉而不更动其他已存在的权限呢?例如要拿掉全部人的可执行权限:
   chmod a-x .bashrc
   
   ```



## 目录与文件的权限意义

**权限对文件的重要性：**

文件是实际含有数据的地方，包括一般文本文件、数据库内容档、二进制可可执行文件(binary program)等等。 因此，权限对于文件来说，他的意义是这样的:

1. r (read):可读取此一文件的实际内容，如读取文本文件的文字内容等;
2. w (write):可以编辑、新增或者是修改该文件的内容(但不含删除该文件); 
3. x (eXecute):该文件具有可以被系统执行的权限。

注意：在Linux下面，我们的文件是否能被执行，则是借由是否具有“x”这个权 限来决定的!跟文件名是没有绝对的关系的!

+ 当你对一个文件具有w权限时，你可以具有写入/编辑/新增/修改文件的内容的权限， 但并不具备有删除该 文件本身的权限!对于文件的rwx来说， 主要都是针对“文件的内容”而言，与文件文件名的存在与否没有关系喔!因为文件记录的是实际的数据 嘛!



**权限对目录的重要性：**

1. **r** (**read contents in directory**)

   表示具有读取目录结构清单的权限，所以当你具有读取(r)一个目录的权限时，表示你可以查询该目录下的文件名数据。 所以你就可以 利用 ls 这个指令将该目录的内容列表显示出来!

2. **w** (**modify contents of directory**):

   写入权限对目录的权限如下：

   + 创建新的文件和目录
   + 删除依据存在的文件与目录（不管文件的权限是什么）
   + 将已经存在的文件或目录更名
   + 搬移该目录内的文件，目录位置

3. **x** (**access directory**):

   目录的x代表的是使用者能否进入该目录成为工作目录

```shell
# 例如：
# drwxr--r-- 3 root root 4096 Jun 25 08:35 .ssh
# 系统有个帐号名称为vbird，这个帐号并没有支持root群组，请问vbird对这个目录有何权限?是否可切换到此目录中?
# vbird可以查询此目录下的文件名列表，但因为没有x权限，并不能切换到此目录内
# 如果你在某目录下不具有x的权限， 那么你就无法切换到该目录下，也就无法执行该目录下的任何指令，即使你具有该目录的r或w的权限。
# 要注意:要开放目录给任何人浏览时，应该至少也要给予r及x的权限，但w权限不可随便给!
```

```shell
# 例题:
假设有个帐号名称为dmtsai，他的主文件夹在/home/dmtsai/，dmtsai对此目录具有[rwx]的权限。 若在此目录下有个名为 the_root.data的文件，该文件的权限如下:
-rwx------ 1 root root 4365 Sep 19 23:20 the_root.data
请问dmtsai对此文件的权限为何?可否删除此文件? 
如上所示，由于dmtsai对此文件来说是“others”的身份，因此这个文件他无法读、无法编辑也无法执行， 也就是说，他无法变动 这个文件的内容就是了。
但是由于这个文件在他的主文件夹下， 他在此目录下具有rwx的完整权限，因此对于the_root.data这个“文件名”来说，他是能 够“删除”的! 结论就是，dmtsai这个用户能够删除the_root.data这个文件!
```



# linux账号管理

每个登陆的使用 者至少都会取得两个 ID ，一个是使用者 ID (User ID ，简称 UID)、一个是群组 ID (Group ID ，简称 GID)。

这个文件的构造是这样的:每一行都代表一个帐号，有几行就代表有几个帐号在你的系统中! 不过需要特别留意的是，里头很多帐号本来就是系统正常运行所必须要的，我们可以简称他为系统帐号， 例如 bin, daemon, adm, nobody 等等

注意：mac系统下的用户操作跟常见的Linux系统有很大的不同。

下面是mac系统操作用户和组的方法：

1. 查看所有的组

   ```shell
   dscl
   cd /Local/Default/Groups
   ls
   
   # 或者
   dscl . -list /Groups
   # 如需查看各组ID
   dscl . -list /Groups PrimaryGroupID
   
   dscl . -readall /groups
   
   # 查看指定的组
   dscl . -read /Groups/admin
   ```

2. 查看所有的用户

   ```shell
   dscl
   cd /Local/Default/Users
   ls
   
   # 或者
   dscl . -list /Users
   
   # 如需查看各用户ID
   dscl . -list /Users UniqueID
   
   
   
   ```

3. 查看指定用户macos的所属组id

   ```shell
   # 查看指定用户macos的详细信息
   dscl . -read /Users/macos
   
   # 单独查看指定用户的ID
   dscl . -read /Users/macos PrimaryGroupID
   
   # 查看指定用户的ID与真实名字
   dscl . -read /Users/maacos PrimaryGroupID RealName
   ```

4. 查看指定组`admin`中的用户:

   ```shell
   dscl . -read /Groups/admin
   dscl . -read /Groups/admin GroupMembership
   ```

5. 创建组:

   ```shell
   dscl . create /Groups/test_group
   # 此处未指定gid, 那么通过dscl . -list /Groups PrimaryGroupID命令会查询不到，而应该使用dscl . -list /Groups
   
   # 给创建的组创建ID       PrimaryGroupID
   dscl . create /Groups/test_group gid 296
   
   sudo dscl . -create /groups/test_group
   sudo dscl . -append /groups/test_group gid 4200
   sudo dscl . -append /groups/test_group passwd "nicepwd"
   
   # 以下命令,会自动创建groupid
   sudo dseditgroup -o create test_group
   ```

6. 删除组

   ```shell
   dscl . -delete /Groups/test_group
   ```

7. 创建指定用户test_user

   ```shell
   dscl . -create /Users/test_user
   dscl . -create /Users/test_user UserShell /bin/bash
   dscl . -create /Users/test_user RealName "Lucius Q. User"
   
   // 注意 UniqueID必须唯一
   dscl . -create /Users/test_user UniqueID "1010"
   dscl . -create /Users/test_user PrimaryGroupID 80
   dscl . -create /Users/test_user NFSHomeDirectory /Users/test_user
   
   // 修改密码
   dscl . -passwd /Users/test_user 'goodpwd'
   
   // 加入指定用户组`admin`
   dscl . -append /Groups/admin GroupMembership test_user
   ```

   

