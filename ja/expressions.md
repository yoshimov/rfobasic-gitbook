式
===========

## 数式 `<nexp>` {#numeric-expression-nexp}

<!-- numeric expression consists of one or more numeric variables or numeric constants separated by binary operators and optionally preceded by unary operators. The definition can be stated more completely using this standard formal notation: -->
数式は、一つ以上の数値変数もしくは数値定数が二項演算で分割されているか、例外的な単項演算で構成されています。
正式な定義は以下の通りです。

```
<nexp> := {<numeric variable>|<numeric constant} {<noperator> <nexp>}
```

<!-- The next few sections define all of the terms. -->
ここからの項で定義に関して説明します。

### 数値演算 `<noperator>`

<!-- The numeric operators are listed by precedence. Higher precedence operators are executed before lower precedence operators. Precedence can be changed by using parentheses. -->
以下は数値演算の優先度順のリストです。上位の演算が、下位の演算よりも先に実行されます。
優先度はカッコを使うことで変更できます。

1.	単項 `+`, 単項 `–`
2.	指数演算 `^`
3.	かけ算 `*`, わり算 `/`
4.	たし算 `+`, ひき算 `–`

<!-- Note that the comma (',') is not an operator in BASIC!. It is sometimes uses as a separator between expressions; for example, see the `PRINT` command. -->
コンマ`,`は演算ではありません。コンマは式を分離する際に使われます。
`PRINT`コマンドを参照してください。

### 数式の例

```
a
a*b + 4/d – 2*(d^2)
a + b + d + RND()
b + CEIL(d/25) + 5
```

### Pre- and Post-Increment Operators

`++x`	Increments the value of x by 1 before the x value is used

`--y`	Decrements the value of y by 1 before the y value is used

`x++`	Increments the value of x by 1 after the x value is used

`y--`	Decrements the value of y by 1 after the y value is used

```
a = 5		% creates the variable a and sets it to 5
PRINT --a	% sets a to 4 and prints 4
PRINT a--	% prints 4 and sets a to 3
```

These operations work only on numeric variables. Their action is performed as part of evaluating the variable, so they do not follow normal precedence rules.

Using these operators on a variable makes the variable unavailable for other operations that require a variable. For example, you cannot pass a variable by reference (see `User-Defined functions`) if you pre- or post-increment or -decrement it, because you cannot pass an expression by reference. An exception is made to allow implicit assignment (actual or implied `LET`).

## String Expression `<sexp>` {#string-expression-sexp}

A string expression consists of one or more string variables or string constants separated by '+' operators. The definition can be stated more completely using this standard formal notation:

`<sexp> := {<string variable>|<string constant>} { + <sexp>}`

There is only one string operator: +. This is the concatenation operator. It is used to join two strings:

```
PRINT "abc" + "def"	% prints abcdef
```

## Logical Expression `<lexp>`

Logical expressions, or Boolean expressions, produce only two results: false or true. False is represented in BASIC! by the numeric value of zero. Anything that is not zero is true. False = 0. True = not 0.

There are two types of logical expressions: Numeric logical expressions and string logical expressions. Both types produce a numerically-represented values of true or false. Each type consists of one or more variables or constants separated by binary logical operators, formally defined like this:

```
<slexp> := {<string variable>|<string constant>} <logical operator> {<string variable>|<string constant>}
<nlexp> := {<numeric variable>|<numeric constant>} <logical operator> {<numeric variable>|<numeric constant>}
```

There is also the unique unary NOT (!) operator. NOT inverts the truth of a logical expression.

### Logical Operators

Most of the logical operators are used for comparison. You can compare strings or numbers (<, =, etc.). You can use the other Boolean operators (!, &, |) on numbers but not on strings.

This table shows all of the Logical operators. They are listed by precedence with the highest precedence first. Precedence may be modified by using parentheses.

|Precedence|Operator|Meaning|Operands|
|----------|--------|-------|--------|
|1|	`!`|	Unary Not|	One `<nlexp>` only|
|2|	`<`<br/> `>`<br/> `<=`<br/> `>=`|	Less Than,<br/> Greater Than,<br/> Less Than or Equal,<br/> Greater Than or Equal|	Two `<nlexp>` or two `<slexp>`|
|3|	`=`<br/> `<>`|	Equal,<br/> Not Equal|	Two `<nlexp>` or two `<slexp>`|
|4|	`&`<br/> <code>&#124;</code>|	And,<br/> Or|	Two `<nlexp>` only|

### Examples of Logical Expressions

```
1 < 2 (true)
3 <> 4 (true)
"a" < "bcd" (true)
1 & 0 (false)
!(1 & 0) (true)
```

## Parentheses

Parentheses can be used to override operator precendence.

```
a = b * c + d		% the multiplication is done first
a = b * (c + d)	% the addition is done first
```

Parentheses can also be placed around a variable, anywhere except to the left of an = sign. This can be useful in places where BASIC! may mistake part of a variable for a special keyword. For an example, see `Program Control Commands – For - To - Step / Next`, below.
