# JAVA

### 计算机软件

- 系统软件：DOS(Disk Operating System)
- 应用软件：office

### 软件开发

- 软件
  - 按照特定顺序组织的计算机数据和指令的集合
- 开发
  - 软件的制作过程
- 软件开发
  - 借助开发工具与计算机语言制作软件

---

### 计算机语言

- 人与计算机之间进行信息交流沟通的一种特殊的语言
- 有字符，符号等等
- 常见的有C、C++、C#、java、python、go、ruby、php等等

---

### 人机交互

- 软件的出现实现了人与计算机这间更好的交互
- 交互方式
  - 图形化界面：这种方式简单直观，使用者易于接受，容易上手操作
  - 命令行方式：需要一上控制台，输入特定的指令，让计算机完成操作，较为麻烦，需要记住一些命令

---

### 键盘功能键介绍

- Tab
- Shift  Ctrl   Alt
- 空格 Enter
- Window
- 上下左右
- PrtSc（Print Screen） 屏幕截图

### 键盘快捷键介绍

- Ctrl+A 全选
- Ctrl+C 复制
- Ctrl+V 粘贴
- Ctrl+X 剪切
- Ctrl+Z 撤销
- Ctrl+S 保存

---

### 常用的DOS命令

- d：回车 盘符切换
- dir(directory):列出当前目录下的文件及文件夹
- md(make directory):创建目录
- rd(remove directory):删除目录
- cd(change directory):改变指定目录
- cd..:回到上一级目录
- cd \:退回到根目录
- del(delete): 只能删除文件，骑白马的不一定是王子，还有可能是唐僧
- exit: 退出DOS命令行
- cls(clear screen):清屏
- notepad:笔记本
- mspaint 画图

---

### Java语言平台版本

- J2SE（Java 2 Platform Standard Edition）
- J2ME（Java 2 Platform Micro Edition）
- J2EE （Java 2 Platform Enterprise Edition）

### Java语言的特点

- 简单性
- 面向对象
- 分布式处理
- 健壮性
- 结构中立
- 开源
- 跨平台
  - 通过Java语言编写的应用程序在不同的系统平台上都可以运行
  - 只要大需要运行Java应用程序的操作系统上，先安装一上Java虚拟机（Java Virtual Machine）即可，由JVM来负责程序在系统中的运行
- 解释性
- 高性能
- 多线程
- 动态
- 安全性

---

### JRE和JDK

- JRE（Java Runtime Environment）
  - 包括Java虚拟机和Java程序所需要的核心类库等。
- JDK（Java Development Kit）
  - JDK是提供给Java开发人员用的，其中包含了Java的形式发工具，也包括了JRE，所以安装了JDK，就不用在单独安装JRE了，其中的形式发工具：编译工具（Javac.exe）打包工具（Jar.exe）等

- 使用JDK开发完成的Java程序，交给JRE去运行，由JVM保证跨平台

### Java开发工具

- Notepad
- notepad++
- Eclipse
- MyEclipse

---

### 程序解析

- 首先定义一上类
  - class类名

- 在类定义后加上一对大括号
  - {}

- 在大括号中间添加一上主（main）方法/函数
  - public static void main(String[] args) {}

- 在主方法的大括号中间添加一行输出语句
  - System.out.println("HelloWorld");

```java 
class HelloWorld {
	public static void main(String[] args) {
		System.out.println("HelloWorld");
	}
}
```

1. 首先写一个Java源代码程序，扩展名为.Java
2.  在命令行模式中，输入Javac命令对源代码进行编译，生成字节码文件
   - javac 源文件名.java

3. 编译完成后，如果没有报错信息，输入java命令对class字节码文件进行解释运行，执行时不需要添加.class扩展名
   - java  Demo

### 运行与工作原理

```mermaid
graph LR 
A[Java源代码]-->|javac|B[Java字节码文件]
B-->|java|C[运行结果]
```

### 常见问题

- 扩展名被隐藏
  - 如何拭到：工具-->文件夹选项-->查看-->去除隐藏扩展名那上勾

- 我要求文件名称和类名一致，实际上不这样做也是可以的，但是要注意
  - javac后面根的是文件名+扩展名
  - java后面跟的类名不带扩展名

- Java语言严格区分大小写，还有就是单词不要写错
- 非法字符：肯定是中英方问题，我们程序标点符号要求全是英文
- 括号都是成对出现的
- 主方法的格式问题

---

### path环境变量的作用

- 程序的执行需要使用外部命令javac，但是javac指令仅仅能在JDK安装目录下的bin目录下的时候，因此程序只能写入bin目录
- 程序开发过程中，不能将源代码写入到JDK的安装目录，因此需要将源代码保存到任意位置的指定目录（英文目录 ），所以需要使javac指令 在任意目录下可以运行。

- path环境变量配置方式

  - 能过配置path环境变量，将javac指令所在的目录，也就是JDk安装目录下的bin目录配置到path变量下，即可使javac指令在任意目录 下运行
    - win7,win8系统，右键点击桌面计算机-->选择属性-->选择高级系统设置-->选择高级选项卡-->点击环境变量-->下方系统变量中查找path-->双击path
    - XP系统右键点击桌面计算机-->选择属性-->选择高级选项卡-->点击环境变量-->下方系统变量中查找path-->双击path
    - 将JDk安装目录下的bin目录添加到最左边并加上分号

  - path环境变量的参照形式配置方式

    - 创建新的变量名称：JAVA_HOME
    - 为JAVA_HOME添加变量值：JDK的安装目录
    - 将path环境变量中JDK目录修改
      - %JAVA_HOME%\bin;

    - path环境变量具有先后顺序

  - classpath环境变量的配置方法
    - 创建新的变量名称：classpath
    - 值设定为指定的还有class文件的目录，多个目录间用（ ;）分割
    - 作用；使classpath目录中的.class文件可以在任意目录运行
    - 技巧：通常将配置的目录最前同加.配置，即便当前目录，使.class文件搜索时首先搜索当前目录，然后根据目录配置的顺序依次查找，找到后即运行，因此classpath目录中配置存在先后顺序。

- path环境变量和classpath环境变量的区别
  - path环境变量里边记录的是可执行性文件，如exe结尾的，对可执行性文件先在当前路径去找，如果没有就去path变量中配置的路径去找
  - classpath环境变量里记录的是java类的运行文件所在的目录