---
title: C++学习笔记整理-类与对象
top: false
cover: false
toc: true
mathjax: true
date: 2020-04-26 18:53:44
password:
summary: 抽象是对具体对象（问题）进行概括，抽出这一类对象的公共性质并加以描述的过程.
tags:
- 学习笔记
categories:
- C++
---





# 第四章 类和对象



## 1.面向对象程序设计的基本特点



### ①抽象



**抽象是对具体对象（问题）进行概括，抽出这一类对象的公共性质并加以描述的过程。**

- 先注意问题的本质及描述，其次是实现过程或细节。

- 数据抽象：描述某类对象的属性或状态（对象相互区别的物理量）。

- 代码抽象：描述某类对象的共有的行为特征或具有的功能。

- 抽象的实现：通过类的声明。





```c++
//数据抽象：
int hour,int minute,int second
//代码抽象：
setTime(),showTime()

class  Clock {
  public: 
   void setTime(int newH, int newM, int newS);   void showTime();
  private: 
   int hour, minute, second;
};

```



### ②封装



**将抽象出的数据成员、代码成员相结合，将它们视为一个整体。**

- 目的是增强安全性和简化编程，使用者不必了解具体的实现细节，而只需要通过外部接口，以特定的访问权限，来使用类的成员。

- 实现封装：类声明中的{}



```c++
//实例：

class  Clock {
  public://公有的访问权限
      void setTime(int newH, int newM, int newS);//外部接口
      void showTime();//外部接口
  private: //私有的访问权限
      int hour, minute, second;
};//边界

```



### ③继承

**是C++中支持层次分类的一种机制，允许程序员在保持原有类特性的基础上，进行更具体的说明。**

- 实现：声明派生类



### ④多态

**多态：同一名称，不同的功能实现方式。**

- 目的：达到行为标识统一，减少程序中标识符的个数。

- 实现：重载函数和虚函数



------



## 2.类和对象



### ①类和对象



**类是具有相同属性和行为的一组对象的集合，它为属于该类的全部对象提供了统一的抽象描述，其内部包括属性和行为两个主要部分。**

- 利用类可以实现数据的封装、隐藏、继承与派生。

- 利用类易于编写大型复杂程序，其模块化程度比C中采用函数更高。

- 定义一个新的class也就定义了一个新的类型



### ②类的定义

类是一种用户自定义类型，声明形式：

```c++
class 类名称
{
   public:
             公有成员（外部接口）
   private:
             私有成员
   protected:
             保护型成员
};
```



- **在关键字public后面声明，它们是类与外部的接口，任何外部函数都可以访问公有类型数据和函数。**

- **在关键字private后面声明，只允许本类中的函数访问，而类外部的任何函数都不能访问。**
  **如果紧跟在类名称的后面声明私有成员，则关键字private可以省略。**

- **protected保护型成员与private类似，其差别表现在继承与派生时对派生类的影响不同**



------

### ③对象



**类的对象是该类的某一特定实体，即类类型的变量。**
声明形式：

```c++c
类名  对象名；
例：Clock  myClock;
```

-  类中成员互访：直接使用成员名

-  类外访问：使用“对象名.成员名”方式访问 public 属性的成员



### ④类的成员函数

- 在类中说明原型，可以在类外给出函数体实现，并在函数名前使用类名加以限定。也可以直接在类中给出函数体，形成内联成员函数。

- 允许声明重载函数和带默认形参值的函数



### ⑤内联成员函数

- **为了提高运行时的效率，对于较简单的函数可以声明为内联形式。**

- 内联函数体中不要有复杂结构（如循环语句和switch语句）。

  

  在类中声明内联成员函数的方式：

  - 将函数体放在类的声明中。
  - 使用inline关键字。



```c++
//example.1类的实现
#include<iostream>
using namespace std;
class Clock{
public:		
	void setTime(int newH = 0, int newM = 0, int newS = 0);
	void showTime();
private:	
	int hour, minute, second;
};
int main()
{
	Clock myClock;
	myClock.setTime(8, 30, 30);
	myClock.showTime();
	return 0;
}

void Clock::setTime(int newH, int newM,int newS)
{
   hour=newH;
   minute=newM;
   second=newS;
}
void Clock::showTime() 
{
   cout << hour << ":" << minute << ":" << second;
}


//运行结果：
8:30:30

```



```c++
//Point类的完整程序

class Point {   //Point 类的定义
public:
	Point(int xx=0, int yy=0) { x = xx; y = yy; }    //构造函数，内联
	Point(const Point& p); //复制构造函数
    void setX(int xx) {x=xx;}
    void setY(int yy) {y=yy;}
	int getX() const { return x; } //常函数（第5章）
	int getY() const { return y; } //常函数（第5章）
private:
	int x, y; //私有数据
};
//成员函数的实现
Point::Point (const Point& p) {
  x = p.x;
  y = p.y;
  cout << "Calling the copy constructor " << endl;
}

//形参为Point类对象的函数
void fun1(Point p) {
	cout << p.getX() << endl;
}
//返回值为Point类对象的函数
Point fun2() {
	Point a(1, 2);
	return a;
}

//主程序
int main() {
	Point a(4, 5);	//第一个对象A
	Point b = a;	//情况一，用A初始化B。第一次调用复制构造函数
	cout << b.getX() << endl;
	fun1(b);	//情况二，对象B作为fun1的实参。第二次调用复制构造函数
	b = fun2();	//情况三，函数的返回值是类对象，函数返回时调用复制构造函数
	cout << b.getX() << endl;
	return 0;
}
```



## 3.构造函数和析构函数



### ①构造函数

- 类中的特殊函数
- 用于描述初始化算法

- 构造函数的作用是在对象被创建时使用特定的值构造对象，将对象初始化为一个特定的初始状态。
- 在对象创建时被自动调用
- 如果程序中未声明，则系统自动产生出一个默认的构造函数，其参数列表为空
- 构造函数可以是内联函数、重载函数、带默认参数值的函数



```c++
//构造函数举例
class Clock {
public:
	Clock(int newH,int newM,int newS);//构造函数
	void setTime(int newH, int newM, int newS);
	void showTime();
private:
	int hour, minute, second;
};

```



```c++
//构造函数的实现：
Clock::Clock(int newH, int newM, int newS): hour(newH), minute(newM), second(newS) {
	}
建立对象时构造函数的作用：
int main() {
  Clock c(0,0,0); //此处将自动调用构造函数
  c.showTime();
	return 0;
}


```



### ②复制构造函数



**复制构造函数是一种特殊的构造函数，其形参为本类的对象引用。作用是用一个已存在的对象去初始化同类型的新对象。**

```c++
class 类名 {
public :
    类名（形参）；//构造函数
    类名（const  类名 &对象名）；//复制构造函数
           ...
}；
类名::类（ const  类名 &对象名）//复制构造函数的实现
{    函数体    }

```



**复制构造函数被调用的三种情况**

- 定义一个对象时，以本类另一个对象作为初始值，发生复制构造；

- 如果函数的形参是类的对象，调用函数时，将使用实参对象初始化形参对象，发生复制构造；

- 如果函数的返回值是类的对象，函数执行完成返回主调函数时，将使用return语句中的对象初始化一个临时无名对象，传递给主调函数，此时发生复制构造。



**有时不应该进行复制和赋值**



- 例如，房屋中介系统有一个类描述待售房屋

```c++
class HomeForSale{…}
//通常没有完全一样的房屋，因此不应有复制构造
```



```c++
//解决方法一：将不应该有的默认函数定义为私有

class HomeForSale{
public:
    …
private:
    …
    HomeForSale(const HomeForSale&);
    HomeForSale& operator=(const HomeForSale&)
        
//解决方法二：定义一个Uncopyable类作为基类

class Uncopyable{
protected:
    Uncopyable(){}
    ~ Uncopyable(){}
private:
     Uncopyable(const Uncopyable&);
     Uncopyable operator=(const Uncopyable&);
};

```





### ③默认构造函数

**调用时可以不需要参数的构造函数都是默认构造函数。**

- 当不定义构造函数时，编译器自动产生默认构造函数

- 在类中可以自定义无参数的构造函数，也是默认构造函数

- 全部参数都有默认形参值的构造函数也是默认构造函数

**下面两个都是默认构造函数，如果在类中同时出现，将产生编译错误：**

```c++
Clock();
Clock(int newH=0,int newM=0,int newS=0);
```



```c++
//example.1
class Clock {
public:
	Clock(int newH,int newM,int newS);//构造函数
	Clock();//默认构造函数
    void setTime(int newH, int newM, int newS);
	void showTime();
private:
	int hour, minute, second;
};
//构造函数的实现：
Clock::Clock(int newH, int newM, int newS): hour(newH), minute(newM), second(newS) { }
//默认构造函数的实现：
Clock::Clock(): hour(0), minute(0), second(0) { }

//建立对象时构造函数的作用：
int main() {
  Clock c(8,10,0); //调用有参构造函数
  Clock c2();//调用无参构造函数
  c.showTime();
  c2.showTime();
	return 0;
}

void Clock::setTime(int newH, int newM,int newS)
{
   hour = newH;
   minute = newM;
   second = newS;
}
void Clock::showTime() 
{
   cout << hour << ":" << minute << ":" << second;
}
```



**有时不应该有默认的构造函数**

- 有些类，不应该有默认初始化。 
  例如，没有姓名的学生对象是没有意义的
  解决：
  至少定义一个有参数的构造函数
  不定义默认构造函数

- 需要深层复制时，默认的复制构造会引起错误。
  解决：
  自定义实现深层复制的复制构造函数







### ④隐含的复制构造函数

如果程序员没有为类声明拷贝初始化构造函数，则编译器自己生成一个隐含的复制构造函数。



这个构造函数执行的功能是：用作为初始值的对象的每个数据成员的值，初始化将要建立的对象的对应数据成员。



### ⑤函数参数尽量传递常引用而不是值

- 传递对象值会引起复制构造和析构，增加时间空间开销。
- 传常引用可避免这一问题。以引用做参数时，尽量使用常引用。

```c++
//例如：
void fun1(const Point &p) {
	cout << p.getX() << endl;
   p.setX(1); //语法错误：p是常引用而setX不是常函数
}
```

基本类型、STL的迭代器和函数对象传值较好。



### ⑥返回值优化

- 当函数返回一个对象时，会构造临时对象用以返回，这会增加开销。

- 用返回引用或者指针替代不是好办法。返回指向局部对象的指针或者引用，会引发错误。返回指向动态内存的指针或引用容易忘记动态空间释放，引起内存泄露。

- 解决显式构造临时对象返回。此举表面上还是构造了一个临时对象，但是编译器通常都会进行优化，使之不产生临时对象。

```c++
//例如：
Point fun2() {
	return Point(1, 2);
}
```





### ⑦析构函数

- 完成对象被删除前的一些清理工作。

- 在对象的生存期结束的时刻系统自动调用它，然后再释放此对象所属的空间。

- 如果程序中未声明析构函数，编译器将自动产生一个隐含的析构函数。



```c++
//构造函数和析构函数举例

#include <iostream>
using namespace std;
class Point {     
public:
  Point(int xx,int yy);
  ~Point();
  //...其他函数原型
private:
  int x, y;
};

Point::Point(int xx,int yy) {
  x = xx;
  y = yy;
}
Point::~Point() {
}
//...其他函数的实现略
```





------



## 3.类的组合

### ①组合

- 类中的成员数据是另一个类的对象。

- 可以在已有抽象的基础上实现更复杂的抽象。



**类组合的构造函数设计**



- 原则：不仅要负责对本类中的基本类型成员数据赋初值，也要对对象成员初始化。

```c++
//声明形式：
类名::类名(对象成员所需的形参，本类成员形参)
       :对象1(参数)，对象2(参数)，......
{  
//函数体其他语句
}

```



**构造组合类对象时的初始化次序**

- 首先对构造函数初始化列表中列出的成员（包括基本类型成员和对象成员）进行初始化，初始化次序是成员在类体中定义的次序。

- 成员对象构造函数调用顺序：按对象成员的声明顺序，先声明者先构造。

- 初始化列表中未出现的成员对象，调用用默认构造函数（即无形参的）初始化

- 处理完初始化列表之后，再执行构造函数的函数体



```c++
//类的组合，线段（Line）类


#include <iostream>
#include <cmath>
using namespace std;
class Point {	//Point类定义
public:
	Point(int xx = 0, int yy = 0) {
		x = xx;
		y = yy;
	}
	Point(Point &p);
	int getX() { return x; }
	int getY() { return y; }
private:
	int x, y;
};
Point::Point(Point &p) {	//复制构造函数的实现
	x = p.x;
	y = p.y;
	cout << "Calling the copy constructor of Point" << endl;
}

public:	//外部接口
	Line(Point xp1, Point xp2);
	Line(Line &l);
	double getLen() { return len; }
private:	//私有数据成员
	Point p1, p2;	//Point类的对象p1,p2
	double len;
};
//组合类的构造函数
Line::Line(Point xp1, Point xp2) : p1(xp1), p2(xp2) {
	cout << "Calling constructor of Line" << endl;
	double x = static_cast<double>(p1.getX() - p2.getX());
	double y = static_cast<double>(p1.getY() - p2.getY());
	len = sqrt(x * x + y * y);
}
Line::Line (Line &l): p1(l.p1), p2(l.p2) {//组合类的复制构造函数
	cout << "Calling the copy constructor of Line" << endl;
	len = l.len;
}

//主函数
int main() {
	Point myp1(1, 1), myp2(4, 5);	//建立Point类的对象
	Line line(myp1, myp2);	//建立Line类的对象
	Line line2(line);	//利用复制构造函数建立一个新对象
	cout << "The length of the line is: ";
	cout << line.getLen() << endl;
	cout << "The length of the line2 is: ";
	cout << line2.getLen() << endl;
	return 0;
}


//运行结果如下：
Calling the copy constructor of Point
Calling the copy constructor of Point
Calling the copy constructor of Point
Calling the copy constructor of Point
Calling constructor of Line
Calling the copy constructor of Point
Calling the copy constructor of Point

```



**前向引用声明**

- 类应该先声明，后使用

- 如果需要在某个类的声明之前，引用该类，则应进行前向引用声明。

- 前向引用声明只为程序引入一个标识符，但具体声明在其他地方。



```c++
//example

class B;  //前向引用声明
class A {
public:
  void f(B b);
};
class B {
public:
  void g(A a);
};
```





**前向引用声明注意事项**



使用前向引用声明虽然可以解决一些问题，但它并不是万能的。需要注意的是，尽管使用了前向引用声明，但是在提供一个完整的类声明之前，不能声明该类的对象，也不能在内联成员函数中使用该类的对象



```c++
class Fred; //前向引用声明
class Barney {
   Fred x; //错误：类Fred的声明尚不完善
};
class Fred {
   Barney y;
};

//更正
class Fred;	//前向引用声明
class Barney {
public:
  ……
  void method() {
    x.yabbaDabbaDo();	//错误：Fred类的对象在定义之前被使用
  }
 private:
  Fred &x;//正确，经过前向引用声明，可以声明Fred类的对象引用
};
 
class Fred {
public:
  void yabbaDabbaDo();
private:
  Barney &y;
}; 

```



**前向引用声明注意事项**



- 应该记住：当使用前向引用声明时，只能使用被声明的符号，而不能涉及类的任何细节。

------



## 4.UML图形标识

### ①UML简介

**UML（Unified Modeling Language）语言是一种可视化的的面向对象建模语言。**

**UML有三个基本的部分**

- 事物（Things）UML中重要的组成部分，在模型中属于最静态的部分，代表概念上的或物理上的元素

- 关系（Relationships）关系把事物紧密联系在一起

- 图（Diagrams）图是很多有相互相关的事物的组



### ②UML类图



**举例：Clock类的完整表示:**



| Clock                                       |
| ------------------------------------------- |
| - hour:  int                                |
| - minute:  int                              |
| - second:  int                              |
| + showTime(): void                          |
| + setTime(newH:int=0,newM:int=0,newS:int=0) |



**Clock类的简洁表示**



| Clock |
| ----- |
|       |



### ③对象图

| myClock:Clock |
| :-----------: |
|  - hour: int  |
| - minute: int |
| - second: int |



### ④几种关系的图形标识



**依赖关系**

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/C-%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%E6%95%B4%E7%90%86/%E5%9B%BE%E7%89%875.png)

图中的“类A”是源，“类B”是目标，表示“类A”使用了“类B”，或称“类A”依赖“类B”



**作用关系—关联**

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/C-%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%E6%95%B4%E7%90%86/%E5%9B%BE%E7%89%874.png)

图中的“重数A”决定了类B的每个对象与类A的多少个对象发生作用，同样“重数B”决定了类A的每个对象与类B的多少个对象发生作用。

**包含关系—聚集和组合**

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/C-%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%E6%95%B4%E7%90%86/%E5%9B%BE%E7%89%876.png)

聚集表示类之间的关系是整体与部分的关系，“包含”、“组成”、“分为……部分”等都是聚集关系。共享聚集：部分可以参加多个整体；组成聚集：整体拥有各个部分，整体与部分共存，如果整体不存在了，那么部分也就不存在了。



***采用UML方法来描述例4-4中Line类和Point类的关系***

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/C-%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%E6%95%B4%E7%90%86/%E5%9B%BE%E7%89%878.png)

**继承关系—泛化**

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/C-%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%E6%95%B4%E7%90%86/%E5%9B%BE%E7%89%877.png)



***带有注释的Line类和Point类关系的描述***

![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/C-%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%E6%95%B4%E7%90%86/%E5%9B%BE%E7%89%873.png)





**注释**

在UML图形上，注释表示为带有褶角的矩形，然后用虚线连接到UML的其他元素上，它是一种用于在图中附加文字注释的机制。

## 5.结构体和联合体

### ①结构体

**结构体是一种特殊形态的类**

- 与类的唯一区别：类的缺省访问权限是private，结构体的缺省访问权限是public

- 结构体存在的主要原因：与C语言保持兼容

**什么时候用结构体而不用类**

- 定义主要用来保存数据、而没有什么操作的类型

- 人们习惯将结构体的数据成员设为公有，因此这时用结构体更方便



**结构体的定义和初始化**

```c++
//结构体定义
struct 结构体名称 {
	 公有成员
protected:
    保护型成员
private:
     私有成员
};


//一些结构体变量的初始化可以用以下形式
类型名 变量名 = { 成员数据1初值, 成员数据2初值, …… };

```



```c++
//1.用结构体表示学生的基本信息

#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

struct Student {	//学生信息结构体
	int num;		//学号
	string name;	//姓名，字符串对象，将在第6章详细介绍
	char sex;		//性别
	int age;		//年龄
};

int main() {
	Student stu = { 97001, "Lin Lin", 'F', 19 };
	cout << "Num:  " << stu.num << endl;
	cout << "Name: " << stu.name << endl;
	cout << "Sex:  " << stu.sex << endl;
	cout << "Age:  " << stu.age << endl;
	return 0;
}

//运行结果：
Num:  97001
Name: Lin Lin
Sex:  F
Age:  19

```





### ②联合体



```c++
//声明形式
union 联合体名称 {
    公有成员
protected:
    保护型成员
private:
    私有成员
};
```



**特点：**

- 成员共用相同的内存单元

- 任何两个成员不会同时有效



**联合体的内存分配**



```c++
union Mark {	//表示成绩的联合体
	char grade;	//等级制的成绩
	bool pass;	//只记是否通过课程的成绩
	int percent;	//百分制的成绩
};

```



![](https://muyiio-1300292673.cos.ap-chongqing.myqcloud.com/%E5%8D%9A%E5%AE%A2/_posts/C-%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0%E6%95%B4%E7%90%86/%E5%9B%BE%E7%89%872.png)





**无名联合**

无名联合没有标记名，只是声明一个成员项的集合，这些成员项具有相同的内存地址，可以由成员项的名字直接访问。

```c++
例：
union {
  int i;
  float f;
}
//在程序中可以这样使用：
i = 10;
f = 2.2;
```



```c++
//example.使用联合体保存成绩信息，并且输出。

#include <string>
#include <iostream>
using namespace std;
class ExamInfo {
private:
	string name;	//课程名称
	enum { GRADE, PASS, PERCENTAGE } mode;//采用何种计分方式
	union {
		char grade;	//等级制的成绩
		bool pass;	//只记是否通过课程的成绩
		int percent;	//百分制的成绩
	};

public:
	//三种构造函数，分别用等级、是否通过和百分初始化
	ExamInfo(string name, char grade)
		: name(name), mode(GRADE), grade(grade) { }
	ExamInfo(string name, bool pass)
		: name(name), mode(PASS), pass(pass) { }
	ExamInfo(string name, int percent)
		: name(name), mode(PERCENTAGE), percent(percent) { }
	void show();
}

void ExamInfo::show() {
	cout << name << ": ";
	switch (mode) {
	  case GRADE: cout << grade;  break;
	  case PASS: cout << (pass ? "PASS" : "FAIL"); break;
	  case PERCENTAGE: cout << percent; break;
	}
	cout << endl;
}

int main() {
	ExamInfo course1("English", 'B');
	ExamInfo course2("Calculus", true);
	ExamInfo course3("C++ Programming", 85);
	course1.show();
	course2.show();
	course3.show();
	return 0;
}

//运行结果：
English: B
Calculus: PASS
C++ Programming: 85
```





------





