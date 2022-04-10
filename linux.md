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

`set`指令查看

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

