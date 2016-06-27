Command Description Syntax
==========================

## Upper and Lower Case

Commands are described using both upper and lower case for ease of reading. BASIC! converts every character (except those between double quotation marks) to lower case when the program is run.

## `<nexp>`, `<sexp>` and `<lexp>`

These notations denote a numeric expression (`<nexp>`), a string expression (`<sexp>`), and a logical expression (`<lexp>`). An expression can be a variable, a number, a quoted string or a full expression such as (a*x^2 + bx + c).

## `<nvar>`, `<svar>` and `<lvar>`

This notation is used when a variable, not an expression, must be used in the command. Arrays with indices (such as n[1,2] or s$[3,4]) are considered to be the same as `<nvar>`, `<svar>` and `<lvar>`.

## `Array[]` and `Array$[]`

This notation implies that an array name without indices must be used.

## `Array[{<start>,<length>}]` and `Array$[{<start>,<length>}]`

In most contexts, numeric expressions inside the brackets are indices specifying a single array element. In some commands, a pair of numeric expressions specifies a segment of the array. Both the start index and length are numeric expressions, and both are optional. This notation is shorthand for:

```
Array [ { {<start_nexp>} {, <length_nexp>} } ]
Array$ [ { {<start_nexp>} {, <length_nexp>} } ]
```

## {something}

Indicates something optional.

## { A | B |C }

This notation suggests that a choice of either A, B, or C, must be made. For example:

```
Text.open {r|w|a}, fn…
```

Indicate that either "r" or "w" or "a" must be chosen:

```
Text.open r, fn…
Text.open w, fn…
Text.open a, fn…
```

## X, ...

Indicates a variable-sized list of items separated by commas. At least one item is required.

## {,n} ...

Indicates an optional list with zero or more items separated by commas.

## `<statement>`

Indicate an executable BASIC! statement. A `<statement>` is usually a line of code but may occur within other commands such as: `IF <lexp> THEN <statement>`.

## Optional Parameters

Many statements have optional parameters. If an optional parameter is omitted, the statement assumes a default value or performs a default action.

If an optional parameter is omitted, use a comma to mark its place, so following parameters are handled correctly. However, if there are no following parameters, omit the comma, too. With a few special exceptions (like `Print`), no statement can end with a comma.
