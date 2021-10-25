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









