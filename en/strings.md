Strings
=======

Strings in BASIC! are written as any set of characters enclosed in quote (") characters. The quote characters are not part of the string. For example, `"This is a string"` is a string of 16 characters.

To include the quote character in a string, you must escape it with a backslash: `\"`. For example:

```
Print "His name is \"Jimbo\" Jim Giudice."
```

prints: His name is "Jimbo" Jim Giudice.

Newline characters (a CR/LF, or carriage return/line feed, combination) may be inserted into a string with the escape sequence `\n`:

```
Print "Jim\nGiudice"
```

prints:

```
Jim
Giudice
```

You can use another escape sequence, `\t`, to put a TAB character into a string. To embed a backslash, escape it with another backslash: `\\`. Other special characters can be inserted using the `CHR$()` function.

Strings with numerical characters can be converted to BASIC! numbers using the `VAL(<sexp>)` function.

For the purposes of this documentation, strings that appear within a BASIC! program are called String Constants.
