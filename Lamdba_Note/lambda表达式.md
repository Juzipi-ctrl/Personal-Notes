# C++ lambda表达式

lambda表达式又称匿名函数（Anonymous function），其构造了一个可以在其作用范围内捕获变量的函数对象。

lambda表达式实际为一个仿函数functor，编译器后会生成一个匿名类（注：这个类重载了()运算符）

与普通函数指针相比，Lambda表达式可以包含数据成员，也就是说它是可以有状态的。下面举一个简单的例子说明一下：
```c++
int sum = 0;
std::vector<int> arry = { 1,2,3,4,5 };
std::for_each(begin(arry), end(arry), [&sum](int x){sum += x;});
```
上述代码被编译器展开后，会变成：
```c++
struct lambda_b53d8cae67476f0e5f04d9defa3a2e2b
{
private:
    int* m_pSum;
public:
    lambda_b53d8cae67476f0e5f04d9defa3a2e2b(int* pSum)
    {
        m_pSum = pSum;
    }

    void operator()(int x) const 
    {
        *m_pSum += x;
    }
};


int sum = 0;
std::vector<int> arry = { 1,2,3,4,5 };
lambda_b53d8cae67476f0e5f04d9defa3a2e2b obj(&sum);
std::for_each(begin(arry), end(arry), obj);
```

##lambda表示式的结构

从C++11起，开始提供了匿名函数的支持，一个lambda表达式形如：
```c++
[capture] (parameters) specifiers -> return_type { body }
```
capture
捕获的外部变量列表，通过逗号分隔，可进行传值捕获或者引用捕获，lambda表达式与这些捕获的外部变量会构成一个闭包（Closure），外部变量为闭包的成员变量

```c++
int g_Value = 0;
class CLambda
{
protected:
    int m_Value;
public:
    void Test1(int InValue)
    {
        int Value = 0;
        auto a1 = [](int x) {/*仅能访问全局外部变量*/};
        auto a2 = [Value](int x) {/*值传递局部变量Value*/};
        auto a3 = [this](int x) {/*值传递this指针*/};
        auto a4 = [&Value](int x) {/*引用传递局部变量Value*/};
        auto a5 = [=](int x) {/*值传递所有可访问的外部变量*/};
        auto a6 = [&](int x) {/*引用传递所有可访问的外部变量*/};
        auto a7 = [=, &Value](int x) {/*引用传递局部变量Value，值传递所有其他可访问的外部变量*/};
        auto a8 = [&, Value](int x) {/*值传递局部变量Value，引用传递所有其他可访问的外部变量*/};
    }
};
```
 全局变量、静态变量不用显示写在外部变量列表中，可直接在lambda表达式中读写

 传值捕获的外部变量是一个副本，默认情况下在lambda表达式中是只读的，若想修改该副本，需要在lambda表达式上添加mutable关键字  如：auto a2 = [Value](int x) mutable {Value++;};




## mutable的作用有两点：

在C++中，mutable是为了突破const的限制而设置的，用来修饰类的非静态、非常量的数据成员，让被修饰的变量永远处于可变的状态

a. 保持常量对象中大部分数据成员仍然是“只读”的情况下，实现对个别数据成员的修改；
	  b. 使类的const函数可以修改其mutable数据成员。

 在类的非静态成员函数中定义的lambda表达式可以通过捕捉this指针，来访问对象的成员变量和成员函数

c++14中增加广义捕获（Generalized capture）：即在捕获子句中增加并初始化新的变量，该变量不需要在lambda表达式所处的闭包域中存在；

即使在闭包域中存在也会被新变量覆盖。新变量类型由它的初始化表达式推导得到。一个用途是可以从闭包域中捕获只供移动的变量并使用它。

```c++
int Value = 0;
auto a1 = [Value = 100] { return Value; };// 捕获子句中定义的Value变量会覆盖同名的外部局部变量
int result = a1(); // result=100

std::vector<int> Vout = { 10, 20, 30, 40, 50 };
auto a2 = [Vin = std::move(Vout)]{ // 将外部局部变量Vout移动到Vin变量，避免发生拷贝耗时操作
    int sum = 0;
    for (auto n : Vin)
    {
        sum += n;
    }

    return sum;
};

int result2 = a2(); // result2=150
```

## lambda表达式自己的参数列表

### 1. 若lambda函数没有形参且没有被mutable等修饰，则参数的空圆括号可以省略

如：auto a = []{ ++g_Value; };

### 2. c++14支持auto类型的形参

```c++
auto a = [](auto x, auto y) {return x + y;};

//相当于定义了模板类型()运算符的函数对象
struct unnamed_lambda                            
{
  template<typename T, typename U> 
  auto operator()(T x, U y) const {return x + y;}
} a;
```

### 3. c++14支持可变参数模板

```c++
int foo(int n1, int n2, bool flag)
{
    return flag ? n1 : n2;
}

auto a = [](auto&&... params) //可变参数的模板
{
    return (foo(std::forward<decltype(params)>(params)...));
};
int result = a(1, 2, true); //result=1
```

### 4. 与普通函数相比，lambda表达式的参数有如下限制

① 参数不能有缺省值   如：int Add1(int a, int b=10) 

② 不能有可变长参数列表  如：int  Add2(int count, ...)

③ 不能有无名参数  如：int Add3(int a, int b, int)  // 第三个参数为无名参数，用于以后扩展

 

specifiers
说明符，可选。如上文中的mutable

 

return_type

## 返回类型

在以下情况下，可省略return_type

① 返回值为void类型  如：auto a = [](int x) {x = 100;};  //返回值类型为void

② 所有返回语句用decltype都能检测到同一类型  如：auto a = [](int x, float y) { if (x > 0) return x + y;  return y; };  //返回值类型推导为float

 

## 使用lambda表达式

lambda表达式实际为一个函数对象，在使用时要注意lambda表达式以及被其捕获的外部变量的生命周期

把匿名函数存储在变量，当做有名函数来使用
lambda表达式的数据类型是函数对象，可用auto类型、std::function模板类型（需#include <functional>）进行保存和调用

当捕获外部变量列表为空时，也可用普通函数指针进行保存和调用

```c++
#include<algorithm> 
int Value = 0;

auto a1 = [&Value](int x) {Value = x;};
std::function<float(int,float)> a2 = [Value](int x, float y) { return x + y; }; //需要#include <functional>
a1(100);
a2(100, 200.0f);

// lambda函数的捕获外部变量列表为空时，可使用普通函数指针来保存
int(*func1_ptr)(int) = [](int x) {return x; };
bool(*func2_ptr)(int, int) = [](int x, int y) { return x > y; };
int n = func1_ptr(1);
bool b = func2_ptr(1, 2);
```

 

## 悬挂引用问题

lambda表达式的闭包含有局部变量的引用（悬挂引用  Dangling references），在超出创建它的作用域之外的地方被使用的话，将引发内存越界访问

```c++
std::function<int()> a;
{
    int Value = 0;
    a = [&Value] {return Value; };
}
        
a(); // 局部变量Value超过作用域，已被回收，调用lambda表达式将产生内存越界访问
```
对于使用lambda表达式写的回调函数（如：窗口处理函数、线程执行函数、控件消息处理函数等），尤其要注意这个问题