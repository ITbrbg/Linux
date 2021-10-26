# python基础语法二

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
