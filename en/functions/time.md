Time Functions
==============

## `CLOCK()`

Returns the time in milliseconds since the last boot.

## `TIME()`

Returns the time in milliseconds since 12:00:00 AM, January 1, 1970, UTC (the "epoch"). The time interval is the same everywhere in the world, so the value is not affected by the `TimeZone` command.

## `TIME(<year_exp>, <month_exp>, <day_exp>, <hour_exp>, <minute_exp>, <second_exp>)`

Like `TIME()`, except the parameters specify a moment in time. The specification is not complete, as it does not include the timezone. You may specify a timezone with the `TimeZone` command. If you do not specify a timezone, your local timezone is used.

The parameter expressions may be either numeric expressions or string expressions. This is an unusual aspect as it isn't allowed anywhere else in BASIC!. If a parameter is a string, then it must evaluate to a number: digits only, one optional decimal point somewhere, optional leading sign, no embedded spaces. If the string parameter does not follow the rules, BASIC! reports a syntax error, like using a string in a place that expects a numeric expression.

`TIME(…)` (the function) and `Time` (the command) are inverse operations. `TIME(…)` can take the first six return parameters of the `Time` command directly as input parameters.

With the `USING$()` or `FORMAT_USING$()` functions, you can express a moment in time as a string in many different ways, formatted for your locale.
