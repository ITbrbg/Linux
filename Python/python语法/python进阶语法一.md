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



