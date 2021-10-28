# python基础语法四

### shutil模块

```python
>>> import shutil
>>> f1 = open('/bin/touch','rb')
>>> f2 = open('/tmp/tch','wb')
>>> shutil.copyfileobj(f1,f2)
>>> f1.close()
>>> f2.close()

>>> shutil.copy('/etc/hosts','/tmp')  #cp /etc/hosts /tmp/
'/tmp/hosts'
>>> shutil.copy2('/etc/hosts','/tmp/zhuji')  #cp -p /etc/hosts /tmp/zhuji
'/tmp/zhuji'
# cp -r /etc/security 	/mnt/anquan
>>> shutil.copytree('/etc/security','/tmp/anquan') 
'/tmp/anquan'
>>> shutil.move('/tmp/anquan','/var/tmp')  #mv /tmp/anquan  /var/tmp
'/var/tmp/anquan'
>>> shutil.chown('/tmp/tch',user='ydg',group='ydg')  #chown ydg.ydg /tmp/tch
>>> shutil.rmtree('/var/tmp/anquan')  #rm -rf /var/tmp/anquan

>>> help(shutil.chown)  #查看shutil.chown的帮助


```

### subprocess模块

- 用于执行系统命令

```python
>>> subprocess.run('ls /tmp',shell=True) #shell = Ture 是表示在shell环境下去运行
>>> result = subprocess.run('ls /tmp',shell=True)#将运行结果保存在变量中
>>> result
CompletedProcess(args='ls /tmp', returncode=0)
>>> result.args
'ls /tmp'
>>> result.returncode #即$？
0
>>> result = subprocess.run('id root;id zhangsan',shell=True)
uid=0(root) gid=0(root) 组=0(root)
id: zhangsan: no such user
#将标准输出保存到stdout，错误保存到stderr        
>>> result = subprocess.run('id root;id zhangsan',shell=True,stdout=subprocess.PIPE,stderr=subprocess.PIPE)
>>> result
CompletedProcess(args='id root;id zhangsan', returncode=1, stdout=b'uid=0(root) gid=0(root) \xe7\xbb\x84=0(root)\n', stderr=b'id: zhangsan: no such user\n')
>>> 
>>> result.stderr
b'id: zhangsan: no such user\n'
>>> result.stdout
b'uid=0(root) gid=0(root) \xe7\xbb\x84=0(root)\n'
>>> result.stdout.decode() #将bytes转换成str类型
'uid=0(root) gid=0(root) 组=0(root)\n'

```

### 语法结构

- 链式多重赋值
  - 注意，因为列表是可变的，所以链式多重赋值，俩个列表使用同一内存空间
  - 链式多重赋值，对数字字符串不会有像列表一样的影响

```python
>>> a = b = 10
>>> a
10
>>> b
10
>>> b = 20
>>> a
10
>>> b
20

>>> alist = blist = [1,2]
>>> alist
[1, 2]
>>> blist
[1, 2]
>>> blist[0] = 10
>>> blist
[10, 2]
>>> alist
[10, 2]


```

- 多元赋值
  - 交换俩上变量的值

```python
>>> a,b = 10,20
>>> c,d = (100,200)
>>> e,f = 'xy'
>>> g,h = ['tom','jerry']
>>> a
10
>>> b
20
>>> c
100
>>> d
200
>>> e
'x'
>>> f
'y'
>>> g
'tom'
>>> h
'jerry'

>>> a,b = 100,200
>>> t = a
>>> a = b
>>> b = t
>>> a
200
>>> b
100


>>> a,b = 100,200
>>> a,b = b,a
>>> a
200
>>> b
100

```

### 标识符

- 标识符就是各种各样的名字：变量、函数、模块

### 关键字

- python也拥有一些被称作关键字的保留字符
- 关键字不能挪作他用

```python
>>> keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
>>> keyword.iskeyword('pass')
True

```

### 内建

- 虽然built-in不是关键字，但是应该把它当作“系统保留字”

```python
>>> len('abc')
3
>>>len = 10
>>>len('abc') #报错，len是数字10，不在了函数
```

### 模块的结构和布局

```python
#! /usr/local/bin/python3
"""文档字符串

用于模块文件的帮助信息
"""

#模块导入
import os
import time
from string import ascii_letters,digits

#全局变量定义
all_chs = ascii_letters + digits
debug = True

#类定义
class MyClass:
    pass

#函数定义
def pstar(n=30):
    print('*' * n)
    
#程序主体
if __name__ == __main__:
    print('hi')
    pstar(n=50)

```

### 编程思路

1. 思考程度的运行方式，交互？非交互？

```python
#python mkfile.py
文件名： /etc
文件已存在，请重试
文件名： /etc/hosts
文件已存在，请重试
文件名： /tmp/abc.txt
请输入内容，在单独的一行输入end结束。
（end to quit）: Hello World
（end to quit）: 2end line
（end to quit）: the end
（end to quit）: end
 #ls /tmp/abc.txt
abc.txt
#cat /tmp/abc.txt
Hello World
2end line
the end
```

2. 思考程度有哪些功能，将功能写为功能函数

```python
def get_fname():
    #用于获取并返回文件名
    
def get_content():
    #用于获取并返回文件内容
    
def wfile(fname,content):
    #用于将文件内容写入到文件
    
```

3. 编写主程序，按逻辑调用相关的函数

```python 
def get_fname():
    #用于获取并返回文件名
    
def get_content():
    #用于获取并返回文件内容
    
def wfile(fname,content):
    #用于将文件内容写入到文件
    
if __name__ == '__main__':
    fname = get_fname()
    content = get_content()
    wfile(fname,content)
```

4. 完成每一个函数

```python
import os


def get_fname():
    #用于获取并返回文件名
    while 1:
        fname = input('文件名：')
        if not os.path.exists(fname):
            break
        print('文件已存在，请重试')
    return fname

def get_content():
    #用于获取并返回文件内容
    content = []
    print('请输入内容，在单独的一行输入end结束')
    while 1:
        line = input('end to quit>')
        if line == 'end':
            break
        content.append(line + '\n')

    return content

def wfile(fname,content):
    #用于将文件内容写入到文件
    with open(fname,'w') as  fobj:
        fobj.writelines(content)

if __name__ == '__main__':
    fname = get_fname()
    content = get_content()
    wfile(fname,content)
```

```python
import os


def get_fname():
    #用于获取并返回文件名
    while 1:
        fname = input('文件名：')
        if not os.path.exists(fname):
            break
        print('文件已存在，请重试')
    return fname

def get_content():
    #用于获取并返回文件内容
    content = []
    print('请输入内容，在单独的一行输入end结束')
    while 1:
        line = input('end to quit>')
        if line == 'end':
            break
        content.append(line)

    return content

def wfile(fname,content):
    #用于将文件内容写入到文件
    with open(fname,'w') as  fobj:
        fobj.writelines(content)

if __name__ == '__main__':
    fname = get_fname()
    content = get_content()
    content = ['%s\n'% line for line in content]
    wfile(fname,content)
```

### 作用于序列对象的函数

```python
#reversed()用于翻转序列对象
>>> reversed(nums)
<list_reverseiterator object at 0x7f3e75ca8400>
>>> nums
[2, 10, 8, 6]
>>> list(reversed(nums))
[6, 8, 10, 2]

>>> for i in reversed(nums):
...     print(i)
... 
6
8
10
2
#sorted()用于排序
>>> sorted(nums)
[2, 6, 8, 10]

#enumerate()可以同时得到下标和值
>>> users = ['tom','jerry','bob','alice']
>>> list(enumerate(users))
[(0, 'tom'), (1, 'jerry'), (2, 'bob'), (3, 'alice')]

>>> users = ['tom','jerry','bob','alice']
>>> list(enumerate(users))
[(0, 'tom'), (1, 'jerry'), (2, 'bob'), (3, 'alice')]
>>> for data in enumerate(users):
...     print(data)
... 
(0, 'tom')
(1, 'jerry')
(2, 'bob')
(3, 'alice')

>>> for i,name in enumerate(users):
...     print(i,name)
... 
0 tom
1 jerry
2 bob
3 alice

```

### 字符串

- 属于标量，不可变，顺序类型
- 字符串格式化

```python
#基本形式
'' % ()
>>> '%s is %s years old'% ('tom',20)
'tom is 20 years old'
#如果字符串只有一个占位符，那后面的（）可以省略
>>>'Hi %s' % 'tom'
'Hi tom'

#%d是整数
>>> '%s is %d years old'% ('tom',20.5)
'tom is 20 years old'

#%f为浮点数
>>> '%f' % (5/3)
'1.666667'
>>> '%.2f' % (5/3)#小数位为俩位
'1.67'
>>> '%6.2f' % (5/3)#总宽度为6，小数位为俩位，不够宽度左侧补空格
'  1.67'

>>> '%8s%8s' %('name','age')
'    name     age'
>>> '%-8s%-8s' %('name','age')
'name    age 

#不常用了解
>>> '%e' % 123000#科学计算法
'1.230000e+05'
>>> '%#o' % 10 #转换成8进制
'0o12'
>>> '%#x' % 10#转换成16进制
'0xa'

#字符串格式化，还可以用字符串的format方法
>>> '{} is {} yares old'.format('ba',20)
'ba is 20 yares old'
>>> '{0[0]} is {0[1]} yars old' .format([20,'bob'])
'20 is bob yars old'
#将[20,'bob']作为一上整体，下标为0的是20，下标为1的是bob
>>> '{0[1]} is {0[0]} yars old' .format([20,'bob'])
'bob is 20 yars old'

```



```python
import sys
import subprocess
from randpass2 import randpass

def add_user(user,passwd,fname):
    result = subprocess.run('id %s &> /dev/unll' % user,shell=True)
    if result.returncode == 0:
        print('用户已存在')
        #return类似于循环的break，函数遇到return就结束了
        return

    subprocess.run('useradd %s' % user,shell=True)
    subprocess.run(
        'echo %s | passwd --stdin %s'% (passwd,user),shell=True
    )

    info = """username: %s
    password: %s
    """%(user,passwd)
    with open(fname,'a') as fobj:
        fobj.write(info)


if __name__ == '__main__':
    user = sys.argv[1]
    fname = sys.argv[2]
    passwd = randpass()
    add_user(user,passwd,fname)
```

### 原始字符串、真实字符串

```python
>>> win_path = 'c:\temp'
>>> print(win_path)
c:      emp
>>> wpath = r'c:\temp' #表示字符串中的所有字符都是其字面本身的意思
>>> print(wpath)
c:\temp
>>> win_path = 'c:\\temp'
>>> print(win_path)
c:\temp

```

### 字符串的方法

```python
>>> s1 = '\tHello World'
>>> s1.strip()
'Hello World'
>>> s1.lstrip()
'Hello World'
>>> s1.rstrip()
'\tHello World'

>>> s2 = 'hao123'
>>> s2.center(30)
'            hao123            '
>>> s2.center(30,'*')
'************hao123************'
>>> s2.ljust(30)
'hao123                        '
>>> s2.rjust(30)
'                        hao123'

>>> s2 = 'hao123'
>>> s2.center(30)
'            hao123            '
>>> s2.center(30,'*')
'************hao123************'
>>> s2.ljust(30)
'hao123                        '
>>> s2.rjust(30)
'                        hao123'
>>> s2.startswith('h')
True
>>> s2.startswith('ha')
True
>>> s2.endswith(3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: endswith first arg must be str or a tuple of str, not int
>>> s2.endswith('3')
True
>>> '1234'.isdigit()
True
>>> s2.isdigit()
False

False
>>> s2.upper()
'HAO123'
>>> 'Hao'.upper()
'HAO'

```

