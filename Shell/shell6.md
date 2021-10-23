# shell6

#### awk if

---

- 单分支
  - if(条件){指令}

```shell
[root@python opt]# awk -F: '{if($3<10){x++}}END{print x}' user
5

```

- 双分支
  - if(条件){指令1}else{指令2}

```shell
[root@python opt]# awk -F: '{if($3>=1000){x++}else{y++}}END{print x,y}' /etc/passwd
6 40
```

- 多分支
  - if(条件){指令1}else if(条件){指令2}...else{指令N}

#### awk数组

---

- 数组可以理解为能存储多个值的特殊变量
- 使用方法：数组名【下标】：值
  - 注：下标和值可以是数字也可以是其它字符，但是要加上双引号

```shell
[root@python opt]# awk 'BEGIN{a[1]=100;a[2]=200;print a[2]}'
200
[root@python opt]# awk 'BEGIN{a[a]=100;a[b]=200;print a[b]}' #注意
awk: cmd. line:1: fatal: attempt to use scalar `a' as an array
[root@python opt]# awk 'BEGIN{a["a"]=100;a["b"]=200;print a["b"]}'
200

[root@python opt]# awk 'BEGIN{abc[1]=10;abc[1]++;print abc[1]}'
11
```

- awk数组中使用for循环遍历数组
  - for (变量名称 in 数组名称){执行的指令}

```shell
[root@python opt]# awk 'BEGIN{abc[1]=10;abc[2]=20;for (i in abc){print i,abc[i]}}'
1 10
2 20
=======================================================================
[root@python opt]# awk '{a[$1]++}END{for(i in a){print i,a[i]}}' a
opq 2
abc 3
xyz 1
[root@python opt]# cat a 
abc
abc
xyz
opq
abc
opq
======================================================================
[root@python opt]# awk '{ip[$2]++}END{for(i in ip){print i,ip[$2]}}' a
192.168.1.10 2
192.168.1.20 2
192.168.1.30 2
[root@python opt]# cat a
abc  192.168.1.10
abc  192.168.1.10
xyz  192.168.1.20
opq  192.168.1.30
abc  192.168.1.10
opq  192.168.1.30
=====================================
[root@python opt]# awk '{ip[$1]++}END{for (i in ip){print i,ip[i]}}' /var/log/httpd/access_log |sort -n -r  -k 2
#-n 以数字排序  -r降序排序 -K 以哪一例来排序
192.168.127.1 94
192.168.127.131 1
127.0.0.1 1

ab -n 1000 -c 100 http://192.168.127.130/ 
```

- 案例

```shell
[root@python opt]# cat test3.sh 
#!/bin/bash
while :
do
	uptime | awk '{print "CPU的平均负载："$8,$9,$10}'
	ifconfig ens33 | awk 'NR==7{print "网卡的接收流量是："$5 }'
	ifconfig ens33 | awk 'NR==8{print "网卡的发送流量是："$5 }'
	free -h | awk '/Mem/{print "主机的内存剩余容量是："$4}'
	df -h | awk '/mapper/{print "主机的磁盘剩余容量是："$4}'
	awk 'END{print "计算机的用户数量 " NR}' /etc/passwd
	uptime | awk '{print "计算机当前登陆数量是："$4}'
	ps -aux | wc -l | awk '{print "主机运行的进程数是："$1}'
	rpm -qa |wc -l | awk '{print "本机已经安的包是：" $1}'
	sleep 5
	clear
done
==========================================================
192.168.127.131访问本机输入密码失败>6次

& Held 7 messages in /var/spool/mail/root
[root@python opt]# cat test4.sh 
#!/bin/bash
x=`awk '/Failed/{ip[$11]++}END{for (i in ip){print ip[i]","i}}' /var/log/secure`
for l in $x
do
	h=${l%,*}
	p=${l#*,}
	[ $h -gt 3 ] && echo "$p访问本机输入密码失败>$h次"|mail -s test root
done

```

