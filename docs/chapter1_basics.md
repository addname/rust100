# 第一章：入门与基础

本章涵盖了开始使用 Rust 所需了解的基础知识，包括安装、Cargo 工具、基本语法和控制流。

---

### 1. 如何在我的电脑上安装 Rust？

**答：**
你可以通过 `rustup` 来安装 Rust，它是 Rust 的官方工具链管理器。

在 Linux 或 macOS 上，打开终端并运行：
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

在 Windows 上，访问 [rust-lang.org](https://www.rust-lang.org/tools/install) 并按照说明下载 `rustup-init.exe` 并运行它。

安装完成后，通过运行 `rustc --version` 和 `cargo --version` 来验证安装是否成功。

---

### 2. `rustc` 和 `cargo` 有什么区别？

**答：**
- `rustc` 是 Rust 的编译器。它负责将你的 `.rs` 源代码文件编译成可执行文件。你通常很少直接使用它。
- `cargo` 是 Rust 的构建系统和包管理器。它是一个功能强大的工具，可以处理依赖管理、编译代码、运行测试、生成文档等。在实际项目中，你几乎总是通过 `cargo` 来工作。

---

### 3. 如何创建一个新的 Rust 项目？

**答：**
使用 Cargo！在终端中运行以下命令：
```bash
# 创建一个二进制程序项目
cargo new my_project

# 创建一个库项目
cargo new my_library --lib
```
这会创建一个包含 `Cargo.toml`（配置文件）和 `src/main.rs`（或 `src/lib.rs`）源文件的新目录。

---

### 4. 如何编译并运行我的 Rust 程序？

**答：**
在你的项目目录中，使用 `cargo run`。这个命令会处理所有事情：
1.  如果需要，它会先编译你的代码。
2.  然后运行生成的可执行文件。

```bash
cd my_project
cargo run
```
如果你只想编译而不运行，使用 `cargo build`。

---

### 5. `Cargo.toml` 文件是做什么用的？

**答：**
`Cargo.toml` 是 Cargo 的清单文件，采用 TOML 格式。它包含了项目的所有元数据和配置，主要包括：
- `[package]`: 项目信息，如名称、版本、作者。
- `[dependencies]`: 项目所依赖的外部库（crates）。

---

### 6. Rust 中的变量默认是可变的还是不可变的？

**答：**
默认是**不可变**的。这是 Rust 强调安全性的一个核心特性。如果你想让一个变量可变，必须使用 `mut` 关键字。

```rust
let x = 5; // 不可变
let mut y = 10; // 可变
y = 15; // 正确
// x = 6; // 编译错误！
```

---

### 7. Rust 有哪些基本的标量类型？

**答：**
Rust 有四种主要的标量类型：
- **整数 (Integer):** 有符号（`i8`, `i32`, `i64`, `isize`）和无符号（`u8`, `u32`, `u64`, `usize`）。`isize` 和 `usize` 的大小取决于你的计算机架构（32位或64位）。
- **浮点数 (Floating-Point):** `f32` 和 `f64`。`f64` 是默认类型，精度更高。
- **布尔值 (Boolean):** `bool`，值为 `true` 或 `false`。
- **字符 (Character):** `char`，表示一个单独的 Unicode 标量值，用单引号括起来（例如 `'a'`）。它的大小是 4 个字节。

---

### 8. `&str` 和 `String` 有什么区别？

**答：**
这是一个常见的问题，涉及到 Rust 的所有权系统。
- `String`: 一个在堆上分配的、可增长的、可变的 UTF-8 编码字符串。当你需要拥有字符串数据并可能修改它时使用。
- `&str`: 通常称为“字符串切片”，它是一个指向 `String` 或字符串字面量中一部分数据的**不可变**引用。它没有所有权，只是“借用”数据。

---

### 9. 如何在 Rust 中定义一个函数？

**答：**
使用 `fn` 关键字。Rust 使用 `snake_case` 作为函数名的约定。如果函数有参数，你需要显式地声明它们的类型。如果函数返回值，你需要使用 `->` 来指定返回类型。

```rust
// 没有参数，没有返回值
fn say_hello() {
    println!("Hello, Rust!");
}

// 有参数，有返回值
fn add_one(x: i32) -> i32 {
    x + 1 // 表达式作为返回值，注意没有分号
}
```

---

### 10. Rust 函数的返回值有什么特别之处？

**答：**
Rust 是一个基于表达式的语言。函数体中的最后一个表达式会自动成为函数的返回值，前提是该表达式后面**没有分号**。你也可以使用 `return` 关键字提前返回。

```rust
fn five() -> i32 {
    5 // 返回 5
}

fn ten() -> i32 {
    return 10; // 使用 return 关键字，效果相同
}
```

---

### 11. Rust 中的 `if` 语句有什么不同？

**答：**
`if` 在 Rust 中是一个表达式，而不是一个语句。这意味着 `if` 可以返回值，你可以用它来给 `let` 语句赋值。

```rust
let number = 6;

if number % 4 == 0 {
    println!("number is divisible by 4");
} else {
    println!("number is not divisible by 4");
}

// `if` 作为表达式
let condition = true;
let x = if condition { 5 } else { 6 }; // x 的值将是 5
```
**注意：** `if` 的每个分支返回的值类型必须相同。

---

### 12. Rust 有哪几种循环？

**答：**
Rust 提供了三种循环结构：
- `loop`: 创建一个无限循环，你需要使用 `break` 来退出。
- `while`: 当条件为 `true` 时循环。
- `for`: 遍历一个迭代器。这是最常用和最安全的循环方式。

```rust
// for 循环
let a = [10, 20, 30, 40, 50];
for element in a.iter() {
    println!("the value is: {}", element);
}

// 遍历一个范围
for number in 1..4 { // 不包括 4
    println!("{}!", number);
}
```

---

### 13. 什么是 `isize` 和 `usize`？

**答：**
它们是“指针大小”的整数类型。
- `usize`: 无符号整数，其大小与计算机的指针大小相同。在 64 位系统上是 64 位，在 32 位系统上是 32 位。它主要用于索引集合。
- `isize`: 有符号整数，大小与指针相同。

当你需要索引数组或 `Vector` 时，应该使用 `usize`。

---

### 14. 如何在 Rust 中写注释？

**答：**
- **行注释:** `//`，注释到行尾。
- **块注释:** `/* ... */`，可以跨越多行。
- **文档注释:** `///` 或 `//!`，用于生成 HTML 文档。`///` 注释它后面的项，`//!` 注释包含它的项（通常是模块或 crate）。

```rust
// 这是一个行注释

/*
  这是一个
  多行块注释
*/

/// 这是一个文档注释，用于描述下面的函数
fn my_function() {}
```

---

### 15. Rust 中的元组 (Tuple) 是什么？

**答：**
元组是一种将多个不同类型的值组合成一个复合类型的方式。元组的长度是固定的，一旦声明就无法改变。

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);

// 解构元组
let (x, y, z) = tup;
println!("The value of y is: {}", y); // 打印 6.4

// 通过索引访问
let five_hundred = tup.0;
```

---

### 16. Rust 中的数组 (Array) 是什么？

**答：**
数组也是一种将多个值组合在一起的方式，但与元组不同，数组中的每个元素的类型**必须相同**。Rust 中的数组长度是固定的，存储在栈上。

```rust
let a = [1, 2, 3, 4, 5]; // 编译器自动推断类型和长度
let months: [&str; 12] = ["January", "February", /* ... */, "December"];

// 访问元素
let first = a[0];
```

---

### 17. 什么是表达式和语句？

**答：**
- **语句 (Statements):** 是执行某些操作但不返回值的指令。例如，`let x = 5;` 是一个语句。
- **表达式 (Expressions):** 会计算并产生一个值。例如，`5 + 6` 是一个表达式，它的值为 `11`。`if`、函数调用等都是表达式。

在 Rust 中，这是一个重要的区别。例如，你不能写 `let x = (let y = 6);` 因为 `let y = 6` 是一个语句，不返回值。

---

### 18. `cargo check` 命令有什么用？

**答：**
`cargo check` 是一个非常有用的命令。它会快速检查你的代码以确保它可以通过编译，但**不会**产生任何可执行文件。这比 `cargo build` 快得多，因为他跳过了代码生成阶段。

在你编码过程中，可以频繁使用 `cargo check` 来快速验证你的代码语法和类型是否正确。

---

### 19. Rust 如何处理整数溢出？

**答：**
这取决于构建模式：
- **Debug 模式 (默认):** 如果发生整数溢出，Rust 会 `panic`（程序崩溃）。这有助于在开发阶段尽早发现 bug。
- **Release 模式 (`--release`):** 如果发生整数溢出，Rust 会执行“环绕”（two's complement wrapping）。例如，一个 `u8` 的值 `255` 再加 `1` 会变成 `0`。

如果你希望明确处理溢出，可以使用标准库提供的 `wrapping_*`、`checked_*`、`overflowing_*` 和 `saturating_*` 系列方法。

---

### 20. 什么是 shadowing (变量遮蔽)？

**答：**
在 Rust 中，你可以声明一个与之前变量同名的新变量。这个新变量会“遮蔽”前一个变量。这允许你重复使用一个更有意义的变量名，甚至改变它的类型。

```rust
let x = 5;

// 在内部作用域中遮蔽 x
let x = x + 1; 

{
    // 在这个作用域内再次遮蔽
    let x = x * 2;
    println!("The value of x in the inner scope is: {}", x); // 打印 12
}

println!("The value of x is: {}", x); // 打印 6
```
这与将变量标记为 `mut` 是不同的，因为遮蔽实际上是创建了一个全新的变量。
