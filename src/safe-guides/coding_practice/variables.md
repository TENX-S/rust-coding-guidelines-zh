# 变量

这里所说变量是指局部变量。默认情况下，Rust 会强制初始化所有值，以防止使用未初始化的内存。

变量命名风格指南请看 [编码风格-命名](../code_style/naming.md)

---

## P.VAR.01 非必要不要像 C 语言那样先声明可变变量然后再去赋值

### 【描述】

不要先声明一个可变的变量，然后再后续过程中去改变它的值。一般情况下，声明一个变量的时候，要对其进行初始化。如果后续可能会改变其值，要考虑优先使用变量遮蔽（继承式可变）功能。如果需要在一个子作用域内改变其值，再使用可变绑定或可变引用。



## P.VAR.02 不要在子作用域中使用变量遮蔽功能

当两个作用域存在包含关系时，不要使用变量遮蔽功能，即，在较小的作用域内定义与较大作用域中相同的变量名，以免引起逻辑Bug。

## P.VAR.03 避免大量栈分配

Rust 默认在栈上存储。局部变量占用过多栈空间，会栈溢出。

## P.VAR.04 禁止将局部变量的引用返回函数外

局部变量生命周期始于其声明终于其作用域结束。如果在其生命周期之外被引用，则程序的行
为是未定义的。


---

## G.VAR.01 交换两个变量的值应该使用 `std::mem::swap` 而非赋值

### 【级别：必须】

必须按此规范执行。

### 【Lint 检测】

| lint name | Clippy 可检测 | Rustc 可检测 | Lint Group | level |
| ------ | ---- | --------- | ------ | ------ | 
| [almost_swapped](https://rust-lang.github.io/rust-clippy/master/#almost_swapped) | yes| no | Correctness | deny |

### 【描述】