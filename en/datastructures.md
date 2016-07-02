Data Structures and Pointers in BASIC!
======================================

BASIC! offers commands that facilitate working with Data Structures in ways that are not possible with traditional Basic implementations. These commands provide for the implementation of Lists, Bundles, Stacks and Queues.

## What is a Pointer

The central concept behind the implementation of these commands (and many other BASIC! commands) is the pointer. A pointer is a numeric value that is an index into a list or table of things.

Do not confuse the pointer with the thing it points to. A pointer to a List is not a List; a pointer to a bitmap is not a bitmap. A pointer is just a number that represents something else.

As an example of pointers think of a file cabinet drawer with folders in it. That file cabinet is maintained by your administrative assistant. You never see the file drawer itself. In the course of your work you will create a new folder into which you put some information. You then give the folder to your assistant to be place into the drawer. The assistant puts a unique number on the folder and gives you a slip of paper with that unique number on it. You can later retrieve that folder by asking your assistant to bring you the folder with that particular number on it.

In BASIC! you create an information object (folder). You then give that information object to BASIC! to put into a virtual drawer. BASIC! will give you a unique number—a pointer—for that information object. You then use that pointer to retrieve that particular information object.

Continuing with the folder analogy, let’s assume that you have folders that contain information about customers. This information could be things such as name, address and phone number. The number that your assistant will give you when filing the folder will become the customer’s customer number. You can retrieve this information about any customer by asking the assistant to bring you the folder with the unique customer number. In BASIC! you would use a Bundle to create that customer information object (folder). The pointer that BASIC! returns when you create the customer Bundle becomes the customer number.

Now let’s assume that a customer orders something. You will want to create a Bundle that contains all the order information. Such bundles are used by the order fulfillment department, the billing department and perhaps even the marketing department (to SPAM the customer about similar products). Each Bundle could contain the item ordered, the price, etc. The Bundle will also need to contain information about the customer. Rather than replicate the customer information you will just create a customer number field that contains the customer number (pointer). The pointer that gets returned when you create the order bundle becomes the Order Number. You can create different lists of bundles for use by different departments.

It would also be nice to have a list of all orders made by a customer in the customer Bundle. You would do this by creating a List of all order numbers for that customer. When you create the customer bundle, you would ask BASIC! to create an empty List. BASIC! will return a pointer to this empty List. You would then place this pointer into the customer record. Later when the customer places an order, you will retrieve that list pointer and add the order number to the List.

You may also want to create several other Lists of order Bundles for other purposes. You may, for example, have one List of orders to be filled, another List of filled orders, another List of returned orders, another List for billing, etc. All of these Lists would simply be lists of order numbers. Each order number would point to the order Bundle which would point to the Customer Bundle.

If you were to actually create such a database in BASIC!, you would probably want to save all these Bundles and Lists onto external storage. Getting that information from the internal data structures to external storage is an exercise left to the user for now.

There are things besides List, Bundle, and Stack data structures that are accessed through pointers. These include bitmaps and graphical objects, described below in the `Graphics` section, audio clips, described in `SoundPool`, and other things.

## Lists

A List is similar to a single-dimension array. The difference is in the way a List is built and used. An array must be dimensioned before being used. The number of elements to be placed in the array must be predetermined. A List starts out empty and grows as needed. Elements can be removed, replaced and inserted anywhere within the list.

There is no fixed limit on the size or number of lists. You are limited only by the memory of your device.

Another important difference is that a List is not a variable type. A numeric pointer is returned when a list is created. All further access to the List is by means of that numeric pointer. One implication of this is that it is easy to make a List of Lists. A List of Lists is nothing more than a numeric list containing numeric pointers to other lists.

Lists may be copied into new Arrays. Arrays may be added to Lists.

All of the List commands are demonstrated in the Sample Program file, `f27_list.bas`.

### List Commands

#### `List.create N|S, <pointer_nvar>`

Creates a new, empty list of the type specified by the N or S parameter. A list of strings will be created if the parameter is `S`. A list of numbers will be created if the parameter is `N`. Do not put quotation marks around the N or S.

The pointer to the new list will be returned in the <pointer_nvar> variable.

The newly created list is empty. The size returned for a newly created list is zero.

#### `List.add <pointer_nexp>{, <exp>}...`

Adds the values of the expressions <exp>... to specified list. The expressions must all be the same type (numeric or string) as the list.

The list of <exp>s may be continued onto the next line by ending the line with the "~" character. The "~" character may be used between <exp> parameters, where a comma would normally appear. The "~" itself separates the parameters; the comma is optional.

The "~" character may not be used to split a parameter across multiple lines.

Examples:

```
List.add Nlist, 2, 4, 8 , n^2, 32

List.add Hours, 3, 4,7,0, 99, 3, 66~	% comma not required before ~
37, 66, 43, 83,~				% comma is allowed before ~
83, n*5, q/2 +j

List.add Name~
"Bill", "Jones"~
"James", "Barnes"~
"Jill", "Hanson"
```

#### `List.add.list <destination_list_pointer_nexp>, <source_list_pointer_nexp>`

Appends the elements in the source list to the end of the destination list.

The two lists must be of the same type (string or numeric).

#### `List.add.array <list_pointer_nexp>, Array[{<start>,<length>}]`

Appends the elements of the specified array (Array[]) or array segment (Array[start,length]) to the end of the specified list.

The Array type must be the same as the list type (string or numeric).

#### `List.replace <pointer_nexp>, <index_nexp>, <sexp>|<nexp>`

The List element specified by `<index_nexp>` in the list pointed to by `<pointer_nexp>` is replaced by the value of the string or numeric expression.

The index is one-based. The first element of the list is 1.

The replacement expression type (string or numeric) must match the list type.

#### `List.insert <pointer_nexp>, <index_nexp>, <sexp>|<nexp>`

Inserts the `<sexp>` or `<nexp>` value into the list pointed to by `<pointer_nexp>` at the index point `<index_nexp>`. If the index point is one more than the current size of the list, the new item is added at the end of the list.

The index is ones based. The first element of the list is 1.

The inserted element type must match the list type (string or numeric).

#### `List.remove <pointer_nexp>,<index_nexp>`

Removes the list element specified by `<index_nexp>` from the list pointed to by `<pointer_nexp>`.

The index is ones based. The first element of the list is 1.

#### `List.get <pointer_nexp>, <index_nexp>, <var>`

The list element specified by `<index_nexp>` in the list pointed to by `<pointer_nexp>` is returned in the specified string or numeric variable `<var>`.

The index is one-based. The first element of the list is 1.

The return element variable type must match the list type (string or numeric).

#### `List.type <pointer_nexp>, <svar>`

The type of list pointed to by the list pointer is returned in the string variable `<svar>`.

- Returns the upper case character "S" if the list is a list of strings.
- Returns the upper case character "N" if the list is a list of numbers.

#### `List.size <pointer_nexp>, <nvar>`

The size of the list pointed to by the list pointer is returned in the numeric variable `<nvar>`.

#### `List.clear <pointer_nexp>`

Clears the list pointed to by the list pointer and sets the list’s size to zero.

#### `List.search <pointer_nexp>, value|value$, <result_nvar>{,<start_nexp>}`

Searches the specified list for the specified string or numeric value. The position of the first (left-most) occurrence is returned in the numeric variable `<result_nvar>`. If the value is not found in the list then the result is zero.

If the optional start expression parameter is present, the search starts at the specified element. The default start position is 1.

#### `List.toArray <pointer_nexp>, Array$[] | Array[]`

Copies the list pointed to by the list pointer into an array. The array type (string or numeric) must be the same as the list type. If the array exists, it is overwritten, otherwise a new array is created. The result is always a one-dimensional array.

## Bundles

A Bundle is a group of values collected together into a single object. A bundle object may contain any number of string and numeric values. There is no fixed limit on the size or number of bundles. You are limited only by the memory of your device.

The values are set and accessed by keys. A key is string that identifies the value. For example, a bundle might contain a person’s first name and last name. The keys for accessing those name strings could be "first_name" and "last_name". An age numeric value could also be placed in the Bundle using an "age" key.

A new, empty bundle is created by using the `Bundle.create` command. The command returns a pointer to the empty bundle. Because the bundle is represented by a pointer, bundles can be placed in lists and arrays. Bundles can also be contained in other bundles. This means that the combination of lists and bundles can be used to create arbitrarily complex data structures.

After a bundle is created, keys and values can be added to the bundle using the `Bundle.put` command. Those values can be retrieved using the keys in the `Bundle.get` command. There are other bundle commands to facilitate the use of bundles.

### Bundle Auto-Create

Every bundle command except `Bundle.create` has a parameter, the `<pointer_nexp>`, which can point to a bundle. If the expression value points to a bundle, the existing bundle is used. If it does not, and the expression consists only of a single numeric variable, then a new, empty bundle is created, and the variable value is set to point to the new bundle.

That may seem complex, but it isn't, really. If there is a bundle, use it. If there is not, try to create a new one – but BASIC! can't create a new bundle if you don't give it a variable name. BASIC! uses the variable to tell you how to find the new bundle.

```
BUNDLE.PUT b,"key1", 1.2		% try to put a value in the bundle pointed to by b
BUNDLE.PUT 10, key2$, value2	% try to put a value in the 10th bundle created
BUNDLE.REMOVE c + d, key$[3],	% try to remove a key/value pair from a bundle
                                % pointed to by c + d
```

In the first example, if the value of `b` points to a bundle, the `Bundle.put` puts `"key1"` and the value 1.2 into that bundle. If `b` is a new variable, its value is 0.0, so it does not point to a bundle. In that case, the `Bundle.put` creates a new bundle, puts `"key1"` and the value 1.2 into the new bundle, and sets `b` to point to the new bundle.

In the second example, if there are at least ten bundles, then the `Bundle.put` tries to put the key named in the variable `key2$` and the value of the variable `value2` into bundle 10. If there is no bundle 10, then the command does nothing. It can't create a new variable because you did not provide a variable to return the bundle pointer.

In the third example, the bundle pointer is the value of the expression `c + d`. If there is no such bundle, the command does nothing. To create a new bundle, the bundle pointer expression must be a single numeric variable.

### Bundle Commands

#### `Bundle.create <pointer_nvar>`

A new, empty bundle is created. The bundle pointer is returned in `<pointer_nvar>`.

Example:

```
BUNDLE.CREATE bptr
```

#### `Bundle.put <pointer_nexp>, <key_sexp>, <value_nexp>|<value_sexp>`

The value expression will be placed into the specified bundle using the specified key. If the bundle does not exist, a new one may be created.

The type of the value will be determined by the type of the value expression.

Example:

```
BUNDLE.PUT bptr, "first_name", "Frank"
BUNDLE.PUT bptr,"age", 44
```

#### `Bundle.get <pointer_nexp>, <key_sexp>, <nvar>|<svar>`

Places the value specified by the key string expression into the specified numeric or string variable. The type (string or numeric) of the destination variable must match the type stored with the key. If the bundle does not exist or does not contain the requested key, the command generates a run-time error.

Example:

```
BUNDLE.GET bptr,"first_name", first_name$
BUNDLE.GET bptr,"age", age
```

#### `Bundle.keys <bundle_ptr_nexp>, <list_ptr_nexp>`

Returns a list of the keys currently in the specified bundle.

The bundle pointer parameter `<bundle_ptr_nexp>` specifies the bundle from which to get the keys. If the bundle does not exist, a new one may be created.

The list pointer parameter `<list_ptr_next>` specifies the list into which to write the keys. The previous contents of the list are discarded. If the parameter does not specify a valid string list to reuse, and the parameter is a string variable, a new list is created and a pointer to the list is written to the variable.

The key names in the returned list may be extracted using the various list commands.

Example:

```
BUNDLE.KEYS bptr, list
LIST.SIZE list, size
FOR i = 1 TO size
	LIST.GET list, i, key$
	BUNDLE.TYPE bptr, key$, type$
	IF type$ = "S"
		BUNDLE.GET bptr, key$, value$
		PRINT key$, value$
	ELSE
		BUNDLE.GET bptr, key$, value
		PRINT key$, value
	ENDIF
NEXT i
```

#### `Bundle.contain <pointer_nexp>, <key_sexp> , <contains_nvar>`

If the key specified in the key string expression is contained in the bundle's keys then the "contains" numeric variable will be returned with a non-zero value. The value returned will be zero if the key is not in the bundle. If the bundle does not exist, a new one may be created.

#### `Bundle.type <pointer_nexp>, <key_sexp>, <type_svar>`

Returns the value type (string or numeric) of the specified key in the specified string variable. The `<type_svar>` will contain an uppercase `"N"` if the type is numeric. The <type_svar> will contain an uppercase `"S"` if the type is a string. If the bundle does not exist or does not contain the requested key, the command generates a run-time error.

Example:

```
BUNDLE.TYPE bptr, "age", type$
PRINT type$   % will print N
```

#### `Bundle.remove <pointer_nexp>, <key_sexp>`

Removes the key named by the string expression `<key_sexp>`, along with the associated value, from the bundle pointed to by the numeric expression `<pointer_nexp>`. If the bundle does not contain the key, nothing happens. If the bundle does not exist, a new one may be created.

#### `Bundle.clear <pointer_nexp>`

The bundle pointed to by `<pointer_nexp>` will be cleared of all tags. It will become an empty bundle. If the bundle does not exist, a new one may be created.

## Stacks

Stacks are like a magazine for a gun.

The last bullet into the magazine is the first bullet out of the magazine. This is also what is true about stacks. The last object placed into the stack is the first object out of the stack. This is called LIFO (Last In First Out).

An example of the use of a stack is the BASIC! Gosub command. When a Gosub command is executed the line number to return to is "pushed" onto a stack. When a return is executed the return line number is "popped" off of the stack. This methodology allows Gosubs to be nested to any level. Any return statement will always return to the line after the last Gosub executed.

A running example of Stacks can be found in the Sample Program file, f29_stack.bas.

There is no fixed limit on the size or number of stacks. You are limited only by the memory of your device.

### Stack Commands

#### `Stack.create N|S, <ptr_nvar>`

Creates a new stack of the designated type (N=Number, S=String). The stack pointer is in <ptr_nvar>.

#### `Stack.push <ptr_nexp>, <nexp>|<sexp>`

Pushes the `<nexp>` or `<sexp>` onto the top of the stack designated by `<ptr_nexp>`.

The type of value expression pushed must match the type of the created stack.

#### `Stack.pop <ptr_nexp>, <nvar>|<svar>`

Pops the top-of-the-stack value designated by `<ptr_nexp>` and places it into the `<nvar>` or `<svar>`.

The type of the value variable must match the type of the created stack.

#### `Stack.peek <ptr_nexp>, <nvar>|<svar>`

Returns the top-of-stack value of the stack designated by `<ptr_nexp>` into the `<nvar>` or `<svar>`. The value will remain on the top of the stack.

The type of the value variable must match the type of the created stack.

#### `Stack.type <ptr_nexp>, <svar>`

The type (numeric or string) of the stack designated by `<ptr_nexp>` will be returned in `<svar>`. If the stack is numeric, the upper case character `"N"` will be returned. If the stack is a string stack, the upper case character `"S"` will be returned.

#### `Stack.isEmpty <ptr_nexp>, <nvar>`

If the stack designated by `<ptr_nexp>` is empty the value returned in `<nvar>` will be 1. If the stack is not empty the value will be 0.

#### `Stack.clear <ptr_nexp>`

The stack designated by `<ptr_nexp>` will be cleared.

## Queues

A Queue is like the line that forms at your bank. When you arrive, you get in the back of the line or queue. When a teller becomes available the person at the head of the line or queue is removed from the queue to be serviced by the teller. The whole line moves forward by one person. Eventually, you get to the head of the line and will be serviced by the next available teller. A queue is something like a stack except the processing order is First In First Out (FIFO) rather than LIFO.

Using our customer order processing analogy, you could create a queue of order bundles for the order processing department. New order bundles would be placed at the end of the queue. The top-of-the-queue bundle would be removed by the order processing department when it was ready to service a new order.

There are no special commands in BASIC! for Queue operations. If you want to make a queue, create a list.

Use `List.add` to add new elements to the end of the queue.

Use `List.get` to get the element at the top of the queue and use `List.remove` to remove that top of queue element. You should, of course, use `List.size` before using `List.get` to ensure that there is a queued element remaining
