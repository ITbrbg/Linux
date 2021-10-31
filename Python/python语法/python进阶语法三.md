## python进阶语法三

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

