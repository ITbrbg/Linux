# Linux文件管理

## 文件系统

```shell 
[root@centos7 ~]#ll /dev/zero 
crw-rw-rw-. 1 root root 1, 5 Jul 21 09:04 /dev/zero #c=character 字符
[root@centos7 ~]#ll /dev/null
crw-rw-rw-. 1 root root 1, 3 Jul 21 09:04 /dev/null
[root@centos7 ~]#ll /dev/sda
brw-rw----. 1 root disk 8, 0 Jul 21 09:04 /dev/sda #b=block 块设备
[root@centos7 ~]#cat /etc/DIR_COLORS #这个文件可以定义目录文件的颜色
# Configuration file for the color ls utility
[root@centos7 ~]#touch -- -a #创建一上-开头的文件，删除也可以加--删除 
[root@centos7 ~]#touch ./-b #这个方式也可以
[root@centos7 ~]#pwd #print working directory
/root

```

- 文件有俩类型的数据
  - data
  - meta

- 文件的类型
  - \-   普通文件
  - d  目录文件
  - b  块设备
  - c   字符设备
  - l    符号链接文件
  - p   管道文件pipe
  - s    套接字文件socket

- 路径
  - 相对路径
  - 绝对路径

```shell
[root@centos7 ~]#basename /etc/sysconfig/network-scripts/ #基名
network-scripts
[root@centos7 ~]#dirname /etc/sysconfig/network-scripts/ #目录名
/etc/sysconfig
[root@centos7 ~]#cd ~root #进入root用户的家目录下  chage directory
[root@centos7 bin]#cd -  #注意下面这个变量
/root
[root@centos7 ~]#echo $OLDPWD  
/usr/bin

```

- ls 

|  a   |  l   |  R   |    ld    |  1   |   S    |   t   |   u   |    U     |  X   |
| :--: | :--: | :--: | :------: | :--: | :----: | :---: | :---: | :------: | :--: |
| 隐藏 | 额外 | 递归 | 目录链接 | 分行 | 大到小 | mtime | atime | 目录顺序 | 后缀 |

- 文件time
  - mtime modify  time
  - atime access    time 
  - ctime  change  time

```shell
[root@centos7 data]#ll --time=atime a
-rw-r--r--. 1 root root 0 Jul 21 15:45 a
[root@centos7 data]#stat a #可以看到文件的一个时间 
  File: ‘a’
  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file
Device: fd00h/64768d	Inode: 943804      Links: 1
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Context: unconfined_u:object_r:admin_home_t:s0
Access: 2021-07-21 15:45:07.449143111 +0800
Modify: 2021-07-21 15:45:07.449143111 +0800
Change: 2021-07-21 15:45:07.449143111 +0800
 Birth: -

```

## 通配符

- \* 匹配0个或多个
- ？匹配任意单个字符
- ~ 当前用户的家目录
- ~mage 用户mage的家目录
- ~+当前工作目录
- ~- 前一个工作目录
- [0-9] 匹配数字范围
- [A-Z]字母
- [a-z]字母
- [wang] 匹配列表中的任意单个字符
- [^匹配列表中的所有字符以外的字符]
- [:digit:] 任意数字 相当于0-9
- [:lower:] 任意小写字母
- [:upper:] 任意大写字母
- [:alpha:] 任意大小写字母
- [:alnum:] 任意数字或字母
- [:blank:] 水平空白字符
- [:space:] 水平或垂直空白字符
- [:punct:] 标点符号
- [:print:] 可打印符
- [:cntrl:] 控制非打印字符
- [:graph:] 图形字符
- [:xdigit:] 十六进制

```shell
[root@centos7 data]#ls [[:alpha:]]
a  b

```

