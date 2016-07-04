Assignment Operations
=====================

Variables get values by means of assignment statements. Simple assignment statements are of the form:

```
<nvar> = <nexp>
<svar> = <sexp>
```

The special form of the statement allows BASIC! to infer the command. The implied command is `LET`.

## Let

The original Basic language used the command, `LET`, to denote an assignment operation as in:

```
LET <nvar> = <nexp>
```

BASIC! also has the `LET` command but it is optional. If you use other programming languages, it may look strange to you, but there are two reasons you might use `LET`.

First, you must use `LET` if you want to have a variable name start with a BASIC! keyword. Such keywords may not appear at the beginning of a new line. The statement:

```
Letter$ = "B"
```

is seen by BASIC! as

```
LET ter$ = "B"
```

If you really want to use Letter$ as a variable, you can safely use it by putting it in a `LET` statement:

```
LET Letter$ = "B"
```

If you do the assignment in a single-line `IF` statement, you must also use the `LET` command:

```
IF 1 < 2 THEN LET letter$ = "B"
```

Second, assignment is faster with the `LET` command than without it.

## OpEqual Assignment Operations

All of the binary arithmetic and logical operators (+, -, *, /, ^, &, |) may be used with the equals sign (=) to make a single "OpEqual" operator. The combined operator works like this:

```
var op= expression  is the same as  var = var op (expression)
```

 Here are some examples:

``` 
a += 1			is the same as		a = a + 1
a$ += "xyz"		is the same as		a$ = a$ + "xyz"
b /= 5 + 3		is the same as		b = b / (5 + 3)
c ^= log(37) + 1	is the same as		c = c ^ (log(37) + 1)
d *= --d + d--		is the same as		d = d * (--d + d--)
m &= (x$ = y$) | (x$ != z$) is the same as	m = m & ((x$ = y$) | (x$ != z$))
```
