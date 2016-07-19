Math Functions
==============

Math functions act like numeric variables in a `<nexp>` (or `<lexp>`).

## `BOR(<nexp1>, <nexp2>)`

Returns the logical bitwise value of `<nexp1> OR <nexp2>`. The double-precision floating-point values are converted to 64-bit integers before the operation.

```
BOR(1,2) is 3
```

## `BAND(<nexp1>, <nexp2>)`

Returns the logical bitwise value of `<nexp1> AND <nexp2>`. The double-precision floating-point values are converted to 64-bit integers before the operation.

```
BAND(3,1) is 1
```

## `BXOR(<nexp1>, <nexp2>)`

Returns the logical bitwise value of `<nexp1> XOR <nexp2>`. The double-precision floating-point values are converted to 64-bit integers before the operation.

```
BXOR(7,1) is 6
```

## `BNOT(<nexp>)`

Returns the bitwise complement value of `<nexp>`. The double-precision floating-point value is converted to a 64-bit integer before the operation.

```
BNOT(7) is -8
HEX$(BNOT(HEX("1234"))) is ffffffffffffedcb
```

## `ABS(<nexp>)`

Returns the absolute value of `<nexp>`.

## `SGN(<nexp>)`

Returns the signum function of the numerical value of `<nexp>`, representing its sign.

|When the value is:|	Return:|
|------------------|-----------|
|`> 0`|	1|
|`= 0`|	0|
|`< 0`|	-1|

## `RANDOMIZE({<nexp>})`

Creates a pseudo-random number generator for use with the `RND()` function. The optional seed parameter `<nexp>` initializes the generator. Omitting the parameter is the same as specifying 0. If you call `RND()` without first calling `RANDOMIZE()`, it is the same as if you had executed `RANDOMIZE(0)`.

A non-zero seed initializes a predictable series of pseudo-random numbers. That is, for a given non-zero seed value, subsequent `RND()` calls will always return the same series of values.

If the seed is 0, the sequence of numbers from `RND()` is unpredictable and not reproducible. However, repeated `RANDOMIZE(0)` calls do not produce "more random" sequences.

The `RANDOMIZE()` function always returns zero.

## `RND()`

Returns a random number generated by the pseudorandom number generator. If a `RANDOMIZE(n)` has not been previously executed then a new random generator will be created using `RANDOMIZE(0)`.

The random number will be greater than or equal to zero and less than one. (`0 <= n < 1`).

```
d = FLOOR(6 * RND() + 1)		% roll a six-sided die
```

## `MAX(<nexp>, <nexp>)`

Returns the maximum of two numbers as an `<nvar>`.

## `MIN(<nexp>, <nexp>)`

Returns the minimum of two numbers as an `<nvar>`.

## `CEIL(<nexp>)`

Rounds up towards positive infinity. 3.X becomes 4 and -3.X becomes -3.

## `FLOOR(<nexp>)`

Rounds down towards negative infinity. 3.X becomes 3 and -3.X becomes -4.

## `INT(<nexp>)`

Returns the integer part of `<nexp>`. 3.X becomes 3 and -3.X becomes -3. This operation may also be called truncation, rounding down, or rounding toward zero.

## `FRAC(<nexp>)`

Returns the fractional part of `<nexp>`. 3.4 becomes 0.4 and -3.4 becomes -0.4.

`FRAC(n)` is equivalent to `"n - INT(n)"`.

## `MOD(<nexp1>, <nexp2>)`

Returns the remainder of `<nexp1>` divided by `<nexp2>`. If `<nexp2>` is 0, the function generates a runtime error.

## `ROUND(<value_nexp>{, <count_nexp>{, <mode_sexp>}})`

In it simplest form, `ROUND(<value_nexp>)`, this function returns the closest whole number to `<nexp>`. You can use the optional parameters to specify more complex operations.

The `<count_nexp>` is an optional decimal place count. It sets the number of places to the right of the decimal point. The last digit is rounded. The decimal place count must be `>= 0`. Omitting the parameter is the same as setting it to zero.

The `<mode_sexp>` is an optional rounding mode. It is a one- or two-character mnemonic code that tells `ROUND()` what kind of rounding to do. It is not case-sensitive. There are seven rounding modes:

|Mode:|	Meaning:|	-3.8|	-3.5|	-3.1|	3.1|	3.5|	3.8|
|-----|---------|-------|-------|-------|------|-------|-------|
|"HD"|	Half-down|	-4.0|	-3.0|	-3.0|	3.0|	3.0|	4.0|
|"HE"|	Half-even|	-4.0|	-4.0|	-3.0|	3.0|	4.0|	4.0|
|"HU"|	Half-up|	-4.0|	-4.0|	-3.0|	3.0|	4.0|	4.0|
|"D"|	Down| 	-3.0|	-3.0|	-3.0|	3.0|	3.0|	3.0|
|"U"|	Up|	-4.0|	-4.0|	-4.0|	4.0|	4.0|	4.0|
|"F"|	Floor|	-4.0|	-4.0|	-4.0|	3.0|	3.0|	3.0|
|"C"|	Ceiling|	-3.0|	-3.0|	-3.0|	4.0|	4.0|	4.0|

In this table, "down" means "toward zero" and "up" means "away from zero" (toward ±∞)

"Half" refers to behavior when a value is half-way between rounding up and rounding down(x.5 or -x.5). "Half-down" rounds x.5 towards zero and "half-up" rounds x.5 away from zero.

"Half-even" is either "half-down" or "half-up", whichever would make the result even. 4.5 and 3.5 both round to 4.0. "Half-even" is also called "banker’s rounding", because it tends to average out rounding errors.

If you do not provide a `<mode_sexp>`, `ROUND()` adds +0.5 and rounds down (toward zero). This is legacy behavior, copied from earlier versions of BASIC!. `ROUND(n)` is NOT the same as `ROUND(n, 0)`.

`ROUND()` generates a runtime error if `<count_nexp> < 0` or `<mode_sexp>` is not valid.

Examples:

```
pi = ROUND(3.14159) 			% pi is 3.0
pi = ROUND(3.14159, 2)			% pi is 3.14
pi = ROUND(3.14159, , "U")		% pi is 4.0
pi = ROUND(3.14159, 4, "F")		% pi is 3.1415
negpi = ROUND(-3.14159, 4, "D")	% negpi is -3.1416
```

Note that `FLOOR(n)` is exactly the same as `ROUND(n, 0, "F")`, but `FLOOR(n)` is a little faster. In the same way, `CEIL(n)` is the same as `ROUND(n, 0, "C")`, and `INT(n)` is the same as `ROUND(n, 0, "D")`.

## `SQR(<nexp>)`

Returns the closest double-precision floating-point approximation of the positive square root of `<nexp>`. If the value of `<nexp>` is negative, the function generates a runtime error.

## `CBRT(<nexp>)`

Returns the closest double-precision floating-point approximation of the cube root of `<nexp>`.

## `LOG(<nexp>)`

Returns the natural logarithm (base e) of `<nexp>`.

## `LOG10(<nexp>)`

Returns the base 10 logarithm of the `<nexp>`.

## `EXP(<nexp>)`

Returns e raised to the `<nexp>` power.

## `POW(<nexp1>, <nexp2>)`

Returns `<nexp1>` raised to the `<nexp2>` power.

## `HYPOT(<nexp_x>, <nexp_y)`

Returns `SQR(x^2+y^2)` without intermediate overflow or underflow.

## `PI()`

Returns the double-precision floating-point value closest to pi.

## `SIN(<nexp>)`

Returns the trigonometric sine of angle `<nexp>`. The units of the angle are radians.

## `COS(<nexp>)`

Returns the trigonometric cosine of angle `<nexp>`. The units of the angle are radians.

## `TAN(<nexp>)`

Returns the trigonometric tangent of angle `<nexp>`. The units of the angle are radians.

## `SINH(<nexp>)`

Returns the trigonometric hyperbolic sine of angle `<nexp>`. The units of the angle are radians.

## `COSH(<nexp>)`

Returns the trigonometric hyperbolic cosine of angle `<nexp>`. The units of the angle are radians.

## `ASIN(<nexp>)`

Returns the arc sine of the angle `<nexp>`, in the range of -pi/2 through pi/2. The units of the angle are radians. If the value of `<nexp>` is less than -1 or greater than 1, the function generates a runtime error.

## `ACOS(<nexp>)`

Returns the arc cosine of the angle `<nexp>`, in the range of 0.0 through pi.The units of the angle are radians. If the value of `<nexp>` is less than -1 or greater than 1, the function generates a runtime error.

## `ATAN(<nexp>)`

Returns the arc tangent of the angle `<nexp>`, in the range of -pi/2 through pi/2. The units of the angle are radians.

## `ATAN2(<nexp_y>, <nexp_x>)`

Returns the angle theta from the conversion of rectangular coordinates (x, y) to polar coordinates (r,theta). (Please note the order of the parameters in this function.)

## `TODEGREES(<nexp>)`

Converts `<nexp>` angle measured in radians to an approximately equivalent angle measured in degrees.

## `TORADIANS(<nexp>)`

Converts <nexp> angle measured in degrees to an approximately equivalent angle measured in radians.

## `VAL(<sexp>)`

Returns the numerical value of the string expression `<sexp>` interpreted as a signed decimal number. If the string is empty ("") or does not represent a number, the function generates a runtime error.

- A sign ("+" or "-"), a decimal point ("." only), and an exponent (power of 10) are optional.
- An exponent is "e" or "E" followed by a number. The number may have a sign but no decimal point.
- The string may have leading and/or trailing spaces, but no spaces between any other characters.

## `IS_NUMBER(<sexp>)`

Tests a string expression `<sexp>` in the same way as `VAL()` and returns a logical value:

- `TRUE` (non-zero) if `VAL()` would successfully convert the string to a number
- `FALSE` (0) if `VAL()` would generate a run-time error.

For example, `VAL("name")` generates a run-time error, but `IS_NUMBER("name")` returns `FALSE`.

If `VAL()` would report a syntax error, `IS_NUMBER()` reports a syntax error.
For example, `IS_NUMBER()`, `IS_NUMBER(num)`, and `IS_NUMBER(5)` are syntax errors.

## `LEN(<sexp>)`

Returns the length of the `<sexp>`.

## `HEX(<sexp>)`

Returns the numerical value of the string expression `<sexp>` interpreted as a hexadecimal integer. The characters of the string can be only hexadecimal digits (0-9, a-h, or A-H), with an optional leading sign ("+" or "-"), or the function generates a runtime error.

## `OCT(<sexp>)`

Returns the numerical value of the string expression `<sexp>` interpreted as an octal integer. The characters of the string can be only octal digits (0-7), with an optional leading sign ("+" or "-"), or the function generates a runtime error.

## `BIN(<sexp>)`

Returns the numerical value of the string expression `<sexp>` interpreted as a binary integer. The characters of the string can be only binary digits (0 or 1), with an optional leading sign ("+" or "-"), or the function generates a runtime error.

## `SHIFT(<value_nexp>, <bits_nexp>)`

Shifts the value `<value_nexp>` by the bit count `<bits_nexp>`. If the bit count is `< 0`, the value will be shifted left. If the bit count is `> 0`, the bits will be shifted right. The right shift will replicate the sign bit. The double-precision floating-point value are truncated to 64-bit integers before the operation.

## `ASCII(<sexp>{, <index_nexp>})`

Returns the ASCII value of one character of `<sexp>`. By default, it is the value of the first character. You can use the optional `<index_nexp>` to select any character. The index of the first character is 1.

A valid ASCII value is between 0 and 255. If `<sexp>` is an empty string ("") the value returned will be 256 (one more than the largest 8-bit ASCII value). For non-ASCII Unicode characters, `ASCII()` returns invalid values; use `UCODE()` instead.

## `UCODE(<sexp>{, <index_nexp>})`

Returns the Unicode value of one character of `<sexp>`. By default, it is the value of the first character. You can use the optional `<index_nexp>` to select any character. The index of the first character is 1.

If `<sexp>` is an empty string ("") the value returned will be 65536 (one more than the largest 16-bit Unicode value). If the selected character of `<sexp>` is a valid ASCII character, this function returns the same value as `ASCII()`.

## `IS_IN(<sub_sexp>, <base_sexp>{, <start_nexp>})`

Returns the position of an occurrence of the substring `<sub_sexp>` in the base string `<base_sexp>`.

If the optional start parameter `<start_nexp>` is not present then the function starts at the first character and searches forward.