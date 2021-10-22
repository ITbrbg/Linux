# shell

### 解释器

```shell
[root@python ~]# ksh #进入解析器
# exit #退出解析器
[root@python ~]# cat /etc/shells 
/bin/sh
/bin/bash
/sbin/nologin
/usr/bin/sh
/usr/bin/bash
/usr/sbin/nologin
/bin/tcsh
/bin/csh
/bin/ksh
/bin/rksh
```

| 快捷键 |             作用             |
| :----: | :--------------------------: |
| Ctrl+A |         光标移到行首         |
| Ctrl+E |         光标移到行尾         |
| Ctrl+C |           终止操作           |
| Ctrl+D |        一般为结束输入        |
| Ctrl+M |             回车             |
| Ctrl+U |        删除光标至行首        |
| Ctrl+S |        挂起，冻结终端        |
| Ctrl+Q |         解除冻结终端         |
| Ctrl+W |    删除光标前面的一个单词    |
| 方向键 |           历史命令           |
|  Tab   |             补齐             |
| Alt+.  | 使用前一个命令的最后一个单词 |

### 标准的shell脚本

1. 声明解释器
2. 注释脚本功能，变量的含义
3. 脚本执行的代码

```shell
[root@python opt]# cat test1.sh 
#!/bin/bash
#这是一个测试脚本
ls
echo hello world

[root@python opt]# chmod +x test1.sh 
[root@python opt]# ./test1.sh 
\rh  test1.sh
hello world

[root@python opt]# cat test2.sh  #配置yum脚本
#!/bin/bash
echo "[abc]
name=test
baseurl=file:///mnt/a
enabled=1
gpgcheck=0"> /etc/yum.repos.d/abc.repo

[root@python opt]# cat test3.sh  #自动安装ftp脚本
#!/bin/bash
yum -y install vsftpd > /dev/null
systemctl restart vsftpd
systemctl enable vsftpd
```

4. 执行脚本的方式
   1. 添加X权限
      
      - chmod +x test1.sh
   2. 使用bash执行(开启了新的子进程)
      
      - bash test1.sh
   3. 使用source命令（不开启新的子进程）
      
      - source test1.sh
      
        

### 变量

---



1. 自定义变量
   - 定义变量 变量名称=变量的值
     - a=b
   - 取消变量  unset 变量名称
     - unset a
   - 名称可以用英文大小写、下划线、数字，不能使用特殊符号，不能以数字开头

2. 环境变量
   - USER HOSTNAME UID GID HOME SHELL PATH PWD  PS1 PS2
   - env 所有的环境变量
   - set  所有变量

3. 预定义变量

   | 变量名 |              作用              |
   | :----: | :----------------------------: |
   |   $0   |             脚本名             |
   |   $1   | 位置变量（脚本后的第一个变量） |
   |   $#   |           参数的个数           |
   |  $\*   |            所有参数            |
   |   $$   |             进程号             |
   |   $?   |   判断上一条命令是否执行成功   |

```shell
[root@python opt]# bash test4.sh  a b
更改用户 a 的密码 。
passwd：所有的身份验证令牌已经成功更新。

[root@python opt]# cat test4.sh  #创建用户的脚本
#!/bin/bash
useradd $1
echo $2 | passwd --stdin $1
```

#### 变量的扩展

1. 双引号“ ” ，界定字符串范围
2. 单引号 ‘ ’ ，界定字符串范围，可以屏蔽特殊符号
3. 反撇号 ``,可以得到命令的执行结果

```shell
[root@python opt]# bash test4.sh 
请输入用户名: c
请输入密码: 更改用户 c 的密码 。
passwd：所有的身份验证令牌已经成功更新

[root@python opt]# cat test4.sh #创建用户并设置密码脚本
#!/bin/bash
read -p "请输入用户名: " u
useradd $u
stty -echo #屏蔽回显
read -p "请输入密码: " p
stty echo #恢复回显
echo $p | passwd --stdin $u
```

#### 发布全局变量

- export a  发布

- export b=10 创建并发布

  

### shell中的运算

---

1. expr 

```shell
[root@python opt]# expr 1 + 1
2
[root@python opt]# expr 2 - 1
1
[root@python opt]# expr 2 \* 2
4
[root@python opt]# expr 2 / 2
1
[root@python opt]# expr 4 '*' 4
16
[root@python opt]# expr 5 % 2
1
```

2. $[]和$(())

```shell
[root@python opt]# echo $[1+1]
2
[root@python opt]# echo $[1-1]
0
[root@python opt]# echo $[3*2]
6
[root@python opt]# echo $[3/2]
1
[root@python opt]# echo $[3%2]
1
[root@python opt]# a=1
[root@python opt]# echo $[a+1] #支持变量运算
2

[root@python opt]# echo $((1+1))
2
[root@python opt]# echo $((1-1))
0
[root@python opt]# echo $((1*2))
2
[root@python opt]# echo $((1/2))
0
[root@python opt]# echo $((1%2))
1
[root@python opt]# echo $((a%2))
1

```

3. let 运算结果不显示通常针对变量来使用，可以修改变量的值

```shell
[root@python opt]# let 1+1
[root@python opt]# let c=1+1
[root@python opt]# echo $c
2
[root@python opt]# let c=a+1
[root@python opt]# echo $c
2
[root@python opt]# let c++ #变量自增1
[root@python opt]# echo $c
3
[root@python opt]# let c--
[root@python opt]# echo $c
2
[root@python opt]# let c+=2
[root@python opt]# echo $c
4
[root@python opt]# let c-=2
[root@python opt]# echo $c
2

```

4. bc 支持小数运算

```shell
[root@python opt]# bc
bc 1.06.95
Copyright 1991-1994, 1997, 1998, 2000, 2004, 2006 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 
1+1
2
10/3
3
10%3
1
scale=3
10/3
3.333

[root@python opt]# echo "scale=3;10/3" | bc
3.333

```

