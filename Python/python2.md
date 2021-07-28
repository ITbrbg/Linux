## python2

### time模块

### 时间的表示方法

- 时间戳：表示是从1970年1 月1日00：00：00开始按秒计算的偏移量
- UTC时间：世界协调时，格林威治天文时间，世界标准时间。
- struct_time: 9元组（年，月，日，时，分，秒，一周中的第几天，一年中的第几天，是否启用夏季节约时间）

```python
>>> import time
>>> time.time()#运行命令时的时间戳
1617601373.7086856
>>> 
>>> time.ctime()#UTC时间
'Mon Apr  5 13:43:21 2021'
>>> time.localtime()#struce_time
time.struct_time(tm_year=2021, tm_mon=4, tm_mday=5, tm_hour=13, tm_min=45, tm_sec=46, tm_wday=0, tm_yday=95, tm_isdst=0)
>>> t = time.localtime()
>>> t
time.struct_time(tm_year=2021, tm_mon=4, tm_mday=5, tm_hour=13, tm_min=48, tm_sec=8, tm_wday=0, tm_yday=95, tm_isdst=0)
>>> t.tm_year
2021
>>> time.sleep(3)# 睡眠3秒
>>> time.strftime('%Y-%m-%d %H:%M:%S')
'2021-04-05 14:00:30'

#将时间字符串转成9元组的时间格式 
>>> t1 = '2020-01-08 10:30:00'
>>> time.strptime(t1,'%Y-%m-%d %H:%M:%S')
time.struct_time(tm_year=2020, tm_mon=1, tm_mday=8, tm_hour=10, tm_min=30, tm_sec=0, tm_wday=2, tm_yday=8, tm_isdst=-1)
>>> t1 = time.strptime(t1,'%Y-%m-%d %H:%M:%S')
>>> t>t1
True
>>> t = time.localtime()

```

```python
import time

result = 0

start = time.time()
for i in range(1,10000001):
    result += i
end = time.time()

print(result)
print(end - start)
```

```python
import time

t9 = time.strptime('2021-04-04 09:00:00','%Y-%m-%d %H:%M:%S')
t12 = time.strptime('2021-04-04 12:00:00','%Y-%m-%d %H:%M:%S')
with open('web.log') as fobj:
    for line in fobj:
        t = time.strptime(line[:19],'%Y-%m-%d %H:%M:%S')
        # if t9 <= t <= t12:
        #     print(line,end='')
        if t > t12:
            break
            
        if t > t9:
            print(line,end='')
```

### datetime模块

```python
>>> datetime.datetime.now()#返回的是（年月日时分秒毫秒）
datetime.datetime(2021, 4, 5, 14, 23, 58, 743932)
>>> t = datetime.now()
>>> t
datetime.datetime(2021, 4, 5, 14, 26, 21, 518993)
>>> t.year
2021
>>> t.month
4
>>> t.minute
26
>>> t.second
21       
>>> t.microsecond
518993
>>> t.day
5
>>> t.hour
14
>>> t.strftime('%Y/%m/%d %H:%M:%S')#转成时间字符串
'2021/04/05 14:26:21'
#时间字符串转换成datetime对象
>>> datetime.strptime('2020-1-8 9:00:00','%Y-%m-%d %H:%M:%S')
datetime.datetime(2020, 1, 8, 9, 0)
#通过timedelta计算时间差额
>>> from datetime import datetime,timedelta
>>> days = timedelta(days=100,hours=1)#定义100天零1小时
>>> t = datetime.now()
>>> t - days#100天一小时之前的时间
datetime.datetime(2020, 12, 26, 13, 52, 11, 99528)
>>> t + days#100天一小时之后的时间
datetime.datetime(2021, 7, 14, 15, 52, 11, 99528)
>>> 

```

```python
try:
    num = int(input('number:'))
    result = 100 / num

except (ValueError,ZeroDivisionError) as e:#将异常保存到变量E中
    print('只接受数字',e)
except (KeyboardInterrupt,EOFError):
    print('\Bye-bye')
    exit(101)#程序遇到exit将会结束，101是退出码，即$?
else:#异常不发生才地执行的语句放到else中
    print(result)
finally:#不管异常是否发生都地执行的语句，都会执行的语句发到finally
    print('Done')

```

### 触发异常

- 通过raise指定触发的异常
- 通过assert触发的AssertionError异常

```python
def get_info(name,age):
    if not 0 < age < 120:
        raise ValueError('年龄超过')
    print('%s is %d years old' % (name,age))

def get_info2(name,age):
    assert 0 < age < 120 ,'年龄超过范围（1~119）'
    print('%s is %s years old'% (name,age))
    
    
    import get_info

name = '邹'
age = 200
try:
    get_info.get_info(name,age)
except ValueError as e:
    print('Error',e)

get_info.get_info2(name,age)
```

### os模块

```python
>>> import os
>>> os.listdir()#ls
>>> os.mkdir('/tmp/aaa')#mkdir /tmp/aaa
>>> os.makedirs('/tmp/bbb/aaa') #mkdir -p /tmp/bbb/aaa
>>> os.chdir('/tmp/aaa') #cd /tmp/aaa
>>> os.getcwd()#pwd
'/tmp/aaa'
>>> import shutil
>>> shutil.copy('/etc/hosts','hosts')#cp /etc/hosts /tmp/aaa/hosts
'hosts'
>>> os.mknod('test.txt')#touch test.txt

>>> os.symlink('/etc/passwd','mima') #ln -s /etc/passwd mima
>>> os.chmod('hosts',0o600)#chmod 600 hosts
>>> 0o644
420
>>> os.chmod('hosts',420)
>>> os.path.abspath('bbb')#返回绝对路径
'/tmp/aaa/bbb'
>>> os.listdir()
['demo', 'hosts', 'test.txt', 'mima']
>>> os.path.isabs('aaa/bbb/ccc')#判断路径是不是绝对路径
False
>>> os.path.isabs('/aaa/bbb/ccc')
True
>>> os.path.isfile('hosts')#hosts存在，并且是文件吗？
True
>>> os.path.ismount('/etc/')#是挂载点吗
False
>>> os.path.isdir('bbb')#是目录吗
False
>>> os.path.islink('mima')#是软链接吗
True
>>> os.path.exists('/etc/hostname')#存在吗
True
>>> os.path.basename('etc/hosts')
'hosts'
>>> os.path.dirname('/etc/hosts')
'/etc'
>>> os.path.split('/etc/hosts')
('/etc', 'hosts')
>>> os.path.join('/etc/hosts')
'/etc/hosts'

```

- os.walk
  - 递归遍历目录下的内容

```python
>>> alist = list(os.walk('/var/aaa'))
>>> len(alist)
4
>>> alist[0]
('/var/aaa', ['aaa', 'bbb', 'ccc'], [])
>>> alist[1]
('/var/aaa/aaa', [], ['a.txt', 'b.txt', 'c.txt'])
>>> alist[2]
('/var/aaa/bbb', [], ['a.txt', 'b.txt', 'c.txt'])
>>> alist[3]
('/var/aaa/ccc', [], ['a.txt', 'b.txt', 'c.txt'])
#经过分析，列表由元组构成
#每上元组都有相同的结构：(路径字符串，路径下目录列表，路径下文件列表)
>>> for data in alist:
...     print(data)
... 
('/var/aaa', ['aaa', 'bbb', 'ccc'], [])
('/var/aaa/aaa', [], ['a.txt', 'b.txt', 'c.txt'])
('/var/aaa/bbb', [], ['a.txt', 'b.txt', 'c.txt'])
('/var/aaa/ccc', [], ['a.txt', 'b.txt', 'c.txt'])
>>> 
>>> for path,folders,files in os.walk('/var/aaa'):
...     print(path,folders,files)
... 
/var/aaa ['aaa', 'bbb', 'ccc'] []
/var/aaa/aaa [] ['a.txt', 'b.txt', 'c.txt']
/var/aaa/bbb [] ['a.txt', 'b.txt', 'c.txt']
/var/aaa/ccc [] ['a.txt', 'b.txt', 'c.txt']
>>> 


>>> for path,folders,files in os.walk('/var/aaa'):
...     print('%s'% path)
...     for dir in folders:
...             print(dir,end='\t')
...     for file in files:
...             print(file,end='\t')
...     print('\n')
... 
/var/aaa
aaa     bbb     ccc     

/var/aaa/aaa
a.txt   b.txt   c.txt   

/var/aaa/bbb
a.txt   b.txt   c.txt   

/var/aaa/ccc
a.txt   b.txt   c.txt   

>>> 

```

### pickle模块

- pickle模块可以将任意的数据类型写到文件中，还可以再无损的取出

```python
>>> import pickle
>>> shopping_list = ['apple','banana','egg']
>>> with open('/tmp/a.txt','wb') as fobj:
...     pickle.dump(shopping_list,fobj)
... 
>>> import pickle
>>> with open('/tmp/a.txt','rb') as fobj:
...     alist = pickle.load(fobj)
... 
>>> type(alist)
<class 'list'>
>>> alist
['apple', 'banana', 'egg']

```

```python
import os
import pickle
from time import strftime

def  save(fname):
    #用于记录收入
    try:
        amount = int(input('金额：　'))
        comment = input('备注：　')
    except ValueError:
        print('无效的金额：')
        return
    except (KeyboardInterrupt,EOFError):
        print('\nBye-Bye')
        exit()

    date = strftime('%Y-%m-%d')
    #取出全部收支情况
    with open(fname,'rb') as fobj:
        records = pickle.load(fobj)
    #计算最新余额
    balance = records[-1][-2] + amount
    #构建收支情况表
    line = [date,amount,0,balance,comment]
    records.append(line)
    #将更新后的收支情况列表写回文件
    with open(fname,'wb') as fobj:
        pickle.dump(records,fobj)

def cost(fname):
    try:
        amount = int(input('金额：　'))
        comment = input('备注：　')
    except ValueError:
        print('无效金额')
        return
    except (KeyboardInterrupt,EOFError):
        print('\nBye-Bye')
        exit()
    date = strftime('%Y-%m-%d')
    with open(fname,'rb') as fobj:
        records = pickle.load(fobj)
    balance = records[-1][-2] - amount
    line = [date,0,amount,balance,comment]
    records.append(line)
    with open(fname,'wb') as fobj:
        pickle.dump(records,fobj)

def query(fname):
    with open(fname,'rb') as fobj:
        records = pickle.load(fobj)
    print('%-12s%-8s%-8s%-12s%-20s'% ('date','save','cost','balance','comment'))
    for line in records:
        print('%-12s%-8s%-8s%-12s%-20s'% tuple(line))

def show_menu():
    cmds = {'0': save,'1':cost,'2':query}
    prompt = """(0) 收入
(1) 开销
(2) 查询
(3) 退出
请选择(0/1/2/3): """
    fname = 'account.data'
    init_data =  [['2021-04-04',0,0,10000,'init data']]
    if not os.path.exists(fname):
        with open(fname,'wb') as fobj:
            pickle.dump(init_data,fobj)

    while 1:
        try:
            choice = input(prompt).strip()
        except (KeyboardInterrupt,EOFError):
            choice = '3'
        if not choice in ['0','1','2','3']:
            print('输入无效，请重试。')
            continue

        if choice == '3':
            print('\nBye-Bye')
            break

        cmds[choice](fname)

if __name__ == '__main__':
    show_menu()
```



### 函数

- 参数
  - 只写参数名，如argv，称作位置参数
  - 写成Key=Value形式的参数，称作关键字参数

```python
>>> def get_age(name,age):
...     print('%s is %s years old'%(name,age))
... 
>>> get_age('tom',20)#ok
tom is 20 years old
>>> get_age(20,'tom')#ok 但语意不对
20 is tom years old
>>> get_age(age=20,name='tom')#ok
tom is 20 years old

>>> get_age('tom',10,20)#参数太多
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: get_age() takes 2 positional arguments but 3 were given
>>> get_age('tom')#参数不足
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError
>>> get_age(age=20,'tom')#Error,位置参数需要在关键字参数的前面
  File "<stdin>", line 1
SyntaxError: positional argument follows keyword argument
>>> get_age(20,name='tom')#name得到了多个值
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: get_age() got multiple values for argument 'name'
>>> get_age('tom',age=20)#ok
tom is 20 years old


```

- 参数组
  - 创建函数时，在参数名前加*，表示参数是元组
  - 创建函数时，在参数名前加**，表示参数是字典
  - 调用函数时，在序列对象前加*表示将序列对象拆分开
  - 调用函数时，在序列对象前加**列示将字典对象拆分成key=value的形式

```python
>>> def func1(*argv):
...     print(argv)
... 
>>> func1('hello')
('hello',)
>>> func1('hello',123)
('hello', 123)
>>> 
>>> def func2(**kwargs):
...     print(kwargs)
... 
>>> func2()
{}
>>> func2(name='tom',age=20)
{'name': 'tom', 'age': 20}


>>> def get_age(name,age):
...     print('%s is %s years old'% (name,age))
... 
>>> user = ['bob',25]
>>> get_age(user[0],user[1])
bob is 25 years old
>>> get_age(*user)
bob is 25 years old
>>> user_dict = {'name': 'tom','age':20}
>>> get_age(**user_dict)
tom is 20 years old

```

```python
from random import randint,choice

def exam():
    nums = [randint(1,100) for i in range(2)]
    nums.sort(reverse=True)
    op = choice('+-')
    if op == '+':
        result = nums[0] + nums[1]
    else:
        result = nums[0] - nums[1]
    prompt ='%s %s %s =' % (nums[0],op,nums[1])
    counter = 0
    while counter < 3:
        try:
            answer = int(input(prompt))
        except:
            print()
            continue
            
        if answer == result:
            print('very good!!!')
            break
        print('不对哟！！！')
        counter += 1
    else:
        print('\033[31;1m正确答案：%s%s\033[0m'% (prompt,result))

def main():
    while 1:
        exam()
        try:
            yn = input('Continue(y/n)?').strip()[0]
        except IndexError:
            continue
        except (KeyboardInterrupt,EOFError):
            yn = 'n'
        if yn in 'Nn':
            print('\nBye-Bye')
            break

if __name__ == '__main__':
    main()
```

### 匿名函数

```python
>>> def add(x,y):
...     return x + y
... 
>>> add(10,3)
13
#可以写成以下的方式 
>>> myadd = lambda x,y: x + y
>>> myadd(10,20)
30


```

```python
from random import randint,choice

def add(x,y):
    return x + y

def sub(x,y):
    return x - y

def exam():
    cmds = {'+': add,'-': sub}
    nums = [randint(1,100) for i in range(2)]
    nums.sort(reverse=True)
    op = choice('+-')
    result = cmds[op](*nums)
    prompt ='%s %s %s =' % (nums[0],op,nums[1])
    counter = 0
    while counter < 3:
        try:
            answer = int(input(prompt))
        except:
            print()
            continue

        if answer == result:
            print('very good!!!')
            break
        print('不对哟！！！')
        counter += 1
    else:
        print('\033[31;1m正确答案：%s%s\033[0m'% (prompt,result))

def main():
    while 1:
        exam()
        try:
            yn = input('Continue(y/n)?').strip()[0]
        except IndexError:
            continue
        except (KeyboardInterrupt,EOFError):
            yn = 'n'
        if yn in 'Nn':
            print('\nBye-Bye')
            break

if __name__ == '__main__':
    main()
```

```python
from random import randint,choice


def exam():
    cmds = {'+': lambda x,y:x + y ,'-': lambda x,y: x + y}
    nums = [randint(1,100) for i in range(2)]
    nums.sort(reverse=True)
    op = choice('+-')
    result = cmds[op](*nums)
    prompt ='%s %s %s =' % (nums[0],op,nums[1])
    counter = 0
    while counter < 3:
        try:
            answer = int(input(prompt))
        except:
            print()
            continue

        if answer == result:
            print('very good!!!')
            break
        print('不对哟！！！')
        counter += 1
    else:
        print('\033[31;1m正确答案：%s%s\033[0m'% (prompt,result))

def main():
    while 1:
        exam()
        try:
            yn = input('Continue(y/n)?').strip()[0]
        except IndexError:
            continue
        except (KeyboardInterrupt,EOFError):
            yn = 'n'
        if yn in 'Nn':
            print('\nBye-Bye')
            break

if __name__ == '__main__':
    main()
```

### filter函数

- filter函数接受俩个参数，第一个参数的函数，第二上是序列对象
  - （filter的参数）函数接受一个参数，返回值必须是True或False
  - 将序列对象中的每个数据交给函数处理，返回直的留下，假的丢弃

```python
from random import randint

def func1(x):
    return True if x % 2 == 1 else False

if __name__ == '__main__':
    nums = [randint(1,100) for i in range(10)]
    print(nums)
    result = filter(func1,nums)
    print(list(result))
    result1 = filter(lambda x: True if x % 2 == 1 else False,nums)
    print(list(result1))
```

### map函数

- map函数接受现个参数，第一个参数是函数，第二个参数是序列对象
  - 函数接受一上参数，对参数进行加工处理，返回处理结果
  - map函数调用时，将序列对象逐一交给函数处理

```python
from random import randint

def func2(x):
    return x * 2

if __name__ == '__main__':
    nums = [randint(1,100) for i in range(10)]
    print(nums)
    result = map(func2,nums)
    print(list(result))
    result1 = map(lambda x:x * 2,nums)
    print(list(result1))
```

### 变量

- 在函数外边定义的变量是全局变量，从定义开始到程序结束，一直可变可用

```python
>>> x = 10
>>> def func1():
...     print(x)
... 
>>> func1()
10

```

- 在函数内部的变量是局部变量，只能在函数内部使用

```python
>>> def func2():
...     y = 100
...     print(y)
... 
>>> func2()
100
>>> y
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'y' is not defined

```

- 全局和局部拥有同名变量，函数调用时，局部变量遮住了全局变量

```python
>>> x = 10
>>> def func3():
...     x = 200
...     print(x)
... 
>>> func3()
200
>>> x
10

```

- 如果需要在函数肉部修改全局变量，需要在函数内部使用global语句声明

```python
>>> x = 10
>>> def func4():
...     global x
...     x = 100
...     print(x)
... 
>>> func4()
100
>>> x
100

```

### 偏函数

- 改造现有的函数，将函数的一些参数固定下来，生成新函数

```python
>>> def add(a,b,c,d,e):
...     return a + b + c + d + e 
... 
>>> add(10,20,30,40,3)
103
>>> add(10,20,30,40,5)
105
>>> add(10,20,30,40,9)
109
>>> from functools import partial
>>> myadd = partial(add,10,20,30,40)
>>> myadd(3)
103
>>> myadd(5)
105
>>> import tkinter
>>> window = tkinter.Tk()
>>> int('101010101')
101010101
>>> int('101010101',base=2)#说明数字字符串是二进制函数
341
>>> int2 = partial(int,base=2)#改造int函数，指定base=2
>>> int2('11111111')
255


```

### 递归函数

- 一个函数又包含了对自身的调用，就是递归函数

```python
5!=5x4x3x2x1
5!=5x4!

def func1(x):
    if x == 1:
        return 1
    return  x * func1(x - 1 )

if __name__ == '__main__':
    result = func1(5)
    print(result)
```

```python
from random import randint

def qsort(seq):
    if len(seq) < 2:
        return seq

    middle = seq[0]
    smaller = []
    larger = []

    for data in seq[1:]:
        if data <= middle:
            smaller.append(data)
        else:
            larger.append(data)

    return qsort(smaller) + [middle] + qsort(larger)
if __name__ == '__main__':
    nums = [randint(1,100) for i in range(10)]
    print(nums)
    print(qsort(nums))
```

### 生成器

- 本质上是一个函数
- 可以通过yield语句返回很多中间结果
- 生成器只能使用一次，产生一次值，再次使用需要重新赋值

```python
>>> def mygen():
...     yield 100
...     a = 10 + 20
...     yield a
...     yield 1000
... 
>>> mg = mygen()
>>> mg
<generator object mygen at 0x7f91755b7830>
>>> list(mg)
[100, 30, 1000]
>>> list(mg)
[100, 30, 1000]
>>> for i in mg:#输出为空取完了
...     print(i)
... 
```

### 模块

```python
#导入模块时，python从sys.path定义的路径下搜索模块
>>> import sys
>>> sys.path
['', '/usr/local/lib/python36.zip', '/usr/local/lib/python3.6', '/usr/local/lib/python3.6/lib-dynload', '/root/helloworld/lib/python3.6/site-packages']
>>> 
#如果希望自己编写的模块能在任意路径位置导入，可以定义pythonpath环境变量
(helloworld) [root@helloworld ydg]# mkdir /tmp/mylibs
(helloworld) [root@helloworld ydg]# cp qsort.py /tmp/mylibs/
(helloworld) [root@helloworld ydg]# export PYTHONPATH=/tmp/mylibs

```

- python将目录当成特殊的模块，称做包(在python2中，目录下必须有一个名为_\_init__.py的

### hashlib模块

- 用于计算函数的hash值

```python
>>> import hashlib
#计算123456的md5值
>>> m = hashlib.md5(b'123456')
>>> m.hexdigest()
'e10adc3949ba59abbe56e057f20f883e'

>>> m1 = hashlib.md5()
>>> m1 = udate(b'12')
>>> m1.update(b'34')
>>> m1.update(b'56')
>>> m1.hexdigest()
'e10adc3949ba59abbe56e057f20f883e'
>>> 

```

```python
import hashlib
import sys

def check_md5(fname):
    m = hashlib.md5()

    with open(fname,'rb') as  fobj:
        while 1:
            data = fobj.read(4096)
            if not data:
                break
            m.update(data)

    return m.hexdigest()

if __name__ == '__main__':
    result = check_md5(sys.argv[1])
    print(result)
```

### tarfile模块

- 用于压缩、解压缩

```python
>>> import tarfile
#压缩
>>> tar = tarfile.open('/tmp/aaa/a.tar.gz','w:gz')
>>> tar.add('/etc/hosts')
>>> tar.add('/etc/security')
#解压 
>>> tar.close()
>>> tar = tarfile.open('/tmp/aaa/a.tar.gz')
>>> tar.extractall('path=/tmp/aaa')
>>> tar.close()

```

```python
from time import strftime
import os
import tarfile
import hashlib
import pickle

def full_backup(sec,dst,md5file):
    fname = os.path.basename(src)
    fname = '%s_full_%s.tar.gz'%(fname,strftime('%Y%m%d'))
    fname =  os.path.join(dst,fname)

    tar = tarfile.open(fname,'w:gz')
    tar.add(src)
    tar.cloce()

    md5dict = {}
    for path,folders,files in os.walk(src):
        for file in files:
            key = os.path.join(path,file)
            md5dict[key] = check_md5(key)

    with open(md5file,'wb') as fobj:
        pickle.dump(md5dict,fobj)

def incr_backup(src,dst,md5file):
    fname = os.path.basename(src)
    fname = '%s_full_%s.tar.gz'%(fname,strftime('%Y%m%d'))
    fname =  os.path.join(dst,fname)

    md5dict = {}
    for path, folders, files in os.walk(src):
        for file in files:
            key = os.path.join(path, file)
            md5dict[key] = check_md5(key)

    with open(md5file,'rb') as fobj:
        old_md5 = pickle.load(fobj)

    tar = tarfile.open(fname,'w:gz')
    for key in md5dict:
        if old_md5.get(key) != md5dict[key]:
            tar.add(key)
    tar.close()
    
    with open(md5dict,'wb') as fobj:
        pickle.dump(md5dict,fobj)

if __name__ == '__main__':
    src = '/tmp/aaa/security'
    dst = '/tmp/aaa/backup'
    md5file = '/tmp/aaa/md5.data'
    if strftime('%a') == 'Mon':
        full_backup(src,dst,md5file)
    else:
        incr_backup(src,dst,md5file)
```

### OOP:面向对象编程

- 在python中，一切皆对象
- 不同的对象有不同的属性
  - 静态的属性，表现为变量
  - 动态的属性，表现为方法（函数）

```python
class Role:
    def __init__(self,name,weapon):
        #__init__是构造器的方法，创建实例时，它自动调用，一般用于将属性绑定到对象
        self.name = name
        self.weapon = weapon

    def show_me(self):
        #绑定实例是的属性，在任意方法中都直接可用
        print('我是%s,我的武器是%s'%(self.name,self.weapon))

    def say(self,words):
        #没有绑定的变量，是临时
        print(words)

if __name__ == '__main__':
    #实例化时，实例名lb将自动作为第一个参数，传给相关的方法
    lb = Role('吕布','方天画戟')
    print(lb.name,lb.weapon)
    lb.show_me()
    lb.say('马中赦免，人中龙凤')

    zf = Role('张飞','八蛇矛')
    zf.show_me()
```

### 组合

- 当俩从此类明显不同，其中一个类是另一个类的组件的时候，使用组合

```python
class Weapon:
    def __init__(self,wname,wtype,strength):
        self.wname = wname
        self.wtype = wtype
        self.strength = strength

class Role:
    def __init__(self,name,weapon):
        self.name = name
        self.weapom = weapon

if __name__ == '__main__':
    ji = Weapon('方天画戟','物理',100)
    lb = Role('吕布',ji)
    print(ji.wname,ji.wtype,ji.strength)
    print(lb.weapom.wname,lb.weapom.wtype,lb.weapom.strength)
```

### 子类继承

- 两个类有很多一致的地方，只有少部分不同，可以使用继承。经常说，父类派生子类，子类继承于父类

```python
class Role:
    def __init__(self,name,weapon):
        #__init__是构造器的方法，创建实例时，它自动调用，一般用于将属性绑定到对象
        self.name = name
        self.weapon = weapon

    def show_me(self):
        #绑定实例是的属性，在任意方法中都直接可用
        print('我是%s,我的武器是%s'%(self.name,self.weapon))

    def say(self,words):
        #没有绑定的变量，是临时
        print(words)

class Warrior(Role):
    def __init__(self,name,weapon,country):
        # Role.__init__(self,name,eapon)
        # self.name = name
        # self.weapon = weapon
        super(Warrior,self).__init__(name,weapon)
        self.country = country

    def attack(self,target):
        print('近程攻击：%s'% target)

class Mage(Role):
    def attack(self,target):
        print('远程攻击：%s'% target)

if __name__ == '__main__':
    gy = Warrior('关习习','青龙偃刀','蜀')
    km = Mage('孔明','习习扇')
    gy.show_me()
    km.show_me()
    gy.attack('吕布')
    km.attack('周瑜')
```

### 多重继承

- 子类可以有多个父类
- 子类可以继承所有父类的方法
- 查找方法的顺序是自下向上，自左向右

```python
class A:
    def func1(self):
        print('A func')

    def func4(self):
        print('A func')

class B:
    def func2(self):
        print('B func')

    def func4(self):
        print('B func')

class C(A,B):
    def func3(self):
        print('C func')

    def func4(self):
        print('C func')

if __name__ == '__main__':
    c1 = C()
    c1.func1()
    c1.func2()
    c1.func3()
    c1.func4()
```

```python
class Book:
    def __init__(self,title,author):
        self.title = title
        self.author = author

    def __str__(self):
        return '<<%s>>'% self.title

    def __call__(self,):
        print('<<%s>>是%s的编著的'% (self.title,self.author))

if __name__ == '__main__':
    py_book = Book('Python基础教程','Hetland')
    print(py_book)
    py_book()
```

## 正则表达式

```python
#给mac地址加一个冒号
192.168.1.1 000c29123456
192.168.1.2 5254A382C909
#定位，取出mac,每俩组份一组，各组间加冒号
：%S/(..)()()()()/\1\2\3\4/
```

### re模块

```python
#match从字符串开头匹配，如果匹配到，返回匹配对象，否则返回None
>>> re.match('f..','food')
<_sre.SRE_Match object; span=(0, 3), match='foo'>
>>> re.match('f..','seafood')
None
>>> re.search('f..','seafood')
<_sre.SRE_Match object; span=(3, 6), match='foo'>
>>> m = re.search('f..','seafood')
>>> m.group()#返回匹配到的内容
'foo'

>>> re.search('f..','seafood is food')#返回列表
<_sre.SRE_Match object; span=(3, 6), match='foo'>
>>> list(re.finditer('f..','seafood is food'))#finditer返回的是由匹配对象构成的生成器
[<_sre.SRE_Match object; span=(3, 6), match='foo'>, <_sre.SRE_Match object; span=(11, 14), match='foo'>]

>>> for m in re.finditer('f..','seafood is food'):
...     m.group()
... 
'foo'
'foo'

#re.split用于切割字符串
>>> re.split('-|\.','hello-world-how-are-you.tar.gz')
['hello', 'world', 'how', 'are', 'you', 'tar', 'gz']
#re.sub用于查找替换
>>> re.sub('X','tom','hi X Nice to meet you ,X')
'hi tom Nice to meet you ,tom'

#在有大量匹配的情况下，先把正则表达模式进行编译，地有更好的执行效率
>>> patt = re.compile('f..')
>>> m = patt.search('seafood')
>>> m.group()
'foo'
>>> patt.findall('seafood is food')
['foo', 'foo']

```

```python
import re

def count_patt(fname,patt):
    patt_dict = {}
    cpatt = re.compile(patt)

    with open(fname) as fobj:
        for line in fobj:
            m = cpatt.search(line)
            if m:
                key = m.group()
                patt_dict[key] = patt_dict.get(key,0) + 1

if __name__ == '__main__':
    fname = 'access_log'
    ip = '^(\d+\.){3}\d+'
    br = 'Firefox|MSIE|Chrome'
    result1 = count_patt(fname,ip)
    result2 = count_patt(fname,br)
    print(result1)
    print(result2)
```

```python
import re

class CountPatt:
    def count_patt(self,fname,patt):
        patt_dict = {}
        cpatt = re.compile(patt)
    
        with open(fname) as fobj:
            for line in fobj:
                m = cpatt.search(line)
                if m:
                    key = m.group()
                    patt_dict[key] = patt_dict.get(key,0) + 1

if __name__ == '__main__':
    fname = 'access_log'
    ip = '^(\d+\.){3}\d+'
    # br = 'Firefox|MSIE|Chrome'
    cp = CountPatt()
    result1 = cp.count_patt(fname,ip)
    # result2 = count_patt(fname,br)
    print(result1)
    # print(result2)
```

```python
import re

class CountPatt:
    def __init__(self,fname):
        self.fname = fname
        
    def count_patt(self,fname,patt):
        patt_dict = {}
        cpatt = re.compile(patt)
    
        with open(fname) as fobj:
            for line in fobj:
                m = cpatt.search(line)
                if m:
                    key = m.group()
                    patt_dict[key] = patt_dict.get(key,0) + 1
                    
        return patt_dict

if __name__ == '__main__':
    fname = 'access_log'
    ip = '^(\d+\.){3}\d+'
    # br = 'Firefox|MSIE|Chrome'
    cp = CountPatt()
    result1 = cp.count_patt(fname,ip)
    # result2 = count_patt(fname,br)
    print(result1)
    # print(result2)
```

### 字典排序

- 字典没有顺序
- 需要将字典转成列表，再排序

### 数据库的应用

### 数据库范式

- 