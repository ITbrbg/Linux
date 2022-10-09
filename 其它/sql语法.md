# sql语法

#### RDBMS-relational database management(关系型数据库管理系统)

#### 表

- 表结构
- 表记录

#### 登陆

- mysql -u root -p123 -h127.0.0.1
  - -u 用户名
  - -p 密码
  - -h IP

### sql

- 什么是sql：结构化查询语言（structured query language）

- 作用是客户端和服务器对话用的语言
- 分类
  - DDL data definition language 数据定义语言，用来 定义数据库的对象：库、表、列（创建、删除、修改）
  - DML data manipulation language 数据操作语言，用来定义数据库记录，增删改表记录
  - DCL data control language 数据控制语言，用来定义访问权限和安全级别
  - SQL data query language 数据查询语言，用来定义查询记录

#### DDL

- 数据库

  - 查看所有数据库： show databases
  - 切换（选择要操作的）数据库：use 数据库名
  - 创建数据库：create database [if not exists] mydb [charset=utf8]
  - 删除数据库： drop database [if exists] mydb
  - 修改数据库编码：alter database mydb character set utf8

- 数据类型(全类型)

  - int： 整数
  - double： 浮点数 
    - 例：double(5,2)表示最多5位，其中必须2位小数
  - decimal： 浮点型，在表单钱方面使用该类型，因为不会出现精度缺失问题
  - char ： 固定长度字符类型：char(255)
  - varchar: 可变长度字符类型：varchar(65535)
  - text(clob): 字符串类型：
    - 很小
    - 小
    - 中
    - 大

  - blob： 字节类型
    - 很小
    - 小
    - 中
    - 大

  - date： 日期类型，格式 ：yyyy-MM-dd:
  - time:  时间类型，格式：hh:mm:ss
  - timestamp：时间戳类型

- 表

  - 创建表
    - create  table [if not exists]  表名( 列名 列类型，......)

  - 查看当前数据库中所有表名称：show tables;
  - 查看指定表的创建语句：show create 表名;
  - 查看表结构：desc 表名;
  - 删除表：drop tables 表名;
  - 修改表：前缀  alter table 表名
    - 添加列：alter table 表名 add (列名 列类型，......);
    - 修改列类型：如果被修改的列已经存在数据，那么亲的列类型可能会影响到已存在的数据
      - alter table 表名 modify  列名  列类型 ;
    -  修改列名： alter table 表名 change 原列名 新列名 列类型;
    - 删除列：alter table 表名 drop 列名;
    - 修改表名：alter table 原表名 rename to 新表名;

### DML(数据操作语言，它是对表记录的操作(增，删，改)！)

- 插入数据
  - insert into 表名 (列名1，.......) values(列值1，......);
    - 在表名后边给出要插入的列名，其它没有指定的列等同与插入null值，所以插入记录总是插入一行，不可能是半行。
    - 在values后给出列的值，值的顺序和个数必须与前面指定的列对应。
  - insert into 表名 values (列值1，......);
    - 没有给出插入的列，那么表示插入所有列。
    - 值的个数必须是该列的个数
    - 值的顺序，必须与表创建时给出的顺序相同
- 修改数据
  - update 表名 set 列名1=列值1，...... [where 条件];
  - 条件
    - 条件必须是一个boolean类型的值或表达式：
    - 运算符：=、!=、<>、>、<、>=、<=、between ... and、in (...)、is null(不能写等于null，=null永远都是false)、not、or、and

- 删除数据
  - delete from 表名 [where 条件];
  - truncate table 表名：truncate是DDL语句，它是先删除drop该表，再create该表，而且无法回滚。

#### DCL

- 创建用户
  - create user 用户名@IP地址 identified by '密码';
    - IP:用户只能在指定的IP地址登陆
    - %：用户可以在任意地址登陆
- 给用户授权
  - grant 权限1,......  on 数据库.表 to 用户名@IP地址;

- 撤销授权
  - revoke 权限1,...... on 数据库.表 from 用户名@IP地址;

- 查看授权
  - show grant for 用户名@IP地址;

- 删除用户
  - drop user 用户名@IP地址;

#### DQL

#### 一、基本查询

- 字段(列)控制

  - 查询所有：select * from 表名;

    - *：表示查询所有列

  - 查询指定列：select [列1，列2，......] from  表名;

  - 完全重复的只记一次：

    - select disitinct *  [列1，......]  from 表名;

  - 列运算

    - 数量类型的可以做加、减、乘、除运算
      - select 列1*1.5 from 表;
- 字符串类型可以做连续运算
      - select concat('$',列名) from 表;
    - 转换null值：有时候要把null转换成其它值
      - select ifnull(列，0)+100 from 表;  列为空则转换成0再加100。
    - 给列起别名：当使用列运算后，查询出的结果集中列名称很不好看，这时我们需要给列起个别名，这样在结果集中列名就显示别名。
      - select ifnull(列1,0)+1000 as 奖金 from 表;
      - 注：as可以省略。
  
  - 条件控制
    - 条件查询：与前面介绍的update和delete一样，select语句也可以使用where子句来控制记录。
    - 模糊查询：当你想查询姓张的，并且姓名一共有俩个字的员工时，这时就可以使用模糊查询
      - select * from 表 where like '张—';
      - 模糊查询需要运算符：like ,其中—(下划线)匹配任意一个字符，注只能匹配一个面不是多个
      - 如果我们查询姓张的，名字不确定时可以把下划线改成%，%可以匹配多个字符
  
  #### 二、排序
  
  - 升序：select * from  表 order by 字段 ASC  ;
    - 按字段排序
    - ASC可以省略的
  - 降序：select * form  表 order by 字段 DESC;
    - 其中DESC不能省略
  - 使用多列作为排序条件
    - select * from 表 order by 列1 [asc,desc],列二 [asc,desc] ,......;

#### 三、聚合函数：用来表示某列的纵向运算

- count(统计行数)
  - select count(*) from 表;    ;    表中所有列都不为null的行数
  - select count(字段1) from 表; 表中字段1列不为空的行数据
- max
  - select max(字段) from 表; 字段的最大值
- min 
- sum
- avg

#### 四、分组查询

- 分组查询是把记录使用某一列进行分组，然后查询组信息(分组列、聚合函数)
  - select 字段， from 表 group by  字段;

#### 五、limit子句(mysql)

- limit用来限定查询结果的起始行，以及总行数
  - select * from 表 limit 4,3;
  - 表示第5行开始，向后查询三行，注编号从0开始



