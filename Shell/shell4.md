# shell4

#### 正则表达式

- 配合某些工具，实现对文本的过滤、匹配、查找

| 普通正则  | 描述                           |
| :-------: | :----------------------------- |
|     ^     | 匹配行首                       |
|     $     | 匹配行尾                       |
|    [^]    | 对集合取反                     |
|     .     | 匹配任务单个字符               |
|    \*     | 匹配前一个字符的任意次数       |
| \\{n,m\\} | 匹配前一个字符n到m次           |
|  \\{n\\}  | 匹配前一个字符n次              |
| \\{n,\\}  | 匹配前一个字符n次及以上        |
|  \\(\\)   | 保留                           |
|    []     | 集合，匹配集合中的任意单个字符 |

| 扩展正则 | 描述             |
| :------: | ---------------- |
|    +     | 最少匹配一次     |
|    ？    | 最多匹配一次     |
|  {n,m}   | 匹配n到m次       |
|    ()    | 组合为整体，保留 |
|    \|    | 或者             |
|    \b    | 单词边界         |

- 扩展正则要使用 grep  -E或者 egrep

#### sed 流式编辑器

---

- 能够实现对文本交互式的增、删、改、查，逐行处理
- 使用方法
  - 前置命令 | sed 选项 （定址符）指令
  - sed  选项 （定址符）指令 文档

| 选项 |     功能     |
| :--: | :----------: |
|  -n  | 屏蔽默认输出 |
|  -r  | 支持扩展正则 |
|  -i  |   写入文件   |

| 指令 |         功能         |
| :--: | :------------------: |
|  p   |     输出文档内容     |
|  d   |         删除         |
|  s   |         替换         |
|  i   | 在指定行之前插入文本 |
|  a   | 在指定行之后插入文本 |
|  c   |     替换指定的行     |

- =号 查看行号
- $=  查看最后一行
- $p 输出最后一行

```shell
[root@python opt]# sed -n '=' user
1
2
3
4
5
[root@python opt]# sed -n '$=' user
5
[root@python opt]# sed -n '$p' user
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```

- 第一行到第九行  用  ‘1，9p
- 第一行和第九行’ '1p;9p'
- 每隔俩行 '1~2p'
- 第1行和后面俩行  '1,+2p'

```shell
[root@python opt]# sed 's/2017/xxx/' test.txt 
xxx 2011 2018
xxx 2017 2024
xxx 2017 2017
[root@python opt]# sed 's/2017/xxx/2' test.txt 
2017 2011 2018
2017 xxx 2024
2017 xxx 2017
[root@python opt]# sed 's/2017/xxx/3' test.txt 
2017 2011 2018
2017 2017 2024
2017 2017 xxx
[root@python opt]# sed '1s/2017/xxx/3' test.txt 
2017 2011 2018
2017 2017 2024
2017 2017 2017
[root@python opt]# sed '3s/2017/xxx/3' test.txt 
2017 2011 2018
2017 2017 2024
2017 2017 xxx
[root@python opt]# sed '2s/2017/xxx/2' test.txt 
2017 2011 2018
2017 xxx 2024
2017 2017 2017
[root@python opt]# sed '2s/2017/xxx/g' test.txt 
2017 2011 2018
xxx xxx 2024
2017 2017 2017
[root@python opt]# sed 's/2017/xxx/g' test.txt 
xxx 2011 2018
xxx xxx 2024
xxx xxx xxx
=======================================================================
[root@python opt]# sed '3s/2017/xxx/2;3s/2017/xxx/2' test.txt   #注意
2017 2011 2018
2017 2017 2024
2017 xxx xxx
=======================================================
[root@python opt]# sed 's/\/bin\/bash/\/bin\/sh/' user
root:x:0:0:root:/root:/bin/sh
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

[root@python opt]# sed 's#/bin/bash#/bin/sh#' user
root:x:0:0:root:/root:/bin/sh
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
============================================
[root@python opt]# cat nssw.txt 
Hello the world
ni hao ma beijing
[root@python opt]# sed 's/.//2;s/.$//' nssw.txt 
Hllo the worl
n hao ma beijin

[root@python opt]# sed -r 's/^(.)(.*)(.)$/\3\2\1/' nssw.txt  #注意
dello the worlH
gi hao ma beijinn+
===================================================================
[root@python opt]# sed 's/[0-9]//g' nssw.txt 
Hello the woRld
ni Hao ma beijIng
[root@python opt]# sed -r 's/([A-Z])/{\1}/g' nssw.txt 
{H}e6llo the w8o{R}ld
ni {H}a7o ma be22ij{I}ng
[root@python opt]# cat nssw.txt 
He6llo the w8oRld
ni Ha7o ma be22ijIng

==================================
[root@python opt]# cat test2.sh #实战
#!/bin/bash
yum -y install vsftpd &>/dev/null
sed -r 's/^#anon_up/anon_up/' /etc/vsftpd/vsftpd.conf
systemctl restart vsftpd
systemctl enable vsftpd
chmod 777 /var/ftp/pub
systemctl stop firewalld
setencforce 0

```

