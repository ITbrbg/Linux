## python进阶语法二

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

