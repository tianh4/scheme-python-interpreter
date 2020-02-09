# scheme-python-interpreter
A simplified interpreter, inspired from https://zhuanlan.zhihu.com/p/28989326

## scheme 语法

语法（syntax），指字母排列成正确表达式或声明的顺序。
语义（semantics），指这些表达式或声明的意义。
求值（evaluating），指计算表达式的值。

```java
if (x.val() > 0){
	fn(A[i] + 1,
		return new String[] {"one", "two"});
}
```

```scheme
(if (> (val x) 0)
	(fn (+ (aref A i) 1)
		(quote (one two)))
```

Scheme 语法非常简单
- Scheme 程序中只有表达式，声明和表达式没有区别。
- 数字（如 1）和符号（如 A，fn，+，>）被称为原子表达式（atomic expression），无法被拆分为更小的表达式。
- 除此之外的都是列表表达式（list expression），在括号中包含 0 或更多个表达式。
	- 若第一个元素是关键字（如 if），那这个列表是一个特殊形式（special form），特殊形式的意义取决于关键字。
	- 若第一个元素不是关键字（如 fn），那这个列表是函数调用。

Scheme 非常简洁，仅由 5 个关键字和 8 个语法形式构成，而 Python 有 33 个关键字和 110 个语法形式，Java 有 50 个关键字和 133 个语法形式。
