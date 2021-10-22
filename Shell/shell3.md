# shell3

####  case 分支

---

```shell
case 变量 in
模式1）
	命令序列1;;
模式2）
	命令序列2;;
...
*)
	默认序列
esac
======================================================
[root@python opt]# vim test8.sh
[root@python opt]# bash test8.sh a
aa
[root@python opt]# cat test8.sh 
#!/bin/bash
case $1 in
a|A)
    echo aa;;
b|B)
    echo bb;;
*)
    echo "a|b"
esac

=================================================
  306  vim test1.sh
  307  bash test1.sh 
  308  ll /usr/local/nginx/sbin/nginx 
  309  systemctl stop firewalld
  310  /usr/local/nginx/sbin/nginx 
  311  history
[root@python opt]# cat test1.sh 
#!/bin/bash
yum -y install gcc pcre-devel openssl-devel
tar -xf nginx-1.10.3.tar.gz
cd nginx-1.10.3
./configure
make && make install

[root@python opt]# netstat -anutpl | grep :80
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      9334/nginx: master  

[root@python opt]# curl 127.0.0.1 | grep title
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   612  100   612    0     0   601k      0 --:--:-- --:--:-- --:--:--  597k
<title>Welcome to nginx!</title>
================================================================================

[root@python opt]# vim test2.sh 
[root@python opt]# bash test2.sh  on
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      10608/nginx: master 
服务已开启
[root@python opt]# cat test2.sh 
#!/bin/bash
case $1 in
on)
    netstat -anutpl | grep nginx 
    [ $? -eq 0 ] && echo -e "\033[32m服务已开启\033[0m" && exit 
    /usr/local/nginx/sbin/nginx;;
off)
    netstat -anutpl | grep nginx   
    [ $? -ne 0 ] && echo -e "\033[31m服务已关闭\033[0m" && exit
    /usr/local/nginx/sbin/nginx -s stop;;
status)
    netstat -anutpl |grep nginx
    [ $? -eq 0 ] && echo "服务开启" || echo "服务没开";;
re)
    /usr/local/nginx/sbin/nginx -s stop
    /usr/local/nginx/sbin/nginx;;
*)
    echo "on | off | status | re"
esac

```

#### 函数

----

- 将公共的语句块存储在一个函数名中，达到精简脚本，增加可读性的目的

```shell
#格式1
function 函数名 {
	命令序列
	...
}
================================
[root@python opt]# vim test3.sh
[root@python opt]# bash test3.sh 
123
abc
[root@python opt]# cat test3.sh 
#!/bin/bash
function a { #定义函数a
    echo 123
    echo abc
}
a			#调用函数a

#格式2
函数名(){
	命令序列
	...
}
================================
[root@python opt]# vim test3.sh
[root@python opt]# bash test3.sh 
123
abc
[root@python opt]# cat test3.sh 
#!/bin/bash
a(){
    echo 123
    echo abc
}
a
==========================================

[root@python opt]# bash test3.sh  31 hello
hello
[root@python opt]# cat test3.sh 
#!/bin/bash
cecho () {
echo -e "\033[$1m$2\033[0m"
}
cecho $1 $2

#bin/bash #死循环系列
a(){ 
	a|a &
}
a
===============================
[root@python opt]# cat test4.sh 
#!/bin/bash
a=0
b=0
myping () {
    ping -c5 -W1 -i0.2 $1 &>/dev/null
    if [ $? -eq 0 ];then
        echo "$1 is up"
    else
        echo "$1 is down"
    fi
}

for i in {1..254}
do 
    myping 192.168.127.$i &>/dev/null &
    if [ $? -eq 0 ];then
        let a++
    else
        let b++
    fi
done
echo "$b up,$a down"
wait #等待放到后台的任务结束完了在退出脚本

```

#### 控制循环

- exit 终止脚本
- break 终止循环，继续执行循环后的任务
- continue 终止当前循环，进行下一次循环

```shell
[root@python opt]# vim test5.sh
[root@python opt]# bash test5.sh 
请输入数字(0是线束)10
请输入数字(0是线束)20
请输入数字(0是线束)30
请输入数字(0是线束)100
请输入数字(0是线束)0
一共是160
[root@python opt]# cat test5.sh 
#!/bin/bash
x=0
while :
do
    read -p "请输入数字(0是线束)" n
    [ $n -eq 0 ] && break
    let x+=n
done
echo "一共是$x"
====================================================
[root@python opt]# vim test6.sh #1到20 6的位数的平方值
[root@python opt]# bash test6.sh 
36
144
324
[root@python opt]# cat test6.sh 
#!/bin/bash
for i in {1..20}
do
    x=$[i%6]
    [ $x -eq 0 ] || continue
    echo $[i*i]
done

```

#### 字符串的处理

---

- ${变量：起始位置：截取长度}  （字符串截取）

```shell
[root@python opt]# a=abcdef
[root@python opt]# echo ${a:1:2} #从第二位开始 取俩位
bc
[root@python opt]# echo ${a::2}
ab
[root@python opt]# echo ${a:0:2}
ab
================================
[root@python opt]# vim test7.sh
[root@python opt]# bash test7.sh
8位密码是: Zbnno9zu
[root@python opt]# cat test7.sh 
#!/bin/bash
a=abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890
for i in {1..8}
do 
    x=$[RANDOM%62]
    p=${a:x:1}
    pa=$pa$p
done
echo "8位密码是: $pa"
```

- ${变量/old/new} (字符串替换)  如果替换成空也有删除的效果  // 所有
- ${变量#删除内容} 左向右（字符串的删除） ##最后一个
-  ${变量%删除内容}右向左（字符串的删除） %%最前面一个

```shell
[root@python opt]# vim test8.sh
[root@python opt]# bash test8.sh  txt doc
[root@python opt]# ll
总用量 924
-rw-r--r--. 1 root root      0 10月 21 22:45 abc1.doc
-rw-r--r--. 1 root root      0 10月 21 22:45 abc2.doc
-rw-r--r--. 1 root root      0 10月 21 22:45 abc3.doc
-rw-r--r--. 1 root root      0 10月 21 22:45 abc4.doc
-rw-r--r--. 1 root root      0 10月 21 22:45 abc5.doc
-rw-r--r--. 1 root root      0 10月 21 22:45 abc6.doc
drwxr-xr-x. 9 a    a       186 10月 21 20:04 nginx-1.10.3
-rw-r--r--. 1 root root 911509 1月  26 2020 nginx-1.10.3.tar.gz
-rw-r--r--. 1 root root    133 10月 21 20:04 test1.sh
-rw-r--r--. 1 root root    542 10月 21 20:46 test2.sh
-rw-r--r--. 1 root root     65 10月 21 21:12 test3.sh
-rw-r--r--. 1 root root    330 10月 21 21:38 test4.sh
-rw-r--r--. 1 root root    134 10月 21 21:48 test5.sh
-rw-r--r--. 1 root root     95 10月 21 21:56 test6.sh
-rw-r--r--. 1 root root    175 10月 21 22:18 test7.sh
-rw-r--r--. 1 root root     89 10月 21 22:45 test8.sh
[root@python opt]# cat test8.sh 
#!/bin/bash
touch abc{1..6}.txt
for i in `ls *.$1`
do
    x=${i%.*}
    mv $i $x.$2
done

```

- ${变量：-初值} 设置变量的初值（备用值）

```shell
[root@python opt]# bash test9.sh 
请输入用户名ipbrbg
请输入密码
更改用户 ipbrbg 的密码 。
passwd：所有的身份验证令牌已经成功更新。
[root@python opt]# cat test9.sh 
#!/bin/bash
read -p "请输入用户名" n
useradd $n
read -p "请输入密码" p
echo ${p:-123456} | passwd --stdin $n

```



