---
title: C++编程题目整合
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-26 18:51:17
password:
summary: 就从第四章类与对象开始吧，前面的章节和c差不多在另一篇文章。
tags:
- 学习笔记
categories:
- C++
---



**就从第四章类与对象开始吧，前面的章节和c差不多。**



### 1.点类定义和使用

**【问题描述】**

定义一个点类，该类包含整形坐标x,y以及用于设置坐标值的函数，名为setxy（）参数自行确定，以及用于显示坐标的函数displayxy()参数自行设置。合理编写主函数，能够实现（3，4）以及（5，6）固定两个点对象的参数设置，以及信息输出

**【输入形式】**

无数据输入，请一定使用类的定义以及对象的创建的相关知识

**【输出形式】**

输出两个固定点的相关信息

**【样例输入】**

**【样例输出】**

The first point is:(3,4)

The second point is:(5,6)



```c++
#include<iostream>
using namespace std;
class Point {
	public:
		  	Point(int a,int b) 
		  	{ 	x=a;
		  		y=b;
			} 
		  void setxy(int a,int b)
		  {
		  	  x=a;
		  	  y=b;
		  }
		 		 void display()
		 {
		 	cout<<"The first point is"<<":"<<"("<<x<<","<<y<<")"<<endl;
		 	//cout<<"The second point is"<<":"<<"("<<5<<","<<6<<")"<<endl;
		 }
	private: 
		int x,y;
};
int main()
{
	//int a,b,c,d;
	Point s1(3,4);
	Point s2(5,6);
	//s.setxy(3,4);
	//s.display();
	//s.setxy(5,6);
	s1.display();
	s2.display();
	return 0;
}
```



------

### 2.三角形类

**【问题描述】**

定义一个描述三角形的类Tri，其具体要求为：  

（1）私有数据成员为三角形的三边 

 （2）公有成员函数      构造函数：用以初始化指定的三角形对象；求三角形的边长的成员函数；求三角形面积的成员函数；输出三角形各种参数的成员函数即用以输出三角形对象的边长、周长和面积。

**【输入形式】**

输入三角形的三边长 【输出形式】若构成三角形，输出三角形的边长、周长及面积，否则输出“不构成三角形!” 

**【样例输入1】**

  3 4 5 

**【样例输出1】**    

三角形的边长:3 4 5  三角形的周长:12  三角形的面积:6

**【样例输入1】** 

 1 2 3 

**【样例输出1】**   

 不构成三角形!



```c++
#include<iostream>
#include<math.h>
using namespace std; 

class Tri
{
		double a,b,c;  //定义三角形的三边
	public:
		Tri(double x, double y, double z) //构造函数，初始化三边
		{		a=x; b=y;c=z;		}
		
		double Peri()  //返回三角形的周长
		{		return (a+b+c);		}
		
		double Area()  //返回三角形的面积
		{	double s=Peri()/2;
			double area=sqrt(s*(s-a)*(s-b)*(s-c));
			return area;
		}
		
		void Show() //输出三角形的参数
		{	cout<<"三角形的边长:"<<a<<' '<<b<<' '<<c<<endl;
			cout<<"三角形的周长:"<<Peri()<<endl;
			cout<<"三角形的面积:"<<Area()<<endl<<endl;
		}
		
};//三角形类的定义结束，定义了三角形的各种属性和可实施的操作

int main()
{	double x,y,z;
	cin>>x>>y>>z;
	Tri tri(x,y,z);
	
	if(x+y>z&&y+z>x&&x+z>y)
		tri.Show();  //输出这两个三角形的参数
	else
		cout<<"不构成三角形!"<<endl;
	
}
```





------



### 3.设计一个Time类

**【问题描述】**

定义了一个以hours, minutes和seconds作为数据成员的Time类。设计了成员函数将两个Time对象相加（即时间相加），并进行相应的检查，查看增加的分钟数及秒数是否大于59。如果秒数大于59，则分钟数向前递增1。类似地，如果分钟数大于59，则小时数向前增1。

**【输入形式】**

输入两个由时、分、秒构成的时间。 

**【输出形式】**

输出输入的两个时间相加后的时间

 **【样例输入】**

  2 34 45  1 47 56

**【样例输出】**

  the result is:4:22:41

**【样例输入】**

​    2 67 100  1 56 200

**【样例输出】**

  the result is:5:8:0



```c++
#include<iostream>
using namespace std; 

class Time
{
	private:
		  int hours, minutes, seconds;
	public:
		void get_time()
		{
		    cin>>hours>>minutes>>seconds;
		}
		
		void display_time()
		{
		    cout<<hours<<':'<<minutes<<':'<<seconds<<endl;
		}
		
		void add_time(Time & t1, Time & t2)
		{	int tmp; 
		    hours=t1.hours+t2.hours;
		    minutes=t1.minutes+t2.minutes;
		    seconds=t1.seconds+t2.seconds;
		    if(seconds>=60)
		    {  tmp=seconds/60;
		       seconds-=tmp*60;
		       minutes=minutes+tmp;
		    }
		    if(minutes>=60)
		    {  tmp=minutes/60;
		       minutes-=tmp*60;
		       hours=hours+tmp;
		    }
		}
};

int main()
{
	   Time one, two, three;
	   //cout<<"Enter the first time(hours minutes seconds):";
	   one.get_time();
	   //cout<<"Enter the second time(hours minutes seconds):";
	   two.get_time();
	   three.add_time(one,two);
	   cout<<"the result is:";
	   three.display_time();
}

```

------



### 4.datatype(数据类型)类

**【问题描述】**

声明一个datatype(数据类型)类，该类能够根据用户的输入，确定输入的数据类型，能处理包含字符型、整形、浮点型3种类型的数据，并给出合理的输出。提示：需要进行构造函数的重载

**【输入形式】**

给用户选择，当输入1时，选择输入整型；输入2时，输入字符型；选择3时，输入浮点型。不考虑其他错误情况

**【输出形式】**

输入该数据以及该数据的类型

**【样例输入1】**

2c

**【样例输出1】**

character:c

**【样例输入2】**

112

**【样例输出2】**

int:12

**【样例输入3】**

31.44F

**【样例输出3】**

float:1.44



```c++
#include <iostream>
using namespace std;

class DataType{
	enum
	{
		character,
		integer,
		floating_point
	} vartype;
	union 
	{
		char c;
		int i;
		float f;
	};
	public:
		DataType(char ch) 
		{
			vartype = character;
			c = ch;
		}
		
		DataType(int ii) 
		{
			vartype = integer;
			i = ii;
		}
		
		DataType(float ff) 
		{
			vartype = floating_point;
			f = ff;
		}
		void print();
};

void DataType::print() 
{
	switch (vartype) 
	{
	    case character:
			cout << "字符型: " << c << endl;
			break;
	    case integer:
			cout << "整型: " << i << endl;
			break;
	    case floating_point:
			cout << "浮点型: " << f << endl;
			break;
	}
}

int main() 
{	DataType a('c'), b(12), c(1.44F);
	a.print();
	b.print();
	c.print();
	return 0;
}
```



------

### 5.复数类Complex

**【问题描述】**

定义一个复数类，使得下面的代码能够工作：    

Complex c1(3,5);   

 Complex c2=4.5;   

 c1.add(c2);    

 c1.show(); 

**【输入形式】**

无 

**【输出形式】** 

c1=3 + 5i 

c2=4.5 + 0i  

c1+c2=7.5 + 5i



```c++
#include <iostream>
using namespace std;

class Complex {
	public:
		Complex(double r, double i) :real(r), image(i) { }
		Complex(double r) :real(r), image(0) {}
		void show();
		void add(Complex c2);
	
	private:
		double real;
		double image;
};
void Complex::add(Complex c2) {
	real += c2.real;
	image += c2.image;
}

void Complex::show() {
	cout << real << "+";
	cout << image << "i";
	cout << endl;
}

int main() {
	Complex c1(3, 5);
	Complex c2=4.5;
	cout<<"c1=";
	c1.show();
	cout<<"c2=";
	c2.show();
	c1.add(c2);
	cout<<"c1+c2=";
	c1.show();
	return 0;
}
```



------

### 6.计算由圆和正方形构成的阴影部分的面积

**【问题描述】**

定义一个圆形类，属性有半径和相应的成员函数。然后定义一个正方形类，属性有边长和相应的成员函数。再编写一个如下图所示的组合类，由一个正方型和一个圆形组成，要求该组合类能求出阴影部分面积和周长。

![image.png](http://jsjjs.ctbu.edu.cn/userfiles/image/2020/1586088754215004939.png)

**【输入形式】**

无 

**【输出形式】** 

 自定义图形的面积49.2656  自定义图形的周长29.1328  自定义图形的面积109.098  自定义图形的周长45.6992



```c++
#include <iostream>
using namespace std; 

const double  PI=3.1416;
/**********Program**********/
class Box  //正方形类 
{
	private:
		int A;
	public:
		Box( ){ }  //默认构造函数 
		Box(int x){	A=x;}  //构造函数 
		void set(double a){ A=a;}  //设置边长 
		double S(){	return A*A;	}  //求面积 
		double BL(){	return 4*A;	}  //求周长 
};

class circle  //圆类 
{
	private:
	    int B;
	public:
	  	circle( ){ }; //默认构造函数 
		circle(int x){B=x;} //构造函数
		void set(double b){ B=b;} //设置半径
		double CL(){	return 2*PI*B;	} //求周长 
		double S(){ return PI*B*B;}   //求面积
};

class NewStyle  //组合类 
{
	private:
		circle A;
		Box B;
	public:
		NewStyle( ) {} //默认构造函数
		NewStyle(circle x,Box y):A(x),B(y){}  //构造函数
		void set(circle x,Box y){ A=x;B=y;}  //设置组合图形 
		double S(){	return A.S()-B.S();}     //求面积
		double L(){	return A.CL()+B.BL();};  //求周长
} ; 
/**********  End  **********/
 
int main()
{
    circle A(4);  //圆的半径为4
    Box B(1);   //正方形的边长为1
    NewStyle C(A,B);  
    cout<<"自定义图形的面积"<<C.S()<<endl; 
    cout<<"自定义图形的周长"<<C.L()<<endl; 
    A.set(6);   //圆的半径变为6
    B.set(2);   //正方形的边长变为2
    C.set(A,B);
    cout<<"自定义图形的面积"<<C.S()<<endl; 
    cout<<"自定义图形的周长"<<C.L()<<endl; 
    return 0;
}  

```



------

### 7.CPU类

**【问题描述】**

声明一个CPU类。包含等级(rank)、频率(frequency)、电压(voltage)等属性，有两个公有成员函数run、stop，分别提示“CPU开始运行!”和“CPU停止运行!”。其中，rank为枚举类型CPU_Rank，声明为enum CPU_Rank{ P1=1, P2, P3, P4, P5, P6, P7 }; frequency为单位是MHz的整型数，voltage为浮点型的电压值。用2个CPU对象进行测试观察构造函数和析构函数的调用顺序。

**【输入形式】**

输入CPU的等级，1表示P1，3代表P3

**【输出形式】**

CPU对象的相关信息：构造函数、析构函数的调用情况，CPU对象的运行状况及CPU的等级

**【样例输入1】**

  2 5 

**【样例输出1】** 

 构造了一个CPU! 

 构造了一个CPU! 

 CPU开始运行! 

 等级为:2  

CPU停止运行!

  CPU开始运行!  

等级为:5  

CPU停止运行!

 析构了一个CPU!  

析构了一个CPU!

**【样例输入2】** 

 1 7 

**【样例输出2】** 

 构造了一个CPU!  

构造了一个CPU!  

CPU开始运行!  

等级为:1 

 CPU停止运行!  

CPU开始运行!  

等级为:7  

CPU停止运行!  

析构了一个CPU!  

析构了一个CPU! 



```c++
#include <iostream>
using namespace std;

enum CPU_Rank {P1=1,P2,P3,P4,P5,P6,P7};
class CPU
{
	private:
		CPU_Rank rank;
		int frequency;
		float voltage;
	public:
	    CPU (CPU_Rank r, int f, float v)
		{
			rank = r;
			frequency = f;
			voltage = v;
			cout << "构造了一个CPU!" << endl;
		}
		
		~CPU () { cout << "析构了一个CPU!" << endl; }
	
	    CPU_Rank GetRank() const { return rank; }
	    int GetFrequency() const { return frequency; }
		float GetVoltage() const { return voltage; }
	
	    void SetRank(CPU_Rank r) { rank = r; }
	    void SetFrequency(int f) { frequency = f; }
	    void SetVoltage(float v) { voltage = v; }
	
	    void Run() {cout << "CPU开始运行!" << "\n等级为:"<<rank<<endl; }
		void Stop() {cout << "CPU停止运行!" << endl; }
};

int main()
{
	int r1,r2;
	cin>>r1>>r2;
	CPU a((CPU_Rank)r1,300,2.8);
	CPU b((CPU_Rank)r2,800,8.8);
	a.Run();
	a.Stop();
	b.Run();
	b.Stop();
}
```



持续更新中