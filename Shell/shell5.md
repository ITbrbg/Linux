# shell5

#### AWK 流式编辑器（精确搜索）

- 使用方式
  - awk 选项 （条件）指令   文件
  - 前置指令 | awk 选项   （条件）指令
  - 选项 -F 定义分隔符
  - 指令 print
  - awk内置变量 $0 $1 $2 ..... NR  NF 

```shell
[root@python opt]# ifconfig ens33 | awk '/TX p/{print "ens33的发送流量是"$5}'
ens33的发送流量是190495
[root@python opt]# ifconfig ens33 | awk '/RX p/{print "ens33的接收流量是"$5}'
ens33的接收流量是229649

[root@python opt]# free -h | awk '/^Mem/{print "主机内存剩余空间是"$4}'
主机内存剩余空间是3.1G

[root@python opt]# awk '/Failed/{print $11}' /var/log/secure 
Interrupted
192.168.127.129
192.168.127.129
[root@python opt]# head -1 /var/log/secure
Oct 17 23:46:54 python polkitd[727]: Loading rules from directory /etc/polkit-1/rules.d
[root@python opt]# tail -1 /var/log/secure
Oct 23 14:23:45 python sshd[6678]: PAM 1 more authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=192.168.127.129  user=root


```

- BEGIN{任务} 执行一次
- {} 逐行任务，执行N次
- END {} 执行一次

```shell
[root@python opt]# awk -F: 'BEGIN{print "User\tUID\tHOME"}{print $1"\t"$3"\t"$6}END{print "总计"NR"行"}' user
User	UID	HOME
root	0	/root
bin	1	/bin
daemon	2	/sbin
adm	3	/var/adm
lp	4	/var/spool/lpd
总计5行 
```

- awk条件
  - 使用正则
  - ~ 包含  
  - ！~不包含

```shell
[root@python opt]# awk '/^root|bin/{print}' user
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

[root@python opt]# awk -F: '$1~/root/{print}' user
root:x:0:0:root:/root:/bin/bash

[root@python opt]# awk -F: '$1!~/root/{print}' user
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

```

- 使用数值/字符串比较设置条件

  - 比较符号

  | 符号 | ==   | ！=    | >    | >=       | <    | <=       |
  | ---- | ---- | ------ | ---- | -------- | ---- | -------- |
  | 描述 | 等于 | 不等于 | 大于 | 大于等于 | 小于 | 小于等于 |

```shell
[root@python opt]# sed -n '2p' user
bin:x:1:1:bin:/bin:/sbin/nologin
[root@python opt]# awk 'NR==2{print}' user
bin:x:1:1:bin:/bin:/sbin/nologin
[root@python opt]# awk 'NR<=3{print}' user
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
[root@python opt]# awk 'NR<4{print}' user
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin

[root@python opt]# awk -F: '$1=="root"{print}' user
root:x:0:0:root:/root:/bin/bash

[root@python opt]# awk -F: '$3>=1000{print $1"--->"$6"--->"$7}' /etc/passwd
nfsnobody--->/var/lib/nfs--->/sbin/nologin
brbg--->/home/brbg--->/bin/bash
a--->/home/a--->/bin/bash
b--->/home/b--->/bin/bash
c--->/home/c--->/bin/bash
ipbrbg--->/home/ipbrbg--->/bin/bash

```

- 使用逻辑符号
  - &&
  - ||

```shell
[root@python opt]# awk 'NR>=2&&NR<=4' user
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin

[root@python opt]# awk 'NR>=2&&NR<=4{print}' user
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin

[root@python opt]# awk -F: '$3<10||$3>1000' /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
a:x:1001:1001::/home/a:/bin/bash
b:x:1002:1002::/home/b:/bin/bash
c:x:1003:1003::/home/c:/bin/bash
ipbrbg:x:1004:1004::/home/ipbrbg:/bin/bash
```

- 运算

```shell
[root@python opt]# seq 20 |awk '$1%3==0' 
3
6
9
12
15
18

[root@python opt]# seq 20 | awk '$1~/7/||$1%7==0'
7
14
17
=========================================================
[root@python opt]# vim test2.sh
[root@python opt]# bash test2.sh 
root--->$6$DqCXuz/STpCnEW3u$6R0lLj..fQc1wz3p.3TlnwIPYApROG5dsKiKVzv13aMIS3KzUzbIHbv1f43ROJ.5aSBJW9MNLnFsrRG/f7EFH1
brbg--->$6$DUNYLl06XxGxRHOe$syolD/U9oVMWAD3ZK3pelBCYgwbG4CuvI0yHLpXigZWYkCP6s/h/xT7PThvZKnyXlpbnS5SgapVIGVeUPcpZi/
a--->$6$dKzFQ4XC$IywXORvxwMlNDoergDZ3YRrUqJb8LVxnpUbqNS9D4/W0gZGdoBiY7zSggpPnlgXt8UXvYSTg14k3/0N7nC0iL/
b--->$6$0agMvXA.$5QzSThf7QMKJfzeV6RUB9fe9EIfbk5xj9x6Bg2SvNBt.sGbMNFyLeXLzh72bYuUvhuPqGOkVhJ.TSu4HJwJK6/
c--->$6$z.xcYpzb$zo2Acjf14RvdaKP9Z0jTX8v4o59HbOraeaOwj12v4PHYceGbmRNLJJPBCrZU1dw1Vox697mTC.rXaFhAasLvn/
ipbrbg--->$6$NrYEKd/i$p795h7E3AP/Va7718UVxzXNYSqn5MYBzJRrwQSNaz6frye.hE.2Xcu0lxtgjg79xcCL6o2iTyhVN/8w2bfy8i.
[root@python opt]# cat test2.sh 
#1/bin/bash
user=`awk -F: '/bash$/{print $1}' /etc/passwd`
for i in  $user
do
    grep ^$i: /etc/shadow |awk -F: '{print $1"--->"$2}'
done

```

