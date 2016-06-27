Numbers
=======

You can type decimal numbers in a BASIC! program:

- A leading sign ("+" or "-"), a decimal point ("." only), and an exponent (power of 10) are optional.
- An exponent is "e" or "E" followed by a number. The number may have a sign but no decimal point.

If you use a decimal point, it MUST follow a digit. 0.15 is a valid number, but .15 is a syntax error.

Numbers in BASIC! are double-precision floating point (64-bit IEEE 754). This means:

- A printed number will always have decimal point. For example, 99 will print as "99.0".You can print numbers without decimal points by using the INT$() or FORMAT$() functions. For example, either INT$(99) or FORMAT$("##", 99) will print "99".
- A number with more than 7 significant digits will be printed in floating point format. For example, the number 12345678 will be printed as 1.2345678E7. INT$() or FORMAT$() can be used to print large numbers in other than floating point format.
- Mathematical operations on decimal values are imprecise. If you are working with currency you should multiply the number by 100 until you need to print it out. When you print it, divide by 100.

A logical value (false = 0, true <> 0) is a kind of number.

You can use string functions to convert numbers to strings. STR$(), INT$(), HEX$() and a few others do simple conversions. FORMAT$() and USING$() can do more complex formatting.

For the purposes of this documentation, numbers that appear in a BASIC! program are called Numeric Constants.
