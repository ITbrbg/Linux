# java03

- 注意

  - 在定义long和float类型的变量的时候，要加上**L或者f**
    - 整数型默认是int类型，浮点数默认是double

  - bytet和short在定义的时候，他们接收的其实是一个int类型的数值
    - 这个是自己做了一个数据检测的，如果不在他们范围内就报错

  - byte值的问题

```java
byte b1 = 127;
byte b2 = 128; //-128
byte b3 = 129; //-127
byte b4 = 130; //-126

//byte值的范围是-128 ~ 127
128 10000000
-128 1000000 （这里的1即是符号位也是数值位）
```

- 数据转换类型的默认转换

  - byte,short,char--int--long--float--double
    - long:8个字节
    - float：4个字节

  - 他们的底层存储结构不同
  - float表示的数据范围比long的范围要大
    - long：2<sup>63</sup>-1
    - float:3.4*10<sup>38</sup> > 2 \*10<sup>38</sup> = 2\*2\*3<sup>38</sup> = 2\*2<sup>114</sup> >2\*<sup>63</sup> - 1

```java
float类型数字在计算机中用4个字节存储。遵循IEEE-754格式标准：
	一个浮点数有2部分组成：底数m和指数e

底数部分 使用二进制数来表示此浮点数的实际值
指数部分 占用8bit的二进制数，可表示数值范围为0-255

但是指数可正可负，所以，IEEE规定，此处算出的次方必须减去127才是真正的指数。
	所以，float类型的指数可从-126到128

底数部分实际是占用24bit的一个值，但是最高位始终为1，所以，最高位省去不存储，在存储中占23bit
	科学计数法。

格式：
SEEE EEEE EMMM MMMM MMMM MMMM MMMM MMMM
S表示浮点数正负    
E指数加上127后的值得二进制数据
M底数

举例：
17.625在内存中的存储

首先要把17.625换算成二进制：10001.101

	整数部分，除以2，直到商为0，余数反转。
	小数部分，乘以2，直到乘位0，进位顺序取。

在将10001.101右移，直到小数点前只剩1位：
	1.0001101 * 2^4 因为右移动了四位

这个时候，我们的底数和指数就出来了
底数：因为小数点前必为1，所以IEEE规定只记录小数点后的就好。所以，此处的底数为：0001101
指数：实际为4，必须加上127(转出的时候，减去127)，所以为131。也就是10000011
符号部分是整数，所以是0
综上所述，17.625在内存中的存储格式是：
01000001 10001101 00000000 00000000	

换算回去：自己做。

```



| 优先级 | 描述         | 运算符                  |
| ------ | ------------ | ----------------------- |
| 1      | 括号         | ()、[]                  |
| 2      | 正负号       | +、-                    |
| 3      | 自增自减，非 | ++、--、!               |
| 4      | 乘除，取余   | *、/、%                 |
| 5      | 加减         | +、-                    |
| 6      | 移位运算     | <<、>>、>>>             |
| 7      | 大小关系     | >、>=、<、<=            |
| 8      | 相等关系     | ==、!=                  |
| 9      | 按位与       | &                       |
| 10     | 按位异或     | ^                       |
| 11     | 按位或       | \|                      |
| 12     | 逻辑与       | &&                      |
| 13     | 逻辑或       | \|\|                    |
| 14     | 条件运算     | ?:                      |
| 15     | 赋值运算     | =、+=、-=、*=、/=、%=   |
| 16     | 位赋值运算   | &=、\|=、<<=、>>=、>>>= |

### 运算符

---

| 算术运算符 |
| :--------: |
| 赋值运算符 |
| 比较运算符 |
| 逻辑运算符 |
|  位运算符  |
| 三目运算符 |

- #### 算术运算符

| 运算符 |    运算    |    范例    |  结果   |
| :----: | :--------: | :--------: | :-----: |
|   +    |    正号    |     +1     |    1    |
|   -    |    负号    |  b=4;-b;   |   -4    |
|   +    |     加     |    5+5     |   10    |
|   -    |     减     |    6-4     |    2    |
|   \*   |     乖     |    3*4     |   12    |
|   /    |     除     |    5/5     |    1    |
|   %    |    取模    |    5%5     |    0    |
|   ++   | 自增（前） | a=2;b=++a; | a=3;b=3 |
|   ++   | 自增（后） | a=2;b=a++; | a=3;b=2 |
|   --   | 自减（前） | a=2;b=--a  | a=1;b=1 |
|   --   | 自减（后） | a=2;b=a--  | a=1;b=2 |
|   +    | 字符串相加 | "he"+"llo" | "hello" |

```java
/*
	运算符：
		就是对常量和变量进行操作的符号。
		
	分类：算术运算符，赋值运算符，比较运算符，逻辑运算符，位运算符，三目运算符

	算术运算符：
		+,-,*,/,%,++,--
		
	注意事项：
		A:整数相除只能得到整数。如果想得到小数，必须把数据变化为浮点数类型
		B:/获取的是除法操作的商，%获取的是除法操作的余数
*/

class OperatorDemo {
	public static void main(String[] args) {
		//定义变量
		int x = 3;  //把3赋值给int类型的变量x
		int y = 4;
		
		System.out.println(x+y);
		System.out.println(x-y);
		System.out.println(x*y);
		System.out.println(x/y); //整数相除只能得到整数
		
		//我就想得到小数，该肿么办呢?
		//只需要把操作的数据中任意的一个数据变为浮点数
		System.out.println(x*1.0/y);
		
		//%的应用
		System.out.println(x%y); //得到的是余数
	}
}
```

```java
/*
	++,--运算符的使用：
		单独使用：
			放在操作数的前面和后面效果一样。(这种用法是我们比较常见的)
		参与运算使用：
			放在操作数的前面，先自增或者自减，然后再参与运算。
			放在操作数的后面，先参与运算，再自增或者自减。
			
	作用：就是对变量进行自增1或者自减1。
*/
class OperatorDemo2 {
		public static void main(String[] args) {
			//定义两个变量
			int x = 3;
			int y = 4;
			
			//字符串的拼接
			//System.out.println("x:"+x);
			//System.out.println("y:"+y);
			
			System.out.println("x:"+x+",y:"+y);
			
			//单独使用
			//x++;
			//y--;
			++x;
			--y;
			//System.out.println(x);
			System.out.println("x:"+x+",y:"+y);
			
			//意外的类型,常量是不可以这样做的
			//System.out.println(10++);
			
			System.out.println("-------------------");
			//参与运算使用
			int a = 3;
			int b = 4;
			
			//int c = a++;
			//int d = b--;
			
			int c = ++a;
			int d = --b;
			
			System.out.println("a:"+a); //4, 4
			System.out.println("b:"+b); //3, 3
			System.out.println("c:"+c); //3, 4
			System.out.println("d:"+d); //4, 3
		}
}
```

```java
/*
	+的用法：
		A:加法
		B:正号
		C:字符串连接符
*/
class OperatorDemo3 {
	public static void main(String[] args) {
		//加法
		System.out.println(3+4);
		
		//正号
		System.out.println(+4);
		
		System.out.println('a');
		System.out.println('a'+1); //这里是加法
		
		//字符串连接符
		System.out.println("hello"+'a'+1);
		System.out.println('a'+1+"hello");
	}
}
```

```java
/*
	++,--的练习题
	
	第一题：
	int a = 10;
	int b = 10;
	int c = 10;

	a = b++;
	c = --a;
	b = ++a;
	a = c--;
	请分别计算出a,b,c的值
	
	第二题：
	int x = 4;
	int y = (x++)+(++x)+(x*10);
	请分别计算出x,y的值
*/
class OperatorTest {
	public static void main(String[] args) {
		int a = 10;
		int b = 10;
		int c = 10;

		a = b++; //a=10,b=11,c=10
		c = --a; //a=9,b=11,c=9
		b = ++a; //a=10,b=10,c=9
		a = c--; //a=9,b=10,c=8
		
		System.out.println("a:"+a);
		System.out.println("b:"+b);
		System.out.println("c:"+c);
		System.out.println("--------------");
		
		int x = 4;
		int y = (x++)+(++x)+(x*10);
		//4+6+60
		//x=5,6
		
		System.out.println("x:"+x);
		System.out.println("y:"+y);
	}
}
```

#### 赋值运算符

---

- 符号 
  - = += -= \*= /= %=
  - =为基本运算符，其他的为扩展运算符
    - 扩展的运算符隐含了一个强制的类型转换

```java
/*
	赋值运算符：
		基本的赋值运算符：=
			把=右边的数据赋值给左边。
			
		扩展的赋值运算符：+=,-=,*=,/=,%=
			+= 把左边和右边做加法，然后赋值给左边。
*/
class OperatorDemo {
	public static void main(String[] args) {
		//定义一个变量
		int x = 10;
		
		//其他用法
		int a,b; 
		a = b = 10;
		System.out.println(a); 
		System.out.println(b);
		System.out.println("-----------");

		//定义一个变量
		int y = 10;
		
		y += 20;
		
		System.out.println(y);
		
	}
}
--------------------------------------------------------
    /*
	面试题：
		short s=1;s = s+1; 
		
		short s=1;s+=1;
		上面两个代码有没有问题，如果有，那里有问题。
		
		为什么第二个木有问题呢?
			扩展的赋值运算符其实隐含了一个强制类型转换。
			
			s += 1;
			不是等价于 s = s + 1;
			而是等价于 s = (s的数据类型)(s + 1);
*/
class OperatorTest {
	public static void main(String[] args) {
		//short s = 1;
		//s = s + 1;
		//System.out.println(s);
		
		short s = 1;
		s += 1; //好像是 s = s + 1;
		System.out.println(s);
	}
}
```

#### 关系运算符

---

- == ！= > < >= <= instanceof(检查是否是类的对象)
  - 比较运算符的结果都是boolean型，也就是要么true要么false
  - 比较运算符的==不能写成=

```java
/*
	比较运算符：
		==,!=,>,>=,<,<=
		
	特点：
		无论你的操作是简单还是复杂，结果是boolean类型。
		
	注意事项：
		"=="不能写成"="。
*/
class OperatorDemo {
	public static void main(String[] args) {
		int x = 3;
		int y = 4;
		int z = 3;
	
		System.out.println(x == y);
		System.out.println(x == z);
		System.out.println((x+y) == (x+z));
		System.out.println("------------");
		
		System.out.println(x != y);
		System.out.println(x > y);
		System.out.println(x >= y);
		System.out.println(x < y);
		System.out.println(x <= y);
		System.out.println("------------");
		
		int a = 10;
		int b = 20;
		
		//boolean flag = (a == b);
		//boolean flag = (a = b); //这个是有问题的，不兼容的类型
		//System.out.println(flag);
		
		int c = (a = b); //把b赋值给a，然后把a留下来
		System.out.println(c);
	}
}
```

#### 逻辑运算符

---

-  & | ^  !  && ||
- 逻辑运算符用于连接boolean型 的表达式，在java中不可以写成3<x<6,应该写成x>3&x<6
- &和&&的区别
  - &时，左边无论真假，右边都得进行运算
  - &&时，如果左边真，右边参与运算，如果左边假，那么右边不参与运算
  - |和||的区别同理，||时，左边为真，右边不参与运算，

- ^和|的不同之处是：当左右都true时，结果为false

```java
/*
	逻辑运算符：
		&,|,^,!
		&&,||
		
	特点：
		逻辑运算符一般用于连接boolean类型的表达式或者值。
			
		表达式：就是用运算符把常量或者变量连接起来的符合java语法的式子。
			算术表达式：a + b
			比较表达式：a == b
			
	结论：
		&逻辑与:有false则false。
		|逻辑或:有true则true。
		^逻辑异或:相同为false，不同为true。
			举例：情侣关系。男男,男女,女男,女女
		!逻辑非:非false则true，非true则false。
			特点：偶数个不改变本身。
*/
class OperatorDemo {
	public static void main(String[] args) {
		int a = 3;
		int b = 4;
		int c = 5;
		
		//&逻辑与
		System.out.println((a > b) & (a > c)); //false & false = false
		System.out.println((a > b) & (a < c)); //false & true = false
		System.out.println((a < b) & (a > c)); //true & false = false
		System.out.println((a < b) & (a < c)); //true & true = true
		System.out.println("---------------");
		
		//|逻辑或
		System.out.println((a > b) | (a > c)); //false | false = false
		System.out.println((a > b) | (a < c)); //false | true = true
		System.out.println((a < b) | (a > c)); //true | false = true
		System.out.println((a < b) | (a < c)); //true | true = true
		System.out.println("---------------");
		
		//^逻辑异或
		System.out.println((a > b) ^ (a > c)); //false ^ false = false
		System.out.println((a > b) ^ (a < c)); //false ^ true = true
		System.out.println((a < b) ^ (a > c)); //true ^ false = true
		System.out.println((a < b) ^ (a < c)); //true ^ true = false
		System.out.println("---------------");
		
		//!逻辑非
		System.out.println(!(a > b)); //!false = true
		System.out.println(!(a < b)); //!true = false
		System.out.println(!!(a > b)); //!!false = false
		System.out.println(!!!(a > b)); //!!false = true
	}
}
------------------------------------------------------------------
/*
	&&和&的区别? 同理||和|的区别?
		A:最终结果一样。
		B:&&具有短路效果。左边是false，右边不执行。
		
	开发中常用的逻辑运算符：
		&&,||,!
*/
class OperatorDemo2 {
	public static void main(String[] args) {
		int a = 3;
		int b = 4;
		int c = 5;
		
		//&&双与
		System.out.println((a > b) && (a > c)); //false && false = false
		System.out.println((a > b) && (a < c)); //false && true = false
		System.out.println((a < b) && (a > c)); //true && false = false
		System.out.println((a < b) && (a < c)); //true && true = true
		System.out.println("----------------");
		
		int x = 3;
		int y = 4;
		
		//boolean b1 = ((x++ == 3) & (y++ == 4));
		//boolean b1 = ((x++ == 3) && (y++ == 4));
		//boolean b1 = ((++x == 3) & (y++ == 4));
		boolean b1 = ((++x == 3) && (y++ == 4));
		System.out.println("x:"+x);
		System.out.println("y:"+y);
		System.out.println(b1);
	}
} 
```

#### 位运算

---

| 运算符 |    运算    |         范例         |
| :----: | :--------: | :------------------: |
|   <<   |    左移    | 3<<2=12-->3\*2\*2=12 |
|  \>>   |    右移    |    3>>1=1-->3/2=1    |
|  \>>>  | 无符号右移 |   3>>>1=1-->3/2=1    |
|   &    |   与运算   |        6&3=2         |
|   \|   |   或运算   |        6\|2=7        |
|   ^    |  异或运算  |        6^3=5         |
|   ~    |    反码    |        ~6=-7         |

```java
/*
	位运算符：
		&,|,^,~
		<<,>>,>>>
		
	注意：
		要做位运算，首先要把数据转换为二进制。
*/
class OperatorDemo {
	public static void main(String[] args) {
		//&,|,^,~
		
		int a = 3;
		int b = 4;
		
		System.out.println(3 & 4);
		System.out.println(3 | 4);
		System.out.println(3 ^ 4);
		System.out.println(~3);
	}
}
/*
	分析：因为是位运算，所以我们必须先把数据换算成二进制。
	
	3的二进制：11
		00000000 00000000 00000000 00000011
	4的二进制：100
		00000000 00000000 00000000 00000100
	
	&位与运算：有0则0。
		00000000 00000000 00000000 00000011
	   &00000000 00000000 00000000 00000100
		-----------------------------------
		00000000 00000000 00000000 00000000
		结果是：0
		
	|位或运算：有1则1。
		00000000 00000000 00000000 00000011
	   |00000000 00000000 00000000 00000100
		-----------------------------------
		00000000 00000000 00000000 00000111
		结果是：7
		
	^位异或运算：相同则0，不同则1。
		00000000 00000000 00000000 00000011
	   &00000000 00000000 00000000 00000100
		-----------------------------------
		00000000 00000000 00000000 00000111
		结果是：7
		
	~按位取反运算符：0变1，1变0
		00000000 00000000 00000000 00000011
	   ~11111111 11111111 11111111 11111100 (补码)
	   
	   补码：11111111 11111111 11111111 11111100
	   反码：11111111 11111111 11111111 11111011
	   原码：10000000 00000000 00000000 00000100
		结果是：-4
*/
-------------------------------------------------------
/*
	^的特点：一个数据对另一个数据位异或两次，该数本身不变。
*/
class OperatorDemo2 {
	public static void main(String[] args) {
		int a = 10;
		int b = 20;
		
		System.out.println(a ^ b ^ b); //10
		System.out.println(a ^ b ^ a); //20
	}
}
-------------------------------------------------------
/*
	<<:左移	左边最高位丢弃，右边补齐0
	>>:右移	最高位是0，左边补齐0；最高为是1，左边补齐1
	>>>:无符号右移 无论最高位是0还是1，左边补齐0
	
	面试题：
		请用最有效率的方式写出计算2乘以8的结果?
			2 * 8
			
			2 << 3

*/
class OperatorDemo3 {
	public static void main(String[] args) {
		//<< 把<<左边的数据乘以2的移动次幂
		System.out.println(3 << 2); //3*2^2 = 3*4 = 12;
	
		//>> 把>>左边的数据除以2的移动次幂
		System.out.println(24 >> 2); //24 / 2^2 = 24 / 4 = 6
		System.out.println(24 >>> 2);
		
		System.out.println(-24 >> 2); 
		System.out.println(-24 >>> 2);
	}
}
/*
	计算出3的二进制：11
		00000000 00000000 00000000 00000011
	(00)000000 00000000 00000000 0000001100
		
	>>的移动：	
	计算出24的二进制：11000
		原码：10000000 00000000 00000000 00011000
		反码：11111111 11111111 11111111 11100111
		补码：11111111 11111111 11111111 11101000
		
		11111111 11111111 11111111 11101000
		1111111111 11111111 11111111 111010(00) 补码
		
		补码：1111111111 11111111 11111111 111010
		反码：1111111111 11111111 11111111 111001
		原码：1000000000 00000000 00000000 000110
		
		结果：-6
		
	>>>的移动：
		计算出24的二进制：11000
		原码：10000000 00000000 00000000 00011000
		反码：11111111 11111111 11111111 11100111
		补码：11111111 11111111 11111111 11101000
		
		11111111 11111111 11111111 11101000
		0011111111 11111111 11111111 111010(00)
		
		结果：
*/
--------------------------------------------------
/*
	面试题：
		请自己实现两个整数变量的交换
		注意：以后讲课的过程中，我没有明确指定数据的类型，默认int类型。
*/
class OperatorTest {
	public static void main(String[] args) {
		int a = 10;
		int b = 20;
		
		System.out.println("a:"+a+",b:"+b);
		
		//方式1：使用第三方变量(开发中用的)
		/*
		int c = a;
		a = b;
		b = c;
		System.out.println("a:"+a+",b:"+b);
		System.out.println("------------");
		*/
		
		//方式2：用位异或实现(面试用)
		//左边：a,b,a
		//右边：a ^ b
		/*
		a = a ^ b;
		b = a ^ b; //a ^ b ^ b = a
		a = a ^ b; //a ^ b ^ a = b
		System.out.println("a:"+a+",b:"+b);
		*/
		
		//方式3：用变量相加的做法
		/*
		a = a + b; //a=30
		b = a - b; //b=10
		a = a - b; //a=20
		System.out.println("a:"+a+",b:"+b);
		*/
		
		//方式4：一句话搞定
		b = (a+b) - (a=b); //b=30-20=10,a=20
		System.out.println("a:"+a+",b:"+b);
	}
}
```

#### 三目运算符

---

- 格式
  - （关系表达式）？表达式1：表达式2：
  - 如果条件为true，运算后的结果表达式为1：
  - 如果条件为false，运算后的表达式为2：、

```java
/*
	单目运算符：~3
	双目运算符：3 + 4

	三目运算符：
		格式：比较表达式?表达式1:表达式2;
		
		比较表达式:结果是一个boolean类型。
		
		执行流程：
			根据比较表达式的计算返回一个true或者false。
			如果是true，就把表达式1作为结果。
			如果是false，就把表达式2作为结果。
*/
class OperatorDemo {
	public static void main(String[] args) {
		int x = 100;
		int y = 200;
		
		int z = ((x > y)? x: y);
		
		//int z = ((x < y)? x: y);
		
		//int z = ((x == y)? x: y);
		
		//报错
		//int z = ((x = y)? x : y);
		
		System.out.println("z:"+z);
	}
}
-------------------------------------
/*
	练习：
		获取两个整数中的最大值
		获取三个整数中的最大值
		比较两个整数是否相同
*/
class OperatorTest {
	public static void main(String[] args) {
		//获取两个整数中的最大值
		int x = 100;
		int y = 200;
		
		int max = (x > y? x: y);
		System.out.println("max:"+max);
		System.out.println("--------");
		
		//获取三个整数中的最大值
		int a = 10;
		int b = 30;
		int c = 20;
		
		//分两步：
		//A:先比较a,b的最大值
		//B:拿a,b的最大值在和c进行比较
		int temp = ((a > b)? a: b);
		//System.out.println(temp);
		int max1 = (temp > c? temp: c);
		System.out.println("max1:"+max1);
		
		//一步搞定
		//int max2 = (a > b)?((a > c)? a: c):((b > c)? b: c);
		//这种做法不推荐。
		//int max2 = a > b?a > c? a: c:b > c? b: c;
		//System.out.println("max2:"+max2);
		System.out.println("--------");
		
		//比较两个整数是否相同
		int m = 100;
		int n = 200;
		
		//boolean flag = (m == n)? true: false;
		boolean flag = (m == n);
		System.out.println(flag);
	}
}
```

#### 键盘录入数据

- 概念
  - 我们目前在写程序的时候，数据值是固定的，但是在实际开发中，数据值肯定是变化的，所以，我们准备把数据改成键盘录入，提高程序的灵活性。

- 如何实现？

  - 导包（位置放到class定义的上面）
    - import java.util.Scaner
  - 创建对象
    - Scanner sc=new Scanner(System.in)

  - 接收数据
    - int x = sc.nextint();

```java
/*
	为了让程序的数据更符合开发的数据，我们就加入了键盘录入。
	让程序更灵活一下。
	
	那么，我们如何实现键盘数据的录入呢?
		A:导包
			格式：
				import java.util.Scanner; 
			位置：
				在class上面。
		B:创建键盘录入对象
			格式：
				Scanner sc = new Scanner(System.in);
		C:通过对象获取数据	
			格式：
				int x = sc.nextInt();
*/
import java.util.Scanner;

class ScannerDemo {
	public static void main(String[] args) {
		//创建键盘录入数据对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请你输入一个数据：");
		int x = sc.nextInt();
		
		System.out.println("你输入的数据是："+x);
	}
}
------------------------------------------------------
/*
	键盘录入练习：
		键盘录入两个数据，并对这两个数据求和，输出其结果
*/
import java.util.Scanner;

class ScannerTest {
	public static void main(String[] args) {
		//键盘录入两个数据，并对这两个数据求和，输出其结果
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入第一个数据：");
		int x = sc.nextInt();
		
		System.out.println("请输入第二个数据：");
		int y = sc.nextInt();
		
		//把键盘录入的数据进行相加即可
		int sum = (x + y);
		System.out.println("sum:"+sum);
	}
}
-------------------------------------------------------------
/*
	键盘录入练习：键盘录入两个数据，获取这两个数据中的最大值
*/

import java.util.Scanner;

class ScannerTest2 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入第一个数据：");
		int a = sc.nextInt();
		
		System.out.println("请输入第二个数据：");
		int b = sc.nextInt();
		
		//获取这两个数据中的最大值
		int max = (a > b? a: b);
		System.out.println("max:"+max);
	}
}
-------------------------------------------------------------
/*
	练习：
		键盘录入三个数据，获取这三个数据中的最大值
		键盘录入两个数据，比较这两个数据是否相等
*/
import java.util.Scanner;

class ScannerTest3 {
	public static void main(String[] args) {
		//键盘录入三个数据，获取这三个数据中的最大值
	
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入第一个数据：");
		int a = sc.nextInt();
		
		System.out.println("请输入第二个数据：");
		int b = sc.nextInt();
		
		System.out.println("请输入第三个数据：");
		int c = sc.nextInt();
		
		//获取这三个数据中的最大值
		int temp = ((a > b)? a: b);
		int max = (temp > c? temp : c);
		System.out.println("max:"+max);
		System.out.println("------------------");
		
		//键盘录入两个数据
		System.out.println("请输入第一个数据：");
		int x = sc.nextInt();
		
		System.out.println("请输入第二个数据：");
		int y = sc.nextInt();
		
		//比较这两个数据是否相等
		boolean flag = (x == y);
		System.out.println("flag:"+flag);
	}
}
```

#### 流程控制语句

----



- 在程序的执行过程中，各条语句的执行顺序对程序的执行结果是有直接影响的。也就是说程序的流程 对运行的结果有影响。所以我们必须清楚的知道每条语句的执行流程。而且，很多时候我们要通过控制语句的执行顺序来实现我们要完成的功能。

- 流程控制语句的分类

  - 顺序结构

    - 是程序中最简单最基本的流程控制，没有特定的语法结构，按照代码的先后顺序依次执行，程序中大多数的代码都是这么执行的。
    - 总的来说：写在前面的先执行，写在后面的后执行

  - 选择结构

    - 也被称为分支结构

    - 选择结构有特定的语法规则，代码要执行具体的逻辑运算进行判断，逻辑运算的结果有俩个，所以产生选择，按照不同的选择不同的代码

    - java语言提供了俩种选择结构的语句

      - if语句

        - if语句有三种格式

          ```java
          //第一种
          if () {
              语句体
          }
          //第二种
          if() {
              语句体1;
          }else{
              语句体2;
          }
          //第三种
          if(表达式1) {
              语句体1;
          }else if(表达式2) {
              语句体2;
          }
          ....
          else {
              语句体n+1;
          }
          ```

        - 执行流程
          - 首先看其着么表达式看其结果是true还是false
          - 如果是true就执行语句体
          - 如果是false就不执行语句体
          - else后面是没有比较表达式的

        - 注意事项
          - 关系表达式无论简单还是复杂，结果必须为boolean类型
          - if 语句控制体如果是一条语句，大括号可以省略，如果是多条语句，就能省略，建议永远不要省略
          - 一般来说：有左大括号就没有分号，有分号就没有大括号
          - 我们前面讲过三元运算符，它根据比较判断后，给出的也是俩个结果，所以这种情况和if的第二种情况相似，它们在某些情况下是可以相互转换的
            - 三元运算符都可以使用if语句改进，反之不成立 
            - 什么时候不成立 
              - 当if控制语句是一条控制语句时候，就不成立 ，因为三元运算符是一个运算符，必须要求一个结果返回，而输出诗句却不能够做为一个返回结果

      -  switch语句

  - 循环结构

```java
/*
	流程控制语句：可以控制程序的执行流程。
	
	分类：
		顺序结构
		选择结构
		循环结构
		
	顺序结构：
		从上往下，依次执行。
*/
class ShunXuJieGouDemo {
	public static void main(String[] args) {
		System.out.println("程序开始了");
		
		System.out.println("我爱Java");
		
		System.out.println("程序结束了");
	}
}
```

```java
/*
	选择结构：
		if语句
		switch语句
		
	if语句：
		格式1
		格式2
		格式3
		
	if语句的格式：
		if(比较表达式) {
			语句体;
		}
		
		执行流程：
			先计算比较表达式的值，看其返回值是true还是false。
			如果是true，就执行语句体；
			如果是false，就不执行语句体；
*/
class IfDemo {
	public static void main(String[] args) {
		int x = 10;
		
		if(x == 10) {
			System.out.println("x等于10");
		}
		
		if(x == 20) {
			System.out.println("x等于20");
		}
		
		System.out.println("over");
	}
}
-------------------------------------------------------
/*
	if语句的注意事项：
		A:比较表达式无论简单还是复杂，结果必须是boolean类型
		B:if语句控制的语句体如果是一条语句，大括号可以省略；
		  如果是多条语句，就不能省略。建议永远不要省略。
		C:一般来说：有左大括号就没有分号，有分号就没有左大括号
*/
class IfDemo2 {
	public static void main(String[] args) {
		int x = 10;
		
		if(x == 10) {
			System.out.println("x等于10");
		}
		
		if((x > 5) || (x == 10)) {
			System.out.println("x大于或者等于10");
		}
		System.out.println("-------------------");
		
		int a = 100;
		
		/*
		if(a == 100) {
			System.out.println("a的值是100");
		}
		*/
		
		if(a != 100) {
			System.out.println("a的值是100");
			System.out.println("over");
		}
		System.out.println("-------------------");
		
		int b = 100;
		if(b != 100);  //这里其实是有语句体的，只不过是空语句体。
		
		//代码块
		{
			System.out.println("b的值是100");
			System.out.println("over");
		}
	}
}
---------------------------------------------------------
/*
	if语句格式2：
		if(比较表达式) {
			语句体1;
		}else {
			语句体2;
		}
	执行流程：
		首先计算比较表达式的值，看其返回值是true还是false。
		如果是true，就执行语句体1；
		如果是false，就执行语句体2；
		
	注意：else后面是没有比较表达式的，只有if后面有。
*/
class IfDemo3 {
	public static void main(String[] args) {
		//判断两个数据是否相等
		
		int a = 10;
		int b = 20;
		
		if(a == b) {
			System.out.println("a等于b");
		}else {
			System.out.println("a不等于b");
		}
	}
}
--------------------------------------------------
/*
	由于if语句的第二种格式刚才也完成了三元运算符可以完成的效果。
	所以，我们就认为他们可以完成一样的操作。
	但是，他们就一点区别没有吗?肯定不是。
	
	区别：
		三元运算符实现的，都可以采用if语句实现。反之不成立。
		
		什么时候if语句实现不能用三元改进呢?
			当if语句控制的操作是一个输出语句的时候就不能。
			为什么呢?因为三元运算符是一个运算符，运算符操作完毕就应该有一个结果，而不是一个输出。
*/
class IfDemo4 {
	public static void main(String[] args) {
		//获取两个数据的最大值
		int a = 10;
		int b = 20;
		
		//用if语句实现
		int max1;
		if(a > b) {
			max1 = a;
		}else {
			max1 = b;
		}
		System.out.println("max1:"+max1);
		
		//用三元改进
		int max2 = (a > b)? a: b;
		System.out.println("max2:"+max2);
		System.out.println("----------");
		
		//判断一个数据是奇数还是偶数,并输出是奇数还是偶数
		int x = 100;
		
		if(x%2 == 0) {
			System.out.println("100是一个偶数");
		}else {
			System.out.println("100是一个奇数");
		} 
		
		//用三元改进
		//这种改进是错误的。
		//String s = (x%2 == 0)?System.out.println("100是一个偶数");:System.out.println("100是一个奇数");;
	}
}
------------------------------------------------------------------
/*
	if语句的格式3：
		if(比较表达式1) {
			语句体1;
		}else if(比较表达式2) {
			语句体2;
		}else if(比较表达式3) {
			语句体3;
		}
		...
		else {
			语句体n+1;
		}
		
	执行流程：
		首先计算比较表达式1看其返回值是true还是false，
		如果是true，就执行语句体1，if语句结束。
		如果是false，接着计算比较表达式2看其返回值是true还是false，
		
		如果是true，就执行语句体2，if语句结束。
		如果是false，接着计算比较表达式3看其返回值是true还是false，
		...
		
		如果都是false，就执行语句体n+1。
*/
import java.util.Scanner;

class IfDemo5 {
	public static void main(String[] args) {
		//需求：键盘录入一个成绩，判断并输出成绩的等级。
		/*
			90-100 优秀
			80-90  好
			70-80  良
			60-70  及格
			0-60   不及格
		*/
		
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		//录入数据
		System.out.println("请输入你的考试成绩：");
		int score = sc.nextInt();
		
		/*
		if(score>=90 && score<=100) {
			System.out.println("优秀");
		}else if(score>=80 && score<90) {
			System.out.println("好");
		}else if(score>=70 && score<80) {
			System.out.println("良");
		}else if(score>=60 && score<70) {
			System.out.println("及格");
		}else {
			System.out.println("不及格");
		}
		*/
		//这样写已经满足我的基本要求，但是可能别人在使用的时候，不会按照你要求的数据给出了。
		//在做一个程序的基本测试的时候，一定要考虑这样的几个问题：
		//正确数据，错误数据，边界数据。
		//而我们刚才写的程序并没有处理错误数据，所以这个程序不是很好，要改进
		/*
		if(score>=90 && score<=100) {
			System.out.println("优秀");
		}else if(score>=80 && score<90) {
			System.out.println("好");
		}else if(score>=70 && score<80) {
			System.out.println("良");
		}else if(score>=60 && score<70) {
			System.out.println("及格");
		}else if(score>=0 && score<60){
			System.out.println("不及格");
		}else {
			System.out.println("你输入的成绩有误");
		}
		*/
		
		//另一种判断改进
		if(score<0 || score>100) {
			System.out.println("你输入的成绩有误");
		}else if(score>=90 && score<=100) {
			System.out.println("优秀");
		}else if(score>=80 && score<90) {
			System.out.println("好");
		}else if(score>=70 && score<80) {
			System.out.println("良");
		}else if(score>=60 && score<70) {
			System.out.println("及格");
		}else {
			System.out.println("不及格");
		}
	}
}
-------------------------------------------------
/*
	if语句格式2的练习：
		A:获取两个数据中较大的值
		B:判断一个数据是奇数还是偶数,并输出是奇数还是偶数
*/
import java.util.Scanner;

class IfTest {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		//获取两个数据中较大的值
		System.out.println("请输入第一个数据：");
		int a = sc.nextInt();
		
		System.out.println("请输入第二个数据：");
		int b = sc.nextInt();
		
		//定义一个变量接收最大值
		int max;
		
		if(a > b) {
			max = a;
		}else {
			max = b;
		}
		
		System.out.println("max:"+max);
		System.out.println("----------------");
		
		//判断一个数据是奇数还是偶数
		System.out.println("请输入你要判断的数据：");
		int x = sc.nextInt();
		
		if(x%2 == 0) {
			System.out.println(x+"这个数据是偶数");
		}else {
			System.out.println(x+"这个数据是奇数");
		}
	}
}
--------------------------------------------------
/*
	三种if语句分别适合做什么事情呢?
		格式1：适合做单个判断
		格式2：适合做两个判断
		格式3：适合做多个判断
		
	需求：
		键盘录入x的值，计算出y的并输出。
		
		x>=3	y = 2x + 1;
		-1<=x<3	y = 2x;
		x<=-1	y = 2x – 1;
		
	分析：
		A:由于数据要键盘录入，所以必须使用Scanner。
		B:由于是三种判断，所以我们选择if语句格式3。
*/
import java.util.Scanner;

class IfTest2 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入x的值：");
		int x = sc.nextInt();
		
		//定义一个y
		int y;
		
		//用if语句格式3进行判断
		if(x >= 3) {
			y = 2*x + 1;
		}else if(x>=-1 && x<3) {
			y = 2*x;
		}else {
			y = 2*x - 1;
		}
		
		System.out.println("y:"+y);
	}
}
--------------------------------------
/*
	键盘录入月份的值，输出对应的季节。
	
	春	3,4,5
	夏	6,7,8
	秋	9,10,11
	冬	12,1,2
	
	分析：
		A:键盘录入月份的值，所以我们要使用Scanner。
		B:我们应该判断这个月份在那个季节，而这个判断情况较多，所以，用if语句格式3。
		
	if语句的使用场景：
		A:针对表达式是一个boolean类型的判断
		B:针对一个范围的判断
*/
import java.util.Scanner;

class IfTest3 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		//录入数据
		System.out.println("请你输入一个月份:");
		int month = sc.nextInt();
		
		//第三种格式实现即可
		if(month<1 || month>12) {
			System.out.println("你输入的月份有误");
		}else if(month == 1) {
			System.out.println("冬季");
		}else if(month == 2) {
			System.out.println("冬季");
		}else if(month == 3) {
			System.out.println("春季");
		}else if(month == 4) {
			System.out.println("春季");
		}else if(month == 5) {
			System.out.println("春季");
		}else if(month == 6) {
			System.out.println("夏季");
		}else if(month == 7) {
			System.out.println("夏季");
		}else if(month == 8) {
			System.out.println("夏季");
		}else if(month == 9) {
			System.out.println("秋季");
		}else if(month == 10) {
			System.out.println("秋季");
		}else if(month == 11) {
			System.out.println("秋季");
		}else {
			System.out.println("冬季");
		}
		System.out.println("--------------");
		
		//这个程序确实是符合了我们的需求，但是就是看起来比较麻烦
		//那么，我们能不能改进一下呢?
		//month == 3
		//month == 4
		//month == 5
		//我们发现，上面三个都是春季。
		//而他们本身每一个都是一个boolean表达式
		//所以，我们就可以考虑使用逻辑运算符给他们连接起来改进
		if(month<1 || month>12) {
			System.out.println("你输入的月份有误");
		}else if(month==3 || month==4 || month==5) {
			System.out.println("春季");
		}else if(month==6 || month==7 || month==8) {
			System.out.println("夏季");
		}else if(month==9 || month==10 || month==11) {
			System.out.println("秋季");
		}else {
			System.out.println("冬季");
		}
		System.out.println("--------------");
		
		//这个时候，程序代码以及可以了。
		//但是呢，假如我要求你输入一个月份，判断是上半年还是下半年。
		//这个时候，我们的判断条件连接就是6个boolean表达式
		//我们可能还有更多的连接
		//这个时候，其实我们还有另外的一种改进方案：
		//month == 3
		//month == 4
		//month == 5
		//month>=3 && month<=5
		//用范围也是可以改进的。
		if(month<1 || month>12) {
			System.out.println("你输入的月份有误");
		}else if(month>=3 && month<=5) {
			System.out.println("春季");
		}else if(month>=6 && month<=8) {
			System.out.println("夏季");
		}else if(month>=9 && month<=11) {
			System.out.println("秋季");
		}else {
			System.out.println("冬季");
		}
		System.out.println("--------------");
	}
}
--------------------------------------------------
/*
	获取三个数据中的最大值
	
	由此案例主要是为了讲解if语句是可以嵌套使用的。而且是可以任意的嵌套。
*/
class IfTest4 {
	public static void main(String[] args) {
		int a = 10;
		int b = 30;
		int c = 20;
		
		//三元实现
		//int temp = (a>b)? a: b;
		//int max = (temp>c)? temp: c;
		//System.out.println("max:"+max);
		//System.out.println("--------");
		
		//用if语句实现
		int max;
		if(a > b) {
			if(a > c) {
				max = a;
			}else {
				max = c;
			}
		}else {
			if(b > c) {
				max = b;
			}else {
				max = c;
			}
		}
		System.out.println("max:"+max);
	}
}
```

