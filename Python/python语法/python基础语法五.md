# python基础语法四

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

