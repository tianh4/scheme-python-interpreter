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

## Lispy

Lispy 是 Scheme 的一个子集，包含 5 种语法形式（2 种原子，2 种特殊形式，1 种调用）。

所有语法形式
| 表达式（expression）| 语法（syntax）| 语义（semantics）|
| ------------------- | ------------- | ---------------- |
| 变量引用（variable reference）| var | 该符号是变量名，该符号的值是变量的值 |
| 字面常量（constant literal） | number| 一个数字，求值得到本身 |
| 条件（conditional） | (if test conseq alt) | 对 test 求值，结果为真对 conseq 求值并返回，结果为假对 alt 求值并返回 |
| 定义（definition）| (define var expr) | 定义一个变量，将 var 的值定义为 expr 求值得到的结果 |
| 过程调用（procedure）| (proc arg...) | 如果 proc 不是 if，define，quote 就被认为是一个过程，将过程作用于所有 args 求值 |

如，计算半径为 10 的圆的面积

```scheme
(begin
	(define r 10)
	(* pi (* r r)))
```

## 解释器做什么

解释器分为两部分
1. 分析（parse）：解释器的分析部分将程序以字符串的形式读入，按照语法规则（syntactic rules）验证正确性，将程序转换成一种内部表达形式。内部表达形式可以是一个树形结构，叫做语法抽象树（abstract syntax tree）。语法抽象书可以转换成可以被计算机执行的指令序列。
2. 执行（execute）：内部表达形式按照语言的语义规则进行处理，以此计算。

例子

```
>> program = "(begin (define r 10) (* pi (* r r)))"

>> parse(program)
['begin', ['define', 'r', 10], ['*', 'pi', ['*', 'r', 'r']]]

>>> eval(parse(program))
314.1592653589793
```

## 分析

## 环境

## 求值

## REPL

REPL，read-eval-print-loop，通过它可以即时读取，求值，输出。

```python
def repl(prompt='lis.py> '):
	"REPL 的简陋实现"
	
	while True:
		val = eval(parse(raw_input(prompt)))
		if val is not None:
			print(schemestr(val))

def schemestr(exp):
	"将一个 Python 对象转换成可以被 Scheme 读取的字符串"

	if isinstance(exp, List):
		return '(' + ' '.join(map(schemestr,exp))+')"
	else:
		return str(exp)
```


















