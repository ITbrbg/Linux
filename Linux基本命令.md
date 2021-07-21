# Linux常用命令

## 计算机系统（冯诺依曼体系）

- 硬件（hardware）-木桶效应

  - 主机
    - CPU
      - 运算器
      - 控制器
    - 内存
      - ROM
      - RAM
  - 外部设备用的是二进制来
    - 外部存储(K M G T P E Z Y  N D B 单位)
      - DAS（direct attached storage）
      - NAS （Network  attache storage）
      - SAN  (storage area network)
    - 输入设备
    - 输出设备
    - 其它设备

- 软件(software)

  - 系统软件

    - 操作系统（operating system）

      - 硬件驱动
      - 进程管理
      - 内存管理 
      - 网络管理
      - 安全管理
      - 文件管理
      - ABI：（application binary interface）
        - 应用程序和操作系统之间的接口

      - API：（application programming interface）
        - 定义了源代码和库之间的接口

      - POSIX：（portable operating system interface）
        - IEEE在操作系统上定义了一系列的API标准

  - 应用软件 

  - user-->app-->libary-->system call --> kernal-->hardware

```shell
[root@localhost ~]#bc #计算器 
obase=2 #输出2进制
ibase=10 #输入10进制
[root@localhost ~]# ldd /usr/bin/who #调用了哪些库
        linux-vdso.so.1 =>  (0x00007fff4b7ff000)
        libc.so.6 => /lib64/libc.so.6 (0x0000003119a00000)
        /lib64/ld-linux-x86-64.so.2 (0x0000003119200000)

```

- 用户空间和内核空间

  - 用户空间：user space
    - 用户程序的运行空间，隔离的
    - 只能执行简单的命令，不能直接调用系统资源，必须要system call 
  - 内核空间：Kernal space
    - 是linux内核的运行空间
    - 可以执行任意命令，调用系统的一切资源 

  

```shell 
[root@localhost ~]# time sleep 1 #在用户空间和内核空间分别花了多少时间

real    0m1.002s
user    0m0.001s
sys     0m0.000s

```

## 编程语言

- 低级语言
  - 机器语言
  - 汇编语言

- 中级语言
  - C

- 高级语言
  - Java python go php c# objectactive-C perl 

http://www.gnu.org/    #gun项目的地址

```shell 
centos=linux(os kernal) +gnu app
[root@localhost ~]# uname -r #内核的版本号
3.10.0-862.el7.x86_64
[root@localhost ~]# cat /etc/redhat-release #系统版本
CentOS Linux release 7.5.1804 (Core)
[root@localhost ~]# lsb_release #查看版本
LSB Version:	:base-4.0-amd64:base-4.0-noarch:core-4.0-amd64:core-4.0-noarch:graphics-4.0-amd64:graphics-4.0-noarch:printing-4.0-amd64:printing-4.0-noarch

```

## linux的哲学思想

- 一切皆文件
- 小型，单一用途的程序
- 链接程序，共同完成复杂的任务
- 避免令人困惑的用户界面
- 配置数据存储在文件里

## linux目录结构

- /usr
- /home
- /boot
- /tmp
- /var/log
- /etc
- /tmp
- /opt
- /dev

```shell 
[root@localhost ~]# sha1sum /dev/sr0 #检测光盘文件是否完好
32c7695b97f7dcd1f59a77a71f64f2957dddf738  /dev/sr0

```

## VMware

- ctrl+alt+enter 全屏
- ctrl+alt   退出光标

# LINUX基本操作

- ctrl+alt+F6 (linux字符图形切换)
- ctrl +alt +F1

```shell
[root@localhost ~]# cat /proc/meminfo #查看内存信息
MemTotal:         997956 kB
MemFree:          631248 kB
[root@localhost ~]# lscpu #查看cpu信息
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
[root@localhost ~]# top #可以看各种信息
top - 10:51:17 up  1:25,  4 users,  load average: 0.39, 0.33, 0.26
Tasks: 127 total,   3 running, 124 sleeping,   0 stopped,   0 zombie
%Cpu(s):  3.0 us,  6.0 sy,  0.0 ni, 91.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :   997956 total,   629356 free,   155464 used,   213136 buff/cache
KiB Swap:  2097148 total,  2097148 free,        0 used.   641676 avail Mem 

   PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                   
  1616 root      20   0  159120   5992   4264 S  1.3  0.6   0:58.64 sshd    
[root@localhost ~]# free -h #查看内存的大小
              total        used        free      shared  buff/cache   available
Mem:           974M        151M        611M        7.8M        212M        627M
Swap:          2.0G          0B        2.0G

[root@localhost ~]# init 5 #切换运行模式
[root@localhost ~]# runlevel #查看运行模式
3 5
[root@localhost ~]# rpm -qa | wc -l #统计包的个数
1107
[root@centos7 ~]# tty #查看当前在哪上终端
/dev/pts/0
[root@centos7 ~]# id root #看看root用户是不是管理员
uid=0(root) gid=0(root) 组=0(root)
[root@centos7 ~]# id -u root
0
[root@localhost ~]# mii-tool eth0 #查看网卡设备名
eth0: negotiated 100baseTx-FD, link ok
[root@localhost ~]# whoami
root
[root@localhost ~]# who am i
root     pts/1        2021-07-20 13:53 (192.168.220.1)
[root@localhost ~]# who 
root     tty1         2021-07-20 09:24 (:0)
root     pts/0        2021-07-20 09:25 (:0.0)
root     pts/1        2021-07-20 13:53 (192.168.220.1)
root     pts/3        2021-07-20 09:29 (192.168.220.1)
[root@localhost ~]# w
 14:29:27 up  4:49,  4 users,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
root     tty1     :0               09:24    5:05m  5.69s  5.69s /usr/bin/Xorg :0 -nr -verbose
root     pts/0    :0.0             09:25    3:13m  0.01s  0.01s /bin/bash
root     pts/1    192.168.220.1    13:53    0.00s  0.23s  0.08s w
root     pts/3    192.168.220.1    09:29    3:12m  0.07s  0.07s -bash
[root@localhost ~]# cat /etc/shells #shell支持哪几个
/bin/sh
/bin/bash
/sbin/nologin
/bin/dash
/bin/tcsh
/bin/csh
[root@localhost ~]# echo $SHELL #当前用的是哪个shell
/bin/bash

```

- GUI:Graphic User interface
- CLI:command line interface

## 命令提示符 ： prompt

```shell
[root@centos7 ~]# echo $PS1
[\u@\h \W]\$
[root@centos7 ~]# PS1="\[\e[1;5;41;33m\][\u@\h \W]\\$\e[0m\]"
#\e \033  \u当前用户名 \h 主机简称 \H 主机名 \w 当前工作目录 \W当前工作目录基名
# \t 24小时时间格式 \T 12小时时间格式 \! 命令历史 \#开机后命令历史
#41-47 背景颜色 31-37 前景颜色  1 高亮
[root@localhost ~]#nano /etc/profile.d/env.sh #写的内容是上边的PS1值 也可以使用gedit,vi,vim等工具来编写文件
[root@localhost ~]#/etc/profile.d/env.sh
-bash: /etc/profile.d/env.sh: 权限不够

```

## 命令

- 内部命令
  - 由shell自带的，而且通过某种命令提供

- 外部命令
  - 在文件系统路径下有对应的可执行文件
    - 查看路径
      - which -a | --skip-alias ; whereis

```shell
[root@localhost ~]#nano /etc/gdm/custom.conf  #设置自动登陆
[root@localhost ~]#cat /etc/gdm/custom.conf 
# GDM configuration storage

[daemon]
AutomaticLoginEnable=true
AutomaticLogin=root
[security]

[xdmcp]

[greeter]

[chooser]

[debug]

[root@localhost ~]#nano /etc/motd #设置登陆后提示语
[root@localhost ~]#cat /etc/motd
hello
[root@centos7 ~]#which echo #看外部命令
/usr/bin/echo
[root@localhost ~]#help #查看外部命令
[root@localhost ~]#enable #查看内部命令
[root@localhost ~]#type help #判断命令是内部命令还是外部命令
help is a shell builtin
[root@localhost ~]#enable -n pwd #禁用内部命令pwd
[root@localhost ~]#enable | grep pwd
[root@localhost ~]#enable pwd #启用内部命令pwd
[root@localhost ~]#enable | grep pwd
enable pwd
root@localhost ~]#which reboot
/sbin/reboot
[root@localhost ~]#whereis init
init: /sbin/init /etc/init /etc/init.d /usr/share/man/man5/init.5.gz /usr/share/man/man8/init.8.gz
[root@localhost ~]#type -a ls
ls is aliased to `ls --color=auto'
ls is /bin/ls
[root@localhost ~]#hash #刚刚执行过的命令缓存在内存里边去了
hits	command
   3	/bin/nano
   1	/bin/hostname
[root@localhost ~]#whereis hash
hash: /usr/share/man/man1p/hash.1p.gz /usr/share/man/man1/hash.1.gz
[root@localhost ~]#echo $PATH 
/usr/lib64/qt-3.3/bin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
[root@localhost ~]#type whereis
whereis is hashed (/usr/bin/whereis)

[root@localhost ~]#hash -d nano #在缓存里清了nano命令
[root@localhost ~]#hash -r #缓存全部清空
[root@localhost ~]#hash -p /bin/ls lsls #给ls起个别名
[root@localhost ~]#hash -l 
builtin hash -p /bin/ls lsls
[root@localhost ~]#hash -d lsls
[root@localhost ~]#hash -l
hash: hash table empty
root@localhost ~]#hash
hits	command
   1	/bin/ls
[root@localhost ~]#hash -t ls #打印结存中的路径
/bin/ls

```

## 命令的执行过程

- 别名-->内部 -->hash表（记录外部命令的表格)-->$PATH -->命令找不到
- 缓存cache：将刚刚执行过的命令放到内存中。下次使用时不需要从硬盘里去找了。提高了性能。

### 别名alias

```shell
[root@localhost ~]#alias  aliasname="command" #离时的
[root@localhost ~]#nano /root/.bashrc #永久的放要改这个配置文件 、/etc/bashrc 全局的改
[root@localhost ~]#unalias  aliasname="command" #取消别名
[root@localhost ~]#/bin/ls #执行原始命令，不执行别名
anaconda-ks.cfg     install.log		mysql-5.5.32.tar.gz  模板  图片  下载  桌面
cmake-2.8.8.tar.gz  install.log.syslog	公共的		     视频  文档  音乐
[root@localhost ~]#\ls  #执行原始命令，不执行别名
anaconda-ks.cfg     install.log		mysql-5.5.32.tar.gz  模板  图片  下载  桌面
cmake-2.8.8.tar.gz  install.log.syslog	公共的		     视频  文档  音乐
[root@localhost ~]#"ls"  #执行原始命令，不执行别名 
anaconda-ks.cfg     install.log		mysql-5.5.32.tar.gz  模板  图片  下载  桌面
cmake-2.8.8.tar.gz  install.log.syslog	公共的		     视频  文档  音乐
[root@localhost ~]#'ls'  #执行原始命令，不执行别名
anaconda-ks.cfg     install.log		mysql-5.5.32.tar.gz  模板  图片  下载  桌面
cmake-2.8.8.tar.gz  install.log.syslog	公共的		     视频  文档  音乐

```

## 命令格式

- command 【options....】  [arguments....]

  - 选项：用于启用或关闭命令的某个或某些功能
    - 短选项  -c -l -h
    - 长选项 --word

  - 参数：命令的作用对象，比如文件，用户名等

  - 注意

    - 多个选项以及多从此参数和命令之间用空白字符分隔
    - 取消和结束命令执行
      - Ctrl + C
      - Ctrl + d

    - 多个命令可以用 ;符号分开
    - 一个命令可以用\分民多行

## 时间和日期

- linux有两种时钟
  - 系统时钟：由Linux内核通过CPU的工作频率进行的
  - 硬件时钟：主板

- 相关命令

  - date 显示和设置时间
    - date +%s
    - date -d@1509536033

  - hwclock,clock:显示硬件时钟
    - -s，--hctosys以硬件时钟为准，校正系统时钟
    - -w,--systohc以系统时钟为准，校正硬件时钟

- 时区：/etc/localtime
- 显示日历：
  - cal -y

```shell
[root@localhost ~]#date MMDDHHmmYYYY.SS #设置时间格式
[root@localhost ~]#clock -s
[root@localhost ~]#clock -w
[root@centos7 ~]#timedatectl set-timezone Asia/Shanghai #修改时区为亚州
[root@centos7 ~]#timedll /etc/localtime 
lrwxrwxrwx. 1 root root 35 3月  25 07:10 /etc/localtime -> ../usr/share/zoneinfo/Asia/Shanghai
[root@centos7 ~]#cal  2019 #2019年的日历
[root@centos7 ~]#cal 9 1752 #显示1752年9月日历
      九月 1752     
日 一 二 三 四 五 六
       1  2 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29 30
```

## 简单命令

- 关机
  - halt
  - poweroff

- 重启： reboot
  - -f :强制，不调用shutdown
  - -p：切断电源

- 关机或重启：shutdown
  - -r：reboot
  - -h: halt
  - -c: cancel
  - time:无指定，默认相当于+1
    - now：立刻，相当于+0
    - +m:相对时间表示法，几分钟后；例+3
    - hh:mm绝对时间表示法，指明具体时间 

```shell
[root@centos7 ~]#screen -S help #创建新的会话
[screen is terminating]
[root@centos7 ~]#screen -ls #显示当前的会话
There is a screen on:
	91758.help	(Attached)
1 Socket in /var/run/screen/S-root.
[root@centos7 ~]#screen -x help #加入help会话  Ctrl +a,d剥离法前会话
[detached from 91758.help] 


```

## echo命令

- e

  - \a 发出警告
  - \b 退格键
  - \c 最后不加上换行符
  - \n换行且光标移至行首
  - \r 回车，即光标移至行首，但不换行
  - \t 插入tab
  - \\\插入\字符
  - \0nnn插入nnn(八进制)4
    - echo -e '\033[43;32;5mmageddu\033[0m'

  - \xHH插入HH(十六进制)

- E 默认不支持\解释功能
- n不自动换行

```shell
[root@centos7 ~]#hexdump -C a.txt #以十六进制的形式显示
0000000 0a61                                   
0000002
[root@centos7 ~]#ls -l `echo $SHELL`
-rwxr-xr-x. 1 root root 964544 4月  11 2018 /bin/bash
[root@centos7 ~]#ls -l $(echo $SHELL)
-rwxr-xr-x. 1 root root 964544 4月  11 2018 /bin/bash
[root@centos7 ~]#ls -l "echo $SHELL"
ls: 无法访问echo /bin/bash: 没有那个文件或目录
[root@centos7 ~]#ls -l 'echo $SHELL'
ls: 无法访问echo $SHELL: 没有那个文件或目录

[root@centos7 ~]#echo 'ibase=16;obase=2;2' |bc
10
[root@centos7 ~]#iconv -f gb2312 w.txt -o 1.txt #转换怎么编码
[root@centos7 ~]#echo $LANG #默认使用的编码
zh_CN.UTF-8
[root@centos7 ~]#cat /etc/locale.conf
LANG="zh_CN.UTF-8"
[root@centos7 ~]#localectl set-locale LANG=en_US.utf8 #设置编码
[root@centos7 ~]#ls -l /etc/locale.conf 
-rw-r--r--. 1 root root 16 7月  21 10:23 /etc/locale.conf
[root@centos7 ~]#echo $LANG
zh_CN.UTF-8
[root@centos7 ~]#echo file{aa,bb,,cc}
fileaa filebb file filecc
[root@centos7 ~]#echo file{aa,bb,,cc}.{1,2,3}
fileaa.1 fileaa.2 fileaa.3 filebb.1 filebb.2 filebb.3 file.1 file.2 file.3 filecc.1 filecc.2 filecc.3
[root@centos7 ~]#echo file{1..2}
file1 file2
[root@centos7 ~]#echo file{1..11}
file1 file2 file3 file4 file5 file6 file7 file8 file9 file10 file11

```

## 获取帮助

- whatis
- command --help
- man and info
- /usr/share/doc
- 度娘

```shell 
[root@centos7 doc]#mandb #生成whatis命令对应的数据库
Purging old database entries in /usr/share/man...
[root@localhost ~]#makewhatis#生成whatis命令对应的数据库
[root@centos7 doc]#type history
history is a shell builtin
[root@centos7 doc]#help history
[root@centos7 ~]#cat .bash_history 
[root@centos7 ~]#!440
hash
hits	command

```

## 命令行历史

- 重复前一个命令
  - 使用上下键
  - ！！
  - ！-1
  - Ctrl + p

- !:0 执行前一条命令（去除参数）
- Ctrl + n 显示当前历史命令中的下一条，但不执行
- Ctrl + j 执行当前的命令
- !n 执行历史命令中对应序号为n的命令
- ！-n 执行历史中倒数第n个命令
- ！string 重复前一上以string开头的命令
- ！？string 重复前一上包含以string的命令
- ！string:p 仅打印命令历史，而不执行
- !$:p 打印输出!$（上一条命令的最后一上参数）的内容
- !*:p 打印输出\!\*(上一条命令的所有参数)的内容
- ^string删除上一条命令中的第一个string
- ^string1 ^string2将上一条命令中的第一个string1参数替换为string2 
- !gs/string1/string2 将上一条命令中的所有string1参数替换为string2 
- Ctrl + r 来 命令历史中搜索命令
- Ctrl + g 从历史搜索模式中退出
- 重新调用前一个命令的最后一个参数
  - !$
  - Esc,.(按Esc健后松开，然后按.)
  - Alt + . (同时按住)

- history

  - c 清楚

  - d 删除历史中指定的命令

  - a 内存里的放到文件里

  - r  读文件的内容到内存里

  - w 保存历史表到指定的文件里

  - n 读历史文件中未读的行到历史列表

  - p 展开历史参数成多行，但不存在历史列表中

  - s 展开历史叁数成一行，附加在历史列表中

  - 变量

    - HISTSIZE 命令历史记录条数

    - HISTFILE  指定历史文件

    - HISTFILESIZE  命令历史文件记录历史的条数

    - HISTTIMEFORMAT  显示时间格式

    - HISTIGNORE   忽略str1开头的

    - 控制历史记录的方式

      - 环境变量 HISTCONTROL
        - ignoredups 默认 忽略重复命令，连续且相同为重复
        - ignorespace  忽略所有以空白开头的
        - ignoreboth 相当于上俩个的组合
        - erasedups 删除重复命令

      - export 变量名="值"
      - 存放在/etc/profile或~/.bash_profile

- date 外部命令

```shell
[root@centos7 ~]#date -d @423432423412 #转换时间格式
Tue Jan 15 13:36:52 CST 15388

```

- man 章节
  1. 用户命令
  2. 系统调用
  3. C库调用
  4. 设备文件及特殊文件
  5. 配置文件格式
  6. 游戏
  7. 杂项
  8. 管理类的命令
  9. Linux内核AAPI

```shell
[root@localhost ~]#cat /etc/issue #设置提示信息
CentOS release 6.5 (Final)
Kernel \r on an \m
[root@localhost ~]#ntpdate 192.168.220.1 #设置把192.168.220.1同步给本机
21 Jul 13:59:06 ntpdate[24903]: the NTP socket is in use, exiting
[root@localhost ~]#man -w issue #帮助自信文件位置
/usr/share/man/man5/issue.5.gz
[root@centos7 ~]#cat /etc/man_db.conf #man帮助的存放路径
[root@localhost ~]#cat /etc/man.config #man帮助的存放路径

[root@localhost doc]#sosreport #系统日志信息，可以给redhat公司来排错，但是要花钱的。
```

## 快捷健

- Ctrl+I 清屏
- Ctrl+O 执行当前命令，并重新显示本命令
- Ctrl+ s 阻止屏幕输出，锁定
- Ctrl+q 允许屏幕输出
- Ctrl+c 终止命令
- Ctrl+z 挂起命令

- Ctrl + a 光标移动到行首
- Ctrl+e 光标移动到行尾
- Ctrl+ f  光标向右移动一个字符
- Ctrl+b 光标向左移动一个字符
- Alt+b  光标向左移动一个单词首
- Alt+f 光标向右移动一个单词尾
- Ctrl+XX 光标在命令行首和光标之间移动
- Ctrl+u 从光标处删除到命令行首
- Ctrl+k 从光标处删除到命令行尾
- Alt+r 删除当前整行
- Ctrl+w 从光标向左处删除到单词首
- Alt+d  从光标处向右删除到单词尾
- Ctrl+d  删除光标处的一个字符
- Ctrl+ h 删除光标前的一个字符
- Ctrl+ y 将删除的字符粘贴到光标后
- Alt+c 从光标处开始向右更改为首字母大写的单词
- Alt+u 从光标处开始，将右边的一上单词更改为大写
- Alt+l 从光标处开始，将右边的一个单词更改为小写
- Ctrl+t 交换光标处和之前的字符位置
- Alt+t 交换光标处和之前的单词位置
- Alt+N 提示输入指定字符后，重复显示该字符N将从
- 注：Alt 组合快捷键经常和其它软件冲突