# Java06

#### 二维数组

- Java基础班每班有多少个学生，所以可以用数组来存储，而我们又有很多Java基础班，这个也应该用一个数组来存储，如何来表示这样的数据呢？Java就提供了二维数组来给我们使用。
- 由此可见：二维数组其实就是一个元素为一维数组的数组。

- 格式

  - 数据类型[]\[] 变量名 = new 数据类型[m]\[n]
    - m表示这个二维数组有多少个一维数组
    - n表示每一个一维数组的元素个数

  - 数据类型[]\[] 变量名 = new 数据类型[m]\[]
    - m表示二维数组有多少个一维数组
    - 这次没有直接给出一维数组的元素个数，可以动态给出

  - 数据类型[]\[] 变量名 = new 数据类型[]\[]{{元素....}}.{{元素....}}.{{元素....}}
    - 简化版格式
      - 数据类型[]\[] 变量名 = {{元素....}}.{{元素....}}.{{元素...}};

```java
/*
	二维数组：就是元素为一维数组的一个数组。
	
	格式1：
		数据类型[][] 数组名 = new 数据类型[m][n];
		
		m:表示这个二维数组有多少个一维数组。
		n:表示每一个一维数组的元素有多少个。
		
	注意：
		A:以下格式也可以表示二维数组
			a:数据类型 数组名[][] = new 数据类型[m][n];
			b:数据类型[] 数组名[] = new 数据类型[m][n];
		B:注意下面定义的区别
			int x;
			int y;
			int x,y;
			
			int[] x;
			int[] y[];
			
			int[] x,y[];
*/
class Array2Demo {
	public static void main(String[] args) {
		 //定义一个二维数组
		 int[][] arr = new int[3][2];
		 //定义了一个二维数组arr
		 //这个二维数组有3个一维数组的元素
		 //每一个一维数组有2个元素
		 //输出二维数组名称
		 System.out.println(arr); //地址值	[[I@175078b
		 //输出二维数组的第一个元素一维数组的名称
		 System.out.println(arr[0]); //地址值	[I@42552c
		 System.out.println(arr[1]); //地址值	[I@e5bbd6
		 System.out.println(arr[2]); //地址值	[I@8ee016
		 //输出二维数组的元素
		 System.out.println(arr[0][0]); //0
		 System.out.println(arr[0][1]); //0
	}
}
-----------------------------------------------------
/*
	格式2：
		数据类型[][] 数组名 = new 数据类型[m][];
		
		m:表示这个二维数组有多少个一维数组。
		列数没有给出，可以动态的给。这一次是一个变化的列数。
*/
class Array2Demo2 {
	public static void main(String[] args) {
		//定义数组
		int[][] arr = new int[3][];
		
		System.out.println(arr);	//[[I@175078b
		System.out.println(arr[0]); //null
		System.out.println(arr[1]); //null
		System.out.println(arr[2]); //null
		
		//动态的为每一个一维数组分配空间
		arr[0] = new int[2];
		arr[1] = new int[3];
		arr[2] = new int[1];
		
		System.out.println(arr[0]); //[I@42552c
		System.out.println(arr[1]); //[I@e5bbd6
		System.out.println(arr[2]); //[I@8ee016
		
		System.out.println(arr[0][0]); //0
		System.out.println(arr[0][1]); //0
		//ArrayIndexOutOfBoundsException
		//System.out.println(arr[0][2]); //错误
		
		arr[1][0] = 100;
		arr[1][2] = 200;
	}
}
--------------------------------------------------
/*
	格式3：
		基本格式：
			数据类型[][] 数组名 = new 数据类型[][]{{元素1,元素2...},{元素1,元素2...},{元素1,元素2...}};
		简化版格式：
			数据类型[][] 数组名 = {{元素1,元素2...},{元素1,元素2...},{元素1,元素2...}};
			
		举例：
			int[][] arr = {{1,2,3},{4,5,6},{7,8,9}};
			int[][] arr = {{1,2,3},{4,5},{6}};
*/
class Array2Demo3 {
	public static void main(String[] args) {
		//定义数组
		int[][] arr = {{1,2,3},{4,5},{6}};
		
		System.out.println(arr);
		System.out.println(arr[0]);
		System.out.println(arr[1]);
		System.out.println(arr[2]);
		
		System.out.println(arr[0][0]); //1
		System.out.println(arr[1][0]); //4
		System.out.println(arr[2][0]); //6
		
		System.out.println(arr[0][1]); //2
		System.out.println(arr[1][1]); //5
		//越界
		System.out.println(arr[2][1]); //错误
	}
}
------------------------------------------------------
/*
	需求：二维数组遍历
	
	外循环控制的是二维数组的长度，其实就是一维数组的个数。
	内循环控制的是一维数组的长度。
*/
class Array2Test {
	public static void main(String[] args) {
		//定义一个二维数组
		int[][] arr = {{1,2,3},{4,5,6},{7,8,9}};
		
		//请问谁代表{1,2,3}
		//arr[0]就是第一个数组
		//arr[0] = {1,2,3};
		for(int x=0; x<arr[0].length; x++) {
			System.out.println(arr[0][x]);
		}
		System.out.println("--------------");
		
		for(int x=0; x<arr[1].length; x++) {
			System.out.println(arr[1][x]);
		}
		System.out.println("--------------");
		
		for(int x=0; x<arr[2].length; x++) {
			System.out.println(arr[2][x]);
		}
		System.out.println("--------------");
		
		//用循环改进
		for(int x=0; x<3; x++) {
			for(int y=0; y<arr[x].length; y++) {
				System.out.print(arr[x][y]+" ");
			}
			System.out.println();
		}
		System.out.println("--------------");
		
		//这个时候，注意了，3是我们根据上面的代码得出来的
		//但是，它不能针对任何的数组都可以这样
		//所以，我们应该想办法改进
		//其实，外面的这个循环的长度就是二维数组的长度
		
		for(int x=0; x<arr.length; x++) {
			for(int y=0; y<arr[x].length; y++) {
				System.out.print(arr[x][y]+" ");
			}
			System.out.println();
		}
		System.out.println("--------------");
		
		//用方法改进
		//调用方法
		printArray2(arr);
		System.out.println("--------------");
		
		//我们再来一个列数是变化的
		int[][] arr2 = {{1,2,3},{4,5},{6}};
		printArray2(arr2);
	}
	
	/*
		需求：遍历二维数组
		两个明确：
			返回值类型：void
			参数列表：int[][] arr
	*/
	public static void printArray2(int[][] arr) {
		for(int x=0; x<arr.length; x++) {
			for(int y=0; y<arr[x].length; y++) {
				System.out.print(arr[x][y]+" ");
			}
			System.out.println();
		}
	}
}
------------------------------------------------------
/*
	公司年销售额求和
	某公司按照季度和月份统计的数据如下：单位(万元)
	第一季度：22,66,44
	第二季度：77,33,88
	第三季度：25,45,65
	第四季度：11,66,99
	
	分析：
		A:把题目的数据用二维数组来表示
			int[][] arr = {{22,66,44},{77,33,88},{25,45,65},{11,66,99}};
		B:如何求和呢?
			求和其实就是获取到每一个元素，然后累加即可。
		C:定义一个求和变量sum，初始化值是0。
		D:通过遍历就可以得到每一个二维数组的元素。
		E:把元素累加即可。
		F:最后输出sum，就是结果。
*/
class Array2Test2 {
	public static void main(String[] args) {
		//把题目的数据用二维数组来表示
		int[][] arr = {{22,66,44},{77,33,88},{25,45,65},{11,66,99}};
		
		//定义一个求和变量sum，初始化值是0。
		int sum = 0;
		
		//通过遍历就可以得到每一个二维数组的元素。
		for(int x=0; x<arr.length; x++) {
			for(int y=0; y<arr[x].length; y++) {
				//把元素累加即可。
				sum += arr[x][y];
			}
		}
		
		//最后输出sum，就是结果。
		System.out.println("一年的销售额为："+sum+"万元");
	}
}
-----------------------------------------------------------
/*

	需求：打印杨辉三角形(行数可以键盘录入)
	
	1
	1 1	
	1 2 1
	1 3 3 1
	1 4 6 4 1 
	1 5 10 10 5 1

	分析：看这种图像的规律
		A:任何一行的第一列和最后一列都是1
		B:从第三行开始，每一个数据是它上一行的前一列和它上一行的本列之和。
	
	步骤：
		A:首先定义一个二维数组。行数如果是n，我们把列数也先定义为n。
		  这个n的数据来自于键盘录入。
		B:给这个二维数组任何一行的第一列和最后一列赋值为1
		C:按照规律给其他元素赋值
			从第三行开始，每一个数据是它上一行的前一列和它上一行的本列之和。
		D:遍历这个二维数组。
*/
import java.util.Scanner;

class Array2Test3 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		//这个n的数据来自于键盘录入。
		System.out.println("请输入一个数据：");
		int n = sc.nextInt();
		
		//定义二维数组
		int[][] arr = new int[n][n];
		
		//给这个二维数组任何一行的第一列和最后一列赋值为1
		for(int x=0; x<arr.length; x++) {
			arr[x][0] = 1; //任何一行第1列
			arr[x][x] = 1; //任何一行的最后1列
		}
		
		//按照规律给其他元素赋值
		//从第三行开始，每一个数据是它上一行的前一列和它上一行的本列之和。
		for(int x=2; x<arr.length; x++) {
			//这里如果y<=x是有个小问题的，就是最后一列的问题
			//所以这里要减去1
			//并且y也应该从1开始，因为第一列也是有值了
			for(int y=1; y<=x-1; y++) {
				//每一个数据是它上一行的前一列和它上一行的本列之和。
				arr[x][y] = arr[x-1][y-1] + arr[x-1][y];
			}
		}
		
		//遍历这个二维数组。
		/*
		for(int x=0; x<arr.length; x++) {
			for(int y=0; y<arr[x].length; y++) {
				System.out.print(arr[x][y]+"\t");
			}
			System.out.println();
		}
		*/
		//这个时候，要注意了，内循环的变化必须和曾经讲过的九九乘法表类似
		for(int x=0; x<arr.length; x++) {
			for(int y=0; y<=x; y++) {
				System.out.print(arr[x][y]+"\t");
			}
			System.out.println();
		}
	}
}
------------------------------------------------------
/*
	思考题1：看程序写结果，然后分析为什么是这个样子的。并画图讲解。最后总结Java中参数传递规律。
	
	Java中的参数传递问题：
		基本类型：形式参数的改变对实际参数没有影响。
		引用类型：形式参数的改变直接影响实际参数。
*/
class ArgsDemo {
	public static void main(String[] args) {
		int a = 10;
		int b = 20;
		System.out.println("a:"+a+",b:"+b); //a:10,b:20
		change(a,b);
		System.out.println("a:"+a+",b:"+b); //???	a:10,b:20

		int[] arr = {1,2,3,4,5}; 
		change(arr);
		System.out.println(arr[1]); //???	4
	}

	public static void change(int a,int b) { //a=10,b=20
		System.out.println("a:"+a+",b:"+b); //a:10,b:20
		a = b;	//a=20
		b = a + b; //b=40
		System.out.println("a:"+a+",b:"+b); //a:20,b:40
	}

	public static void change(int[] arr) { //arr={1,2,3,4,5};
		for(int x=0; x<arr.length; x++) {
			if(arr[x]%2==0) {
				arr[x]*=2;
			}
		}
		//arr={1,4,3,8,5};
	}
}
-----------------------------------------------------------------
/*
	某个公司采用公用电话传递数据信息，数据是小于8位的整数，为了确保安全，
	在传递过程中需要加密，加密规则如下：
		首先将数据倒序，然后将每位数字都加上5，再用和除以10的余数代替该数字，
		最后将第一位和最后一位数字交换。 请任意给定一个小于8位的整数，
		然后，把加密后的结果在控制台打印出来。 
		
	题目要求：
		A:数据是小于8位的整数
			定义一个int类型的数据
			int number = 123456;
		B:加密规则
			a:首先将数据倒序
				结果 654321
			b:然后将每位数字都加上5，再用和除以10的余数代替该数字
				结果 109876
			c:最后将第一位和最后一位数字交换
				结果 609871
		C:把加密后的结果输出在控制台
		
		通过简单的分析，我们知道如果我们有办法把这个数据变成数组就好了。
		不是直接写成这个样子的：
			int[] arr = {1,2,3,4,5,6};
			
		如何把数据转成数组呢?
			A:定义一个数据
				int number = 123456;
			B:定义一个数组,这个时候问题就来了，数组的长度是多少呢?
				int[] arr = new int[8]; //不可能超过8
				在赋值的时候，我用一个变量记录索引的变化。
				定义一个索引值是0
				int index = 0;
			C:获取每一个数据
				int ge = number%10
				int shi = number/10%10
				int bai = number/10/10%10
				
				arr[index] = ge;
				index++;
				arr[index] = shi;
				index++;
				arr[index] = bai;
				...
*/
class JiaMiDemo {
	public static void main(String[] args) {
		//定义一个数据
		int number = 123456;
		
		//定义一个数组
		int[] arr = new int[8];
		
		//把数据中每一位上的数据获取到后存储到数组中
		/*
		int index = 0;
		arr[index] = number%10; //arr[0]=6;
		index++;
		arr[index] = number/10%10; //arr[1]=5;
		index++;
		arr[index] = mumber/10/10%10; //arr[2]=4;
		*/
		
		//通过观察这个代码，我们发现应该是可以通过循环改进的
		int index = 0;
		
		while(number > 0) { //number=123456,number=12345,number=1234,number=123,number=12,number=1,number=0
			arr[index] = number%10; //arr[0]=6,arr[1]=5,arr[2]=4,arr[3]=3,arr[4]=2,arr[5]=1
			index++;//index=1,index=2,index=3,index=4,index=5,index=6
			number/=10;//number=12345,number=1234,number=123,number=12,number=1,number=0
		}
		
		//然后将每位数字都加上5，再用和除以10的余数代替该数字
		for(int x=0; x<index; x++) {
			arr[x] += 5;
			arr[x] %= 10;
		}
		
		//最后将第一位和最后一位数字交换
		int temp = arr[0];
		arr[0] = arr[index-1];
		arr[index-1] = temp;
		
		//输出数据
		for(int x=0; x<index; x++) {
			System.out.print(arr[x]);
		}
		System.out.println();
	}
}
-----------------------------------------------------
/*
	把刚才的代码改进一下：
		A:把数据改进为键盘录入
		B:把代码改进为方法实现
		
		
		另一个数据的测试：
		number:1234567
		第一步：7654321
		第二步：2109876
		第三步：6109872
		
	知识点：
		变量
		数据类型
		运算符
		键盘录入
		语句
		方法
		数组
*/
import java.util.Scanner;

class JiaMiDemo2 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		//请输入一个数据
		System.out.println("请输入一个数据(小于8位)：");
		int number = sc.nextInt();
		
		//写功能实现把number进行加密
		//调用
		String result = jiaMi(number);
		System.out.println("加密后的结果是："+result);
	}
	
	/*
		需求：写一个功能，把数据number实现加密。
		两个明确：
			返回值类型：String 做一个字符串的拼接。
			参数列表：int number
	*/
	public static String jiaMi(int number) {
		//定义数组
		int[] arr = new int[8];
		
		//定义索引
		int index = 0;
		
		//把number中的数据想办法放到数组中
		while(number > 0) {
			arr[index] = number%10;
			index++;
			number /= 10;
		}
		
		//把每个数据加5，然后对10取得余数
		for(int x=0; x<index; x++) {
			arr[x] += 5;
			arr[x] %= 10;
		}
		
		//把第一位和最后一位交换
		int temp = arr[0];
		arr[0] = arr[index-1];
		arr[index-1] = temp;
		
		//把数组的元素拼接成一个字符串返回
		//定义一个空内容字符串
		String s = "";
		
		for(int x=0; x<index; x++) {
			s += arr[x];
		}
		
		return s;
	}
}
```

#### 面向对象

- 面向对象思想的引入
  - 我们讲过数组，当有多人数组都需要遍历时，我们可以将遍历的代码封装到方法中，需要遍历时就调用相应的方法即可，提高代码的复用性，在对数组遍历的基础上继续增加需求，比如获取最大值，数值逆序等，同样需要这些封装到方法中，这样封装会发现方法越来越多，于是想能不能把这些方法继续封装呢，前面讲解我们了解到类似可以存放方法的，所以，我们就考虑使用类似封装这多个方法，将来在做数组操作时，不用去找具体的方法，先找到这个类，然后在使用这个类中的方法，这就是我们所说的**面向对象编程的思想**
  - 我们完成一个需求的步骤：首先是要搞清楚我们要做什么，然后在分析怎么做，最我我们在代码体现，一步一步的去实现，而具体的每一步都需要我们去实现和操作，这些步骤相互协调和调用，完成我们的需求
  - 在上面的步骤中，每一步我们都是参与者，并且都需要面对每一个步骤和过程，这就是**面向过程**最直接的体现
  - 那么什么是面向过程开发呢?面向过程其实就是面向着具体的第一个步骤和过程，把每一个不予和过程完成，然后由这些功能方法相互调用，完成需求
  - 面向过程的代表语言：C语言

- 面向对象的思想概述
  - 面向对象是基于面向过程的编程思想
    - 是一种更符合我们思想习惯的思想
    - 可以将复杂的事情简单化
    - 将我们从执行者变成了指挥者
      - 角色发生了转换

```java
1:面向对象思想
	面向对象是基于面向过程的编程思想。
	
	面向过程：强调的是每一个功能的步骤
	面向对象：强调的是对象，然后由对象去调用功能
	
2:面向对象的思想特点
	A:是一种更符合我们思想习惯的思想
	B:可以将复杂的事情简单化
	C:将我们从执行者变成了指挥者
		
	举例：
		买电脑：
			面向过程：我的了解电脑--了解我自己的需求--找对应的参数信息--去中关村买电脑--讨价还价--买回电脑
			面向对象：我知道我要买电脑 -- 班长去给我买 -- 班长就买回来了
		洗衣服：
			面向过程：把衣服脱下--找一个盆--放点洗衣粉--加点水--把衣服扔进去--搓一搓--清洗衣服--拧干--晾起来
			面向对象：把衣服脱下--打开全自动洗衣机--扔进去--一键即可--晾起来
		吃饭：
			面向过程：去超市买菜--摘菜--洗菜--切菜--炒菜--盛起来--吃
			面向对象：上饭店吃饭，你--服务员(点菜)--厨师(做菜)--服务员(端菜)--吃
			
			家常事物，买洗衣机和去饭店太不划算了，所以，找个对象。
			但是，你不跟我好好学习，你将来4000，你对象8000。
			
3:把大象装进冰箱
	面向过程：
		动作有哪些呢?
			A:打开冰箱门
			B:装进大象
			C:关闭冰箱门
			
		代码体现；
			class Demo {
				public static void main(String[] args) {
					/*
					System.out.println("打开冰箱门");
					//打开冰箱门的东西，我现在仅仅是为了演示，就写了一个输出语句
					//其实，它可能需要做很多操作。
					//这个时候代码就比较多一些了
					//假设我要多次打开冰箱门，
					//代码一多，每次都写一遍，麻烦不
					//我们就应该用方法改进
					
					System.out.println("装进大象");
					System.out.println("关闭冰箱门");
					*/
					
					//写了方法以后，调用就改变了
					open();
					in();
					close();
				}
				
				public static void open() {
					System.out.println("打开冰箱门");
				}
				
				public static void in() {
					System.out.println("装进大象");
				}
				
				public static void close() {
					System.out.println("关闭冰箱门");
				}
			}
	
	面向对象：
		我们怎么才能更符合面向对象思想呢?
			A:有哪些类呢?
			B:每个类有哪些东西呢?
			C:类与类直接的关系是什么呢?
			
		把大象装进冰箱的分析? (如何分析有哪些类呢?UML。名词提取法。)
			A:有哪些类呢?
				大象
				冰箱
				Demo
			B:每个类有哪些东西呢?
				大象：
					进去
				冰箱：
					开门
					关门
				Demo:
					main方法
			C:类与类直接的关系是什么呢?
				Demo中使用大象和冰箱类的功能。
				
		代码体现：
			class 大象 {
				public static void in() {
					System.out.println("装进大象");
				}
			}
			
			class 冰箱 {
				public static void open() {
					System.out.println("打开冰箱门");
				}
				
				public static void close() {
					System.out.println("关闭冰箱门");
				}
			}
			
			class Demo {
				public static void main(String[] args) {
					冰箱调用开门
					大象调用进去
					冰箱调用关门
				}
			}
			
4:开发，设计，特征
面向对象开发
	就是不断的创建对象，使用对象，指挥对象做事情。
	
面向对象设计
	其实就是在管理和维护对象之间的关系。

面向对象特征
	封装(encapsulation)
	继承(inheritance)
	多态(polymorphism)
------------------------------------------------
现实世界中是如何描述一个事物的呢?
	举例：学生
			姓名,年龄,性别...
			学习,吃饭,睡觉
			
	属性：该事物的描述信息
	行为：该事物能够做什么
	
我们学习编程语言，是为了模拟现实世界的事物的。
而我们学习的编程语言Java中最基本的单位是：类。
所以，我们就应该把事物通过类来体现出来：
由此，我们就得到了现实世界事物和类的对应关系：

事物：						类：	
	属性						成员变量
	行为						成员方法
	
	
类：是一组相关的属性和行为的集合。是一个抽象的概念。
对象：是该类事物的具体表现形式。具体存在的个体。

举例：
	学生：类
	班长：对象
```



```java
/*
	手机事物：
		属性：品牌，价格，颜色...
		行为：打电话，发短信，玩游戏...
		
	手机类：
		成员变量：品牌，价格，颜色
		成员方法：打电话，发短信，玩游戏
*/
class Phone {
	//品牌
	String brand;
	//价格
	int price;
	//颜色
	String color;
	
	//打电话的方法
	public void call(String name) {
		System.out.println("给"+name+"打电话");
	}
	
	//发短信的方法
	public void sendMessage() {
		System.out.println("群发短信");
	}
	
	//玩游戏的方法
	public void playGame() {
		System.out.println("玩游戏");
	}
}
---------------------------------------------------
/*
	手机类的测试
*/
class Phone {
	//品牌
	String brand;
	//价格
	int price;
	//颜色
	String color;
	
	//打电话的方法
	public void call(String name) {
		System.out.println("给"+name+"打电话");
	}
	
	//发短信的方法
	public void sendMessage() {
		System.out.println("群发短信");
	}
	
	//玩游戏的方法
	public void playGame() {
		System.out.println("玩游戏");
	}
}

class PhoneDemo {
	public static void main(String[] args) {
		//创建手机对象
		//类名 对象名 = new 类名();
		Phone p = new Phone();
		
		//直接输出成员变量值
		System.out.println(p.brand+"---"+p.price+"---"+p.color);
		
		//给成员变量赋值
		p.brand = "诺基亚";
		p.price = 100;
		p.color = "灰色";
		//再次输出
		System.out.println(p.brand+"---"+p.price+"---"+p.color);
		
		//调用方法
		p.call("林青霞");
		p.sendMessage();
		p.playGame();
	}
}
-----------------------------------------------------
/*
	事物：
		属性	事物的信息描述
		行为	事物的功能
	
	类：
		成员变量	事物的属性
		成员方法	事物的行为
		
	定义一个类，其实就是定义该类的成员变量和成员方法。
	
	案例：我们来完成一个学生类的定义。
	
	学生事物：
		属性：姓名，年龄，地址...
		行为：学习，吃饭，睡觉...
		
	把事物要转换为对应的类：
	
	学生类：
		成员变量：姓名，年龄，地址...
		成员方法：学习，吃饭，睡觉...
		
	成员变量：和以前变量的定义是一样的格式，但是位置不同，在类中方法外。
	成员方法：和以前的方法定义是一样的格式，但是今天把static先去掉。
	
	首先我们应该定义一个类，然后完成类的成员。
*/
//这是我的学生类
class Student {
	//定义变量
	//姓名
	String name;
	//年龄
	int age;
	//地址
	String address;
	
	//定义方法
	//学习的方法
	public void study() {
		System.out.println("学生爱学习");
	}
	
	//吃饭的方法
	public void eat() {
		System.out.println("学习饿了,要吃饭");
	}
	
	//睡觉的方法
	public void sleep() {
		System.out.println("学习累了,要睡觉");
	}
}
------------------------------------------------
/*
	在一个java文件中写两个类：一个基本的类，一个测试类。
	注意：文件名称和测试类名称一致。
	
	如何使用呢?
		创建对象使用。
		
	如何创建对象呢?
		格式：类名 对象名 = new 类名();
		
	如何使用成员变量呢?
		对象名.变量名
	如何使用成员方法呢?
		对象名.方法名(...)
*/
//这是学生类
class Student {
	//姓名
	String name; //null
	//年龄
	int age; //0
	//地址
	String address; //null
	
	//学习
	public void study() {
		System.out.println("学生爱学习");
	}
	
	//吃饭
	public void eat() {
		System.out.println("学习饿了，要吃饭");
	}
	
	//睡觉
	public void sleep() {
		System.out.println("学习累了，要睡觉");
	}
}

//这是学生测试类
class StudentDemo {
	public static void main(String[] args) {
		//类名 对象名 = new 类名();
		Student s = new Student();
		
		//输出成员变量值
		//System.out.println(s.name);
		//System.out.println(s.age);
		//System.out.println(s.address);
		//改进写法
		System.out.println(s.name+"---"+s.age+"---"+s.address);
		
		
		//给成员变量赋值
		s.name = "林青霞";
		s.age = 27;
		s.address = "北京";
		//赋值后的输出
		System.out.println(s.name+"---"+s.age+"---"+s.address);
		
		//调用方法
		s.study();
		s.eat();
		s.sleep();
	}
}
```

