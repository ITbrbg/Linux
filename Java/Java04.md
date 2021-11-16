# Java04

#### 选择结构（switch语句）

```java
switch (表达式) {
    case 值1:
        语句体1;
        break;
    case 值2:
        语句体2;
        break;
    ....
    default:
        语句体n+1;
        break; 
}
```

- 格式解析

  - switch表示这是switch语句
    - 表达式的聚会：byte、short、int、char
    - JDK5以后可以是枚举
    - JDK7以后可以是string

  - case后面跟的是要和表达式比较的值
  - 语句体部分可以是一条或者多条语句
  - break表示中断，结束的意思，可以结束switch语句
  - default语句表示所有情况都不匹配的时候，就执行该处内容，和if语句的else相似

- 执行流程
  - 首先计算出表达式的值
  - 其次和case依次比较，一但有对应的值，就会执行相应的语句，在执行过程中，遇到break就会结束。
  - 最后，如果所有的case都和表达式的值不匹配，就会执行default语句体部分，然后结束程序。

```java
/*
	switch语句格式：
		switch(表达式) {
			case 值1:
				语句体1;
				break;
			case 值2:
				语句体2;
				break;
			...
			default:
				语句体n+1;
				break;
		}
		
	格式的解释：
		switch:表示这是switch选择结构
		表达式:这个地方的取值是有限定的
			byte,short,int,char
			JDK5以后可以是枚举
			JDK7以后可以是字符串
		case:后面跟的是要和表达式进行比较的值
		语句体:要执行的代码
		break:表示中断，结束的意思，可以控制switch语句的结束。
		default:当所有的值都和表达式不匹配的时候，就执行default控制的语句。其实它就相当于if语句的else。
	
	面试题：
		byte可以作为switch的表达式吗?
		long可以作为switch的表达式吗?
		String可以作为switch的表达式吗?
		
	案例：
		键盘录入一个数据，根据这个数据，我们输出对应的星期?
			键盘录入1,对应输出星期一
			键盘录入2,对应输出星期二
			...
			键盘录入7,对应输出星期日
			
	分析：
		1:键盘录入，用Scanner实现
		2:判断我们既可以使用if语句，也可以使用我们要讲解的switch语句
		
	注意：
		A:遇到左大括号缩进一个tab的位置。
		B:关联不是很大的语句间空行
*/
import java.util.Scanner;

class SwitchDemo {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		//控制键盘录入数据
		System.out.println("请输入一个数据(1-7):");
		int week = sc.nextInt(); //3
		
		//switch判断语句
		switch(week) {
			case 1:
				System.out.println("星期一");
				break;
			case 2:
				System.out.println("星期二");
				break;
			case 3:
				System.out.println("星期三");
				break;
			case 4:
				System.out.println("星期四");
				break;
			case 5:
				System.out.println("星期五");
				break;
			case 6:
				System.out.println("星期六");
				break;
			case 7:
				System.out.println("星期日");
				break;
			default:
				System.out.println("你输入的数据有误");
				break;
		}
	}
}
-----------------------------------------------------------
/*
	switch语句的注意事项：
		A:case后面只能是常量，不能是变量，而且，多个case后面的值不能出现相同的
		B:default可以省略吗?
			可以省略，但是不建议，因为它的作用是对不正确的情况给出提示。
			特殊情况：
				case就可以把值固定。
				A,B,C,D
		C:break可以省略吗?
			可以省略，但是结果可能不是我们想要的。
			会出现一个现象：case穿透。
			最终我们建议不要省略
		D:default一定要在最后吗?
			不是，可以在任意位置。但是建议在最后。
		E:switch语句的结束条件
			a:遇到break就结束了
			b:执行到末尾就结束了
*/
import java.util.Scanner;

class SwitchDemo2 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		//控制键盘录入数据
		System.out.println("请输入一个数据(1-7):");
		int week = sc.nextInt(); //3
		
		//定义常量
		//int number = 3;
		//然后把case后面的值改为number，就会报错
		
		//switch判断语句
		switch(week) {
			case 1:
				System.out.println("星期一");
				break;
			case 2:
				System.out.println("星期二");
				break;
			case 3:
				System.out.println("星期三");
				break;
			case 4:
				System.out.println("星期四");
				break;
			case 5:
				System.out.println("星期五");
				break;
			case 6:
				System.out.println("星期六");
				break;
			case 7:
				System.out.println("星期日");
				break;
			default:
				System.out.println("你输入的数据有误");
				//break;
		}
	}
}
-----------------------------------------------------------
/*
	模拟单项选择题。
	
	分析：
		A:出一个选择题，然后供你选择。
		B:键盘录入选择的数据。
		C:根据选择来给出你选择的结论。
*/
import java.util.Scanner;

class SwitchTest2 {
	public static void main(String[] args) {
		//出一个选择题，然后供你选择。
		//由于我们现在没有办法键盘录入得到一个'A','B'
		//这样的东西，我就用65，66这样的值替代
		//将来我们获取到这样的值以后，强制转换为字符类型
		System.out.println("下面的几个人你最爱谁?");
		System.out.println("65 林青霞");
		System.out.println("66 张曼玉");
		System.out.println("67 刘德华");
		System.out.println("68 王力宏");
		
		//键盘录入选择的数据。
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入你的选择：");
		int choiceNumber = sc.nextInt();
		
		//强制转换为字符类型
		char choice = (char) choiceNumber;
		
		switch(choice) {
			case 'A':
				System.out.println("恭喜你,选择正确");
				break;
			case 'B':
				System.out.println("不好意思，你选择有误");
				break;
			case 'C':
				System.out.println("不好意思，你选择有误");
				break;
			case 'D':
				System.out.println("不好意思，你选择有误");
				break;
			default:
				System.out.println("没有该选项");
				break;
		}
	}
}
------------------------------------------------------
/*
	根据你键盘录入的字符串，判断是否有满足要求的，如果有就输出。
	否则，提示有误。
	
	String s = sc.nextLine();
*/
import java.util.Scanner;

class SwitchTest3 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		//录入数据
		System.out.println("请输入你要判断的字符串：");
		String s = sc.nextLine();
		
		switch(s) {
			case "hello":
				System.out.println("你输入的是hello");
				break;
			case "world":
				System.out.println("你输入的是world");
				break;
			case "java":
				System.out.println("你输入的是java");
				break;
			default:
				System.out.println("没有找到你输入的数据");
				//break;
		}
	}
}
---------------------------------------------------------
/*
	用switch语句实现键盘录入月份，输出对应的季节
	
	分析：
		A:键盘录入一个月份，用Scanner实现
		B:用switch语句实现即可
		
	if语句和switch语句的区别?
		if语句：
			A:针对结果是boolean类型的判断
			B:针对一个范围的判断
			C:针对几个常量值的判断
		
		switch语句：
			针对几个常量值的判断
*/
import java.util.Scanner;

class SwitchTest4 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		//录入数据
		System.out.println("请输入月份(1-12)：");
		int month = sc.nextInt();
		
		/*
		switch(month) {
			case 1:
				System.out.println("冬季");
				break;
			case 2:
				System.out.println("冬季");
				break;
			case 3:
				System.out.println("春季");
				break;
			case 4:
				System.out.println("春季");
				break;
			case 5:
				System.out.println("春季");
				break;
			case 6:
				System.out.println("夏季");
				break;
			case 7:
				System.out.println("夏季");
				break;
			case 8:
				System.out.println("夏季");
				break;
			case 9:
				System.out.println("秋季");
				break;
			case 10:
				System.out.println("秋季");
				break;
			case 11:
				System.out.println("秋季");
				break;
			case 12:
				System.out.println("冬季");
				break;
			default:
				System.out.println("你输入的月份有误");
		}
		*/
		
		//这样写太麻烦了，我们使用一个我们不想使用的东西：case穿透
		switch(month) {
			case 1:
			case 2:
			case 12:
				System.out.println("冬季");
				break;
			case 3:
			case 4:
			case 5:
				System.out.println("春季");
				break;
			case 6:
			case 7:
			case 8:
				System.out.println("夏季");
				break;
			case 9:
			case 10:
			case 11:
				System.out.println("秋季");
				break;
			default:
				System.out.println("你输入的月份有误");
		}
	}
}
```

- 选择结构（各自使用场景）

  - 在做判断的时候我们有俩种选择，if和switch语句，那么，我们到底如何选择使用哪种语句呢？

    - if语句的使用场景
      - 针对结果是boolean类型的
      - 针对一个范围的判断
      - 针对几个常量的判断

    - switch语句的使用场景
      - 针对几个常量的判断

#### 循环语句

---

- 循环语句可以在满足循环条件的情况下，反复执行某一段代码，这段被重复的执行的代码被称为循环语句体，当反复执行这段循环语句体时，需要在合适的时候把循环判断条件改为false，从而结束循环，否则循环会一直执行下去，形成死循环。

- 循环语句的组成部分

  - ​      初始化语句
    - 一条或多条语句，这些语句完成一些初始化操作

  - 判断条件语句
    - 是一个boolean表达式，这个表达式决定是否执行循环体

  - 循环体语句
    - 这个部分是循环体语句，也就是我们要多次做的事情

  - 控制条件语句
    - 这个部分在一次循环体语句结束后，下一次循环执行前执行，通过控制循环条件中的变量，使得循环的合适的时候结束

- 格式

  ```java
  #for 循环语句的格式
  for (初始化语句;判断条件语句;控制条件语句){
      循环体语句;
  }
  ```

- 执行流程

  - 执行初始化语句
  - 执行判断条件语句，看其结果是true还是false
    - 如果是false,结束语句
    - 如果是true则继续执行

  - 执行循环体
  - 执行控制语句
  - 回到第二步继续执行

- 注意事项
  - 判断条件语句是一个boolean类型
  - 循环体语句是一条语句，大行号可以省略，如果是多条语句，大括号不能省略
  - 一般来说有左大括号就没有分号，有分号就没有左大括号

```java
/*
	循环语句：for循环,while循环,do...while循环。
	
	for循环格式：
		for(初始化语句;判断条件语句;控制条件语句) {
			循环体语句;
		}
		
		执行流程：
			A:执行初始化语句
			B:执行判断条件语句,看其返回值是true还是false
				如果是true，就继续执行
				如果是false，就结束循环
			C:执行循环体语句;
			D:执行控制条件语句
			E:回到B继续。
			
	注意事项：
		A:判断条件语句无论简单还是复杂结果是boolean类型。
		B:循环体语句如果是一条语句，大括号可以省略；如果是多条语句，大括号不能省略。建议永远不要省略。
		C:一般来说：有左大括号就没有分号，有分号就没有左大括号
			
	需求：请在控制台输出10次"HelloWorld"
*/
class ForDemo {
	public static void main(String[] args) {
		//最原始的做法
		System.out.println("HelloWorld");
		System.out.println("HelloWorld");
		System.out.println("HelloWorld");
		System.out.println("HelloWorld");
		System.out.println("HelloWorld");
		System.out.println("HelloWorld");
		System.out.println("HelloWorld");
		System.out.println("HelloWorld");
		System.out.println("HelloWorld");
		System.out.println("HelloWorld");
		System.out.println("----------");
		
		//这种做法不好,代码的重复度太高。
		//所以呢，我们用循环改进
		for(int x=1;x<=10;x++) {
			System.out.println("HelloWorld");
		}
	}
}
----------------------------------------------------
/*
	需求：请在控制台输出数据1-10
*/
class ForDemo2 {
	public static void main(String[] args) {
		//原始做法
		System.out.println(1);
		System.out.println(2);
		System.out.println(3);
		System.out.println(4);
		System.out.println(5);
		System.out.println(6);
		System.out.println(7);
		System.out.println(8);
		System.out.println(9);
		System.out.println(10);
		
		System.out.println("-------------");
		
		//如何改进呢?用循环改进
		for(int x=1; x<=10; x++) {
			System.out.println(x);
		}
		
		System.out.println("-------------");
		
		//从0开始
		for(int x=0; x<10; x++) {
			System.out.println(x+1);
		}
	}
}	
------------------------------------------
/*
	需求：求出1-10之间数据之和
	
	分析：
		0+1=1
			1+2=3
				3+3=6
					6+4=10
						10+5=15
							 ...
							 
		由此可见我们要定义两个变量：
			一个变量用于存储第一个加数，第一个加数其实保存的是以前的所有数据和。默认初始化值应该是0。
			一个变量用于存储第二个加数，第二个加数其实就是每次的数据变化的值。
			
	求和思想。		
*/
class ForDemo3 {
	public static void main(String[] args) {
		//原始做法
		System.out.println(1+2+3+4+5+6+7+8+9+10);
		
		//定义第一个加数
		int sum = 0;
		
		for(int x=1; x<=10; x++) {
			//这里的x其实是第二个加数
			sum = sum + x;
			/*
				0 + 1 = 1
						1 + 2 = 3
								3 + 3 = 6
								...
			*/
			
			//sum += x;
		}
		
		System.out.println("sum:"+sum);
	}
}
-----------------------------------------------
/*
	需求：
		A:求1-100之和。
		B:求出1-100之间偶数和
		C:求出1-100之间奇数和(自己做)
*/
class ForDemo4 {
	public static void main(String[] args) {
		//求1-100之和。
		int sum1 = 0;
		
		for(int x=1; x<=100; x++) {
			sum1 +=x;
		}
		
		System.out.println("1-100之和是："+sum1);
		System.out.println("------------------");
		
		//求出1-100之间偶数和
		//方式1
		int sum2 = 0;
		
		for(int x=1; x<=100; x++) {
			if(x%2 == 0) {
				sum2 += x;
			}
		}
		
		System.out.println("1-100偶数之和是："+sum2);
		System.out.println("------------------");
		
		//方式2
		int sum3 = 0;
		
		for(int x=0; x<=100; x+=2) {
				sum3 += x;
		}
		
		System.out.println("1-100偶数之和是："+sum3);
		System.out.println("------------------");
	}
}
--------------------------------------------------------------
/*
	需求：求5的阶乘。
	
	什么是阶乘呢?
		n! = n*(n-1)! 规则
		n! = n*(n-1)*(n-2)*...*3*2*1
		
	求和思想。
	求阶乘思想。
*/
class ForDemo5 {
	public static void main(String[] args) {
		//定义最终结果变量
		int jc = 1;
		
		//这里的x其实可以直接从2开始
		//for(int x=1; x<=5; x++) 
		
		for(int x=2; x<=5; x++) {
			jc *=x;
		}
		
		System.out.println("1-5的阶乘是："+jc);
	}
}
--------------------------------------------------
/*
	天将降大任于斯人也,必先盗其QQ,封其微博,收其wifi,夺其手机。让其静心学习Java欧耶。

	需求：在控制台输出所有的”水仙花数”
	
	分析：
		我们都不知道什么叫"水仙花数"，你让我怎么做呢?
		
		所谓的水仙花数是指一个三位数，其各位数字的立方和等于该数本身。
		举例：153就是一个水仙花数。
		153 = 1*1*1 + 5*5*5 + 3*3*3 = 1 + 125 + 27 = 153

		A:三位数其实是告诉了我们范围。
		B:通过for循环我们就可以实现获取每一个三位数
		  但是麻烦是如何获取这个三位数的个,十,百位上的数据
		  
		  我们如何获取一个数据的个,十,百呢?
			假设有个一个数据:153
			ge:	153%10 = 3
			shi: 153/10%10 = 5
			bai：153/10/10%10 = 1
			qian：x/10/10/10%10
			wan:  x/10/10/10/10%10
			...

		C:让ge*ge*ge+shi*shi*shi+bai*bai*bai和该数据比较
		  如果相同，就把该数据在控制台输出。
*/
class ForDemo6 {
	public static void main(String[] args) {
		//三位数其实是告诉了我们范围。
		for(int x=100; x<1000; x++) {
			int ge = x%10;
			int shi = x/10%10;
			int bai = x/10/10%10;
			
			//让ge*ge*ge+shi*shi*shi+bai*bai*bai和该数据比较
			if(x == (ge*ge*ge+shi*shi*shi+bai*bai*bai)) {
				//如果相同，就把该数据在控制台输出。
				System.out.println(x);
			}
		}
	}
}
----------------------------------------------------------------
/*
	练习：
		请在控制台输出满足如下条件的五位数
		个位等于万位
		十位等于千位
		个位+十位+千位+万位=百位
		
	分析：
		A:五位数就告诉了我们范围。
		B:分解每一个五位数的个，十，百，千，万位上的数据
		C:按照要求进行判断即可
*/
class ForDemo7 {
	public static void main(String[] args) {
		//五位数就告诉了我们范围。
		for(int x=10000; x<100000; x++) {
			//分解每一个五位数的个，十，百，千，万位上的数据
			int ge = x%10;
			int shi = x/10%10;
			int bai  = x/10/10%10;
			int qian = x/10/10/10%10;
			int wan = x/10/10/10/10%10;
			
			//按照要求进行判断即可
			if((ge==wan) && (shi==qian) && (ge+shi+qian+wan==bai)) {
				System.out.println(x);
			}
		}
	}
}
------------------------------------------------------------
/*
	需求：统计”水仙花数”共有多少个
	
	分析：
		A:首先必须知道什么是水仙花数
			所谓的水仙花数是指一个三位数，其各位数字的立方和等于该数本身。
			举例：153就是一个水仙花数。
			153 = 1*1*1 + 5*5*5 + 3*3*3 = 1 + 125 + 27 = 153
		B:定义统计变量，初始化值是0
		C:三位数告诉了我们范围，用for循环就可以搞定
		D:获取每一个三位数的个，十，百的数据
		E:按照要求进行判断
		F:如果满足要求就计数。
*/
class ForDemo8 {
	public static void main(String[] args) {
		//定义统计变量，初始化值是0
		int count = 0;
		
		//三位数告诉了我们范围，用for循环就可以搞定
		for(int x=100; x<1000; x++) {
			//获取每一个三位数的个，十，百的数据
			int ge = x%10;
			int shi = x/10%10;
			int bai = x/10/10%10;
			
			//按照要求进行判断
			if(x == (ge*ge*ge+shi*shi*shi+bai*bai*bai)) {
				//如果满足要求就计数。
				count++;
			}
		}
		
		System.out.println("水仙花数共有"+count+"个");
	}
}
-----------------------------------------------------
/*
	需求：请统计1-1000之间同时满足如下条件的数据有多少个：
			对3整除余2
			对5整除余3
			对7整除余2

	分析：
		A:定义统计变量,初始化值是0
		B:1-1000之间是一个范围，用for很容易就可以实现。
		C:每个数据要同时满足如下要求
			x%3==2
			x%5==3
			x%7==2
		D:如果满足条件，统计数据++即可，最后输出统计变量
*/
class ForDemo9 {
	public static void main(String[] args) {
		//定义统计变量,初始化值是0
		int count = 0;
	
		//1-1000之间是一个范围，用for很容易就可以实现。
		for(int x=1; x<=1000; x++) {
			/*
				每个数据要同时满足如下要求
				x%3==2
				x%5==3
				x%7==2
			*/
			if(x%3==2 && x%5==3 && x%7==2) {
				count++;
				System.out.println(x);
			}
		}
		
		//输出数据
		System.out.println("满足这样条件的数据共有："+count+"个");
	}
}
```

#### 循环结构（while循环语句）

---

- while循环语句格式
- for循环和while循环语句可以等价转换，但还是有小的区别
  - 使用区别：控制条件语句所控制的那个变量，在for循环结束后，就不能在被访问到了，而while循环结束还可以继续使用，如果你想继续使用，就用while循环，否则推荐使用for，原因是for循环结束后，该变量就从内存中消失，就能够提高内存的使用效率
  - 使用场景
    - for循环针对一个范围判断进行操作
    - while循环适合判断次数不明的操作

```java
#基本格式
while (判断条件语句){
    循环语句体;
}
#扩展格式
初始化语句;
while (判断条件语句){
    循环体语句;
    控制条件语句; 
}
```

```java
/*
	while循环的基本格式：
		while(判断条件语句) {
			循环体语句;
		}
		
		扩展格式：
		
		初始化语句;
	    while(判断条件语句) {
			 循环体语句;
			 控制条件语句;
		}
		
		通过这个格式，我们就可以看到其实和for循环是差不多的。
		
		for(初始化语句;判断条件语句;控制条件语句) {
			循环体语句;
		}
*/
class WhileDemo {
	public static void main(String[] args) {
		//输出10次"HelloWorld"
		//for语句版
		for(int x=0; x<10; x++) {
			System.out.println("HelloWorld");
		}
		System.out.println("--------------");
		//while语句版
		int x=0;
		while(x<10) {
			System.out.println("HelloWorld");
			x++;
		}
		
	}
}
-------------------------------------------------
/*
	练习：用while循环实现
	左边：求出1-100之和
	右边：统计水仙花数有多少个
	
	初始化语句;
	while(判断条件语句) {
		 循环体语句;
		 控制条件语句;
	}
	
	
	
	for(初始化语句;判断条件语句;控制条件语句) {
		循环体语句;
	}

*/
class WhileDemo2 {
	public static void main(String[] args) {
		//求出1-100之和
		//for语句版本
		int sum = 0;
		
		for(int x=1; x<=100; x++) {
			sum+=x;
		}
		
		System.out.println("sum:"+sum);
		System.out.println("--------");
		//while语句版本
		int sum2 = 0;
		
		int y=1;
		while(y<=100) {
			sum2+=y;
			y++;
		}
		
		System.out.println("sum2:"+sum2);
		System.out.println("--------");
	}
}
-------------------------------------------
/*
	需求：统计水仙花数有多少个
*/
class WhileDemo3 {
	public static void main(String[] args) {
		//for循环版本
		int count = 0;
		
		for(int x=100; x<1000; x++) {
			int ge = x%10;
			int shi = x/10%10;
			int bai = x/10/10%10;
			
			if((ge*ge*ge+shi*shi*shi+bai*bai*bai) == x) {
				count++;
			}
		}
		
		System.out.println("count:"+count);
		System.out.println("------------");
		
		//while循环版本
		int count2 = 0;
		
		int y = 100;
		while(y<1000) {
			int ge = y%10;
			int shi = y/10%10;
			int bai = y/10/10%10;
			
			if((ge*ge*ge+shi*shi*shi+bai*bai*bai) == y) {
				count2++;
			}
			
			y++;
		}
		
		System.out.println("count2:"+count2);
	}
}
-------------------------------------------------
/*
	while循环和for循环的区别?
		使用区别：如果你想在循环结束后，继续使用控制条件的那个变量，用while循环，否则用for循环。不知道用for循环。
		          因为变量及早的从内存中消失，可以提高内存的使用效率。
				  
		其实还有一种场景的理解:
			如果是一个范围的，用for循环非常明确。
			如果是不明确要做多少次，用while循环较为合适。
				举例：吃葡萄。
*/
class WhileDemo4 {
	public static void main(String[] args) {
		//for循环实现
		for(int x=0; x<10; x++) {
			System.out.println("学习Java技术哪家强,中国北京传智播客");
		}
		//这里不能在继续访问了
		//System.out.println(x);
		
		//while循环实现
		int y = 0;
		while(y<10) {
			System.out.println("学习Java技术哪家强,中国北京传智播客");
			y++;
		}
		//这里是可以继续访问的
		System.out.println(y);
	}
} 
----------------------------------------------------------------
/*
	我国最高山峰是珠穆朗玛峰：8848m，我现在有一张足够大的纸张，厚度为：0.01m。
	请问，我折叠多少次，就可以保证厚度不低于珠穆朗玛峰的高度?

	分析：
		A:定义一个统计变量，默认值是0
		B:最高山峰是珠穆朗玛峰：8848m这是最终的厚度
		  我现在有一张足够大的纸张，厚度为：0.01m这是初始厚度
		C:我折叠多少次，就可以保证厚度不低于珠穆朗玛峰的高度?
		  折叠一次有什么变化呢?就是厚度是以前的2倍。
		D:只要每次变化的厚度没有超过珠穆朗玛峰的高度，就折叠，统计变量++
		E:输出统计变量。
*/

class WhileDemo5 {
	public static void main(String[] args) {
		//定义一个统计变量，默认值是0
		int count = 0;
		
		//最高山峰是珠穆朗玛峰：8848m这是最终的厚度
		//我现在有一张足够大的纸张，厚度为：0.01m这是初始厚度
		//为了简单，我把0.01变成1，同理8848就变成了884800
		int end = 884800;
		int start = 1;
		
		while(start<end) {
			//只要每次变化的厚度没有超过珠穆朗玛峰的高度，就折叠，统计变量++
			count++;
			
			//折叠一次有什么变化呢?就是厚度是以前的2倍。
			start *= 2;
			
			System.out.println("第"+count+"次厚度是"+start);
		}
		
		//输出统计变量。
		System.out.println("要叠"+count+"次");
	}
}
```

#### 循环结构（do....while循环）

----

- do ....while循环语句格式

```java
#基本格式 
do{
    循环体语句;
}while(判断条件语句);
#扩展格式
初始花语句;
do{
    循环体语句;
    控制条件语句;
}while(判断条件语句);
```

```java
/*
	do...while循环的基本格式：
		do {
			循环体语句;
		}while(判断条件语句);
		
		扩展格式；
		初始化语句;
		do {
			循环体语句;
			控制条件语句;
		}while(判断条件语句);
*/
class DoWhileDemo {
	public static void main(String[] args) {
		//输出10次HelloWorld。
		int x = 0;
		do {
			System.out.println("HelloWorld");
			x++;
		}while(x<10);
		
		System.out.println("--------------");
		
		//求和1-100
		int sum = 0;
		int a = 1;
		do {
			sum += a;
			a++;
		}while(a<=100);
		
		System.out.println(sum);
	}
}
----------------------------------------
/*
	循环语句的区别:
		do...while循环至少执行一次循环体。
		而for,while循环必须先判断条件是否成立，然后决定是否执行循环体语句。
		
	那么，我们一般使用哪种循环呢?
		优先考虑for，其次考虑while，最后考虑do...while
*/
class DoWhileDemo2 {
	public static void main(String[] args) {
		int x = 3;
		while(x < 3) {
			System.out.println("我爱林青霞");
			x++;
		}
		
		System.out.println("--------------");
		
		int y = 3;
		do {
			System.out.println("我爱林青霞");
			y++;
		}while(y < 3);
	}
}
---------------------------------------------
/*
	注意死循环：
		A:一定要注意控制条件语句控制的那个变量的问题，不要弄丢了，否则就容易死循环。
		B:两种最简单的死循环格式
			while(true){...}
			for(;;){...}
			
*/
class DoWhileDemo3 {
	public static void main(String[] args) {
		int x = 0;
		while(x < 10) {
			System.out.println(x);
			x++;
		}
		System.out.println("--------------");
		
		/*
		while(true) {
			System.out.println("今天我很高兴，学习了死循环");
		}
		*/
		
		for(;;){
			System.out.println("今天我很高兴，学习了死循环");
		}
		
		//System.out.println("--------------");
	}
}
--------------------------------------------------
/*
	需求：请输出一个4行5列的星星(*)图案。
	结果：
		*****
		*****
		*****
		*****
		
	循环嵌套：就是循环语句的循环体本身是一个循环语句。
	
	通过结果我们知道这样的一个结论：
		外循环控制行数
		内循环控制列数
*/
class ForForDemo {
	public static void main(String[] args) {
		//原始做法
		System.out.println("*****");
		System.out.println("*****");
		System.out.println("*****");
		System.out.println("*****");
		System.out.println("-------------");
		
		//虽然可以完成需求，但是不是很好
		//如果是多行多列就会比较麻烦
		//所以我们准备改进
		//如何改进呢?
		//我先考虑如何实现一行*的问题
		//System.out.println("*****");
		//我们要想的是如何实现一次输出一颗*的问题
		//System.out.println("*");
		//System.out.println("*");
		//现在虽然可以一次一颗*，但是却换行了，我要求不能换行，怎么办呢?
		//输出语句的另一种格式：System.out.print(); 这个是不带换行的
		//System.out.print("*");
		//System.out.print("*");
		//System.out.print("*");
		//System.out.print("*");
		//System.out.print("*");
		//如果我要在一行上打出多颗*，比较麻烦，而代码是重复的，所以我决定用循环改进
		for(int x=0; x<5; x++) {
			System.out.print("*");
		}
		//我们可以通过空的输出语句实现换行：System.out.println();
		System.out.println();
		
		//既然我可以打出一行，我就可以打出第二行
		for(int x=0; x<5; x++) {
			System.out.print("*");
		}
		//我们可以通过空的输出语句实现换行：System.out.println();
		System.out.println();
	
		//同理打出第三行，第四行
		for(int x=0; x<5; x++) {
			System.out.print("*");
		}
		//我们可以通过空的输出语句实现换行：System.out.println();
		System.out.println();
		
		//既然我可以打出一行，我就可以打出第二行
		for(int x=0; x<5; x++) {
			System.out.print("*");
		}
		//我们可以通过空的输出语句实现换行：System.out.println();
		System.out.println();
		System.out.println("-----------------");
		//同样的代码出现了4次，说明我们程序写的不好，用循环改进
		for(int y=0; y<4; y++) {
			for(int x=0; x<5; x++) {
				System.out.print("*");
			}
			//我们可以通过空的输出语句实现换行：System.out.println();
			System.out.println();
		}
	}
}
-------------------------------------------------------------------
/*
	需求：请输出下列的形状
		*
		**
		***
		****
		*****
*/
class ForForDemo2 {
	public static void main(String[] args) {
		//通过简单的观察，我们看到这是一个行是5，列数是变化的形状
		//我们先打印出一个5行5列的形状
		for(int x=0; x<5; x++) {
			for(int y=0; y<5; y++) {
				System.out.print("*");
			}
			System.out.println();
		}
		
		System.out.println("--------------");
		
		//我们实现了一个5行5列的形状
		//但是这不是我们想要的
		//我们要的是列数变化的
		//列数是如何变化的呢?
		//第一行：1列	y=0,y<=0,y++
		//第二行：2列	y=0,y<=1,y++
		//第三行：3列	y=0,y<=2,y++
		//第四行：4列	y=0,y<=3,y++
		//第五行：5列	y=0,y<=4,y++
		//在看外循环x的变化，恰好就是x=0,1,2,3,4
		//所以这个最终版的程序就是如下
		for(int x=0; x<5; x++) {
			for(int y=0; y<=x; y++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
----------------------------------------
/*
	需求：在控制台输出九九乘法表。
	
	首先我们写出九九乘法表：
		1*1=1
		1*2=2	2*2=4
		1*3=3	2*3=6	3*3=9
		1*4=4	2*4=8	3*4=12	4*4=16
		...
		1*9=9	2*9=18	3*9=27	...
		
	我们先把这个九九乘法表看出是这样的一个形状：
		*
		**
		***
		****
		*****
		******
		*******
		********
		*********
		
	注意：
		'\x' x表示任意，这种做法叫转移字符。
		
		'\t'	tab键的位置
		'\r'	回车
		'\n'	换行
*/
class ForForDemo3 {
	public static void main(String[] args) {
		for(int x=0; x<9; x++) {
			for(int y=0; y<=x; y++) {
				System.out.print("*");
			}
			System.out.println();
		}
		System.out.println("--------------");
		//为了使用数据，我们从1开始
		for(int x=1; x<=9; x++) {
			for(int y=1; y<=x; y++) {
				System.out.print(y+"*"+x+"="+y*x+"\t");
			}
			System.out.println();
		}
	}
}
```

#### 跳转控制语句

- 前面我们已经说过了，Java中的goto是保留字，目前不能使用，虽然没有goto语句可以增强程序的安全性，但是也带来了很多不便，比如说，我想在某个循环知道某一步的时候就结束，现在就做不了这件事情，为了弥补这个缺陷，Java就提供了break，continue和reture来实现控制语句跳转和中断

- break中断

  - 使用场景
    - 在选择结构switch语句中
    - 在循环语句中
    - 离开使用场景的存在是没有意义的

  - break的作用
    - 跳出单层循环
    - 跳出多层循环
      - 带标签的跳出
      - 格式，标签名，循环语句
      - 标签名要符合Java的命名规则

- continue继续

  - 使用场景
    - 在循环语句中
    - 离开使用场景的存在是没有意义的

  - 作用

    - 单层循环对比break，然后总结俩个区别
      - break跳出当前循环
      - continue跳出本次循环

    - 也可以带标签的使用

- reture返回

  - reture关键字不是为了跳转出循环体，更常用的功能是结束一个方法，也就是退出一个方法。跳转到上层调用的方法。
  - 案例
    - 结束循环其实是结束了main方法

```java
/*
	控制跳转语句：
		break:中断
		continue:继续
		return:返回
	
	break:中断的意思
	使用场景：
		A:switch语句中
		B:循环语句中。
			(循环语句中加入了if判断的情况)
		注意：离开上面的两个场景，无意义。
		
	如何使用呢?
		A:跳出单层循环
		B:跳出多层循环
			要想实现这个效果，就必须知道一个东西。带标签的语句。
			格式：
				标签名: 语句
*/
class BreakDemo {
	public static void main(String[] args) {
		//在 switch 或 loop 外部中断
		//break;
		
		//跳出单层循环
		for(int x=0; x<10; x++) {
			if(x == 3) {
				break;
			}
			System.out.println("HelloWorld");
		}
		
		System.out.println("over");
		System.out.println("-------------");
		
		wc:for(int x=0; x<3; x++) {
			nc:for(int y=0; y<4; y++) {
				if(y == 2) {
					//break nc;
					break wc;
				}
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
--------------------------------------------
/*
	continue:继续
	
	使用场景：
		循环中。离开此场景无意义。
		
	测试，找到和break的区别：
		break:跳出单层循环
		continue:跳出一次循环，进入下一次的执行
		
	练习题：
		for(int x=1; x<=10; x++) {
			if(x%3==0) {
				//在此处填写代码
			}
			System.out.println(“Java基础班”);
		}
		
		我想在控制台输出2次:“Java基础班“
			break;
		我想在控制台输出7次:“Java基础班“
			continue;
		我想在控制台输出13次:“Java基础班“	
			System.out.println(“Java基础班”);


*/
class ContinueDemo {
	public static void main(String[] args) {
		for(int x=0; x<10; x++) {
			if(x == 3) {
				//break;
				continue;
			}
			
			System.out.println(x);
		}
	}
}
---------------------------------------------------
/*
	return:返回
	
	其实它的作用不是结束循环的，而是结束方法的。
*/
class ReturnDemo {
	public static void main(String[] args) {
		for(int x=0; x<10; x++) {
			if(x == 2) {
				System.out.println("退出");
				//break;
				//continue;
				return;
			}
			
			System.out.println(x);
		}
		
		System.out.println("over");
	}
}
---------------------------------------
/*
	需求：小芳的妈妈每天给她2.5元钱，她都会存起来，但是，
	      每当这一天是存钱的第5天或者5的倍数的话，她都会花去6元钱，
		  请问，经过多少天，小芳才可以存到100元钱。

	分析：
		A:小芳的妈妈每天给她2.5元钱
			double dayMoney = 2.5;
		B:她都会存起来
			double daySum = 0;
		C:从第一天开始存储
			int dayCount = 1;
		D:经过多少天，小芳才可以存到100元钱。
			double result = 100;
		E:这一天是存钱的第5天或者5的倍数的话，她都会花去6元钱，
			说明要判断dayCount的值，如果对5整除就减去6元钱。
				daySum -= 6;
		  由此还隐含了一个问题，就是如果不是5的倍数天的话，钱要累加
				daySum += dayMoney;
		F:因为不知道是多少天，所以我用死循环，一旦超过100元我就退出循环。
*/
class WhileDemo {
	public static void main(String[] args) {
		//每天要存储的钱是2.5元
		double dayMoney = 2.5;
		
		//存钱的初始化值是0
		double daySum = 0;
		
		//从第一天开始存储
		int dayCount = 1;
		
		//最终存储不小于100就不存储了
		int result = 100;
		
		//因为不知道是多少天，所以我用死循环，
		while(true) {
			//累加钱
			daySum += dayMoney;
			
			//一旦超过100元我就退出循环。
			if(daySum >= result) {
				System.out.println("共花了"+dayCount+"天存储了100元");
				break;
			}
			
			if(dayCount%5 == 0) {
				//花去6元钱
				daySum -= 6;
				System.out.println("第"+dayCount+"天花了6元钱");
			}
			
			//天数变化
			dayCount++;
		}
	}
}
```

