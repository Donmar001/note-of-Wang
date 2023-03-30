### C++之对象和类

##### 面向对象编程oop

~~**oop**~~的特性

1. 抽象
2. 封装和数据隐藏
3. 多态
4. 继承
5. 代码的可重用性

用户自定义类时必须完成三项操做：

* 决定数据对象需要的内存数量
* 决定任何解释内存中的位
* 决定可使用数据对象执行的操作或者方法

#### c++中的类

类是一种将抽象转换为用户定义类型的c++工具，他将数据表示和操纵数据的方法组合成一个整洁的包。

##### 类定义的规范

* 类声明：以数据成员的方式描述数据部分，以成员函数（被称为方法）的方式描述共有接口
* 类方法的定义： 描述如何实现类成员函数

简单来说就是类声明提供了蓝图，而类方法的定义提供了实现细节



#### 实现示例

以表示一股股票的类**Stock**举例

储存的信息有：

* 公司名称
* 所持有股票的数量
* 每股的价格
* 股票总值

可执行的操作有（方法）：

* 获得股票
* 增持
* 卖出股票
* 更新股票价格
* 显示关于所持股票的信息



**Stock类的声明**

```C++
#ifndef STOCK__H__
#define STOCK__H__
#include <string>
using namespace std;
class Stock00
{
private:
	std::string company;
	long shares;
	double share_val;
	double total_val;
	void set_tot() { total_val = shares * share_val; }          //使用私有函数来实现不属于公有接口的实现细节
public:
	void acquire(const std::string & co,long n, double pr);
	void buy(long num, double price);
	void sell(long num, double price);
	void update(double price);
	void show();
};

/*另一种定义成员内部函数的方法
inline void Stock00::set_tot(){total_val = shares * share_val;}
*/

#endif
```



**Stock方法的定义**

```C++
#include <iostream>
#include "stock00.h"
using namespace std;

void Stock00::acquire(const std::string & co, long n, double pr) {
	company = co;
	if (n < 0) {
		cout << "Number of shares can't be negative;" << company << " shres set to 0.\n";
		shares = 0;
	}
	else
		shares = n;
	share_val = pr;
	set_tot();                 //Stock类的私有方法
}

void Stock00::buy(long num, double price) {
	if (num < 0) {
		cout << "Number of shares purchases=d can't be negative. " << "Transcation is aborted.\n";
	}
	else
	{
		shares += num;
		share_val = price;
		set_tot();
	}
}

void Stock00::sell(long num, double price) {
	if (num < 0) {
		cout << "Number of shares sold can't be negative. " << "Transcation is aborted.\n";
	}
	else
	{
		shares -= num;
		share_val = price;
		set_tot();
	}
}

void Stock00::update(double price) {
	share_val = price;
	set_tot();
}

void Stock00::show()
{
	ios_base::fmtflags orig = cout.setf(ios_base::fixed, ios_base::floatfield);
	streamsize prec = cout.precision(3);                     //设置数字的显示格式，三位小数
	cout << "Company: " << company
		 << " Sharess: " << shares << "\n"
		 << "Shares Price: $" << share_val
	     << " Total Worth: $" << total_val << "\n";
	cout.setf(orig, ios_base::floatfield);                 ///恢复数字显示格式，原有的科学计数法
	cout.precision(prec);
}

```



##### 访问控制

使用类的对象都可以使用共有部分即定义中的*public*，但只能使用共有公有成员函数（或者友元函数）来访问定义中的私有部分即*private*

故公有成员函数时程序和对象私有成员之间的桥梁，提供了对象和程序之间的接口。防止程序直接访问数据被称为**数据隐藏**

类设计应尽可能将公有接口和实现细节分开。

数据隐藏是一种封装就想上述例子中的set_tot()函数一样，将实现的细节隐藏在私有部分，另外将函数定义和类声明放在不同的文件中也是一种封装



##### 控制对成员的访问

数据项通常放在私有部分，组成类接口的成员函数放在公有部分，使用私有函数来处理不属于公有接口的实现细节

关键字private可忽略，默认位私有成员。



##### 实现类成员函数

* 定义成员函数时使用域解析运算符：：来标识函数所属的类
* 类方法可以访问私有部分private组件

不同类的成员函数的名称可以相通

##### 内联函数

使用关键字inline



##### 使用*Stock*类

```c++
void usestock00() {
	Stock00 fluffy_the_cat;
	fluffy_the_cat.acquire("NanoSart", 20, 12.50);
	fluffy_the_cat.show();
	fluffy_the_cat.buy(15,18.125);
	fluffy_the_cat.show();
	fluffy_the_cat.sell(400, 20.00);
	fluffy_the_cat.show();
	fluffy_the_cat.buy(300000, 40.125);
	fluffy_the_cat.show();
	fluffy_the_cat.sell(300000, 0.125);
	fluffy_the_cat.show();
}
```





#### 类的构造函数与析构函数

对于上述例子不能将类像*int*型一样初始化

不能的原因在于类的数据是私有的，程序不能直接访问，因此需要设计适合的成员函数才能成功初始化对象（如果是数据成员公有化则违背了类的初衷数据隐藏）

##### 构造函数

c++提供了特殊的成员函数类构造函数，c++提供了成员函数德名称和使用语法，而程序员需提供方法定义。名称与类名相同。构造函数没有声明类型。

构造函数的定义：

```c++

Stock::Stock(const std::string & co, long n, double pr) {
	std::cout << "Constructor using " << co << " called\n";
	company = co;

	if (n < 0) {
		std::cout << "Number of shares can't be negative; " << company << " shares set to 0.\n";
		shares = 0;
	}
	else
		shares = n;
	share_val = pr;
	set_tot();
}

```

使用构造函数的方法

1. 显示调用构造函数：
```C++
Stock food = Stock("World Cabbage",50,1.25);
```
2. 隐式调用构造函数：

```c++
Stock garment("Furry Mason",50,2.5);
```

构造函数的使用方法不同于普通的类方法，一般用对象来调用方法，如```stock1.show()```,但是无法使用对象来调用构造函数，因为构造函数构造出对象前对象是不存在的。因此构造函数被用来创建对象，而不能通过对象来调用。**构造函数是一类特殊方法**



##### 默认构造函数

默认构造函数是在未提供显示初始值时用来创建对象的构造函数。

隐式的调用默认构造函数的时候，不使用圆括号```Stock third```



#### 析构函数

用构造函数创建对象后，程序负责跟踪对象，指导其过期为止。对象使用周期结束后，程序自动调用析构函数销毁对象，完成清理工作。，析构函数的名称为~stock()，析构函数也可以没有返回值和声明类型，且一定没有参数。



##### 由此改进的stock类为

stock.h

```c++
#ifndef STOCK10_H_
#define STOCK10_H_
#include<string>
class Stock
{
private:
	std::string company;
	long shares;
	double share_val;
	double total_val;
	void set_tot()
	{
		total_val = shares * share_val;
	}
public:
	Stock();      //默认构造函数
	Stock(const std::string & co, long n = 0, double pr = 0.0);    //构造函数
	~Stock();               //析构函数
	void buy(long num, double price);
	void sell(long num, double price);
	void update(double price);
	void show();

};
#endif

```



stock.cpp(函数方法的定义)

```c++
#include<iostream>
                                                                                                                 #include"stock10.h"
/*默认构造函数，当构造函数未提供任何参数时*/
Stock::Stock() {
	std::cout << "Default constructor called\n";
	company = "no name";
	shares = 0;
	share_val = 0.0;
	total_val = 0.0;
}

Stock::Stock(const std::string & co, long n, double pr) {
	std::cout << "Constructor using " << co << " called\n";
	company = co;

	if (n < 0) {
		std::cout << "Number of shares can't be negative; " << company << " shares set to 0.\n";
		shares = 0;
	}
	else
		shares = n;
	share_val = pr;
	set_tot();
}

Stock::~Stock() {
	std::cout << "Bye, " << company << "!\n";
}

void Stock::buy(long num, double price) {
	if (num < 0)
		std::cout << "NUmber of shares purchased can't be negative. " << "Transation is aborted.\n";
	else
	{
		shares += num;
		share_val = price;
		set_tot();
	}
}

void Stock::sell(long num, double price) {
	using std::cout;
	if (num < 0 )
	{
		cout << "NUmber of shares purchased can't be negative. " << "Transation is aborted.\n";
	}
	else if (num > shares)
	{
		cout << "you can't sell more than yoyu have" 
			<< "Tansaction is aborted.\n";
	}
	else
	{
		shares -= num;
		share_val = price;
		set_tot();
	}
}

void Stock::update(double price) {
	share_val = price;
	set_tot();
}
void Stock::show() {
	using std::cout;
	using std::ios_base;
	ios_base::fmtflags orig =
		cout.setf(ios_base::fixed, ios_base::floatfield);
	std::streamsize prec = cout.precision(3);

	cout << "company: " << company << " Shares:" << shares << "\n";

	cout << " shre price: $" << share_val;
	cout.precision(2);
	cout << "Total Worth: $" << total_val << "\n";

	cout.setf(orig, ios_base::floatfield);
	cout.precision(prec);                          //重置格式
}


```



main()类的使用

```c++
void usestock10() {
	cout << "Using constructors to create new objects\n";
	Stock stock1("NanoSmart", 12, 20.0);
	stock1.show();
	Stock stock2 = Stock("Boffo Objects", 2, 2.0);
	stock2.show();

	cout << "Assigning stock1 to stock2:\n";
	stock2 = stock1;
	cout << "Listing stock1 and stock2\n";
	stock1.show();
	stock2.show();

	cout << "Using a constructor to reset an object\n";
	stock1 = Stock("Nifty Foods", 10, 50.0);
	cout << "Revised stock:\n";
	stock1.show();
	cout << "Done\n";
}

```





##### const成员函数

```c++
const Stock land = Stock("Kludgehron Properties");
land.show();
```

当前代码会报错，因为show方法不能保证数据不被修改。故对于没有参数的方法来说不能使用参数声明或者指向其的指针来解决。

故提供新的方法

```c++
void show() const
```

该方法被称为const成员函数，只要类方法不修改调用对象，就应该声明为const。



#### This指针

this指针指向用来调用成员函数的对象。每个成员函数都有一个this指针，this指针指向调用对象若方法需要引用整个调用对象，则可以使用*this。

例如若要引入比较功能则可以

```c++
const Stock & Stock::topval(const Stock & s) const
{
    if(s.total_val > total_val)
        return s;
    else
        return *this
}
```



#### 对象数组

当需要创建多数对象时，单独创建多个对象效率太低，故需要对象数组。

声明数组的方法

```c++
Stock mystuff[4];
```

可以使用构造函数来初始化对象数组。需对元素调用构造函数

```c++
const int SKTS = 10;
Stock stocks[SKTS]={
    Stock("NanoSmart",12.5,20),
    Stock(),
    Stock("NIhao",12,13),
};
```

上述对象数组使用了构造函数Stock(const std::string & co, long n, double pr)初始化了stock[0]和stock[2],使用构造函数stock()初始化了stock[1],剩余的7个元素将使用默认构造函数进行初始化。

初始化对象数组的方案是，首先使用默认构造函数创建数组元素，然后花括号中的构造函数将创建临时对象，将临时对象的内容复制到相应的元素中。故要**创建类对象数组**，则这个**类必须要有默认构造函数**



### 使用类

#### 运算符重载

要重载运算符，就要使用被称为运算符函数的特殊函数形式。运算符函数格式为 ```operatorop(argument-list)```

且运算符的重载必须使用已有的运算符，如：operator+（）重载+运算符，operator*（）重载\*运算符，而不能重载operator@（）



一个示例，处理时间的Time类，通过名为Sum（）的常规方法来计算时间相加，之后将其改为重载运算符计算。



mytime0.h  类的声明

```c++
#ifndef MYTIME_H_
#define MYTIME_H_
class Time {
private:
	int hours;
	int minutes;
public:
	Time();
	Time(int h,int m = 0);
	void AddMin(int m);
	void AddHr(int h);
	void Reset(int h=0,int m=0);
	Time Sum(const Time & t) const;
	void Show() const;
};
#endif

```



mytime0.cpp   类方法的定义

```c++
#include<iostream>
#include"mytime0.h"

Time::Time() {
	hours = minutes = 0;
}

Time::Time(int h,int m){
	hours = h;
	minutes = m;
}

void Time::AddMin(int m) {
	minutes += m;
	hours += minutes / 60;
	minutes %= 60;
}

void Time::AddHr(int h) {
	hours += h;
}

void Time::Reset(int h, int m) {
	hours = h;
	minutes = m;
}

Time Time::Sum(const Time &t) const {          
	Time sum;
	sum.minutes = minutes + t.minutes;
	sum.hours = hours + sum.minutes / 60 + t.hours;
	sum.minutes %= 60;
	return sum;
}

void Time::Show() const {
	std::cout << hours << " hours, " << minutes << " minutes.\n";

}
```

其中的Sum（）函数中参数为引用，但是返回类型却不是引用  **Time Time::Sum(const Time &t) const**

参数使用引用的理由是传递引用速度更快且使用的内存更少

而函数返回值不能使用引用。因为函数将创建一个新的对象来表示另外两个对象的和。想代码中的这样返回对象时将创建对象的副本，而调用函数可以使用。若返回对象是&Time 则引用的是sum对象，sum对象是一个局部对象，在函数结束后将被销毁，则引用将指向一个不存在的对象。使用返回类型Time则程序在删除sum之前将构造他的拷贝。



usemytime0（）

```
void usetime0() {
	Time Planning;
	Time coding(2, 40);
	Time fixing(5,55);
	Time total;

	cout << "Planning time = ";
	Planning.Show();
	cout << endl;

	cout << "coding time = ";
	coding.Show();
	cout << endl;

	cout << "fixing time = ";
	fixing.Show();
	cout << endl;

	total = coding.Sum(fixing);
	cout << "coding.Sum(fixing) = ";
	total.Show();
	cout << endl;
}
```

**改进后的函数重载**

mytime1.h

```c++
#ifndef MYTIME1_H_
#define MYTIME1_H_
class Time1 {
private:
	int hours;
	int minutes;
public:
	Time1();
	Time1(int h, int m = 0);
	void AddMin(int m);
	void AddHr(int h);
	void Reset(int h = 0, int m = 0);
	Time1 operator+(const Time1 & t) const;        //使用运算符重载来处理时间
	void Show() const;
};
#endif


```

mytime1.cpp

```c++
#include<iostream>
#include"mytime1.h"

Time1::Time1() {
	hours = minutes = 0;
}

Time1::Time1(int h, int m) {
	hours = h;
	minutes = m;
}

void Time1::AddMin(int m) {
	minutes += m;
	hours += minutes / 60;
	minutes %= 60;
}

void Time1::AddHr(int h) {
	hours += h;
}

void Time1::Reset(int h, int m) {
	hours = h;
	minutes = m;
}

Time1 Time1::operator+(const Time1 &t) const {
	Time1 sum;
	sum.minutes = minutes + t.minutes;
	sum.hours = hours + sum.minutes / 60 + t.hours;
	sum.minutes %= 60;
	return sum;
}

void Time1::Show() const {
	std::cout << hours << " hours, " << minutes << " minutes.\n";

}
```

usemytime1()

```c++
void usetime1() {
	Time1 planning;
	Time1 coding(2,40);
	Time1 fixing(5,55);
	Time1 total;

	cout << "Planning time = ";
	planning.Show();
	cout << endl;

	cout << "coding time = ";
	coding.Show();
	cout << endl;

	cout << "fixing time = ";
	fixing.Show();
	cout << endl;

	total = coding + fixing;     //使用重载符号
	cout << "coding + fixing = ";
	total.Show();
	cout << endl;

	Time1 morefixing(3, 28);
	cout << "More fixing time = ";
	morefixing.Show();
	cout << endl;
	total = morefixing.operator+(total);            //将重载符号函数当作一个普通的类方法
	cout << "morefixing.operator+(total) = ";
	total.Show();
	cout << endl;

}
```

有两种方法使用重载符号：

1. 将其当作重载符号使用

```
	total = coding + fixing;     //使用重载符号
```

2. 将其当作方法使用

```
	total = morefixing.operator+(total);            //将重载符号函数当作一个普通的类方法
```



##### 重载限制

1. 重载后的**运算符**必须至少有一个操作数是用户定义的类型。可防止用户为标准类型重载运算符。因此不能将减法运算符重载为两个double型的和。

2. 使用运算符时不能违反原来的句法规则，例如不能将加法运算符重载为使用一个操作数。

   ```
   int x;
   Time shiva;
   +x;          //不被允许
   +shiva;            //不被允许
   ```

   且不能修改运算符的优先级。因此将加号运算符重载为两个类相加时，新的运算符与原来的加号有相同的优先级。

3. 不能创建新的运算符。例如不能定义operator **()函数来表示幂

4. 不能重载下面的运算符

   * sizeof
   * .
   * *
   * ::     作用域解析运算符
   * ?:     条件运算符
   * typeidd    一个RTTI运算符  
   * const_cast    强制类型转换运算符
   * dynamic_cast    强制类型转换运算符
   * reinterpret_cast     强制类型转换运算符
   * static_cast     强制类型转换运算符

5. 表中的运算符可以重载

   ![可重载符号](D:\王朝栋\Markdown笔记\重载运算符.png)



