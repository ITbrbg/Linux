# shell2

#### 条件测试

---



1. test 表达式
2. [ 表达式 ]

#### 字符串

```shell
#字符串
[root@python opt]# test a == a #常量
[root@python opt]# echo $?
0
[root@python opt]# [ a == a ] #== 判断条件是否相等
[root@python opt]# echo $?
0
[root@python opt]# a=1
[root@python opt]# test $a == a  #变量
[root@python opt]# echo $?
1

[root@python opt]# echo $a
1
[root@python opt]# [ -z $a ]  #-z测试变量是否为空
[root@python opt]# echo $?
1
[root@python opt]# [ a != $a ] # ！= 判断条件是否不相等
[root@python opt]# echo $?
0

```

#### 逻辑组合

- && 并且 符号前面的任务执行成功才执行后面的任务
- ||  或者 符号前面的执行失败才执行后面的任务
- ; 分号  前边命令执行完了就执行后边的

```shell
[root@python opt]# [ $USER == root ] && exit #如果是管理员就退出
登出
Connection closing...Socket close.

Connection closed by foreign host.

Disconnected from remote host(192.168.127.128) at 20:35:34.

Type `help' to learn how to use Xshell prompt.
[G:\~]$

[root@python ~]# [ $USER == root ] || exit #如果不是管理员就退出
[root@python ~]# 
```

#### 数字

| 符号 | -eq  |  -ne   | -gt  |   -ge    | -lt  |   -le    |
| :--: | :--: | :----: | :--: | :------: | :--: | :------: |
| 意义 | 等于 | 不等于 | 大于 | 大于等于 | 小于 | 小于等于 |

```shell
[root@python ~]# [ 100 -eq 101 ]
[root@python ~]# echo $?
1
[root@python ~]# a=10
[root@python ~]# b=20
[root@python ~]# [ $a -eq $b ] && echo '相等' || echo '不相等'
不相等

```

```shell
[root@python opt]# vim test1.sh
[root@python opt]# crontab -e
no crontab for root - using an empty one
crontab: installing new crontab
[root@python opt]# chmod +x test1.sh 
[root@python opt]# bash test1.sh 
[root@python opt]# mail
Heirloom Mail version 12.5 7/5/10.  Type ? for help.
"/var/spool/mail/root": 4 messages 4 new
>N  1 user@localhost.local  Mon Oct 18 19:44 2189/150478 "[abrt] kernel: NMI watchdog: BUG: s"
 N  2 user@localhost.local  Mon Oct 18 19:44 2184/150238 "[abrt] kernel: NMI watchdog: BUG: s"
 N  3 root                  Wed Oct 20 21:13  18/621   "hello world"
 N  4 root                  Wed Oct 20 21:14  18/621   "hello world"
& 

[root@python opt]# cat test1.sh 
#!/bin/bash
a=`who | wc -l`
[ $a -gt 3 ] && echo "机密文件管理仓库，非请勿进" | mail -s "hello world" root

```

#### 文件

| 类型 |    -e    |        -d        |        -f        |  -r  |  -w  |  -x  |
| :--: | :------: | :--------------: | :--------------: | :--: | :--: | :--: |
| 意义 | 存在就行 | 存在并且要是目录 | 存在并且要是文件 |  读  |  写  | 执行 |

#### if判断

---

- 双分支

  ```shell
  if 条件测试;then
  	执行指令1
  else
  	执行指令2
  fi
  
  [root@python opt]# if [ a == a ] ; then 
  > echo 你好
  > else
  > 好
  > fi
  你好
  ----------------------------------------------------------------------------
       #-c 次数 -i 间隔 -W 1 多久返回结果
  [root@python opt]# ping -c 2 -i 0.2  -W 1 192.168.127.129 
  PING 192.168.127.129 (192.168.127.129) 56(84) bytes of data.
  64 bytes from 192.168.127.129: icmp_seq=1 ttl=64 time=0.514 ms
  64 bytes from 192.168.127.129: icmp_seq=2 ttl=64 time=0.515 ms
  
  --- 192.168.127.129 ping statistics ---
  2 packets transmitted, 2 received, 0% packet loss, time 200ms
  rtt min/avg/max/mdev = 0.514/0.514/0.515/0.022 ms
  
  [root@python opt]# vim test2.sh
  [root@python opt]# bash test2.sh 
  通了
  [root@python opt]# cat test2.sh 
  #!/bin/bash
  ping -c 2 -i 0.2 -W 1 192.168.127.129 &>/dev/null #也可以把Ip改成位置变量
  if [ $? -eq 0 ];then
      echo "通了"
  else
      echo "不通"
  fi
  ```

- 单分支

  ```shell
  if 条件测试;then
  	执行指令1
  fi
  
  [root@python opt]# if [ a == a ] ; then
  > echo 你好
  > fi
  你好
  
  ```

- 多分支

  ```shell
  if 条件测试;then
  	执行指令1
  elif 条件测试;then
  	执行指令2
  	...
  else
  	执行指令x
  fi
  ----------------------------------------------------------------------------
  [root@python opt]# if [ a == a ] ; then
  > echo 123
  > elif [ b == b ] ;then
  > echo 12
  > else
  > echo 1
  > fi
  123
  ----------------------------------------------------------------------------
  [root@python opt]# vim test3.sh
  [root@python opt]# bash test3.sh
  清输入一个数字（0-9）9
  大了
  [root@python opt]# cat test3.sh 
  #!/bin/bash
  x=$[RANDOM%10]
  read -p "清输入一个数字（0-9）" n
  if [ $x -eq $n ];then
      echo "对了"
  elif [ $x -gt $n ];then
      echo "小了"
  else 
      echo "大了"
  fi
  
  ```

  

#### for循环

---

```shell
for 变量 in 变量值 
do
	执行任务
done
--------------------------------------------------------------------------------
[root@python opt]# for i in a b c 
> do
> echo litter
> done
litter
litter
litter
--------------------------------------------------------------------------------
[root@python opt]# vim test4.sh
[root@python opt]# bash test4.sh 
1
2
3
4
5
6
7
8
9
10
[root@python opt]# cat test4.sh 
#!/bin/bash
for i in {1..10}
do
    echo $i
done
--------------------------------------------------------------------------------
[root@python opt]# vim test4.sh
[root@python opt]# bash test4.sh 
1
2
3
4
5
6
7
8
9
10
[root@python opt]# cat test4.sh 
#!/bin/bash
a=10
for i in `seq $a`
do
    echo $i
done
```

#### 综合实例

```shell
[root@python opt]# vim test5.sh
[root@python opt]# bash test5.sh 
192.168.127.120不通
192.168.127.121不通
192.168.127.122不通
192.168.127.123不通
192.168.127.124不通
192.168.127.125不通
192.168.127.126不通
192.168.127.127不通
192.168.127.128通了
192.168.127.129通了
192.168.127.130不通
192.168.127.131不通
192.168.127.132不通
192.168.127.133不通
192.168.127.134不通
192.168.127.135不通
2台通了
14台不通
[root@python opt]# cat test5.sh 
#!#/bin/bash
a=0
b=0
for i in {120..135}
do
    ping -c 2 -i 0.2 -W 1 192.168.127.$i &>/dev/null
    if [ $? -eq 0 ];then
        echo "192.168.127.$i通了"
        let a++
    else
        echo "192.168.127.$i不通"
        let b++
    fi
done
echo "$a台通了"
echo "$b台不通"

```

#### while循环

---

```shell
while 条件测试
do
    执行任务
done
--------------------------------------------------------------------------------
[root@python opt]# vim test6.sh
[root@python opt]# bash test6.sh 
10
9
8
7
6
[root@python opt]# cat test6.sh 
#!/bin/bash
a=10
while [ $a -gt 5 ]
do
    echo $a
    let a--
done
--------------------------------------------------------------------------------
[root@python opt]# vim test7.sh
[root@python opt]# bash test7.sh 
请输入一个数字(0-99)50
猜小了
请输入一个数字(0-99)75
猜小了
请输入一个数字(0-99)85
猜小了
请输入一个数字(0-99)90
猜对了
[root@python opt]# cat test7.sh 
#!/bin/bash
x=$[RANDOM%99]
while :
do
    read -p "请输入一个数字(0-99)" n
    if [ $x -eq $n ];then
        echo "猜对了"
        exit
    elif [ $x -gt $n ];then
        echo "猜小了"
    else 
        echo "猜大了"
    fi
done

```

