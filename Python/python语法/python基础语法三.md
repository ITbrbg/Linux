# python基础语法三

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

