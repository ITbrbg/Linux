# python

### python的语法结构

- ### 变量

  - 会变化的量
  - 字面量literal，是不会变化的量
  - 变量的命名
    - 首字母只能是字母或下划线
    - 其他字符可以是字母，数字和下划线
    - 区分大小写
  - 推荐的命名方法
    - 变量名全部采用小写字母 pythonstring
    - 简短，有意义 pystr
    - 多个单词之间用下划线分隔 py_str
    - 变量名用名词，函数名用谓词（动词+名词） phone/update_phone
    - 类名采用陀峰形式 MyClass
  - 变量赋值是自右向左完成的
    - 将=号右边的表达式计算结果 赋值给左边的变量
    - 变量使用之前，必须先赋值进行初始化



```python
>>> a = 10
>>> b = 10  + 5
>>> a =c + 5 # C未定义。报错
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'c' is not defined
>>> 
>>> a = a + 5
>>> a
15
>>> a += 5#以上写法的简化方式
>>> a
20
>>> a++ #没有a++ 和++a的写法
  File "<stdin>", line 1
    a++
      ^
SyntaxError: invalid syntax
>>> ++a
20
>>> a
20
>>> 
>>> import this
The Zen of Python, by Tim Peters

Beautiful is better than ugly.   #美胜丑
Explicit is better than implicit.#明胜暗
Simple is better than complex.   #简胜繁


```

### 运算符

- 算术运算行
  - _ + / // % **

```python
>>> 5 / 3
1.6666666666666667
>>> 5 // 3 #只保留商
1
>>> 5 % 3
2
>>> divmod(5,3) #同时得到商和余数
(1, 2)
>>> a,b = divmod(5,3) #将商和余数分别赋值给a和b
>>> a
1
>>> b
2
>>> 22 ** 3 #乖方，幂运算
10648
>>> 3 ** 4
81

```

- 比较运算行，返回True或False  < <= > >= == !=

```python
>>> 10 < 20 < 30 #python 支持连续比较
True
>>> 10 < 20 > 15 #10 < 20 and 20 > 15 可读性不好，不介意使用
True

```

- 逻辑运算符 and not or

```python
>>> 10 > 5 or 5 > 8 #or两侧全为False,最终才为False,否则为False
True
>>> 10 > 50 or 5 > 8
False
>>> 10 > 5 and 5 > 3 #and 两侧全为True,最终结果True，否则为False
True
>>> 10 > 5 and 5 < 3
False
>>> 5 > 3 
True
>>> not 5 > 30 	#not取反，将False变True，将True变为False
True

```

### 数据类型

- 数字
  - 没有小数的整数
  - 有小数的浮点数

```python
>>> True + 5	#True的值为1，False的址为0
6
>>> False + 5
5
#python 中没有任何前缀的数是十进制数
>>> 11
11
#以0o开头的是八进制
>>> 0O11
9
#以0x开头的是十六进制
>>> 0x11
17
#以0b开头的是二进制
>>> 0b11
3
>>> divmod(10000,60)
(166, 40)
>>> divmod(100,8)
(12, 4)
>>> divmod(166,60)
(2, 46)
>>> divmod(100,16)
(6, 4)
>>> divmod(12,8)
(1, 4)
>>> hex(100)#转成16进制
'0x64'
>>> oct(100)#转成8进制
'0o144'
>>> bin(100)#转成2进制
'0b1100100'

```

- 字符串
  - 字符串被定义为引号之间的字符集合
  - 支持使用成对的单引号或双引号
  - 无论是单引还是双引，表示的意义相同
  - python还支持三引号

```python
>>> words ="""hello
... welcome
... hao"""
>>> print(words)
hello
welcome
hao
>>> wds = "abc\nhello\nni\nhao"
>>> print(wds)
abc
hello
ni
hao

>>> s1 = 'python'
>>> len(s1)
6
>>> s1[0]
'p'
>>> s1[2:4]	#取切片，起始下标包含，结束下标不包含
'th'
>>> s1[2:]	#结束下标不写，表示争到结尾
'thon'
>>> s1[2:6]	#切片时，下标越界不报错
'thon'
>>> s1[:2]  #起始下标不写，表示从头开始起
'py'
>>> s1
'python'
>>> s1[:] #从开头取到结尾
'python'
>>> s1[::2]#第2上冒号后面的数字是步长值
'pto'
>>> s1[::-1]#步长为负是自右向左取
'nohtyp'
>>> 't' in s1#成员关系判断，t在字符串中吗
True
>>> 'th' in s1
True
>>> 'to' in s1
False
>>> 'to' not in s1
True
>>> s1 + ' is cool'
'python is cool'
>>> '*' * 30#*号重复30遍
'******************************'

```

- 列表
  - 

```python
>>> len(alist)
5
>>> alist[0]
10
>>> alist
[10, 20, 'tom', 'jerry', [1, 2]]
>>> alist[2:4]
['tom', 'jerry']
>>> alist[-1]
[1, 2]
>>> 'o' in alist
False
>>> alist + 200
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate list (not "int") to list
>>> alist + [200]	#列表拼接，返回新列表，原始列表不变
[10, 20, 'tom', 'jerry', [1, 2], 200]
>>> alist * 3 #列表重复3次，返回新列表，原始列表不变
[10, 20, 'tom', 'jerry', [1, 2], 10, 20, 'tom', 'jerry', [1, 2], 10, 20, 'tom', 'jerry', [1, 2]]

```

- 元组
  - 无组相当于不可变的列表

```python
>>> atuple = (10,20,'tom','jerry')
>>> atuple[0]
10
>>> atuple[:2]
(10, 20)
>>> 'tom' in atuple
True
>>> atuple[0] = 100
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment

```

- 字典
  - 它是映射类型

```python
>>> adict = {'name': 'tom','age': 20}
>>> 'tom' in adict #tom是字典的key吗？
False
>>> 'name' in adict
True
>>> adict['name'] #通过key，找到对应的value
'tom'

```

```python
if 3 > 0:
    print('yes')
    print('ok')
    
if 'to' in 'python':
    print('True')
else:
    print('False')

if -0.0:
    print('任何值为0的数字都是False')

if 0.001:
    print('任何值为非0 的数字都是Ture')

if ' ':
    print('空格也是一个字符，非空字符串为Ture')

if []:
    print('任何空对象都是False')

if not None:
    print('None为False，取反为Ture')

if not 0:
    print('数字0为False，取反为Ture')
    
   
a,b = 10,20
if a<=b:
    smaller = a
else:
    smaller = b
print(smaller)

a,b = 10,20
smaller = a if a <=b else b
print(smaller)
```

- login.py

```python
import getpass #导入getpass模块

uname = input('username: ')
upass = getpass.getpass('password: ')#调用getpass模块的getpass功能

if uname == 'bob' and upass== '123456':
    print('登陆成功')
else:
    print('登陆失败')
```

- grade.py

```python
score = int(input('分数： ')

if score >= 90:
    print('优秀')
elif score >= 80:
    print('好')
elif score >= 70:
    print('良')
elif score >=60:
    print('及格')
else:
    print('你得努力了！！！')
```

```python
score = int(input('分数： '))

if score >=60 and score < 70:
    print('及格')
elif 70 <=score < 80:
    print(良)
elif 80<= score <90:
    print('好')
elif score >= 90:
    print('优秀')
else:
    print('你要努力了！！！')
```

### random模块

- game.py

```python
import random

choices = ['石头','剪刀','布']
computer = random.choice(choices)
player = input('请出拳（石头/剪刀/布): ')

print("you choice:%s,computer's choice: %s" % (player,computer))
if player == '石头':
    if computer == '石头':
        print('\033[32;1m平局\033[0m')
    elif computer == '剪刀':
        print('\033[31;1myou win\033[0m')
    else:
        print('\033[31;1myou lose!!!\033[0m')
elif player == '剪刀':
    if computer == '石头':
        print('\033[31;1myou lose!!!\033[0m')
    elif computer == '剪刀':
        print('\033[32;1m平局')
    else:
        print('\033[31;1myou win !!!\033[0m')
else:
    if computer == '石头':
        print('y\033[31;1mou win !!!\033[0m')
    elif computer == '剪刀':
        print('\033[31;1myou lose!!!\033[0m')
    else:
        print('\033[32;1m平局\033[0m')
```

```python
import random

choices = ['石头','剪刀','布']
win_list = [['石头','布'],['剪刀','布'],['布','石头'],]
computer = random.choice(choices)
player = input('请出拳（石头/剪刀/布): ')

print("you choice:%s,computer's choice: %s" % (player,computer))
if player == computer:
    print('\033[32;1m平局\033[0m')
elif [player,computer] in win_list:
    print('\033[31;1myou win\033[0m')
else:
    print('\033[31;1myou lose!!!\033[0m')

```

```python
import random

choices = ['石头','剪刀','布']
win_list = [['石头','布'],['剪刀','布'],['布','石头'],]
computer = random.choice(choices)
prompt =  """(0)石头
(1)剪刀
(2)布
请选择(0/1/2): """
ind = int(input(prompt))
player = choices[ind]

print("you choice:%s,computer's choice: %s" % (player,computer))
if player == computer:
    print('\033[32;1m平局\033[0m')
elif [player,computer] in win_list:
    print('\033[31;1myou win\033[0m')
else:
    print('\033[31;1myou lose!!!\033[0m')
```

### while

-  while.py

```python
result = 0  #定义一个用于存储的变量
counter = 1 #定义计数器，计数器自增，每个计数器的值都累加到result中

while counter < 100:
    result += counter
    counter += 1

print(result)
```

```python
import random

choices = ['石头','剪刀','布']
win_list = [['石头','布'],['剪刀','布'],['布','石头'],]
prompt =  """(0)石头
(1)剪刀
(2)布
请选择(0/1/2): """
cwin = 0
pwin = 0

while pwin < 2 and  cwin < 2:
    ind = int(input(prompt))
    player = choices[ind]
    computer = random.choice(choices)

    print("you choice:%s,computer's choice: %s" % (player,computer))
    if player == computer:
        print('\033[32;1m平局\033[0m')
    elif [player,computer] in win_list:
        pwin += 1
        print('\033[31;1myou win\033[0m')
    else:
        cwin += 1
        print('\033[31;1myou lose!!!\033[0m')
```

```python
import random

choices = ['石头','剪刀','布']
win_list = [['石头','布'],['剪刀','布'],['布','石头'],]
prompt =  """(0)石头
(1)剪刀
(2)布
请选择(0/1/2): """
cwin = 0
pwin = 0

while 1:
    ind = int(input(prompt))
    player = choices[ind]
    computer = random.choice(choices)

    print("you choice:%s,computer's choice: %s" % (player,computer))
    if player == computer:
        print('\033[32;1m平局\033[0m')
    elif [player,computer] in win_list:
        pwin += 1
        print('\033[31;1myou win\033[0m')
    else:
        cwin += 1
        print('\033[31;1myou lose!!!\033[0m')

    if pwin == 2 or cwin == 2:
        break 
```

```python
result = 0
counter = 0

while counter <= 100:
    counter += 1
    if counter % 2 == 1:
        continue
    else:
        result += counter
print(result)
```

```python 
result = 0
counter = 0

while counter <= 100:
    counter += 1
    #if counter % 2 == 1:
    if counter % 2: #counter % 2 的值只有1和0，0为False，1为Ture
        continue
    result += counter
print(result)
```

```python
import random

num = random.randint(1,100) #生成一个一到一百之间的整数，也可能会包含1到100
counter = 0
while counter  < 7:
    answer = int(input('guess: '))
    if answer > num:
        print('猜大了')
    elif answer < num:
        print('猜小了')
    else:
        print('猜对了')
        break
    counter +=1

else:
    print('正确答案是：',num)
```

### for循环

```python
s1 = 'abc'

for ch in s1:
    print(ch)
print('*'*30)

nums = [101,123,2000]
for i in nums:
    print(i)
print('*'*30)

users = {'tom','jerry','bob'}
for user in users:
    print(user)
print('*' * 30)

adict = {'name':'tom','age':20}
for key in adict:
    print(key,adict[key])

```

### range函数

```python
>>> for i in range(10):
...     print(i)
>>> list(range(6,11))
[6, 7, 8, 9, 10]
>>> range(1,11,2)
range(1, 11, 2)
>>> list(range(1,11,2))
[1, 3, 5, 7, 9]
>>> list(range(10,0,-1))
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

```

```python

result = 0

for i in range(1,10000001):
    result += i

print(result)
```

```python
fib = [0,1]

for i in range(8):
    fib.append(fib[-1] + fib[-2])

print(fib)
```

```python
fib = [0,1]
n = int(input('长度： '))
for i in range(n - 2):
    fib.append(fib[-1] + fib[-2])

print(fib)
```

```python
>>> [10 + i for i in range(10) if i % 2 == 1]#循环表达式可以用循环的变量，if作为过滤条件
[11, 13, 15, 17, 19]
>>>[10 + 5]#表达式计算结果放到列表中
>>> ['192.168.1.%s'% i for i in range(1,11)]
['192.168.1.1', '192.168.1.2', '192.168.1.3', '192.168.1.4', '192.168.1.5', '192.168.1.6', '192.168.1.7', '192.168.1.8', '192.168.1.9', '192.168.1.10']

```

```python
for i in range(3):
    for j in range(3):
        print('hello',end=' ')#print默认在结尾打印\n，改为空格
    print()#打印回车
    
    
for i in range(3):
    for j in range(i + 1):
        print('hello',end=' ')#print默认在结尾打印\n，改为空格
    print()#打印回车
    
for i in range(1,10):
    for j in range(1,1 + i ):
        print('%sx%s=%s'%(j,i,i*j),end=' ')
    print()
```

### 文件

- 文件操作的步骤：打开、读写、关闭
- 读取文本文件

```python
>>>f = open('/tmp/passwwd') #默认以r的方式打开
>>>data = f.read() #默认读取全部内容
>>>data
'root:x:0:0:root:/root:/bin/bash\89:89::/var/spool/postfix:/sbin/nologin\nntp:x:38:38::/etc/ntp:/sbin/nologin\ntcpdump:x:72:72::/:/sbin/nologin\nydg:x:1000:1000:ydg:/home/ydg:/bin/bash\n'
>>>print(data)
>>> data = f.read()#继续向后读取
>>> data
''
>>> f.close()
>>> f = open('/tmp/passwd')
>>> f.read(4) #指定一次最多读取的字节数
'root'
>>> f.read(4)
':x:0'
>>> f.readline()#继续向后读取一行
':0:root:/root:/bin/bash\n'
>>> f.readlines()#继续向后读取，将所有的行读取到列表中
['bin:x:1:1:bin:/bin:/sbin/nologin\n', 'daemon:x:2:2:/sbin/nologin\n', 'tcpdump:x:72:72::/:/sbin/nologin\n', 'ydg:x:1000:1000:ydg:/home/ydg:/bin/bash\n']
>>>f.close()

#***重要：以下方法昌最常用的遍历文件的方法***
>>> f = open('/tmp/passwd')
>>>for line in f:
    print(line,end=' ')
>>>f.close()
```

- 读取非文本文件

```python
>>>f = open('/tmp/a.jpg','rb')#b表示bytes
>>>f.read(5)#读取5个字节
#2进制与16进制互转：4上二进制数转换成一个16进制数
>>>f.read(4096)#介意一次读4K或4K的倍数
b''
>>>f.close()

```

- 写入文本文件

```python
>>>f = open('/tmp/a.txt','w')
>>>f.write('hello world!\n')#将字符串写入文件
13
>>>f.flush()#立即将缓存数据同步到磁盘
>>>f.writelines('2nd line\n','3nd line\n')#将字符串中的每一个记录写入文件
>>>f.close()
```

- 以非文本文件写入文件

```python
>>> f = open('/tmp/a.txt','wb')
#字符串前面加上b，表示这是bytes类型的数据，一上英文字符正好是一个字节。
>>> f.write(b'hello world\n')
12
>>> f.write(b'你好\n') #错误，困为一上汉字不是一个字节，是3个字节
  File "<stdin>", line 1
SyntaxError: bytes can only contain ASCII literal characters.
>>> b1 = '你好!\n'
>>> type(b1)
<class 'str'>
>>> b1.encode()
b'\xe4\xbd\xa0\xe5\xa5\xbd!\n'
>>> f.write(b1.encode())
8
>>>f.close()

```

### 字符编码

- 每个字符在计算机上存储的时候，都是用2进制01进行表示
- 美国常用的ASCII码用7位来表示一上字符；欧洲使用ISO-8859-1作为字符编码它是在ASCII的基础之上在扩展1位，使用8位来表示一上字符；中国常用的字符集是用GB2312，GB18030，GBK
- ISO推出了unicode编码，被称作万国码，utf8编码是unicode的一种编码，它采用变长的字节表示一个字符。如一个英文字符占1个字节，一个汉字字符占3个字节。

### with语句

- with打开文件，当with语句结束时，文件自动关闭

```python
>>> with open('/tmp/passwd') as f:
...     f.readline()
... 
'root:x:0:0:root:/root:/bin/bash\n'
>>> f.readline()#报错，因为文件已经关闭了
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: I/O operation on closed file.

```

### seek语句

- 了解即可
- 用于移动文件指针
- 它的第二上参数是数字：0->开头，1->指针当前位置，2->结尾
- 它的第一上参数是相对于第二个参数的偏移量

```python
>>> f = open('/tmp/passwd'，'wb')
>>> f.seek(16,0)#文件指针移动到距离开头向右16个字节处
16
>>> f.read(5)
'/root'
>>>f.seek(-5,2)#文件指针移动到离结尾5上字符处
2714
>>>f.read()
b'bash\n'
```

- 拷贝文件的代码分析

```python
f1 = open('/bin/ls','rb')
f2 = open('/tmp/list','wb')

data = f1.read()
f2.write(data)

f1.close()
f2.close()
```

1. 介意使用变量，而不是直接使用字面量，open的参数最好使用变量
2. 变量名应该有意义，f1,f2这样的变量不能体现出它代表什么
3. 如果文件很大，一次性将所有内空读取出来 将会消耗太多的内存

```python
src_fname = '/bin/ls'
dst_fname = '/tmp/list2'
src_fobj = open(src_fname,'rb')
dst_fobj = open(dst_fname,'wb')
    
while 1:
    data = src_fobj.read(4096)
    # if len(data) == 0:
    # if data == b'':
    if not data:
        break
    dst_fobj.write(data)
    
src_fobj.close()
dst_fobj.close()
```

### 函数的基本概念

```python
def mk_fib():

    fib = [0,1]

    n = int(input('长度： '))
    for i in range(n - 2):
        fib.append(fib[-1] + fib[-2])

    print(fib)

mk_fib()
```

- 函数返回值 
  - 函数使用return返回支行结果
  - 如果没有return语句，则返回None

```python
def mk_fib():

    fib = [0,1]

    n = int(input('长度： '))
    for i in range(n - 2):
        fib.append(fib[-1] + fib[-2])

    return fib

alist= mk_fib()
print(alist)
blist = [i * 2 for i in alist]
print(blist)
```

```python
def mk_fib(n):

    fib = [0,1]

    # n = int(input('长度： '))
    for i in range(n - 2):
        fib.append(fib[-1] + fib[-2])

    return fib
for i in [5,8,6,10,20]:
    print(mk_fib(i))
```

- 参数
  - 函数定义时，写的（）中的变量名叫形式参数、形参
  - 调用函数时，传递给函数的具体数据，叫实际参数，实参

```python
import sys

def copy(src_fname,dst_fname):
    # src_fname = '/bin/ls'
    # dst_fname = '/tmp/list2'
    src_fobj = open(src_fname,'rb')
    dst_fobj = open(dst_fname,'wb')

    while 1:
        data = src_fobj.read(4096)
        # if len(data) == 0:
        # if data == b'':
        if not data:
            break
        dst_fobj.write(data)

    src_fobj.close()
    dst_fobj.close()
copy(sys.argv[1],sys.argv[2])
```

- 默认参数
  - 提供了默认值的参数

```python
>>> def pstar(n=30):
...     print('*' * n)
... 
>>> pstar()
******************************
>>> pstar(20)
********************
>>> 

```

### 模块

- 模块就是一个python程序文件
- 将程序文件的扩展名.py移除，剩下的文件名就是模块名

```python
#vim star.py
hi = 'hello world'

def pstar(n=30):
    print('*' * n)
    
>>> star.hi
'hello world' 
>>> star.pstar()
*******************************

```

### 导入模块的方法

```python
>>>import star #常用
>>>from random import choice,randint#常用
>>>choice('abcd')
'a'
>>>randint(1,100)
57
>>>import sys,getpass #一行导入多个模块，不常用
>>>import getpass as gp#导入模块的同时，为它起别名，不常用
>>>gp.getpass('password: ')

```

- 导入模块时，模块文件的代码将会支行一遍，这叫加载load
- 不管导入多少次，只运行一次

###  _\_name__特殊属性

- 每个模块都有一个特殊的变量叫_\_name__
- _\_name__变量可以有俩个值
  - 如果模块名直接运行，值为_\_main__
  - 如果模块文件间接运行，值为模块名

```python
(helloworld) [root@helloworld ydg]# echo 'print(__name__)' > foo.py
(helloworld) [root@helloworld ydg]# echo 'import foo' >  bar.py
(helloworld) [root@helloworld ydg]# cat fo
foo.py   for1.py  
(helloworld) [root@helloworld ydg]# cat foo.py 
print(__name__)
(helloworld) [root@helloworld ydg]# cat bar.py 
import foo
(helloworld) [root@helloworld ydg]# python foo.py
__main__
(helloworld) [root@helloworld ydg]# python bar.py 
foo

```

```python
hi = 'hello world'

def pstar(n=30):
    print('*' * n)

if __name__ == '__main__':
    print(hi)
    pstar(n=50)
```

```python
from random import choice

all_chs = '1234567890qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM'
def randpass(n=8):
    result = ''

    for i in range(n):
        ch = choice(all_chs)
        result += ch

    return result
if __name__ == '__main__':
    print(randpass())
    print(randpass(6))

```

```python
from random import choice
from string import ascii_letters,digits

all_chs = ascii_letters + digits
def randpass(n=8):
    result = ''

    for i in range(n):
        ch = choice(all_chs)
        result += ch

    return result
if __name__ == '__main__':
    print(randpass())
    print(randpass(6))
```

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

### 列表

- 属于可变、容器、顺序类型

```python
>>> alist = [1,8,54,10,3,1]
>>> alist[2]
54
>>> alist[2] = 80
>>> alist
[1, 8, 80, 10, 3, 1]
>>> alist[2:4]
[80, 10]
>>> alist[2:4] = [1,3,5,10]
>>> alist
[1, 8, 1, 3, 5, 10, 3, 1]
>>> alist[3:3]
[]
>>> alist[3:3]=[10,20]
>>> alist
[1, 8, 1, 10, 20, 3, 5, 10, 3, 1]
>>> alist.append(10)
>>> alist
[1, 8, 1, 10, 20, 3, 5, 10, 3, 1, 10]
>>> alist.in
alist.index(   alist.insert(  
>>> alist.insert(1,10)#在下标为1的地方插入数字10
>>> alist
[1, 10, 8, 1, 10, 20, 3, 5, 10, 3, 1, 10]
>>>>>> alist.count(10)#统计列表中10的个数
4
>>> alist.extend([100,200,300])#向列表中加入三项
>>> alist
[1, 10, 8, 1, 10, 20, 3, 5, 10, 3, 1, 10, 100, 200, 300]
>>> alist.pop()#移除并返回列表的最后一项
300
>>> alist.pop(2)#移除并返回下标为2的项
8
>>> alist.remove(10)#删除列表中出现的第一个10
>>> 


>>> def fun1():
...     a = 10 + 20
...     return a
... 
>>> def fun2():
...     a = 10 + 20
... 
>>> fun1()
30
>>> fun2()
>>> 
    
>>> alist.index(5) #返回下标
5
>>> alist
[1, 1, 10, 20, 3, 5, 10, 3, 1, 10, 100, 200]
>>> alist.sort()#升序排序
>>> alist.reverse()#翻转列表
>>>clist = alist.copy()#将alist的址赋值给clist，它们使用不同的地址空间
>>>clist.clear()#清空clist
```

### 元组

- 属于容器、不可变的、顺序类型
- 元组相当玩是不可变的列表
- 单元素元组，必须在元素后面加上逗号

```python
>>> atuple =(10,20,30,20,40,20,8)
>>> atuple.count(20)#统计20出现的次数
3
>>> atuple.index(30)#返回30的下标
2

>>> a = (10)
>>> type(a)
<class 'int'>
>>> a = (10,)
>>> type(a)
<class 'tuple'>
>>> len(a)
1

```

- 列表的练习
  1. 思考程序的运行方式

```python
(0) 压栈
(1)	出栈
(2) 查询
(3) 退出
请选择(0/1/2/3): 10
无效的选择，请重试。
(0) 压栈
(1)	出栈
(2) 查询
(3) 退出
请选择(0/1/2/3): 2
[]
(0) 压栈
(1)	出栈
(2) 查询
(3) 退出
请选择(0/1/2/3): 0
数据：
输入为空
(0) 压栈
(1)	出栈
(2) 查询
(3) 退出
请选择(0/1/2/3): 0
数据：hello
(0) 压栈
(1)	出栈
(2) 查询
(3) 退出
请选择(0/1/2/3): 2
 ['hello']
(0) 压栈
(1)	出栈
(2) 查询
(3) 退出
请选择(0/1/2/3): 1
从栈中，弹出了：hello
(0) 压栈
(1)	出栈
(2) 查询
(3) 退出
请选择(0/1/2/3): 1
栈已经为空
(0) 压栈
(1)	出栈
(2) 查询
(3) 退出
请选择(0/1/2/3):2
[]
(0) 压栈
(1)	出栈
(2) 查询
(3) 退出
请选择(0/1/2/3): 3
Bye-Bye
```

2. 思考程序有哪些功能，将功能写成功能函数
3. 编写主程序代码，按照一定的规则调用函数

```python
def push_it():#用于实现压栈功能
    
    
def pop_it():# 用于实现出栈功能
    
    
def view_it():#用于实现查询功能
    
    
def show_menu():#用于在屏幕上打印菜单，根据用户选择，调用相关功能函数
    
if __name__ == '__main__':
    show_menu()
```

4. 完成每个具体的函数

```python


stack = []

def push_it():#用于实现压栈功能
    data = input('数据: ').strip()
    if data:
        stack.append(data)
    else:
        print('\033[31;1m输入为空\033[0m')

def pop_it():# 用于实现出栈功能
    if stack:
        print('从列表中弹出了：\033[34;1m%s\033[0m'% stack.pop())
    else:
        print('\033[31;1m列表为空\033[0m')

def view_it():#用于实现查询功能
    print('\033[32;1m%s\033[0m'%stack)

def show_menu():#用于在屏幕上打印菜单，根据用户选择，调用相关功能函数
    cmds = {'0': push_it,'1': pop_it,'2': view_it}
    prompt ="""(0) 压栈
(1)出栈
(2)查询
(3)退出
请选择(0/1/2/3):"""
    while 1:
        choice = input(prompt).strip()#将输入的两端空白字符删除
        if choice not in ['0','1','2','3']:
            print('无效的选择，请重试')
            continue
        if choice == '3':
            print('\nBye-Bye')
            break
        cmds[choice]()
        
        # elif choice == '0':
        #     push_it()
        # elif choice == '1':
        #     pop_it()
        # elif choice == '2':
        #     view_it()
        # else:
        #     print('\nBye-bye')
        #     break



if __name__ == '__main__':
    show_menu()
```

### 字典

- 属于容器、可变、映射
- 字典的key不能重复，赋值时，key不存在 则向字典加新值key存在则修改值
- 字典的key只能是不可变对象

```python
>>> adict = dict(['ab',('name','tom'),['age',20]])
>>> adict
{'a': 'b', 'name': 'tom', 'age': 20}
>>> dict([('name','tom'),('age',20),('email','tom@163.com')])
{'name': 'tom', 'age': 20, 'email': 'tom@163.com'}
>>> 
>>> {}.fromkeys(['tom','bob','jerry'],20)
{'tom': 20, 'bob': 20, 'jerry': 20}

>>> 'tom' in adict
False
>>> 'name' in adict
True
>>> for key in adict:
...     print(key,adict[key])
... 
a b
name tom
age 20
>>> adict['email'] = 'tom@167.c9m'
>>> adict
{'a': 'b', 'name': 'tom', 'age': 20, 'email': 'tom@167.c9m'}
>>> adict['age'] = 22
>>> adict
{'a': 'b', 'name': 'tom', 'age': 22, 'email': 'tom@167.c9m'}
>>> len(adict)
4

>>> hash(10)
10
>>> hash('abc')
2205970290797005180
>>> hash([10,20])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
>>> hash({'age':20})
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'dict'
>>> 
#字典的方法
>>> adict.get('name')#最常用 的方法，通过key取出value
'tom'
>>> adict.get('phone')#如果key不在字典中，默认返回None
None
>>> 
>>> adict.get('name','not found')#key不在字典中，返回值可以自行按规定
'tom'
#adict.clean()和adict.copy()与列表的相关方法是一样的
>>> adict.keys()
dict_keys(['a', 'name', 'age', 'email'])
>>> list(adict.keys())
['a', 'name', 'age', 'email']
>>> adict.values()#取出所有的value
dict_values(['b', 'tom', 22, 'tom@167.c9m'])
>>> adict.items()#将字典每一项以key,value的形式返回
dict_items([('a', 'b'), ('name', 'tom'), ('age', 22), ('email', 'tom@167.c9m')])
>>> list(adict.items())
[('a', 'b'), ('name', 'tom'), ('age', 22), ('email', 'tom@167.c9m')]
>>> adict.pop('a')#通过key编出value
'b'
>>> adict
{'name': 'tom', 'age': 22, 'email': 'tom@167.c9m'}

```

```python
import getpass

userdb = {}

def register():#用于注册用户
    user = input('用户名：　').strip()
    if user and user not in userdb:
        passwd = input('密码：　')
        userdb[user] = passwd
    else:
        print('用户名为空或用户已经存在')


def login():#用于验证登陆
    user = input('用户名：　 ').strip()
    passwd =getpass.getpass('密码：')
    # if user in userdb and userdb[user] == passwd:
    if userdb.get(user) == passwd:
        print('登陆成功')
    else:
        print('登陆失败')


def show_menu():#菜单
    cmds = {'0': register,'1': login}
    prompt =  """(0) 注册
(1)　登陆
(2)　退出  
请选择(0/1/2): """
    while 1:
        choice = input(prompt).strip()
        if choice not in ['0','1','2']:
            print('无效输入，请重试')
            continue

        if choice == '2':
            print('\nBye-Bye')
            break

        cmds[choice]()


if __name__ == '__main__':
    show_menu()
```

### 哈希算法

- 单向加密，只能通过原始数据生成密文，不能反制作人推
- 原始数据相同，得到的密文也是一样的
- linux的密文说明，#$算法$salt$通过密码和salt算出来的密文  算法如果是md5为1,如果是sha512为6，salt是随机字符串

```python
>>> import crypt
>>> crypt.crypt('1','$6$no1111111$')
'$6$no1111111$.5KKJGGUK164ZP8sEbg4UK1ugH5gTSXzV2X8CpPIa/aFIA3Z4uUNoC/1jpdddit6NYfNIDBKCOC9adg7pQc4n0'

```

 

### 集合

- 在数学上，把set称做由不同元素组成的集合
- 集合元素必须是不可变对象
- 集合元素没有顺序
- 集合的元素不能重复
- 集合就像是一个无值的字典

```python
>>> aset =set('abc')
>>> bset = set('bcd')
>>> cset = set(['tom','jerry','bob'])
>>> aset
{'b', 'c', 'a'}
>>> bset
{'b', 'c', 'd'}
>>> cset
{'tom', 'bob', 'jerry'}
>>> for name in cset:
...     print(name)
... 
tom
bob
jerry
>>> len(cset)
3
>>> 'tom' in cset
True
>>> set('hello')
{'l', 'e', 'h', 'o'}

>>> aset&bset #交集
{'b', 'c'}
>>> aset | bset#并集
{'b', 'd', 'c', 'a'}
>>> aset -bset#差补，aset中有，bset中没有的
{'a'}
>>> bset -aset
{'d'}

>>> cset
{'tom', 'bob', 'jerry'}
>>> cset.add('alice')#增加元素
>>> cset
{'tom', 'bob', 'jerry', 'alice'}
>>> cset.remove('bob')#删除元素
>>> cset.update(['zhangsan','lisi'])#批量更新
>>> cset
{'jerry', 'alice', 'zhangsan', 'tom', 'lisi'}
>>> dset = aset | bset
>>> dset
{'b', 'd', 'c', 'a'}
>>> aset.issubset(dset)#aset是dset的子集吗
True
>>> dset.issuperset(aset)#dset是aset的超集吗
True
>>> aset.union(bset) #aset | bset
{'b', 'd', 'c', 'a'}
>>> aset.intersection(bset)#aset & bset
{'b', 'c'}
>>> aset.difference(bset)#aset - bset
{'a'}


```

1. log->昨天的日志文件->url1.txt
2. log->今天的日志文件->url2.txt

```python
#比较两个文件，取出b文件中存在，a文件中不存在的行
(helloworld) [root@helloworld ydg]# cp /etc/passwd /tmp/
(helloworld) [root@helloworld ydg]# cp /etc/passwd /tmp/mima
>>> nums = [randint(1,20) for i in range(30)]
>>> nums
[14, 3, 3, 11, 19, 18, 15, 16, 8, 10, 20, 3, 11, 14, 6, 9, 14, 6, 2, 5, 14, 15, 3, 8, 11, 6, 5, 15, 3, 10]
>>> set(nums)
{2, 3, 5, 6, 8, 9, 10, 11, 14, 15, 16, 18, 19, 20}
>>> 
>>> with open('/tmp/passwd') as f1:
...     set1 = set(f1)
>>> with open('/tmp/mima') as f2:
...     set2 = set(f2)
>>> with open('/tmp/r.txt','w') as f3:
...     f3.writelines(set2 - set1)
... 

```

