

# lambda表达式补充

###### 语法

[捕获] <模板形参> (形参) 说明符 异常说明 arr -> ret requies {函数体}

[捕获] （形参） -> ret {函数体}

[捕获] （形参） {函数体}

[捕获]  {函数体}

1. 完整声明
2. const lambda 的声明：复制捕获的对象在 lambda 体内为 const。
3. 省略尾随返回类型：闭包的 operator() 的返回类型从 return 的**推导**，如同对于声明类型为 auto 的函数的推导一样。
4. 省略形参列表：不接受实参的函数，如同形参表是()。仅当 constexpr、mutable、异常说明、属性或尾随返回类型都不使用时才能使用此形式。

### 解释

#### 捕获

零或更多捕获符的都好分隔列表，可选地以默认捕获符(capture-default)起始。

若变量满足以下条件，则lambda表达式可以不捕获就使用它。

- 该变量为非局部变量，或具有静态或线程局部存储期（该情况下无法捕获该变量），或者该变量为以常量表达式初始化的引用。

若变量满足下列条件，则lambda表达式可以不捕获就读取其值。

- 该变量具有const而非volatile的整型或枚举类型，并已用常量表达式初始化，或者该变量为 constexpr 且无 mutable 成员。

#### <模板参数>

(角括号中的)模板形参列表，用于泛型lambda提供各模板形参的名字。与在模板声明中相似，模板形参可以在以后附可选的requiree 子句，它指定各模板实参上的制约。若提供，则模板形参列表不能为空（不允许<>）。

#### 形参

形参列表，如在具名函数中，但不允许默认实参。当auto为形参类型时，该lambda为泛型lambda。

#### 说明符

可选的说明符的序列。允许下列说明符：

- mutable: 允许 函数体 修改各个复制捕获的对象，以及调用其非const成员函数。
- constexpr： 显式指定函数调用运算符为 constexpr函数。此说明符不存在时，若函数调用运算符恰好满足针对 constexpr：函数的所有要求，则它也会是 consrexpr。
- consteval：指定函数调用运算符为立即函数。不能同时使用 consteval 和 constexpr 。

#### 异常说明

​		为闭包类型的 operator() 提供异常说明或noexcept 子句。

#### attr

​		为闭包类型的函数调用运算符的类型提供属性说明。这样指定的任何属性均属于函数调用运算符的类型，而非函数调用运算符自用。

#### ret

​		返回类型。若缺失，则由函数的 return 语句所蕴含（或当函数不返回任何值时为void）。

#### requires

​		向闭包类型的 operator() 添加制约。

​		lambda 表达式时纯右值表达式，其类型是独有的无名非联合类类型，被称为闭包类型（closure type），它（对于 ADL） 声明包含有该lambda		表达式的最小块作用域、类作用域或明明空间作用域。闭包类型有下列成员：

​		ClosureType::operator()(形参)

```c++
ret operator()(形参) const {函数体}
ret operator()(形参) {函数体}
template<模板形参>
ret operator()(形参) const {函数体}
template<模板形参>
ret operator()(形参) {函数体}
```

​		当被调用时，执行lambda表达式的函数体。当访问变量时，访问的是其被捕获的副本（对于复制捕获的实体）或原对象（对于以引用捕获的实体）。除非 lambda 表达式中使用了关键词 mutable ，否则函数调用表达式被 const 限定，且以复制捕获的对象从这个 operator() 的内部不可修改。函数调用运算符始终不被 volatile 限定且始终非虚。

​		若在 lambda 表达式使用关键字 consteval ，则函数调用运算符是立即函数。

​		对于形参中每个类型指定为 auto 的参数，以其出现顺序向 模板形参 中添加一个虚设的模板形参。当虚设的模板形参所对应的形参中的函数形参包时，它可为形参包。

```c++
//泛型 lambda， operator() 是有两个形参的模板
  auto glambda = [] (auto a, auto&& b) {return a < b; };
  bool b = glambda(3, 3.14);  //ok

  //泛型 lambda， operator() 是一个形参的模板
  auto vglambda = [] (auto printer) {
    return [=] (auto&& ... ts) //泛型 lambda ts 是形参包
    {
        printer(std::forward<decltype(ts)>(ts)...);
        return [=]{printer(ts...);};  //零元 lambda （不接受形参）
    };
  };
  auto p = vglambda([](auto v1, auto v2, auto v3){std::cout << v1 << v2 << v3; })
  auto q = p(1, 'a', 3.14);
  q();
```

​		ClosureType 的 operator() 不能被显式实例化或显式特化。

​		若 lambda 定义使用显式的模板形参列表，则该模板形参列表用于 operator()。对于 形参中每个类型指定为 auto 的形参，都向模板形参列表尾部追加一个额外的虚设模板形参：

```c++
//泛型 lambda， operator() 是有两个形参的模板
    auto glambda = []<class T>(T a, auto&& b) {return a < b; };
    //泛型 lambda， operator() 是有一个形参包的模板
    auto r = []<typename ...Ts>(Ts&& ...ts){
      return foo(std::forward<Ts>(ts)...);
    };
```

​		lambda 表达式的异常说明异常说明应用于函数调用运算符或运算符模板。

​		对于名字查找，确定this指针的类型和值，以及对于访问非静态类成员而言，闭包类型的函数调用运算符的函数体被认为处于lambda表达式的语境中。

```c++
struct x{
  int x, y;
  int operator()(int);
  void r(){
    //下列lambda的语境是成员函数 x::f
    [=]()->int 
    {
      return operator()(this -> x + y);  //x::operator()(this -> x + (*this).y)  拥有类型 x*
    }
  }
};
```

​		closureType 的 operator() 不能在友元声明中指明。

#### 悬垂引用

​		若以引用隐式或显式捕获非引用实体，而在该实体的生存期结束之后调用闭包对象的函数调用运算符，则发生未定义行为。c++ 的闭包并不延长被捕获的引用的生存期。

​		这同样适用于被捕获的 this 指针所指向的对象的生存期。

​		ClosureType::operator ret(*)(形参)()

```c++
//无捕获的非泛型 lambda
using F = ret(*)(形参);
operator F() const;
using F = ret(*)(形参);
constexpr operator F() const;

template<模板形参> using fptr_t = 
template<模板形参> constexpr operator fptr_t<模板形参>() const;
template<模板形参> using fptr_t = 
template<模板形参> operator fptr_t<模板形参>() const;
```

​		仅当 lambda 表达式的捕获符列表为空时才定义这个用户定义转换函数。它是闭包对象的公开，constexpr，非虚，非 explicit，const noexcept 成员函数。若lambda的函数调用运算符是 立即函数，则转换函数亦为立即函数。

​		泛型无捕获 lambda 拥有一个用户定义的转换函数模板，它具有与函数调用运算符模板相同的虚设模板形参列表。若其返回类型为空或auto，则函数模板特化上的返回类型推导获得，而它则以转换函数模板的模板实参推导获得。

```c++
void f1(int (*)(int)) {}
void f2(char (*)(int)) {}
void h(int (*)(int)) {} //#1
void h(char (*)(int)) {} //#2
auto glambda = [](auto a) {return a; }
f1(glambda);  //ok
f2(glambda);  //错误： 不可转换
h(glambda);  //ok ： 调用 #1， 因为 #2 不可转换

int& (*fpi)(int*) = [](auto* a) -> auto& {return *a; }; //ok
```

​		若闭包对象的 operator() 具有无抛出异常说明，则此函数返回的指针具有指向 noexcept 函数的指针类型。

​		若函数调用运算符（或对于泛型 lambda 为其特化） 是立即函数，则此函数是立即函数。

Closure::Type::ClosureType()

```c++
ClosureType() = delete;
ClosureType() = default;
ClosureType(const ClosureType&) = default;
ClosureType(ClosureType&& ) = default;
```

​		闭包类型非可默认构造。闭包类型带有被弃置的默认构造函数。

​		若未指定捕获，则闭包类型拥有预置的默认构造函数。否则，它没有默认构造函数（这包含有 默认捕获符的情况，即使实际上它不捕获任何变量也是知此）。

​		复制构造函数与移动构造函数被隐式声明，并按照复制构造函数与移动构造函数的通常规则隐式定义。

ClosureType::oprator = (const ClosureType&)

```c++
ClosureType& operator = (const ClosureType& ) = delete;
ClosureType& operator = (const ClosureType& ) = default;
ClosureType& operator = (ClosureType&& )  = default;
ClosureType& operator = (const ClosureType& ) = delete;
```

​		复制赋值运算符被定义为弃置的（且未声明移动复制运算符）。闭包类型非可复制赋值。

若不指定 捕获 ，则闭包类型拥有预置的复制赋值运算符和预置的移动赋值运算符。否则，它拥有弃置的复制赋值运算符（这包含 默认捕获的 情况，即实际上它不捕获任何变量也是如此）。

```c#
ClosureType::~ClosureType()
    ~closureType() = default;
```

​		析构函数式隐式的。

​		若lambda表达式以复制（隐式地以捕获子句 [=] 或显式地以不含字符 &  的捕获符，例如 [a, b, c]） 捕获子句任何内容，则闭包类型包含有所有被如此捕获的实体的副本的无名非静态数据成员，它们以未指明的顺序声明。

​		对应于无初始化的捕获符的数据成员，在求值 lambda 表达式时被 直接初始化。对应于带有初始化器的捕获符的，则按其初始化的要求初始化（可为复制或直接初始化）。若捕获了数组，则各数组元素以下标递增顺序直接初始化。初始化各数据成员所用的顺序是它们的声明的顺序（它是未指明的）。

​		每个数据成员的类型是其对应被捕获实体的类型，除非实体拥有引用类型（该情况下，到函数的引用被捕获为到被引用函数的左值引用，而到对象的引用被捕获为被引用对象的副本）。

​		对于以引用捕获（以默认捕获符 [&] 或使用了字符 & ，例如 [&a, &b, &c] 的实体，闭包类型中是否声明额外的数据成员是否未指明的，但任何这种附和成员必须满足字面类型。

​		不允许在不求值表达式、模版实参、别名声明、typedef声明，以及函数（或函数模版） 声明中除了函数体外的默认实参以外的任何位置出现 lambda 表达式。

#### lambda 捕获

捕获是零或更多捕获的都好分隔列表，可选地以 默认捕获符开始。仅有的默认捕获符是

- & （以引用隐式捕获被使用的自动变量） 和  = （以复制隐式捕获被使用的自动变量）。

当出现任一默认捕获符时，都能隐式捕获当前对象（*this）。当它被隐式捕获时，始终被以引用捕获，即使默认捕获符是 - 也是如此。当默认捕获符为 - 时，*this 的隐式捕获被弃用。



​		捕获 中单独的捕获的语法

| 说明符                    | 解释                             |
| ------------------------- | -------------------------------- |
| 1、标识符                 | 简单以复制捕获                   |
| 2、标识符 ...             | 作为包展开的简单以复制捕获       |
| 3、标识符 初始化器        | 带初始化器的以复制捕获           |
| 4、& 标识符               | 简单以引用捕获                   |
| 5、& 标识符 ...           | 作为包展开的简单引用捕获         |
| 6、& 标识符 初始化器      | 带初始化器的简单以引用捕获       |
| 7、this                   | 当前对象的简单以引用捕获         |
| 8、* this                 | 当前对象的简单以复制捕获         |
| 9、... 标识符初始化器     | 用作为包展开的初始化器以复制捕获 |
| 10、& ... 标识符 初始化器 | 用作为包展开的初始化器以引用捕获 |

当默认捕获是 & 时，后继的简单捕获符必须不以 & 开始。

```C++
struct s2 { void f(int i); };
void s2::f(int i)
{
  [&]{};    //OK： 默认以引用捕获
  [&, i]{};   //Ok：以引用捕获，但i以值捕获
  [&, &i]{};   //错误：以引用捕获为默认时的以引用捕获
  [&, this]{};  // ok：等价于 [&]
  [&, this, i]{};   //ok：等价于 [&, i]
}
```

当默认捕获是 =  时， 后续的简单捕获符必须以 & 开始，或者为 *this 或 this

```c++
struct s2 { void f(int i); };
void s2::f(int i) 
{
  [=]{};   //ok：默认以复制捕获
  [=, &i]{};  //ok：以复制捕获，但 i 以引用捕获
  [=, *this]{};   //c++17前：错误：无效语法  之后： ok：以复制捕获外围的 s2 
  [=, this]{};    //c++20前： 错误： = 为默认时的 this 之后 ok：同 [=]
}
```

任何捕获只可能出现一次：

```c++
struct s2 { void f(int i); };
void s2::f(int i)
{
  [i, i]{};   //错误： i 重复
  [this, *this]{};  //错误：“this” 重复
}
```

​	只有定义于块作用域或默认成员初始化器中的 lambda 表达式能拥有默认捕获符或无初始化器的捕获符。对于这种 lambda 表达式，其可打作用域定义为直至并包含其最内层的外围函数（及其形参）的外围作用域的集合。这其中包含各个嵌套的块作用域，以及当此 lambda 为嵌套的 lambda 时也包含其各个外围 lambda 的作用域。

​	（除了 this 捕获符之外的） 任何无初始化器的捕获符中的 表示符，使用通常的无限名字查找在 lambda 的可达作用域中查找。查找结果必须是声明可达作用域中的，具有自动存储期的变量。该变量（或 this） 被显式捕获。

​	带有初始化器的捕获符，其行为如同它声明并显式捕获一个以类型 auto 声明的变量，该变量的声明是 lambda 表达式体（即它不在其初始化器的作用域中），但是：

- 若以复制捕获，则闭包对象的非静态数据成员是指代这个 auto 变量的另一种方式。
- 若以引用捕获，则引用变量的生存期在闭包对象的生存期结束时结束。

这可用于如 x = std::move(x) 这样的捕获符捕获仅可移动的类型。

这亦使得以 const 引用进行捕获称为可能，比如以 &cr = std::as_const(x) 或类似的方式。

```c++
int x = 4;
auto y = [&r = x, x = x + 10]() -> int 
{
  r += 2;
  return x * x;

}(); //更新 ::x 为 6 并初始化 y 为 25
```

​	若捕获符列表具有默认捕获符，且未显式（以 this 或 *this） 捕获其外围对象，或捕获任何自动变量，以下情况，它隐式捕获：

- lambda 体 ODR 式使用了变量或 this 指针
- 或者，变量或 this 在取决于某个泛型 lambda 形参的表达式内的潜在求值表达式中被指明（包括在使用非静态类成员的前添加隐含的 this -> ）。就此而言，始终认为 typeid 的操作数被潜在求值。即使仅在弃用语句中知名实体，也可能会隐式捕获它。

```c++
void f(int, const int (&)[2] = {}){}  //#1
void f(const int&, const int (&)[1]){}  //#2
void test()
{
  const int x = 17;
  auto g0 = [](auto a) { f(x); };  //ok：调用 #1， 不捕获 x
  auto g1 = [=](auto) { f(x); };  // 捕获 x 捕获能被优化掉

  auto g2 = [=] (atuo a) {
    int selector[sizeof(a) == 1 ? 1 : 2] = {};
    f(x, selector); //ko： 此为待决表达式，故 x 被捕获
  };
  auto g3 = [=](auto a) {
    typeid(a + x);  //捕获 x， 不管 a + x 是否为不求值操作数
  };
}
```

若 lambda 体 ODR 式使用了复制捕获的实体，则它访问的事闭包类型的成员。若它未 ODR 式使用该实体，则访问是原对象：

```c++
void f(const int *);
void g() {
  const int N = 10;
  [=] {
    int arr[N]; //非 ODR 式使用： 指代 g 的 const int N
    f(&N);  //ODR 式使用： 导致 N  被（以复制） 捕获
            //&N 是闭包对象的成员 N 的地址，而非 g 中的 N 
  }();
}
```

若 lambda ODR 式使用了以引用捕获的引用，则它使用原引用所指代的对象，而非被捕获的引用自身：

运行以下代码：

```c++
#include <iostream>

auto make_function(int& x){
  return [&] {std::cout << x << std::endl;};
}

int main(){
  int i = 3;
  auto f = make_function(i);  //  f 中对 x 的使用直接绑定到 1
  i = 5;
  f();  //ok 打印 5
}
```

在 lambda 体内，在任何具有自动存储期的变量上使用的 decltype， 都如同将它捕获并 ODR 式使用，尽管 decltype 自身不是 ODR 式使用且不实际发生捕获：

```c++
void f3() {
  float x, &r = x;
  [=] {  //x与 r 不被捕获（出现与 decltype 的操作数中并不是 ODR 式使用）
    decltype(x) y1;   //y1 拥有 float 类型
    decltype((x)) y2 = y1;  //y2 拥有 float const& 类型， 因为此 lambda 
                            // 非 mutable 且 x 式左值
    decltype(r) r1 = r2;    //r1 拥有 float& 类型 （不考虑变换）
    decltype((r)) r2 = y2;  //r2 拥有 float const& 类型
  };
}
```

lambda 所（隐式或显式）捕获的任何实体均被改 lambda 表达式所 ODR 式使用（因此，嵌套的 lambda 的隐式捕获将触发其外围 lambda 的隐式捕获）。

所有隐式捕获的变量必须声明于 lambda 的可达作用域中。

若 lambda （以 this 或 *this）捕获了其外围对象，则要么其最接近的外围函数必须是非静态成员函数，要么该 lambda 必须处于某个默认成员初始化器中：

```c++
struct s2 {
    double ohseven = .007;
    auto f() {  //以下两个 lambda 的最接近外围函数
        return [ this ] { //以引号捕获外围的 s2
            return [*this] { //以复制捕获外围的 s2
                return ohseven; //ok
            }
        }(); 
    }
    auto g() {
        return [] {
            return [*this]{};   //错误：*this 未被外层 lambda 表达式所捕获
        }();
    }
};
```

若 lambda 表达式（或泛型 lambda 的函数调用运算符的一个实例化）ODR 式使用了 this 或任何具有自动存储期的变量，则它必须被该 lambda 表达式所捕获。

```c++
void f1( int i ) {
    int const N = 20;
    auto m1 = [ = ] {
        int const M = 30;
        auto m2 = [ i ] {
            int x [ N ][ M ];    // N与 M 未被 ODR 式使用 （它闷未被捕获是 ok 的）

            x[0][0] = i;  //i 被 m2 显式捕获 并被 m1 隐式捕获
        };
    };

    struct s1 {  //f1() 中的局部类
        int f;
        void sork(int n) //非静态成员函数
        {
            int m = n * m;
            int j = 40;
            auto m3 = [this, m] {
                auto m4 = [&, j] {  //错误： j 未被 m3 所捕获
                    
                    int x = n;  // 错误：n 未被 m4 隐式捕获 但未被 m3 所捕获

                    x += m;     //ok：m 被 m4 捕获 且 m3 显式捕获

                    x += i      //错误： i 在可达作用域之外 （该作用域终于 work()）

                    x += f;     //ko： this 被 m4 隐式不糊 且被 m3 显式捕获
                };
            };
        }
    };
}
```

以下不带有初始化的捕获符不能捕获类成员（如以上提及，捕获符列表中仅容许变量）

```c++
class s {
    int x = 0;
    void f( ) {
        //auto l1 = [i, x] { use(i, x); };  //错误： x 非变量
        auto l2 = [ i, x = x ] { use( i, x ); };    //OK： 复制捕获
        i = 1; x = 1; l2( );     //调用 use(0, 0)
        auto l3 = [ i, &x = x ] { use( i, m ); };  //ok， 引用捕获
        i = 2; x = 2; l3( );  //调用 use(1, 2)
    }
};
```

当 lambda 用隐式的以复制捕获某个成员时，它并不产生成员变量的副本；对成员变量 m 的使用被处理成表达式 (*this).m， 而 *this 始终被隐式以引用捕获：

```c++
class s {
    int x = 0;
    void f( ) {
        int i = 0;
        auto l1 = [ = ] { use( i, x ); }; // 捕获 i 的副本和 this 指针的副本
        i = 1;
        x = 1;
        l1( ); // 调用 use(0,1)，如同 i 以复制而 x 以引用捕获

        auto l2 = [ i, this ] { use( i, x ); }; // 同上，令之为显式捕获
        i = 2;
        x = 2;
        l2( ); // 调用 use(1,2)，如同 i 以复制而 x 以引用捕获

        auto l3 = [ & ] { use( i, x ); }; // 以引用捕获 i，并捕获 this 指针的副本
        i = 3;
        x = 2;
        l3( ); // 调用 use(3,2)，如同 i 与 x 均以引用捕获

        auto l4 = [ i, *this ] { use( i, x ); }; // 制造 *this 的副本，包含 x 的副本
        i = 4;
        x = 4;
        l4( ); // 调用 use(3,2)，如同 i 与 x 均以复制捕获
    }
};
```

若 lambda 表达式出现于默认实参中，则它不能显式隐式捕获任何变量。

不能捕获匿名合体的成员。

若嵌套的 lambda m2 捕获了也被其直接外围 lambda m1 所捕获的实体，则以如下方式将 m2 的捕获进行变换：

- 若外围lambda m1 以复制捕获，则 m2 捕获 m1 的闭包类型的非静态成员，而非原变量货 this。
- 若外围 lambda m1 以引用捕获，则 m2 捕获原变量的货 this。

```c++
#include <iostream>
int main( ) {
    int a = 1, b = 1, c = 1;

    auto m1 = [ a, &b, &c ] ( ) mutable {
        auto m2 = [ a, b, &c ] ( ) mutable {
            std::cout << a << b << c << std::endl;
            a = 4; b = 4; c = 4;
        };
        a = 3; b = 3; c = 3;
        m2( );
    };
    a = 2; b = 2; c = 2;
    m1( );       //调用 m2() 并打印 123
}
/*
123
234
*/
```

#### 示例

以下示例如何传递 lambda 给泛型算符，以及 lambda 表达式所产生的对象能如何存储于 std::function对象。

```c++
#include <vector>
#include <iostream>
#include <algorithm>
#include <functional>

int main( ) {
    std::vector<int> ctor = { 1,2,3,4,5,6,7 };
    int xcode = 5;

    ctor.erase( std::remove_if( ctor.begin( ), ctor.end( ), [ xcode ] ( int nona ) {
        return nona < xcode;
        } ), ctor.end( ) );

    std::cout << "ctor: ";
    std::for_each( ctor.begin( ), ctor.end( ), [ ] ( int iRelu ) {
        std::cout << iRelu << ' ';
    } );
    std::cout << std::endl;

    //闭包的类型不能被指明，但可用 auto 提及
    //C++14起， lambda 能拥有自身的默认实参
    auto func1 = [ ] ( int iRelu = 6 ) {
        return iRelu + 4;
    };
    std::cout << "func1: " << func1( ) << std::endl;

    //与所有可能对象相同，闭包能可以被捕获到 std::function 之中
    //（这可能带来不必要的开销）
    std::function<int( int )> func2 = [ ] ( int iRelu ) {
        return iRelu + 4;
    };
    std::cout << "func2: " << func2( 6 ) << std::endl;
}

/*
ctor: 5 6 7 
func1: 10
func2: 10
*/
```

