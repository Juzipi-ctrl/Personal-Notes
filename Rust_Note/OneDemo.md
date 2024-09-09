# 准备一个项目

要创建一个新项目，进入第一章中创建的 *projects* 目录，使用 Cargo 新建一个项目，如下：

```powershell
$ cargo new guessing_game
$ cd guessing_game
```

第一个命令，`cargo new`，它获取项目的名称（`guessing_game`）作为第一个参数。第二个命令进入到新创建的项目目录。



查看生成的 `Cargo.toml` 文件：

```bash
[package]
name = "guessing_game"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```

再查看 `src/main.rs` 文件：

```rust
fn main() {
    println!("Hello, world!");
}
```

使用 `cargo run` 命令，一步完成程序的编译和运行：

```bash
Book@Matebook ~\Project\Rust_Project\guessing_game git:master ❯❯❯ cargo run
   Compiling guessing_game v0.1.0 (C:\Users\Administrator\Project\Rust_Project\guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 0.37s
     Running `target\debug\guessing_game.exe`
Hello, world!
```

当你需要在项目中快速迭代时，`run` 命令就能派上用场，正如我们在这个游戏项目中做的，在下一次迭代之前快速测试每一次迭代。

重新打开 `src/main.rs`文件。我们将会在这个文件中编写全部的代码。



## 处理一次猜测

猜猜看程序的第一部分请求和处理用户输入，并检查输入是否符合预期的格式。首先，允许玩家输入猜测。在 `src/main.rs`中输入示例

```rust
use std::io;  // 导入标准输入/输出库

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();  // 创建一个空字符串，用于接收用户输入

    io::stdin()  // 获取标准输入
        .read_line(&mut guess)  // 读取一行输入并存入 guess 变量
        .expect("Failed to read line");  // 读取失败时 panic

    println!("You guessed: {}", guess);  // 打印用户输入的数字
}

```

这些代码包含很多信息，我们一行一行地过一遍。为了获取用户输入并打印结果作为输出，我们需要将 `io`输入/输出库引入当前作用域。`io` 库来自于标准库，也被称为 `std`：

```rust
use std::io;
```

默认情况下，Rust 设定了若干个会自动导入到每个程序作用域中的标准库内容，这组内容被称为 *预导入（preclude）* 内容。你可以在[标准库文档](https://doc.rust-lang.org/std/prelude/index.html)中查看预导入的所有内容。

如果你需要的类型不在预导入内容中，就必须使用 `use` 语句显式地将其引入作用域。`std::io` 库提供很多有用的功能，包括接收用户输入的功能。

如第一章所提及，`main` 函数是程序的入口点：

```rust
fn main() {
```

`fn` 语法声明了一个新函数，小括号 `()` 表明没有参数，大括号 `{` 作为函数体的开始。

第一章也提及了 `println!` 是一个在屏幕上打印字符串的宏：

```rust
    println!("Guess the number!");

    println!("Please input your guess.");
```

这些代码仅仅打印提示，介绍游戏的内容然后请求用户输入。



## 使用变量储存值

接下来，创建一个 **变量**（*variable*）来储存用户输入，像这样：

```rust
    let mut guess = String::new();
```

现在程序开始变得有意思了！这一小行代码发生了很多事。我们使用 `let` 语句来创建变量。这里是另外一个例子：

```rust
let apples = 5;
```

这行代码新建了一个叫做 `apples` 的变量并把它绑定到值 `5` 上。在 Rust 中，变量默认是不可变的，这意味着一旦我们给变量赋值，这个值就不再可以修改了。下面的例子展示了如何在变量名前使用 `mut` 来使一个变量可变：

```rust
let apples = 5; // 不可变
let mut bananas = 5; // 可变
```

> 注意：`//` 语法开始一个注释，持续到行尾。Rust 忽略注释中的所有内容，[第三章](https://kaisery.github.io/trpl-zh-cn/ch03-04-comments.html)将会详细介绍注释。

回到猜猜看程序中。现在我们知道了 `let mut guess` 会引入一个叫做 `guess` 的可变变量。等号（`=`）告诉 Rust 我们现在想将某个值绑定在变量上。等号的右边是 `guess` 所绑定的值，它是 `String::new` 的结果，这个函数会返回一个 `String` 的新实例。[`String`](https://doc.rust-lang.org/std/string/struct.String.html) 是一个标准库提供的字符串类型，它是 UTF-8 编码的可增长文本块。

`::new` 那一行的 `::` 语法表明 `new` 是 `String` 类型的一个 **关联函数**（*associated function*）。关联函数是针对类型实现的，在这个例子中是 `String`，而不是 `String` 的某个特定实例。一些语言中把它称为 **静态方法**（*static method*）。

`new` 函数创建了一个新的空字符串，你会发现很多类型上有 `new` 函数，因为它是创建类型实例的惯用函数名。

总的来说，`let mut guess = String::new();` 这一行创建了一个可变变量，当前它绑定到一个新的 `String` 空实例上。



## 接收用户输入

回忆一下，我们在程序的第一行使用 `use std::io;` 从标准库中引入了输入/输出功能。现在调用 `io` 库中的函数 `stdin`：

```rust
    io::stdin()
        .read_line(&mut guess)
```

如果程序的开头没有使用 `use std::io;` 引入 `io` 库，我们仍可以通过把函数调用写成 `std::io::stdin` 来使用函数。`stdin` 函数返回一个 [`std::io::Stdin`](https://doc.rust-lang.org/std/io/struct.Stdin.html) 的实例，这代表终端标准输入句柄的类型。

代码的下一部分，`.read_line(&mut guess)`，调用 [`read_line`](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_line) 方法从标准输入句柄获取用户输入。我们还将 `&mut guess` 作为参数传递给 `read_line()` 函数，让其将用户输入储存到这个字符串中。`read_line` 的工作是，无论用户在标准输入中键入什么内容，都将其追加（不会覆盖其原有内容）到一个字符串中，因此它需要字符串作为参数。这个字符串参数应该是可变的，以便 `read_line` 将用户输入附加上去。

`&` 表示这个参数是一个 **引用**（*reference*），它允许多处代码访问同一处数据，而无需在内存中多次拷贝。引用是一个复杂的特性，Rust 的一个主要优势就是安全而简单的操纵引用。完成当前程序并不需要了解如此多细节。现在，我们只需知道它像变量一样，默认是不可变的。因此，需要写成 `&mut guess` 来使其可变，而不是 `&guess`。（第四章会更全面的解释引用。）



## 使用 Result类型来处理潜在的错误

我们还没有完全分析完这行代码。虽然我们已经讲到了第三行代码，但要注意：它仍是逻辑行（虽然换行了但仍是语句）的一部分。后一部分是这个方法（method）：

```rust
        .expect("Failed to read line");
```

我们也可以将代码这样写：

```rust
io::stdin().read_line(&mut guess).expect("Failed to read line");
```

不过，过长的代码行难以阅读，所以最好拆开来写。通常来说，当使用 `.method_name()` 语法调用方法时引入换行符和空格将长的代码行拆开是明智的。现在来看看这行代码干了什么。

之前提到了 `read_line` 会将用户输入附加到传递给它的字符串中，不过它也会返回一个类型为 `Result` 的值。 [`Result`](https://doc.rust-lang.org/std/result/enum.Result.html) 是一种[*枚举类型*](https://kaisery.github.io/trpl-zh-cn/ch06-00-enums.html)，通常也写作 *enum*。枚举类型变量的值可以是多种可能状态中的一个。我们把每种可能的状态称为一种 *枚举成员（variant）*。

`Result` 的成员是 `Ok` 和 `Err`，`Ok` 成员表示操作成功，内部包含成功时产生的值。`Err` 成员则意味着操作失败，并且包含失败的前因后果。

这些 `Result` 类型的作用是编码错误处理信息。`Result` 类型的值，像其他类型一样，拥有定义于其上的方法。`Result` 的实例拥有 [`expect` 方法](https://doc.rust-lang.org/std/result/enum.Result.html#method.expect)。如果 `io::Result` 实例的值是 `Err`，`expect` 会导致程序崩溃，并显示当做参数传递给 `expect` 的信息。如果 `read_line` 方法返回 `Err`，则可能是来源于底层操作系统错误的结果。如果 `Result` 实例的值是 `Ok`，`expect` 会获取 `Ok` 中的值并原样返回。在本例中，这个值是用户输入到标准输入中的字节数。

如果不调用 `expect`，程序也能编译，不过会出现一个警告：

```bash
Book@Matebook ~\Project\Rust_Project\guessing_game git:master ❯❯❯ cargo build   
   Compiling guessing_game v0.1.0 (C:\Users\Administrator\Project\Rust_Project\guessing_game)
warning: unused `Result` that must be used
  --> src\main.rs:10:5
   |
10 | /     io::stdin()  // 获取标准输入
11 | |         .read_line(&mut guess);  // 读取一行输入并存入 guess 变量
   | |______________________________^
   |
   = note: this `Result` may be an `Err` variant, which should be handled
   = note: `#[warn(unused_must_use)]` on by default
help: use `let _ = ...` to ignore the resulting value
   |
10 |     let _ = io::stdin()  // 获取标准输入
   |     +++++++

warning: `guessing_game` (bin "guessing_game") generated 1 warning
    Finished dev [unoptimized + debuginfo] target(s) in 0.46s
```

Rust 警告我们没有使用 `read_line` 的返回值 `Result`，说明有一个可能的错误没有处理。

消除警告的正确做法是实际去编写错误处理代码，不过由于我们就是希望程序在出现问题时立即崩溃，所以直接使用 `expect`。



## 使用 `println!` 占位符打印值

除了位于结尾的右花括号，目前为止就只有这一行代码值得讨论一下了，就是这一行：

```rust
    println!("You guessed: {guess}");
```

这行代码现在打印了存储用户输入的字符串。里面的 `{}` 是预留在特定位置的占位符：把 `{}` 想象成小蟹钳，可以夹住合适的值。当打印变量的值时，变量名可以写进大括号中。当打印表达式的执行结果时，格式化字符串（format string）中大括号中留空，格式化字符串后跟逗号分隔的需要打印的表达式列表，其顺序与每一个空大括号占位符的顺序一致。在一个 `println!` 调用中打印变量和表达式的值看起来像这样：

```rust
let x = 5;
let y = 10;

println!("x = {x} and y + 2 = {}", y + 2);
```

这行代码会打印出 `x = 5 and y + 2 = 12`。



## 测试第一部分代码

让我们来测试下猜猜看游戏的第一部分。使用 `cargo run` 运行：

```bash
 Book@Matebook ~\Project\Rust_Project\guessing_game git:master ❯❯❯ cargo run  
   Compiling guessing_game v0.1.0 (C:\Users\Administrator\Project\Rust_Project\guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 0.44s
     Running `target\debug\guessing_game.exe`
Guess the number!
Please input your guess.
6
You guessed: 6
```



## 生成一个秘密数字

接下来，需要生成一个秘密数字，好让用户来猜。秘密数字应该每次都不同，这样重复玩才不会乏味；范围应该在 1 到 100 之间，这样才不会太困难。Rust 标准库中尚未包含随机数功能。然而，Rust 团队还是提供了一个包含上述功能的 [`rand` crate](https://crates.io/crates/rand)。



### 使用 crate 来增加更多功能

记住，*crate* 是一个 Rust 代码包。我们正在构建的项目是一个 *二进制 crate*，它生成一个可执行文件。 `rand` crate 是一个 *库 crate*，库 crate 可以包含任意能被其他程序使用的代码，但是不能自执行。

Cargo 对外部 crate 的运用是其真正的亮点所在。在我们使用 `rand` 编写代码之前，需要修改 *Cargo.toml* 文件，引入一个 `rand` 依赖。现在打开这个文件并将下面这一行添加到 `[dependencies]` 片段标题之下。在当前版本下，请确保按照我们这里的方式指定 `rand`，否则本教程中的示例代码可能无法工作。

文件名：Cargo.toml

```toml
[dependencies]
rand = "0.8.5"
```

在 *Cargo.toml* 文件中，标题以及之后的内容属同一个片段，直到遇到下一个标题才开始新的片段。`[dependencies]` 片段告诉 Cargo 本项目依赖了哪些外部 crate 及其版本。本例中，我们使用语义化版本 `0.8.5` 来指定 `rand` crate。Cargo 理解 [语义化版本（Semantic Versioning）](http://semver.org/)（有时也称为 *SemVer*），这是一种定义版本号的标准。`0.8.5` 事实上是 `^0.8.5` 的简写，它表示任何至少是 `0.8.5` 但小于 `0.9.0` 的版本。

Cargo 认为这些版本与 `0.8.5` 版本的公有 API 相兼容，这样的版本指定确保了我们可以获取能使本章代码编译的最新的补丁（patch）版本。任何大于等于 `0.9.0` 的版本不能保证和接下来的示例采用了相同的 API。

现在不修改任何代码，构建项目：

```bash
-1073741510   Book@Matebook ~\Project\Rust_Project\guessing_game git:master ❯❯❯ cargo build
    Updating `sjtu` index
warning: spurious network error (3 tries remaining): request failed with status code: 504; class=Http (34)
  Downloaded getrandom v0.2.12 (registry `sjtu`)
  Downloaded rand_core v0.6.4 (registry `sjtu`)
  Downloaded rand_chacha v0.3.1 (registry `sjtu`)
  Downloaded rand v0.8.5 (registry `sjtu`)
  Downloaded ppv-lite86 v0.2.17 (registry `sjtu`)
  Downloaded 5 crates (124.6 KB) in 18.52s
   Compiling cfg-if v1.0.0
   Compiling ppv-lite86 v0.2.17
   Compiling getrandom v0.2.12
   Compiling rand_core v0.6.4
   Compiling rand_chacha v0.3.1
   Compiling rand v0.8.5
   Compiling guessing_game v0.1.0 (C:\Users\Administrator\Project\Rust_Project\guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 3m 02s
```

可能会出现不同的版本号（多亏了语义化版本，它们与代码是兼容的！），同时显示顺序也可能会有所不同。

现在我们有了一个外部依赖，Cargo 从 *registry* 上获取所有包的最新版本信息，这是一份来自 [Crates.io](https://crates.io/) 的数据拷贝。Crates.io 是 Rust 生态环境中的开发者们向他人贡献 Rust 开源项目的地方。

在更新完 registry 后，Cargo 检查 `[dependencies]` 片段并下载列表中包含但还未下载的 crates。本例中，虽然只声明了 `rand` 一个依赖，然而 Cargo 还是额外获取了 `rand` 所需要的其他 crates，因为 `rand` 依赖它们来正常工作。下载完成后，Rust 编译依赖，然后使用这些依赖编译项目。

如果不做任何修改，立刻再次运行 `cargo build`，则不会看到任何除了 `Finished` 行之外的输出。Cargo 知道它已经下载并编译了依赖，同时 *Cargo.toml* 文件也没有变动。Cargo 还知道代码也没有任何修改，所以它不会重新编译代码。因为无事可做，它简单的退出了。

如果打开 *src/main.rs* 文件，做一些无关紧要的修改，保存并再次构建，则会出现两行输出：

```bash
 Book@Matebook ~\Project\Rust_Project\guessing_game git:master ❯❯❯ cargo build
    Finished dev [unoptimized + debuginfo] target(s) in 0.02s
```

这一行表示 Cargo 只针对 *src/main.rs* 文件的微小修改而更新构建。依赖没有变化，所以 Cargo 知道它可以复用已经为此下载并编译的代码。它只是重新构建了部分（项目）代码。



### Cargo.lock 文件确保构建是可重现的

Cargo 有一个机制来确保任何人在任何时候重新构建代码，都会产生相同的结果：Cargo 只会使用你指定的依赖版本，除非你又手动指定了别的。例如，如果下周 `rand` crate 的 `0.8.6` 版本出来了，它修复了一个重要的 bug，同时也含有一个会破坏代码运行的缺陷。为了处理这个问题，Rust 在你第一次运行 `cargo build` 时建立了 *Cargo.lock* 文件，我们现在可以在*guessing_game* 目录找到它。

当第一次构建项目时，Cargo 计算出所有符合要求的依赖版本并写入 *Cargo.lock* 文件。当将来构建项目时，Cargo 会发现 *Cargo.lock* 已存在并使用其中指定的版本，而不是再次计算所有的版本。这使得你拥有了一个自动化的可重现的构建。换句话说，项目会持续使用 `0.8.5` 直到你显式升级，多亏有了 *Cargo.lock* 文件。由于 *Cargo.lock* 文件对于“可重复构建”非常重要，因此它通常会和项目中的其余代码一样纳入到版本控制系统中。



## 更新 crate 到一个新版本

当你 **确实** 需要升级 crate 时，Cargo 提供了这样一个命令，`update`，它会忽略 *Cargo.lock* 文件，并计算出所有符合 *Cargo.toml* 声明的最新版本。Cargo 接下来会把这些版本写入 *Cargo.lock* 文件。不过，Cargo 默认只会寻找大于 `0.8.5` 而小于 `0.9.0` 的版本。如果 `rand` crate 发布了两个新版本，`0.8.6` 和 `0.9.0`，在运行 `cargo update` 时会出现如下内容：

```powershell
$ cargo update
    Updating crates.io index
    Updating rand v0.8.5 -> v0.8.6
```

Cargo 忽略了 `0.9.0` 版本。这时，你也会注意到的 *Cargo.lock* 文件中的变化无外乎现在使用的 `rand` crate 版本是`0.8.6` 。如果想要使用 `0.9.0` 版本的 `rand` 或是任何 `0.9.x` 系列的版本，必须像这样更新 *Cargo.toml* 文件：

```toml
[dependencies]

rand = "0.9.0"
```

下一次运行 `cargo build` 时，Cargo 会从 registry 更新可用的 crate，并根据你指定的新版本重新计算。

第十四章会讲到 [Cargo](http://doc.crates.io/) 及其[生态系统](http://doc.crates.io/crates-io.html) 的更多内容，不过目前你只需要了解这么多。通过 Cargo 复用库文件非常容易，因此 Rustacean 能够编写出由很多包组装而成的更轻巧的项目。



### 生成一个随机数

使用 rand 来生成一个猜猜看随机数，下一步是更新 `src/main.rs`：

```rust
use rand::Rng;
use std::io; // 导入标准输入/输出库 // 导入随机数生成器库

fn main() {
    println!("Guess the number!");
    let secret_number = rand::thread_rng().gen_range(1..100); // 生成一个1到100的随机数
    println!("The secret number is: {}", secret_number); // 输出随机数

    println!("please input your guess:");
    let mut guess = String::new(); // 创建一个空字符串变量
    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line"); // 读取用户输入
    let guess: u32 = guess.trim().parse().expect("Please enter a number"); // 转换为数字类型

    println!("You guessed: {}", guess); // 输出用户输入
}

/*
Guess the number!
The secret number is: 92
please input your guess:
5
You guessed: 5
*/
```

首先，我们新增了一行 `use rand::Rng;`。`Rng` 是一个 trait，它定义了随机数生成器应实现的方法，想使用这些方法的话，此 trait 必须在作用域中。第十章会详细介绍 trait。

接下来，我们在中间还新增加了两行。第一行调用了 `rand::thread_rng` 函数提供实际使用的随机数生成器：它位于当前执行线程的本地环境中，并从操作系统获取 seed。接着调用随机数生成器的 `gen_range` 方法。这个方法由 `use rand::Rng` 语句引入到作用域的 `Rng` trait 定义。`gen_range` 方法获取一个范围表达式（range expression）作为参数，并生成一个在此范围之间的随机数。这里使用的这类范围表达式使用了 `start..=end` 这样的形式，也就是说包含了上下端点，所以需要指定 `1..=100` 来请求一个 1 和 100 之间的数。

> 注意：你不可能凭空就知道应该 use 哪个 trait 以及该从 crate 中调用哪个方法，因此每个 crate 有使用说明文档。Cargo 有一个很棒的功能是：运行 `cargo doc --open` 命令来构建所有本地依赖提供的文档，并在浏览器中打开。例如，假设你对 `rand` crate 中的其他功能感兴趣，你可以运行 `cargo doc --open` 并点击左侧导航栏中的 `rand`。

新增加的第二行代码打印出了秘密数字。这在开发程序时很有用，因为可以测试它，不过在最终版本中会删掉它。如果游戏一开始就打印出结果就没什么可玩的了！

### 代码解释：

```rust
io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line"); // 读取用户输入
```

在这段代码中，`io::stdin()` 表示标准输入流，用于从用户获取输入。`read_line()` 是 `stdin()` 对象的一个方法，用于读取输入流中的一行文本。

`&mut guess` 是一个可变引用，它用于接收用户输入的文本并存储在变量 `guess` 中。变量 `guess` 的类型应该是一个字符串类型，通过 `&mut` 关键字将其转换为可变引用。

`expect("无法读取行")` 是一个错误处理机制。如果读取行操作失败，它会打印错误消息 "无法读取行" 并终止程序的执行。



### 比较猜测的数字和秘密数字

现在有了用户输入和一个随机数，现在可以比较他们：

注意：这段代码暂时还不能通过编译！！！！

```rust
use rand::Rng;
use std::cmp::Ordering;
use std::io; // 导入标准输入/输出库 // 导入随机数生成器库

fn main() {
    println!("You guessed: {guess}");

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}
```



首先我们增加了另一个 use 声明，从标准库中引入了一个叫做 `std::cmp::Ordering` 的类型到作用域中。`Ordering` 也是一个枚举，不过它的成员是 ==Less、Greater 和 Equal==。这是比较两个值时可能出现的三种结果。

接着，底部的五行新代码使用了 `Ordering` 类型，`cmp` 方法用来比较两个值并可以在任何可比较的值上调用。它获取一个被比较值的引用：这里是把 `guess` 与 `secret_number` 做比较。然后它会返回一个刚才通过 `use` 引入作用域的 `Ordering` 枚举的成员。使用一个 [`match`](https://kaisery.github.io/trpl-zh-cn/ch06-02-match.html) 表达式，根据对 `guess` 和 `secret_number` 调用 `cmp` 返回的 `Ordering` 成员来决定接下来做什么。

一个 `match` 表达式由 **分支（arms）** 构成。一个分支包含一个 **模式**（*pattern*）和表达式开头的值与分支模式相匹配时应该执行的代码。Rust 获取提供给 `match` 的值并挨个检查每个分支的模式。`match` 结构和模式是 Rust 中强大的功能，它体现了代码可能遇到的多种情形，并帮助你确保没有遗漏处理。这些功能将分别在第六章和第十八章详细介绍。

让我们看看使用 `match` 表达式的例子。假设用户猜了 50，这时随机生成的秘密数字是 38。

比较 50 与 38 时，因为 50 比 38 要大，`cmp` 方法会返回 `Ordering::Greater`。`Ordering::Greater` 是 `match` 表达式得到的值。它检查第一个分支的模式，`Ordering::Less` 与 `Ordering::Greater`并不匹配，所以它忽略了这个分支的代码并来到下一个分支。下一个分支的模式是 `Ordering::Greater`，**正确** 匹配！这个分支关联的代码被执行，在屏幕打印出 `Too big!`。`match` 表达式会在第一次成功匹配后终止，因为该场景下没有检查最后一个分支的必要。

比如：尝试编译：

```bash
 Book@Matebook ~\Project\Rust_Project\guessing_game git:master ❯❯❯ cargo build   
   Compiling guessing_game v0.1.0 (C:\Users\Administrator\Project\Rust_Project\guessing_game)
error[E0425]: cannot find value `guess` in this scope
 --> src\main.rs:6:29
  |
6 |     println!("You guessed: {guess}");
  |                             ^^^^^ not found in this scope 

error[E0425]: cannot find value `guess` in this scope
 --> src\main.rs:8:11
  |
8 |     match guess.cmp(&secret_number) {
  |           ^^^^^ not found in this scope

error[E0425]: cannot find value `secret_number` in this scope 
 --> src\main.rs:8:22
  |
8 |     match guess.cmp(&secret_number) {
  |                      ^^^^^^^^^^^^^ not found in this scope
```

错误的核心表明这里有 **不匹配的类型**（*mismatched types*）。Rust 有一个静态强类型系统，同时也有类型推断。当我们写出 `let guess = String::new()` 时，Rust 推断出 `guess` 应该是 `String` 类型，并不需要我们写出类型。另一方面，`secret_number`，是数字类型。几个数字类型拥有 1 到 100 之间的值：32 位数字 `i32`；32 位无符号数字 `u32`；64 位数字 `i64` 等等。Rust 默认使用 `i32`，所以它是 `secret_number` 的类型，除非增加类型信息，或任何能让 Rust 推断出不同数值类型的信息。这里错误的原因在于 Rust 不会比较字符串类型和数字类型。

所以我们必须把从输入中读取到的 `String` 转换为一个真正的数字类型，才好与秘密数字进行比较。这可以通过在 `main` 函数体中增加如下代码来实现：

```rust
use rand::Rng;
use std::cmp::Ordering;
use std::io; // 导入随机数模块 // 导入比较模块

fn main() {
    println!("猜数！");

    let secret_number = rand::thread_rng().gen_range(1..101); // 生成一个1到100的随机数

    println!("这个神秘数字是：{}", secret_number);
    println!("请输入一个数字：");

    let mut guess = String::new(); // 定义一个空字符串

    io::stdin().read_line(&mut guess).expect("无法读取行"); // 读取用户输入

    let guess: u32 = match guess.trim().parse() {
        // 转换输入的字符串为数字
        Ok(num) => num, // 成功转换
        Err(_) => {
            // 转换失败
            println!("输入的不是数字！");
            return;
        }
    };

    println!("你猜的数字是：{}", guess);

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("你猜的数字小了！"),
        Ordering::Greater => println!("你猜的数字大了！"),
        Ordering::Equal => println!("你猜的数字对了！"),
    }
}

/*
Book@Matebook ~\Project\Rust_Project\guessing_game git:master ❯❯❯ cargo run
   Compiling guessing_game v0.1.0 (C:\Users\Administrator\Project\Rust_Project\guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 0.45s
     Running `target\debug\guessing_game.exe`
Guess the number!
The secret number is: 24
please input your guess:
  76
You guessed: 76
Too big!
*/
```

漂亮！即便是在猜测之前添加了空格，程序依然能判断出用户猜测了 76。多运行程序几次，输入不同的数字来检验不同的行为：猜一个正确的数字，猜一个过大的数字和猜一个过小的数字。

现在游戏已经大体上能玩了，不过用户只能猜一次。增加一个循环来改变它吧！



### 使用循环来允许多次猜测

loop 关键字创建了一个无限循环，会增加循环来给用户更多机会猜测数字：

```rust
use rand::Rng; // 导入随机数生成器库
use std::cmp::Ordering; // 导入比较大小的库
use std::io; // 导入标准输入/输出库 // 导入随机数生成器库

fn main() {
    println!("Guess the number!");
    let secret_number = rand::thread_rng().gen_range(1..100); // 生成一个1到100的随机数
    loop {    // 循环
        println!("The secret number is: {}", secret_number); // 输出随机数
        println!("please input your guess:"); // 输出提示信息

        let mut guess = String::new(); // 创建一个空字符串，用于接收用户输入

        io::stdin() // 获取标准输入
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = guess.trim().parse().expect("Please type a number!"); // 读取用户输入并转换为数字

        println!("You guessed: {guess}");

        match guess.cmp(&secret_number) {
            // 比较用户输入和随机数
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => println!("You win!"),
        }
    }
}

/*
Book@Matebook ~\Project\Rust_Project\guessing_game git:master ❯❯❯ cargo run
   Compiling guessing_game v0.1.0 (C:\Users\Administrator\Project\Rust_Project\guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 0.46s
     Running `target\debug\guessing_game.exe`
Guess the number!
The secret number is: 65
please input your guess:
73
You guessed: 73
Too big!
The secret number is: 58
please input your guess:
22
You guessed: 22
Too small!
The secret number is: 5
please input your guess:
*/
```

如上所示，我们将提示用户猜测之后的所有内容移动到了循环中。确保 loop 循环中的代码多缩进四个空格，再次运行程序。



### 猜测正确后退出

增加一个 break 语句，让猜对是退出游戏：

```rust
match guess.cmp(&secret_number) {
    // 比较用户输入和随机数
    Ordering::Less => println!("Too small!"),
    Ordering::Greater => println!("Too big!"),
    Ordering::Equal => {
        println!("You win!");
        break; // 退出循环
    }
}
```

通过在 `You win!` 之后增加一行 `break`，用户猜对了神秘数字后会退出循环。退出循环也意味着退出程序，因为循环是 `main` 的最后一部分。

### 处理无效输入

为了进一步改善游戏，不要在用户输入非数字时崩溃，需要忽略非数字，让用户可以继续猜测。可以通过以下修改 `guees` 将 `String` 转换为 `u32` 那部分代码来实现，实例如下：

```rust
 let guess: u32 = guess.trim().parse().expect("Please type a number!"); // 读取用户输入并转换为数字

// 将以上实例修改为

let guess: u32 = match guess.trim().parse() {
    // 尝试将用户输入转换为数字
    Ok(num) => num,
    Err(_) => continue, // 输入非数字，重新输入
};
```

将 `expect` 调用换成 `match` 语句，以从遇到错误就崩溃转换为处理错误。须知 `parse` 返回一个 `Result` 类型，而 `Result` 是一个拥有 `Ok` 或 `Err` 成员的枚举。这里使用的 `match` 表达式，和之前处理 `cmp` 方法返回 `Ordering` 时用的一样。

如果 `parse` 能够成功的将字符串转换为一个数字，它会返回一个包含结果数字的 `Ok`。这个 `Ok` 值与 `match` 第一个分支的模式相匹配，该分支对应的动作返回 `Ok` 值中的数字 `num`，最后如愿变成新创建的 `guess` 变量。

如果 `parse` **不**能将字符串转换为一个数字，它会返回一个包含更多错误信息的 `Err`。`Err` 值不能匹配第一个 `match` 分支的 `Ok(num)` 模式，但是会匹配第二个分支的 `Err(_)` 模式：`_` 是一个通配符值，本例中用来匹配所有 `Err` 值，不管其中有何种信息。所以程序会执行第二个分支的动作，`continue` 意味着进入 `loop` 的下一次循环，请求另一个猜测。这样程序就有效的忽略了 `parse` 可能遇到的所有错误！

```bash
The secret number is: 87
please input your guess:
foo
The secret number is: 14
please input your guess:
14
You guessed: 14
You win!
```

太棒了！再有最后一个小的修改，就能完成猜猜看游戏了：还记得程序依然会打印出秘密数字。在测试时还好，但正式发布时会毁了游戏。删掉打印秘密数字的 `println!`

完整代码如下：

```rust
use rand::Rng;
use std::cmp::Ordering;
use std::io; // 导入随机数模块 // 导入比较模块

fn main() {
    println!("猜数！");

    let secret_number = rand::thread_rng().gen_range(1..101); // 生成一个1到100的随机数

    println!("这个神秘数字是：{}", secret_number);

    loop {
        println!("请输入一个数字：");

        let mut guess = String::new(); // 定义一个空字符串

        io::stdin().read_line(&mut guess).expect("无法读取行"); // 读取用户输入

        let guess: u32 = match guess.trim().parse() {
            // 转换输入的字符串为数字
            Ok(num) => num, // 成功转换
            Err(_) => {
                // 转换失败
                println!("输入的不是数字！");
                continue;
            }
        };

        println!("你猜的数字是：{}", guess);

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("你猜的数字小了！"),
            Ordering::Greater => println!("你猜的数字大了！"),
            Ordering::Equal => {
                println!("你猜对了！");
                break;
            }
        }
    }
}
```









