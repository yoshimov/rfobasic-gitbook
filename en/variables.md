Variables
=========

A BASIC! variable is a container for some numeric or string value.

## Variable Names

Variable names must start with the characters "a" through "z", "#", "@", or "_". The remaining characters in the variable name may also include the digits, "0" through "9".

A variable name may be as long as needed.

Upper case characters can be used in variable names but they will be converted to lower case characters when the program is run. The variable name "gLoP" is the same as the name "glop" to BASIC!

BASIC! command keywords should not be used to start the name of a variable. For example, `Donut = 5` is interpreted as `Do Nut=5`. BASIC! thus expects this `Do` statement to be followed by an Until statement somewhere before the program ends. A list of BASIC! commands can be found in Appendix A.

BASIC! statement labels and the names of user-defined functions, both described later in this manual, follow the same naming rules as BASIC! variables.

## Variable Types

There are two types of variables: Variables that hold numbers and variables that hold strings. Variables that hold strings end with the character "$". Variables that hold numbers do not end in "$".

`Age`, `amount` and `height` are all numeric variable names.

`First_Name$`, `Street$` and `A$` are all string variable names.

If you use a numeric variable without assigning it a value, it has the value 0.0. If you use a string variable without assigning it a value, its value is the empty string, "".

## Scalar and Array Variables

There are two classes of variables: Scalars and Arrays.

## Scalars

A scalar is a variable that can hold only one value. When a scalar is created it is assigned a default value. Numeric scalars are initialized to 0.0. String scalars are initialized to an empty, zero-length string, "".

You create a scalar variable just by using its name. You do not need to predeclare scalars.

## Arrays

An array is variable that can hold many values organized in a systematically arranged way. The simplest array is the linear array. It can be thought of as a list of values. The array `A[index]` is a linear array. It can hold values that can accessed as `A[1], A[2],...,A[n]`. The number (variable or constant) inside the square brackets is called the index.

If you wanted to keep a list of ten animals, you could use an array called Animals$[] that can be accessed with an index of 1 to 10. For example: `Animals$[5] = "Cat"`

Arrays can have more than one index or dimension. An array with two dimensions can be thought of as a list of lists. Let’s assume that we wanted to assign a list of three traits to every animal in the list of animals. Such a list for a "Cat" might be "Purrs", "Has four legs" and "Has Tail". We could set up the Traits array to have two dimensions such that `Traits$[5,2] = "Has four legs"`. If someone asked what are the traits of cat, search Animals$[index] until "Cat" is found at index =5. Index=5 can then be used to access Traits[index,[ {1|2|3}].

BASIC! arrays can have any number of dimensions of any size.

BASIC! arrays are "one-based". This means that the first element of an array has an index of "1". Attempting to access an array with an index of "0" (or less than 0) will generate a run-time error.

Before an array can be used, it must be dimensioned using the `DIM` command. The `DIM` command tells BASIC! how many indices are going to be used and the sizes of the indices. Some BASIC! Commands automatically create a one-dimensional array. Auto-dimensioned array details will be seen in the description of those commands.

Note: It is recommended that the List commands (see below) be used in place of one-dimensional arrays. The List commands provide more versatility than the Array commands.

### Array Segments

Some BASIC! Commands take an array as an input parameter. If the array is specified with nothing in the brackets (for example, "`Animals$[]`"), then the command reads the entire array.

Most of these commands allow you to limit their operation to a segment of the array, using the notation "`Array[start, length]`", where both "start" and "length" are numeric expressions.

For example, you can write "`Animals$[2,3]`". Usually that means "the animal at row 2 and column 3 of a two dimensional array called Animals$". When used to specify an array segment, it has a different meaning: "read only the segment of the `Animals$` array that starts at index 2 and includes 3 items". Notice that this notation applies only to one-dimensional arrays. In fact, it treats all arrays as one-dimensional, regardless of how they are declared.

Both of the expressions in the "[start, length]" pair are optional. If the "start" value is omitted, the default starting index is 1. If the "length" value is omitted, the default is the length from the starting index to the end of the array. If both are omitted, the default is to use the entire array.

### Array Commands

These commands all operate on Arrays. Commands operate on both numeric and string arrays, unless otherwise indicated.

#### `Dim Array[<nexp>{, <nexp> } ... ] {, Array[<nexp>{, <nexp> } ... ] } ...`

The `Dim` command tells BASIC! how many dimensions an array will have and how big those dimensions are. BASIC! creates the array, reserving and initializing memory for the array data. All elements of a numeric array are initialized to the value 0.0. String array elements are initialized to the empty string, "". If you `Dim` an array that already exists, the existing array is destroyed and a new one created.

Multiple arrays can be dimensioned with one `Dim` statement. String and numeric arrays can be dimensioned in a single `Dim` command.

Examples:

```
DIM A[15]
DIM B$[2,6,8], C[3,1,7,3], D[8]
```

#### `UnDim Array[]{, Array[] } ...`

Un-dimensions an array. The array is destroyed, releasing all of the memory it used. Multiple arrays can be destroyed with one `UnDim` statement. Each Array[] is specified without any index. This command is exactly the same as `Array.delete`.

#### `Array.average <Average_nvar>, Array[{<start>,<length>}]`

Finds the average of the values in a numeric array (Array[]) or array segment (Array[start,length]), and places the result into `<Average_nvar>`.

#### `Array.copy SourceArray[{<start>,<length>}], DestinationArray[{{-}<extras>}]`

The previously Dimensioned or Loaded SourceArray[] will be copied to the DestinationArray[]. If the Destination Array does not exist, a new array is created. If the Destination Array already exists, some or all of the existing array will be overwritten. The arrays may be either numeric or string arrays but they must both be of the same type.

You may copy an entire array (SourceArray[]) or an array segment (SourceArray[start,length]).

If `<start>` is `<= 1` or `<start>` is not present then the copy will begin with the first element of the SourceArray. If `<length>` is not present or if `<start>+<length>` exceeds the number of elements in the SourceArray then the entire array or segment from `<start>` to the end of the array will be copied.

If the Destination Array does not exist, the optional `<extras>` parameter specifies that `<extras>` empty elements are to be added to the new Destination Array before or after the copy. These elements will be added to the start of the array if the optional minus(-) sign is present. If minus is not present then these elements will be added to end of the array.

The extra elements for a new numeric array will be initialized to zero. The extra elements for a new string array will be the empty string, "".

If the Destination Array already exists, the optional `<extras>` parameter specifies a starting index into the Destination Array. If the remaining length of the Destination Array starting at the `<extras>` index is less than the number of elements to be copied from the Source Array, anything that would not fit is not copied.

See the Sample Program file, `f26_array_copy.bas`, for working examples of this command.

#### `Array.delete Array[]{, Array[]} ...`

Does the same thing as `UnDim Array[]`.

#### `Array.dims Source[]{, {Dims[]}{, NumDims}}`

Provides information about the dimensions of the Source[] array parameter. The Source[] parameter may be a numeric or string array name with nothing in the brackets ("[]"). The array must already exist. The Source[] parameter is required, and both of the other parameters are optional.

The dimensions of the Source[] array are written to the Dims[] array, if you provide one. The Dims[] parameter must be a numeric array name with nothing in the brackets ("[]"). If the Dims[] array exists, it is overwritten. Otherwise a new array is created. The result is always a one-dimensional array.

The number of dimensions of the Source[] array is written to the NumDims parameter, if you provide one. NumDims must be a numeric variable. This value is the length of the Dims[] array.

#### `Array.fill Array[{<start>,<length>}], <exp>`

Fills an existing array or array segment with a value. The types of the array and value must match.

#### `Array.length <length_nvar>, Array[{<start>,<length>}]`

Places the number of elements in an entire array (Array[] or Array$[]) or an array segment (Array[start,length] or Array$[start,length]) into <Length_nvar>.

#### `Array.load Array[], <exp>, ...`

Creates a new array, evaluates the list of expressions "`<exp>, ...`", and loads values into the new array. Specify the array name with no index(es). The array has one dimension; its size is the same as the number of expressions in the list. If the named array already exists, it is overwritten.

The array may be numeric (Array[]) or string (Array$[]), and the expressions must be the same type as the array.

The list of expressions may be continued onto the next line by ending the line with the "~" character. The "~" character may be used between `<exp>` parameters, where a comma would normally appear. The "~" itself separates the parameters; the comma is optional.

The "~" character may not be used to split a parameter across multiple lines.

Examples:

```
Array.load Numbers[], 2, 4, 8 , n^2, 32
Array.load Hours[], 3, 4,7,0, 99, 3, 66~	% comma not required before ~
37, 66, 43, 83,~				% comma is allowed before ~
83, n*5, q/2 +j
Array.load Letters$[], "a", "b","c",d$,"e"
```

#### `Array.max <Max_nvar> Array[{<start>,<length>}]`

Finds the maximum value in a numeric array (Array[]) or array segment (Array[start,length]), and places the result into the numeric variable `<max_nvar>`.

#### `Array.min <Min_nvar>, Array[{<start>,<length>}]`

Finds the minimum value in a numeric array (Array[]) or array segment (Array[start,length]), and places the result into the numeric variable `<min_nvar>`.

#### `Array.reverse Array[{<start>,<length>}]`

Reverses the order of values in a numeric or string array (Array[] or Array$[]) or array segement (Array[start,length] or Array$[start,length]).

#### `Array.search Array[{<start>,<length>}], <value_exp>, <result_nvar>{,<start_nexp>}`

Searches in the numeric or string array (Array[] or Array$[]) or array segment (Array[start,length] or Array$[start,length]) for the specified numeric or string value, which may be an expression. If the value is found in the array, its position will be returned in the result numeric variable `<result_nvar>`. If the value is not found the result will be zero.

If the optional start expression parameter is present, the search will start at the specified element. The default value is 1.

#### `Array.shuffle Array[{<start>,<length>}]}`

Randomly shuffles the values of the specified array (Array[] or Array$[]) or array segment (Array[start,length] or Array$[start,length]).

#### `Array.sort Array[{<start>,<length>}]}`

Sorts the values of the specified array (Array[] or Array$[]) or array segment (Array[start,length] or Array$[start,length]) in ascending order.

#### `Array.std_dev <sd_nvar>, Array[{<start>,<length>}]}`

Finds the standard deviation of the values in a numeric array (Array[]) or array segment (Array[start,length]), and places the result into the numeric variable `<sd_nvar>`.

#### `Array.sum <sum_nvar>, Array[{<start>,<length>}]`

Finds the sum of the values in a numeric array (Array[]) or array segment (Array[start,length]), and then places the result into the numeric variable `<sum_nvar>`.

#### `Array.variance <v_nvar>, Array[{<start>,<length>}]`

Finds the variance of the values in a numeric array (Array[]) or array segment (Array[start,length]), and places the result into the numeric variable `<v_nvar>`.
