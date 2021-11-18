# Java05

#### 方法的概述

- 假设有一个游戏程序，程序在运行的过程中，要不断的发射炮弹，发射炮弹的代码需要编写100行代码，每次实现发射炮弹都要编写这100行代码，这样程序会变得很臃肿，可读性也非常差，为了解决代码重复编写的问题，可以将发射炮弹的代码提取出来放到一个**{}**中，并为这个代码起一个名字，这样每次发射炮弹的地方就通过这个名字来调用发射炮弹代码就可以了，一述过程中，所提取出来的代码可以看作是程序中定义的一个方法，程序在发射炮弹时调用该方法即可。

- 简单的说：方法就是完成特定功能的代码块
  - 在很多语言里面都有函数的定义
  - **函数在Java是被称做方法**

- 格式

```java
修饰符 返回值类型 方法名（参数类型 参数名1，参数名2.....）{
    函数体;
    reture 返回值;
}
```

- 如何写一个方法呢？
  - 返回值类型明确功能结果的数据类型
  - 参数列表 要明确要几个参数，以完成参数的类型

- 方法的执行特点
  - 不调用不执行

- 如何调用

  - 单独调用
    - 一般来说没有什么意义，所以不推荐

  - 输出调用
    - 有意义，但是不够好因为我们可能需要针对结果进行近一步的操作

  - 赋值调用

```java
/*
	方法：完成特定功能的代码块。
	
	注意：在很多语言里面有函数的定义，而在Java中函数被称为方法。

	方法格式：
		修饰符 返回值类型 方法名(参数类型 参数名1,参数类型 参数名2...) {
			方法体语句;
			return 返回值; 
		}
	详细解释：
		修饰符：目前就用 public static。后面我们再详细的讲解其他的修饰符。
		返回值类型：就是功能结果的数据类型。
		方法名：符合命名规则即可。方便我们的调用。
		参数：
			实际参数：就是实际参与运算的。
			形式参数；就是方法定义上的，用于接收实际参数的。
		参数类型：就是参数的数据类型
		参数名：就是变量名
		方法体语句：就是完成功能的代码。
		return：结束方法的。
		返回值：就是功能的结果，由return带给调用者。
		
	要想写好一个方法，就必须明确两个东西：
		A:返回值类型
			结果的数据类型
		B:参数列表
			你要传递几个参数，以及每个参数的数据类型
			
	需求：求两个数据之和的案例
	
	方法的执行特点：
		不调用，不执行。
		
	如何调用呢?(有明确返回值的调用)
		A:单独调用,一般来说没有意义，所以不推荐。
		B:输出调用,但是不够好。因为我们可能需要针对结果进行进一步的操作。
		C:赋值调用,推荐方案。
		
*/
class FunctionDemo {
	public static void main(String[] args) {
		int x = 10;
		int y = 20;
		
		//方式1：单独调用
		//sum(x,y);
	
		//方式2：输出调用
		//System.out.println(sum(x,y));
		//System.out.println(30);
	
		//方式3：赋值调用
		int result = sum(x,y);
		//result在这里可以进行操作
		System.out.println(result);
	}
	
	/*
		需求：求两个数据之和的案例
		
		两个明确：
			返回值类型：int
			参数列表：2个，都是int类型。
	*/
	public static int sum(int a,int b) {
			//如何实现呢?
			//int c = a + b;
			//return c;
			
			//c就是a+b,所以，我可以直接返回a+b
			return a + b;
	}
	
}
---------------------------------------------------------
/*
	方法的注意事项：
		A:方法不调用不执行
		B:方法与方法是平级关系，不能嵌套定义
		C:方法定义的时候参数之间用逗号隔开
		D:方法调用的时候不用在传递数据类型
		E:如果方法有明确的返回值，一定要有return带回一个值
*/
class FunctionDemo2 {
	public static void main(String[] args) {
		/*
		错误的
		public static int sum(int a,int b){
			return a + b;
		}
		*/
		
		//sum(10,20);
		
		//int x = 10;
		//int y = 20;
		//错误
		//sum(int x,int y);
	}
	
	public static int sum(int a,int b){
		return a + b;
	}
}
-----------------------------------------------
/*
	需求：在控制台输出如下的形状
		*****
		*****
		*****
		*****
		
	void类型返回值的方法调用：
		单独调用
		输出调用(错误)
		赋值调用(错误)
*/
class FunctionDemo3 {
	public static void main(String[] args) {
		//for循环嵌套输出图形
		for(int x=0; x<4; x++) {
			for(int y=0; y<5; y++) {
				System.out.print("*");
			}
			System.out.println();
		}
		System.out.println("--------------");
		
		//需求：我要在控制台输出一个6行7列的星形图形
		for(int x=0; x<6; x++) {
			for(int y=0; y<7; y++) {
				System.out.print("*");
			}
			System.out.println();
		}
		System.out.println("--------------");
		
		//如果需要继续改变，我们就应该考虑使用方法改进。
		//单独调用
		pringXing(3,4);
		System.out.println("--------------");
		pringXing(6,7);
		System.out.println("--------------");
		pringXing(8,9);
		
		//输出调用
		//此处不允许使用 '空' 类型
		//System.out.println(pringXing(3,4));
		
		//赋值调用
		//非法的表达式开始
		//void v = pringXing(3,4);
	}
	
	/*
		写一个什么样子的方法呢?写一个m行n列的代码
		
		两个明确：
			返回值类型：这个时候没有明确的返回值，不写东西还不行，所以，这里记住是void
			参数列表：int m,int n
	*/
	public static void pringXing(int m,int n) {
		for(int x=0; x<m; x++) {
			for(int y=0; y<n; y++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
---------------------------------------------------------
/*
	需求：我要求数的和
	
	我们的需求不断的发生改变，我们就对应的提供了多个求和的方法。
	但是呢，他们的名字是不一样的。
	而我们又要求方法命名做到：见名知意。
	但是，很明显，现在没有做到。
	那么，肿么办呢?
	针对这种情况：方法的功能相同，参数列表不同的情况，为了见名知意，Java允许它们起一样的名字。
	
	其实，这种情况有一个专业名词：方法重载。
	
	方法重载：
		在同一个类中，方法名相同，参数列表不同。与返回值类型无关。
		
		参数列表不同：
			A:参数个数不同
			B:参数类型不同
*/
class FunctionDemo4 {
	public static void main(String[] args) {
		//jvm会根据不同的参数去调用不同的功能
		System.out.println(sum(10,20));
		System.out.println(sum(10,20,30));
		System.out.println(sum(10,20,30,40));
		
		System.out.println(sum(10.5f,20f));
	}
	
	//需求1:求两个数的和
	public static int sum(int a,int b) {
		System.out.println("int");
		return a + b;
	}
	
	//需求2:求三数的和
	/*
	public static int sum1(int a,int b,int c) {
		return a + b + c;
	}
	*/
	
	public static int sum(int a,int b,int c) {
		return a + b + c;
	}
	
	//需求3:求四个数的和
	/*
	public static int sum2(int a,int b,int c,int d) {
		return a + b + c + d;
	}
	*/
	public static int sum(int a,int b,int c,int d) {
		return a + b + c + d;
	}
	
	public static float sum(float a,float b) {
		System.out.println("float");
		return a + b;
	}
}
--------------------------------------------------------
/*
	键盘录入两个数据，返回两个数中的较大值
*/
import java.util.Scanner;

class FunctionTest {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入第一个数据:");
		int a = sc.nextInt();
		
		System.out.println("请输入第二个数据:");
		int b = sc.nextInt();
		
		int result = getMax(a,b);
		System.out.println("较大值是："+result);
	}
	
	/*
		需求：两个数中的较大值
		两个明确：
			返回值类型：int
			参数列表：int a,int b			
	*/
	public static int getMax(int a,int b) {
		//if语句
		/*
		if(a > b) {
			//System.out.println(a);
			return a;
		}else {
			//System.out.println(b);
			return b;
		}
		*/
		
		//用三元改进
		//int c = ((a > b)? a: b);
		//return c;
		
		//由于c就是后面的式子
		return ((a>b)? a : b);
	}
}
-------------------------------------------
/*
	键盘录入两个数据，比较两个数是否相等
	
	分析：
		比较两个数是否相等结果是一个boolean类型。
*/
import java.util.Scanner;

class FunctionTest2 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入第一个数据:");
		int a = sc.nextInt();
		
		System.out.println("请输入第二个数据:");
		int b = sc.nextInt();
		
		boolean flag = compare(a,b);
		System.out.println(flag);
	}
	
	/*
		需求：比较两个数是否相等
		两个明确：
			返回值类型：boolean
			参数列表：int a,int b
	*/
	public static boolean compare(int a,int b) {
		//if语句的格式2实现
		/*
		if(a == b) {
			return true;
		}else {
			return false;
		}
		*/
		
		//三元改进
		//boolean flag = ((a==b)? true: false);
		//return flag;
		
		//继续改进
		//return ((a==b)? true: false);
		
		//最终版
		return a == b;
	}
}
----------------------------------------
/*
	键盘录入三个数据，返回三个数中的最大值
*/
import java.util.Scanner;

class FunctionTest3 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入第一个数据:");
		int a = sc.nextInt();
		
		System.out.println("请输入第二个数据:");
		int b = sc.nextInt();
		
		System.out.println("请输入第三个数据:");
		int c = sc.nextInt();
		
		int max = getMax(a,b,c);
		System.out.println("三个数据中的最大值是："+max);
	}
	
	/*
		需求；返回三个数中的最大值
		
		两个明确：
			返回值类型：int
			参数列表：int a,int b,int c
	*/
	public static int getMax(int a,int b,int c) {
		//if嵌套
		/*
		if(a > b) {
			if(a > c) {
				return a;
			}else {
				return c;
			}
		}else {
			if(b > c) {
				return b;
			}else {
				return c;
			}
		}
		*/
		
		//用三元改
		/*
		if(a > b) {
			return (a>c? a: c);
		}else {
			return (b>c? b: c);
		}
		*/
		
		//继续改进
		//return (a>b)? (a>c? a: c): (b>c? b: c);
		//不建议，写代码一定要注意阅读性强
		int temp = ((a>b)? a: b);
		int max = ((temp>c)? temp: c);
		return max;
	}
}
-----------------------------------------------------
/*
	键盘录入行数和列数，输出对应的星形
*/
import java.util.Scanner;

class FunctionTest4 {
	public static void main(String[] args) {
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入行数：");
		int m = sc.nextInt();
		
		System.out.println("请输入列数：");
		int n = sc.nextInt();
		
		//void类型的方法调用
		pringXing(m,n);
	}
	
	/*
		输出星形
		
		两个明确：
			返回值类型：void
			参数列表：int m,int n
	*/
	public static void pringXing(int m,int n) {
		for(int x=0; x<m; x++) {
			for(int y=0; y<n; y++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
-------------------------------------------
/*
	键盘录入一个数据n(1<=n<=9)，输出对应的nn乘法表
*/
import java.util.Scanner;

class FunctionTest5 {
	public static void main(String[] args) {
		//创建对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入n的值：(1~9)");
		int n = sc.nextInt();
		
		//调用
		printNN(n);
	}
	
	/*
		需求：输出对应的nn乘法表
		两个明确：
			返回值类型：void
			参数列表：int n
	*/
	public static void printNN(int n) {
		for(int x=1; x<=n; x++) {
			for(int y=1; y<=x; y++) {
				System.out.print(y+"*"+x+"="+y*x+"\t");
			}
			System.out.println();
		}
	}
}
--------------------------------------------------------------
/*
	比较两个数据是否相等。参数类型分别为
		两个byte类型，两个short类型，两个int类型，两个long类型，
	并在main方法中进行测试
*/
class FunctionTest6 {
	public static void main(String[] args) {
		//测试
		byte b1 = 3;
		byte b2 = 4;
		System.out.println("byte:"+compare(b1,b2));
		
		//测试
		short s1 = 5;
		short s2 = 5;
		System.out.println("short:"+compare(s1,s2));
		
		//后面的两个自己测试
	}
	
	//byte类型
	public static boolean compare(byte a,byte b) {
		System.out.println("byte");
		return a == b;
	}
	
	//short类型
	public static boolean compare(short a,short b) {
		System.out.println("short");
		return a == b;
	}
	
	//int类型
	public static boolean compare(int a,int b) {
		System.out.println("int");
		return a == b;
	}
	
	//long类型
	public static boolean compare(long a,long b) {
		System.out.println("long");
		return a == b;
	}
}
```

#### 数组概述

---

- 需求
  - 现在需要统计某公司员工的工资情况，例如计算平均工资，找到最高工资等，假设该公司有80名员工，用前面所学知识，程序首先需要声明80个变量来分别记住每个员工的工资，然后进行操作，这样做会显得很麻烦，为了解决这个问题，Java就提供了数组给我们使用。

- 数组是什么呢？
  - 数据是存储多个变量(元数)的东西（容器）
  - 这多个变量的数据类型要一致

- 数组的概念
  - 数组是存储同一种类型多个元素的集合，也可以看成是一个容器
  - 数组即可以存储基本数据类型，也可以存储引用数据类型

- 格式
  - 格式1：数据类型[] 数组名;
  - 格式2：数据类型 数组名[];
  - 注意：这俩种定义做完了数组中没有元素值的，如何对数组元素初始化呢？

- 数组的初始化
  - Java中的数组必须先初始化，然后才能使用
  - 所谓初始化，就是为数组中的数组元素分配内容空间，并为每个元素赋值

- 数组初始化的方式
  - 动态初始化：初始化时只指定数组的长度，由系统为数组分配初始化值
    - 格式：数据类型[] 数组名 = new数据类型[数组长度];
    - 数组长度其实就是数组中元数的个数
    - 例子
      - int[] arr = new int[3] ;
      - 解析：定义了一个数组 arr,这个数组可以存放三个int类型的值
  - 静态初始化 ：初始化时指定每个数组元素的初始值，由系统决定数组的长度
    - 格式
      - 数据类型[] 数组名 = new 数据类型[]{元素1，元素2，.....}
    - 举例
      - int[] arr = new int[] {1,2,3};
      - 解释：定义一个int类型的数组，这个数组中存放了三个int类型的数值，并且分别为1，2，3
      - 其实这种写法还有一种简化的写法
        - int[] arr= {1,2,3};

- Java中的内存分配
  - Java程序运行时，需要在内存中分配空间，为了让其提高运算效率，有对空间进行了不同区域的划分，因为每一个区域都有特定的处理数据方式和内存管理方式
  - 栈存储局部变量
  - 堆存储new出来的东西
  - 方法区
  - 本地方法区（和系统相关）
  - 寄存器（给CPU使用）

```java
/*
	数组:存储同一种数据类型的多个元素的容器。
	
	定义格式：
		A:数据类型[] 数组名;
		B:数据类型 数组名[];
		
	举例：
		A:int[] a; 定义一个int类型的数组a变量
		B:int a[]; 定义一个int类型的a数组变量
		
	注意：效果可以认为是一样的，都是定义一个int数组，但是念法上有些小区别。推荐使用第一种。
	
	如何对数组进行初始化呢?
		A:何谓初始化呢? 就是为数组开辟内存空间，并为每个数组元素赋予值
		B:有几种方式呢?
			a:动态初始化 只指定长度，由系统给出初始化值
			b:静态初始化 给出初始化值，由系统决定长度
			
	动态初始化的格式：
		数据类型[] 数组名 = new 数据类型[数组长度];
		
		举例：
		int[] arr = new int[3];	
		
	如何获取数组中的元素呢?
		通过:
			数组名[索引]
			索引其实就是每个元素的编号，从0开始，最大索引是数组的长度-1。
*/
class ArrayDemo {
	public static void main(String[] args) {
		//定义一个数组
		//int[] a;
		//可能尚未初始化变量a
		//System.out.println(a);
		
		int[] arr = new int[3];
		/*
			左边：
				int:说明数组中的元素的数据类型是int类型
				[]:说明这是一个数组
				arr:是数组的名称
				
			右边：
				new:为数组分配内存空间。
				int:说明数组中的元素的数据类型是int类型
				[]:说明这是一个数组
				3:数组长度，其实也就是数组中元素的个数
		*/
		
		System.out.println(arr); //[I@175078b 地址值。
		//我要地址值没有意义啊，我就要数据值，怎么办呢?
		//不用担心，java为你考虑到了。
		//其实数组中的每个元素都是有编号的，并且是从0开始。最大编号是数组的长度-1。
		//用数组名和编号的配合就可以获取数组中的指定编号的元素。这个编号的专业叫法：索引
		//通过数组名访问数据的格式是：数组名[索引];
		System.out.println(arr[0]);
		System.out.println(arr[1]);
		System.out.println(arr[2]);
	}
}
-------------------------------------------------
/*
	定义一个数组，输出该数组的名称和数组元素值。
	给数组元素赋值，再次输出该数组的名称和数组元素值。
*/
class ArrayDemo2 {
	public static void main(String[] args) {
		//定义一个数组
		int[] arr = new int[3];
		
		//输出数组名称
		System.out.println(arr);
		//输出数组元素值
		System.out.println(arr[0]);
		System.out.println(arr[1]);
		System.out.println(arr[2]);
		System.out.println("----");
		
		//给数组元素赋值
		arr[0] = 100;
		arr[2] = 200;
		
		//输出数组名称
		System.out.println(arr);
		//输出数组元素值
		System.out.println(arr[0]);
		System.out.println(arr[1]);
		System.out.println(arr[2]);
	}
}
-----------------------------------------------
/*
	定义两个数组，分别输出两个数组各自的数组名及元素值。
	然后给每个数组的元素重新赋值，再次分别输出两个数组各自的数组名及元素值。
*/
class ArrayDemo3 {
	public static void main(String[] args) {
		//定义第一个数组
		int[] arr = new int[2];
		//定义第二个数组
		int[] arr2 = new int[3];
		
		//输出数组名和元素值
		System.out.println(arr);
		System.out.println(arr[0]);
		System.out.println(arr[1]);
		System.out.println("----");
		
		System.out.println(arr2);
		System.out.println(arr2[0]);
		System.out.println(arr2[1]);
		System.out.println(arr2[2]);
		System.out.println("----");
		
		//给元素重新赋值
		arr[1] = 20;
		
		arr2[1] = 30;
		arr2[0] = 40;
		
		//输出数组名和元素值
		System.out.println(arr);
		System.out.println(arr[0]);
		System.out.println(arr[1]);
		System.out.println("----");
		
		System.out.println(arr2);
		System.out.println(arr2[0]);
		System.out.println(arr2[1]);
		System.out.println(arr2[2]);
	}
}
---------------------------------------------
/*
	定义第一个数组,定义完毕后，给数组元素赋值。赋值完毕后，在输出数组名称和元素。
	定义第二个数组,定义完毕后，给数组元素赋值。赋值完毕后，在输出数组名称和元素。
	定义第三个数组,把第一个数组的地址值赋值给它。(注意类型一致)，通过第三个数组的名称去把元素重复赋值。
	最后，再次输出第一个数组数组名称和元素。
*/
class ArrayDemo4 {
	public static void main(String[] args) {
		//定义第一个数组
		int[] arr = new int[3];
		arr[0] = 88;
		arr[1] = 33;
		arr[2] = 66;
		System.out.println(arr);
		System.out.println(arr[0]);
		System.out.println(arr[1]);
		System.out.println(arr[2]);
		System.out.println("----");
		
		//定义第二个数组
		int[] arr2 = new int[3];
		arr2[0] = 22;
		arr2[1] = 44;
		arr2[2] = 55;
		System.out.println(arr2);
		System.out.println(arr2[0]);
		System.out.println(arr2[1]);
		System.out.println(arr2[2]);
		System.out.println("----");
		
		//定义第三个数组
		int[] arr3 =  arr;
		arr3[0] = 100;
		arr3[1] = 200;
		System.out.println(arr);
		System.out.println(arr[0]);
		System.out.println(arr[1]);
		System.out.println(arr[2]);
	}
}
--------------------------------------------
/*
	数组的静态初始化：
		格式：数据类型[] 数组名 = new 数据类型[]{元素1,元素2,…};
		简化格式：
			数据类型[] 数组名 = {元素1,元素2,…};
		
		举例：
			int[] arr = new int[]{1,2,3};
			
			简化后：
			
			int[] arr = {1,2,3};
			
	注意事项：
		不要同时动态和静态进行。
		如下格式：
			int[] arr = new int[3]{1,2,3}; //错误
*/
class ArrayDemo5 {
	public static void main(String[] args) {
		//定义数组
		int[] arr = {1,2,3};
		
		System.out.println(arr);
		System.out.println(arr[0]);
		System.out.println(arr[1]);
		System.out.println(arr[2]);
	}
}
-----------------------------------------------------
/*
	数组操作的两个常见小问题：
		ArrayIndexOutOfBoundsException:数组索引越界异常
			原因：你访问了不存在的索引。
		
		NullPointerException:空指针异常
			原因：数组已经不在指向堆内存了。而你还用数组名去访问元素。
			
		作用：请自己把所有的场景Exception结尾的问题总结一下。以后遇到就记录下来。
			  现象，原因，解决方案。
*/
class ArrayDemo6 {
	public static void main(String[] args) {
		//定义数组
		int[] arr = {1,2,3};
		
		//System.out.println(arr[3]);
	
		//引用类型的常量：空常量 null
		arr = null;
		System.out.println(arr[0]);
	}
}
-----------------------------------------------
/*
	数组遍历：就是依次输出数组中的每一个元素。
	
	注意：数组提供了一个属性length，用于获取数组的长度。
		  格式：数组名.length
*/
class ArrayTest {
	public static void main(String[] args) {
		//定义数组
		int[] arr = {11,22,33,44,55};
		
		//获取每一个元素
		//如何获取呢?我们知道数组名结合编号(索引)就可以找到数据
		System.out.println(arr[0]);
		System.out.println(arr[1]);
		System.out.println(arr[2]);
		System.out.println(arr[3]);
		System.out.println(arr[4]);
		System.out.println("--------------------");
		
		//虽然这种做法可以，但是不是我想要的
		//我们发现，代码的重复度很高
		//输出语句，数组名都是相同的，仅仅是索引是变化的
		//我们就可以使用循环搞定索引值
		for(int x=0; x<5; x++) {
			//x=0,1,2,3,4
			System.out.println(arr[x]);
		}
		System.out.println("--------------------");
		
		//从0开始我们是明确的，但是为什么到5呢，我们是数了一下数组的个数
		//继续看下个数组如何遍历
		int[] arr2 = {1,2,3,4,5,6,7,8,9,10,11,2,2,3,4,5,7,8,5,3,5,6,8,7,8,5,3,5,6,8,7,8,5,3,5,6,8,7,8,5,3,5,6,8,7,8,5,3,5,6,8};
		//而我们在很多时候，数组的元素不能靠数
		//这个时候，数组就给我们提供了一个属性：length专门用于获取数组的长度
		//格式：数组名.length 返回数组的长度
		System.out.println(arr.length);
		System.out.println(arr2.length);
		System.out.println("--------------------");
		
		//改进第一个程序
		for(int x=0; x<arr.length; x++) {
			System.out.println(arr[x]);
		}
		System.out.println("--------------------");
		
		//我们如果想要对多个数组进行遍历，每个数组的遍历我们都把代码写一遍，麻烦不
		//麻烦，所以，我们准备用方法改进。
		//用方法改进后，请调用
		printArray(arr);
		System.out.println("--------------------");
		printArray(arr2);
		System.out.println("--------------------");
		printArray2(arr);
	}
	
	/*
		遍历数组的方法
		
		两个明确：
			返回值类型：void
			参数列表：int[] arr
	*/
	public static void printArray(int[] arr) {
		for(int x=0; x<arr.length; x++) {
			System.out.println(arr[x]);
		}
	}
	
	//请看改进版本
	public static void printArray2(int[] arr) {
		System.out.print("[");
		for(int x=0; x<arr.length; x++) {
			if(x == arr.length-1) { //这是最后一个元素
				System.out.println(arr[x]+"]");
			}else {
				System.out.print(arr[x]+", ");
			}
		}
	}
}
----------------------------------------------------
/*
	数组获取最值(获取数组中的最大值最小值)
	
	分析：
		A:定义一个数组，并对数组的元素进行静态初始化。
		B:从数组中任意的找一个元素作为参照物(一般取第一个),默认它就是最大值。
		C:然后遍历其他的元素，依次获取和参照物进行比较，如果大就留下来，如果小，就离开。
		D:最后参照物里面保存的就是最大值。
*/
class ArrayTest2 {
	public static void main(String[] args) {
		//定义一个数组
		int[] arr = {34,98,10,25,67};
		
		//请获取数组中的最大值
		/*
		//从数组中任意的找一个元素作为参照物
		int max = arr[0];
		//然后遍历其他的元素
		for(int x=1; x<arr.length; x++) {
			//依次获取和参照物进行比较，如果大就留下来，如果小，就离开。
			if(arr[x] > max) {
				max = arr[x];
			}
		}
		//最后参照物里面保存的就是最大值。
		System.out.println("max:"+max);
		*/
	
		//把这个代码用方法改进
		//调用方法
		int max = getMax(arr);
		System.out.println("max:"+max);
			
		//请获取数组中的最小值
		int min = getMin(arr);
		System.out.println("min:"+min);
	}
	
	/*
		需求：获取数组中的最大值
		两个明确：
			返回值类型：int
			参数列表：int[] arr
	*/
	public static int getMax(int[] arr) {
		//从数组中任意的找一个元素作为参照物
		int max = arr[0];
		//然后遍历其他的元素
		for(int x=1; x<arr.length; x++) {
			//依次获取和参照物进行比较，如果大就留下来，如果小，就离开。
			if(arr[x] > max) {
				max = arr[x];
			}
		}
		//最后参照物里面保存的就是最大值。
		return max;
	}
	
	public static int getMin(int[] arr) {
		//从数组中任意的找一个元素作为参照物
		int min = arr[0];
		//然后遍历其他的元素
		for(int x=1; x<arr.length; x++) {
			//依次获取和参照物进行比较，如果小就留下来，如果大，就离开。
			if(arr[x] < min) {
				min = arr[x];
			}
		}
		//最后参照物里面保存的就是最小值。
		return min;
	}
}
--------------------------------------------------------
/*
	数组元素逆序 (就是把元素对调)
	
	分析：
		A:定义一个数组，并进行静态初始化。
		B:思路
			把0索引和arr.length-1的数据交换
			把1索引和arr.length-2的数据交换
			...
			只要做到arr.length/2的时候即可。
*/
class ArrayTest3 {
	public static void main(String[] args) {
		//定义一个数组，并进行静态初始化。
		int[] arr = {12,98,50,34,76};
		
		//逆序前
		System.out.println("逆序前：");
		printArray(arr);
		
		//逆序后
		System.out.println("逆序后：");
		//reverse(arr);
		reverse2(arr);
		printArray(arr);
	}
	
	/*
		需求：数组逆序
		两个明确：
			返回值类型：void (有人会想到应该返回的是逆序后的数组，但是没必要，因为这两个数组其实是同一个数组)
			参数列表：int[] arr
	*/
	public static void reverse(int[] arr) {
		/*
		//第一次交换
		int temp = arr[0];
		arr[0] = arr[arr.length-1-0];
		arr[arr.length-1-0] = temp;
		
		//第二次交换
		int temp = arr[1];
		arr[1] = arr[arr.length-1-1];
		arr[arr.length-1-1] = temp;
		
		//第三次交换
		int temp = arr[2];
		arr[2] = arr[arr.length-1-2];
		arr[arr.length-1-2] = temp;
		*/
		//用循环改进
		for(int x=0; x<arr.length/2; x++) {
			int temp = arr[x];
			arr[x] = arr[arr.length-1-x];
			arr[arr.length-1-x] = temp;
		}
	}
	
	public static void reverse2(int[] arr) {
		for(int start=0,end=arr.length-1; start<=end; start++,end--) {
			int temp = arr[start];
			arr[start] = arr[end];
			arr[end] = temp;
		}
	}
	
	//遍历数组
	public static void printArray(int[] arr) {
		System.out.print("[");
		for(int x=0; x<arr.length; x++) {
			if(x == arr.length-1) { //这是最后一个元素
				System.out.println(arr[x]+"]");
			}else {
				System.out.print(arr[x]+", ");
			}
		}
	}
}
---------------------------------------------------------
/*
	数组查表法(根据键盘录入索引,查找对应星期)
		意思是：String[] strArray = {"星期一","星期二",...};
*/
import java.util.Scanner;

class ArrayTest4 {
	public static void main(String[] args) {
		//定义一个字符串数组
		String[] strArray = {"星期一","星期二","星期三","星期四","星期五","星期六","星期日"};
		
		//创建键盘录入对象
		Scanner sc = new Scanner(System.in);
		
		System.out.println("请输入一个数据(0-6)：");
		int index = sc.nextInt();
		
		System.out.println("你要查找的日期是："+strArray[index]);
	}
}
--------------------------------------------------------------
/*
	需求：数组元素查找(查找指定元素第一次在数组中出现的索引)
	
	分析：
		A:定义一个数组，并静态初始化。
		B:写一个功能实现
			遍历数组，依次获取数组中的每一个元素，和已知的数据进行比较
			如果相等，就返回当前的索引值。
*/
class ArrayTest5 {
	public static void main(String[] args) {
		//定义一个数组，并静态初始化
		int[] arr = {200,250,38,888,444};
		
		//需求：我要查找250在这个数组中第一次出现的索引
		int index = getIndex(arr,250);
		System.out.println("250在数组中第一次出现的索引是："+index);
		
		int index2 = getIndex2(arr,250);
		System.out.println("250在数组中第一次出现的索引是："+index2);
		
		int index3 = getIndex2(arr,2500);
		System.out.println("2500在数组中第一次出现的索引是："+index3);
	}
	
	/*
		需求：查找指定数据在数组中第一次出现的索引
		两个明确：
			返回值类型：int
			参数列表：int[] arr,int value
	*/
	public static int getIndex(int[] arr,int value) {
		//遍历数组，依次获取数组中的每一个元素，和已知的数据进行比较
		for(int x=0; x<arr.length; x++) {
			if(arr[x] == value) {
				//如果相等，就返回当前的索引值。
				return x;
			}
		}
		
		//目前的代码有一个小问题
		//就是假如我要查找的数据在数组中不存在，那就找不到，找不到，你就对应的返回吗?
		//所以报错。
		
		//只要是判断，就可能是false，所以大家要细心。
		
		
		//如果找不到数据，我们一般返回一个负数即可，而且是返回-1
		return -1;
	}
	
	public static int getIndex2(int[] arr,int value) {
		//定义一个索引
		int index = -1;
		
		//有就修改索引值
		for(int x=0; x<arr.length; x++) {
			if(arr[x] == value) {
				index = x;
				break;
			}
		}
		
		//返回index
		return index;
	}
}
```

