Programming and Algorithms - COMP1005 - University of Nottingham - Undergraduate Year 1
# Basics

There are 4 data types in C

- char
- int
- float
- double.

#Functions
# Functions

```c
return-type function-name { parameter declaration }
{
	variable declarations;

	statements;

	return value;
}
```

Default value to return if not specified is `int`. Functions should always specify what the return value is.

## Parameters

Parameters allow values to be passed between values.

Parameters are automatic variables. A copy of the value passed in is created in memory (passing by value).
- The scope is local to the function that is running, with a lifetime of when that function is executing, so is destroyed when the function returns.

A function cannot change the values of its arguments outside the function. Changing its values will not change the values of the calling function.

> We can use `void` to declare no parameters, in addition to using `void` as a keyword to declare that no return value is expected. `void return_void(void) { printf("void"); }` is valid.


## The Entrypoint `main()`
The main() function is where the program entry point is, and often the exit point too (returns the exit code to the OS). The return type is typically int, with good practice being `return 0;` signifying that there was an error exiting (non-zero return = err).


Main is called with:
- `argc`, an int of number plus one of amount of command line arguments
- `argv`, an array of strings of length `argc` containing the command line arguments.


## printf

A variable length argument function. It outputs to the standard output `stdout`, typically the terminal, but can be redirected to a printer, monitor, etc.. It is part of the C standard input/output library (`stdio`).

Regular characters in the format string are copied directly to the stdout. 

Conversion specifers begin with `%`. It takes in the next argument, convert it, inserts into the string, then printing the string to the stdout.
We can be very specific about how things are formatted, including precision, amount of leading zeroes.


> C lines should be 80 chars long at maximum. We an use the `, \` followed by a new line to continue the command on the next line.

A floating point to 2dp is conversion specifier'd with `%0.2f`. 

Format specifiers:
![[Pasted image 20241013190004.png]]

Escape sequences are special character combinations to insert within a `printf` string argument to perform certain tasks, such as carriage returns, backspaces, and printing out keys like the `\` or `"` that would otherwise interfere with the string handling itself.

## Data types and keywords

https://en.wikipedia.org/wiki/C_data_types

##### Summary:
*Note: bits are specifed at their **minimums**.*

- `char` can be signed or unsigned, and is 8 bits.
- `int` can be just "`short`", short ints, signed, signed short. They are 16 bits.
	- `short` can be replaced by `long` in all cases. Longs are 32 bits.
		- ~~`long` can also be `long long` too~~     *this is not ansi C standard.*
- `float` is a single-precision real floating point (decimal) number. 32 bits.
- `double` is a double-precision floating point, 64 bits.
	- `double` can be a `long` for extra precision and length
 
### Naming conventions

- Variable names must begin with a letter or underscore.
- Must only contain letters, digits and underscores.

#### Constants
- may start with 1 to 9, followed by any decimal number
- may start with 0, followed by any octal number
- 0x followed by any valid hex
- may be followed by an L to denote `long`
- integers may be followed by u or ul
- A *character* constant is **written with single quotes** 'l'
- A *string* constant is **written with double quotes** "hello!"

https://user-web.icecube.wisc.edu/~dglo/c_class/constants.html



# LP 3 notes


Indentation and tabs are not important in C.

The next statement after it is executed, and only the next statement. No curly brackets are needed. However, this is only one statement only. 
To execute multiple statements, we use curly brackets. This is considered as a single statement syntactically by C - they are also known as compound statements. Here, scope rules apply, if not static will be only available within the curly brackets. No semi colon is needed after the closing curly brackets.
We can chain (and nest) if-else statements, until the closing else statement.
The else statement associates with the last else-less if, I.e. the last if without an else. Use curly brackets to form a block to change this.

There are 3 logical (Boolean) operators to create compound conditions. 
- ! logical NOT
- && logica AND
- || logical OR
they evaluate to true/false in e.g. an ifelse conditional statement 

When evaluating expressions, C does not specify the order of evaluation of operands .

# Pointers

Variable names are shorthand for memory address, with its value being the value at that memory address.

C allows us to have direct access to memory through #pointers.
**A pointer is a variable that stores a memory address.**
> **pointer = memory address**

`double *a` -> `a` stores the memory address of where a double value is stored.

To declare pointers, we use an asterisk `*` before the variable name. When declared, the value is undefined for automatic variable types and `NULL` for static variables. (`NULL` is a constant in standard libraries, and its value is an invalid memory address like `0x0000`)

We need to assign memory addresses to the pointer, typically the address of another variable. We do this by using the `&` operator, or "address of".

> Use & to pass the address of the variable.

A pointer is a variable containing an address in memory. Assigning it and changing it with simple assignment (=) will change the address.

> In C, `*` as an Operator is multiply.
> As a unary operator (in front of a variable names) it means a pointer

https://c-for-dummies.com/caio/pointer-cheatsheet.php

> It is good practice to initialise pointers to be `NULL e.g. `int i, \*p = NULL, ...;`

## Arrays

Arrays and pointers are closely linked.

The name of an array is **a constant** and is a **pointer to the first element of the array**. (i.e. `&a[0]`)

Therefore, you cannot directly assign arrays with equals:

```c
  char a[5] = "Bump", b[5];
  
  b = a;  /* This is wrong!! */
```
> Instead, `strcpy` should be used.

However, if `b` was a pointer to array `a` such that `*b` is declared and `b = a;`, then all changes to `b` would also change `a`, such as `b[0] = 'J';` would make `a` equal to `{'J', 'u', 'm', 'p', '\0'}` therefore printed as `%s` as `Jump`.


## Strings
When defining strings, we must use an array of characters. This can be done in two ways;
- use curly brackets for each character, such as `char s[] = {'S', 't', 'r', '\0'};` 
	  We must ensure there is a **null terminator** at the end (the character `\0`)
- use the string inverted commas, such as `char s[] = "Str";` which hides the null terminator (but is there in memory implicitly)

## Pointers Quick Guide
- Pointers are literally just variables that contain memory locations
- You can get/change the value by dereferencing it
- You can get/change the memory location by referring to it normally
- `array[0]` is the same as accessing `*a` (and `array[1]` is `*(a+1)`)


# Dynamic Memory Allocation
Most things dynamically allocated will be placed in the heap, as opposed to the stack.

```c
int *maps = malloc(wordsSize * sizeof(int));
```

`calloc` returns a `void` or null pointer. This means we need to use **type casting** for the data type. To do this, we change the above to:

```c
int *maps = (int *) malloc(wordsSize * sizeof(int));
```

With everything allocated dynamically, there should also be a `free()`. Else, it may cause a memory leak as the OS will never free the memory allocated as it may be being used.
The `free()` system call requires a null pointer, so we need to type casting this too:

```C
free ((void *) word);
```


## Runtime memory
Array size is set at compile time. However, it would be better to set the size of it at runtime. 
## Program memory layout
All memory is identical, but the program sees it as several different sections or segments, used for different purposes.


**Text** is compiled executable code (machine code), often set to be read only. Pointers to it when tried to be modified will be segfault.

Initialised data refers to initialised variables in code

**Uninitialized data (BSS) contains uninitialised statics** (aren't specifically initialized) and set to zero.

The **heap is used for dynamically allocated memory**, going from low address to high address.

The **stack is used to store automatic variables and function return values**, that grows downwards from high to low.
Command line args mat be stored at te top.

> Automatic variables are on the stack and local to the function with a name in the source code. We can get a pointer to them using the `&` operator.  `*p = &a` 

We can also store values on the heap - which is essentially the rest of available program memory. 
We only use a pointer to access heap data with no direct access. (the area cannot have a name but the pointer can.)

The standard library functions to manage the heap are `malloc`, `calloc`, `realloc` and `free`. in stdlib.h.


The memory layout is as follows:

- Stack (grows DOWN)
	- a big gap here
- Heap (grows UP)
> below here is static memory layout, above is dynamic
- Uninitialised data/statics (bss)
- Initialised data (variables)
- Text (machine code)


### malloc
```c
void *malloc(size_bytes size)
```

Allocates or reserves memory on the heap. It allocates `size` bytes of the heap

We can use the `sizeof` operator (to return number of bytes of a specific data type) to calculate the size. We can allocate the number of bytes for a string of 256 characters with `256 * sizeof(char)`.

The return values is a void pointer to the first address of allocated of memory of the heap. THey are uninitialised (random value). To set them we need to se a loop after the malloc.

Example use:
```c
pi = (int *) malloc(4 * sizeof(int));
```

### Type casts
To perform type casting, we put the type name to convert in parenthesis before the variable to convert. 

```python
x = int y
```

```c
x = (int) y;
```

If the value converging to is smaller than the value converting from, it is truncating. E.g. float 256.8 to int would be `256`. Converting to a char would yield `0`.

We can also cast pointers:
```c
void *pv;

pi = (int *) pv;
```
casts from the `void` to an `int`.


Using this with `malloc()` which returns `void` pointers, we can use `pchar = (char *) malloc(256 * sizeof(char));` to assign 256 values of new memory with characters.

### Using allocated memory
We can only access allocated memory via pointers, or with array notation.

### Dynamic allocation safety
The heap is not infinite. Once there is no more space left, it returns `NULL`, so we must always check if the value returned by it is `== NULL` to verify that it was allocated correctly.

The most idiomatic way to check if there was an error is:
```c
if(!(pi = (int *) malloc(256 * sizeof(str)))) { /* error - do something here */ }
```
which allocates and checks for an error all in one line.

When finished using dynamically allocated memory, we use `free()` that releases it back to the OS.

```c
void free (void *ptr)

/* and free’d as */

free((void *) pi); /* or just “free(pi);” sometimes */
```
where the pointer `ptr` is a pointer previously returned by `alloc`.


## calloc

`void *calloc(num_member, mem_size)`

Instead of using `malloc` which requires manual calculation of number of bytes, `calloc` takes the number of members as the 1st argument, and the size of an individual member as the 2nd argument.

`calloc` also initialises all memory addresses to `0`. This is safer for arrays as it avoids integer overflows.

Example use:
```c
pi = (int *) calloc(4, sizeof(int));
```


## realloc
Allows us to enlarge or shrink allocated memory.

`void *realloc(void *ptr, size_t size)`

where `*ptr` is a pointer for the previous call for `malloc`/`calloc` and `size_t` is the size in bytes of new memory. 

Similar to `alloc`, the new memory is not initialised, and the original pointer may move. 

If the pointer moves or memory size shrunk, `free` will be called.


## Garbage collection

**Garbage**: memory occupied by objects no longer in use.
**Memory leak**: memory no longer needed is not released.

This is important as memory is not infinite and there is no automatic garbage collection. 

Therefore, we must keep track of the dynamic memory allocated and release it after we have finished with using it.


We can use valgrind to check for memory leaks, using the `gcc -g` flag for line numbers. The last line will be the most important:

`valgrind --tool=memcheck --leak-check=yes --show-reachable=yes ./executable`


>> K&R 5.4,7.8.5, 8.7
# Compilation
The translation of source code into object (machine) code. It produces an executable program or compiled library. The `gcc` compiler compiles source code in 4 stages:

- preprocessing
- compilation
- assembly
- linking

## Preprocessing
Preprocessing parses and removes all lines beginning with a `#` (these are Preprocessor Directives) and removes comments, in addition to include information about where the code comes from (e.g. the platform it was compiled).

This can be done by using the `-E` flag or by using `cpp` instead of `gcc`:

```sh
gcc -o test-processing -E test.c
cpp -o test-processing.c test.c
```


### Preprocessor Directives

The C preprocessor has its own language. Directves start with a `#` and do not end with a `;`. There are 4:
- `#define`
		This is used for token and macro substitution.
			- We can use `#define SYMBOLIC_CONSTANT "the value"`. (if the value is a string, can just be e.g. 3.142)
			- It has no effect on runtime.
		In addition, macros are similar to functions and have arguments:
			- `#define NAME(arg1, arg2) TEXT`
			- There is no type checking or overhead for function calls as it is a direct copy and paste/substitution for when it appears in the code
			- Common mistakes: `#define times_two(a) 2 * a` will not have the correct output if calling it with `times_two(x + y);`, so should put parentheses around all text (here, the raw `2 * a` becomes `(2 * a)`.)
- `#include`
		Includes the contents of another source file from another source file. `#include <file>` means look in system library locations, whereas `#include "file"` means look in the local directory first. This is useful for including own libraries and code.
- `#if`, `#endif`, `#else`, `#elif`
		Conditionally executes code depending on a condition being met.
		- For example, it is useful for debugging and removing some code from a production binary. We can use `#ifdef DEBUG` and `#endif` with the code between to check if the DEBUG symbol is defined. If it is not defined, the code will not be compiled.
		- We can then provide the symbol with a `#define` OR by using the `-D` flag when compiling; in this case `gcc -DDEBUG` would set it
		- Another example is for cross-compilation, e.g. setting the directory separator to `/` on Linux `#ifdef linux` `#define DIR_SEP '/` vs `\` on Windows.
		- Also useful for preventing double inclusion of header files.
- `#pragma`
		Provides the compiler with additional information, similar to using a flag.
		For each compiler, we use different pragmas, so it is generally avoided.

We can define a macro to only compile certain code by using `#ifdef` in the code, and by using the `-D` flag.

## Compilation
This stage compiles the preprocessed code into assembly language. Uses the `-S` flag.

`gcc -S test.c` -> produces `test.s`

It can also be used to cross compile for a different architecture than the host machine by using using the `-v` flag.

## Assembly
Translates the assembly language into machine (object) code. This can be done with the `-c` flag (`gcc -c test.c`)


## Linking
This organises the object code and adds missing pieces, such as library code. This is done with the `-o` flag. (`gcc -o test.o`)


# Keyboard Input

### getchar

The `getchar` function is defined in the standard library `stdio.h` and is a special case of file input.

`getchar` **returns the ascii code of the key pressed**. To do this, it waits for the EOF and then goes through the **input buffer** to get the characters inputted. 
It may also return an EOF (an int, -1) if it is the end of file or an error occurs. It’s easier to use character literals instead of character ASCII codes. 
### scanf

`scanf` is used for formatted input, using the same format string and conversion specification syntax as `printf`. Each argument after the **format string is a pointer** (memory address), as we need to be able to change the value of the arguments (**pass by reference**).

We can use the carat character `^` to specify which character specifically to stop at.

`scanf("%[^\n]", name);` - read every character and store in `name` until the `\n` key is pressed.

If `scanf` is not successful, it will not return the number of arguments successfully read and converted. e.g. `return_val = scanf("%d", &age);` - we can check `if(ret == 1)` and if it is not, then there was an error. (it may also return EOF) if end of input/file error before reading a value)

We can read multiple values as scanf is designed to support formatted input. However, we need to specify how multiple values are separated ina  good way (e.g. *not* by using a space to separate strings, using something like a `/` to separate e.g. `scanf("%d/%d/%d", &day, &month, &year);).
The function will only take in values it can convert, leaving invalid characters in the input buffer.

#### caveats
Buffer overflows are possible.

```c
char name[16];

scanf("%s", name);
```

Up to 15 characters, this is fine. However `scanf` has no way of checking the length of the array.

The `gets()` function is similar. 

> **Both are unsafe and there are better alternatives** (such as `fgets`)

>> k&r Appendix B1.3-1.4


# Streams and files

I/O is generally performed with streams.

**A stream is a sequence of bytes** (the data being input or output).

A "file" does not have to be a file - it can be keyboard, screen, serial port, network socket, etc. Any input/output device

To perform I/O, we **associate a stream with a file, through `open`ing it.**
Streams provide a common, similar logical interface, for any I/O device.

## Standard streams
`stdin` - keyboard input
`stdout` - screen output
`stderr` - error output

(getchar, printf and scanf are also examples from keyboard input and writing output to the screen.)

C also provides general functions to read/write from other devices with similar names:
- fgetc
- fprintf
- fscanf

FILE is a new variable type - user-defined and defined in `stdio.h`. 

# User-defined data types

There are 4 data types: int, char, double and float.
There are 4 type modifiers: unsigned, signed, long, short.
We can also use `void`.

### typedef keyword
C allows us to use aliases for existing data types using `typedef`.

```c
typedef double Decimal; /* keyword, type, name */

Decimal a;

Decimal add_decimals(Decimal x, Decimal y)
{
	/* Code here */
}
```

`typedef` has a scope of local (type available only inside a statement block), or global (if declared outside all function blocks; is available across the entire program).

As `typedef` just is an alias, we can use the underlying type when referring to it, no need for casting:

```c
typedef double Decimal

Decimal add_decimals(Decimal, Decimal);

double b, c; 

add_decimals(b, c);
/* 
Although b and c are not "Decimal", the code will compile: 
"Decimal" is actually an alias of the "double" data type.
*/
```

It is useful for the portability of libraries, and gives extra clarity with complex data types.

>> k&r 6.7

# Composite data types
(aka compound data types)

We need to record data as a set of related values, e.g. a student may have an ID, a name, firstname, lastname, DOB, etc. It would be good to group data together -- a solution is to use composite data types. In C, this is done with **structures**.

To declare a structure in C, the **struct** keyword is used.

Variables inside struct are called its members. We often capitalise the type name of struct:

```c
struct StudentRecord {
	int id;
	char first_name[256];
	char dob[256];
};
```

To use variables of the struct type, we initialise them (in the same way as an int or str) but using the structure name instead. To assign initial values, we use curly brackets in the variable declaration:

```c
struct StudentRecord record;

struct StudentRecord record2 = {10, "beans", "02/10/2013"};
```

We can also combine the type declaration and variable declaration by adding the variable name directly after the type declaration.

```c
struct StudentRecord {
	int id;
	char first_name[256];
	char dob[256];
} record;
```

This is effectively saying that `record` is a `StudentRecord` with properties `id, first_name, dob` - so we do not need to define it again. More below:

## Combining with typedef

We can also use the `typedef` keyword to avoid using `struct` when declaring variables.

```c
struct StudentRecord {
	int id;
	char first_name[256];
	char dob[256];
} StudentRecord;


/* Here: */

StudentRecord record;
```

This will declare `record` to be of type `StudentRecord`, improving readability and... *struct*ure.

To access the members of a `struct`, we use the member operator `.` (similar to Python classes):
```c
record.id = 349;
strcpy(record.first_name, "mega beans"); /* cannot assign strings directly */
```

## nested structures

We can also nest structures, e.g. here declaring a new `struct Date` that includes three members, all ints: `day`, `month` and `year`.

```c
typedef struct Date {
	int day;
	int month;
	int year;
} Date;

typedef struct StudentRecord {
	...
	Date dob;
} StudentRecord;

StudentRecord record = {..., {02, 10, 2013}}; /* nested curly brackets */

record.dob.day = 7; /* nested member operator */
```

## struct operations

There are only a few operations we can do:
- access members with `.`
- assign or copy struct as a unit with `record2 = record1;`
- get the address of struct with `&`
- pass as a function argument
- have arrays of structs `StudentRecord records[10]`;
> We **cannot** compare, add, or do anything else with them

To access members using pointers, we dereference the variable (getting its actual value not memory address) and using the member operator `.` - or the arrow operator, which means get the value of the member and do something with it:
```c
StudentRecord records[10] *p;

p = records;

/* The following lines to the same thing */
(*p).id = 10;
p->id = 10
```

We can also dynamically allocate memory for structires
```c
records = (StudentRecord *) calloc(10, sizeof(StudentRecord));
```

It is also much more efficient to pass by reference the structure vs the value of it:

```c
void update_record(StudentRecord *a) {
	...
	a->id = 10;
	...
}

StudentRecord record;

update_record(&record);
```


# Libraries
Libraries are a set of rated functions, often grouped together.
useful to reuse in different programs.

Header (interface) file: .h - function declarations.
implementation file (.c) - function definitions.
This is used to separate the implementation from the interface, allowing one to be modified without affecting the things depending on it.

> Don't name functions the same as in standard library functions, or header files the same as other header files.


to compile multi-file programs, we compile each file separately into machine code (using -c) and linking object code together. The program needs to incldue the header file so that the compler can see the functions exist, and the imlementation file to have the declarations of the code.

We cannot run object code directly but an link it together with other object code to make an executable. 

## makefiles and make
To avoid lots of typing in linking object code when compiling, we use makefiles (a special scripting language).

```makefile
target : prerequisite
	recipie
````

e.g.

```makefile
my_string : my_string.h my_string.c
	gcc -Wall -pedantic-errors -ansi -c my_string.c

string_test : string_test.c my_string
	gcc -Wall -pedantic-errors -ansi -o string_test string_test.c my_string.o
```
will do both creating `my_string.o` and then compile this into the `string_test` executable - saving lots of typing.

(`-c` in `my_string` creates the `.o` file for `string_test`)


# data structures
Data strctres have differnet operations with different efficiencies

## Arrays
- same size elements stored sequentially in memory
- can **randomly access** any element as fast as any other
- insertion will be slower as we need to keep the sequential property of arrays.

![[Pasted image 20241124195916.png]]

## Linked list
- Ordered list of elements with each element containing a reference to the next entry and stores the data
- First is the head, last is the tail
- Doubly-linked list has reference to previous as well as next element
- Data can be stored of any size, stored anywhere in memory.
- Access is generally slower than random access
- Insertion is generally faster

```c
typedef struct Node {
	struct Node *next; /* store the address of the next node */
	int data; /* presuming data is an int, store the actual data */
} Node;
```

![[Pasted image 20241124201732.png]]


```c
LinkedList *list;

list = (LinkedList *) malloc(sizeof(LinkedList));

list->head = NULL; /* signify the list is empty */


/* Create a new node */

node = (Node *) malloc(sizeof(Node));`

node->next = NULL; /* The tail node (or orphan node) - else this would access a random address and segfault*/
```

![[Pasted image 20241130112604.png]]

## Generic lists
Instead of replacing all `int`s to `double`s (etc) we *can* just replace all int with double.

OR, a better way is that **we can declare either an `int` or `double` by using a `void` pointer**. These pointers point to a memory location where there is something of an unknown type.

> We cannot declare variables of type `void`, just `void *`.



```c
void *ptr;

int = a;
ptr = &a; /* point to address of a */

/* &a will return the address of a, i.e. a pointer to an int; type int *     */
/* Therefore we should usually cast to change the type to a void *     */

ptr = (void *) &a;
```


### Pointer arithmetic

```c
int *a;

a = a + 1;
```

This will set `a` to the address of `a` plus the number of bytes in the data type int (4). 

We cannot do this with void pointers.

## Void pointers

We **cannot dereference void pointers**; instead, we first need to cast it to the type of the value it points at, then dereference the cast pointer.

```c
int a = a;

void *ptr;

ptr = (void *) &a;

printf("%d\n", *((int *) ptr)); /* Cast first and then dereference - work from the inside out */
```


> The only valid operation with two variables `*p` and `*q` declared as void pointers would be p = q.

We also cannot do pointer arithmetic with void pointers.

```c
int a;

void *ptr;

ptr (void *) &a; /* Gets the address of A, and casts it into a void pointer */

ptr = ptr + 1; /* Compilaton error here. */
```
The reason is that the compiler does not know how many bytes it requires to increment `ptr + 1` (similar to how in assembly we add 4 to numbers and 1 to characters) - void has no length.


We can store any data type in a linked list with such a pointer:

```c
typedef struct Node {
	struct Node *next; /* pointer to address of next node */
	void *data;
} Node;
```

## Pointers to functions

In C, the **name of the function** is actually a **pointer to the address where the function is stored in memory** -- similar to how an array name is a pointer to the first element at index 0.

To do this, you can implement a single function.

For a linked list, we can simplify this by having the first argument being a pointer to the list structure to read from, and the second argument be a user-defined/supplied function that prints/reads and process each of the data types required.

```c
print_list(List *, void (*)(void *))
```

#### Aside
Pointers to functions are useful for programs that have plugins - each plugin has parameters and can be linked dynamically. Accessing a DLL/.o file. 

Define an interface that the program can use - accept parameter X and return parameter Y. 
This is done in the Linux kernel with `grub`.


### Function types

Examples: 

- A function declared as `int sub(int x, int y)` has a **type** of `int (*) (int, int)`.
- A function declared as `*strcpy(char *)` has a type of `char * (*)(char *).



## Stacks and Queues
Very common strutures with linked lists.
There are some operations that are commonly associated with linked lists:
- Push: add an entry to the list
- Pop - remove an entry from thelist
- Peek - look at the top entry of the list

>  In a queue, the property is first in, first out. The first element to be pushed is the next element to be popped. Push to tail, pop and peek from head.

> In a stack, the property is last in, first out. The last element to be pushed is the next element to be popped. We push, pop and peek from the head.




# Algorithms
An algorithm is an unambiguous specification for solving a problem - a set of rules for performing a task.
The instructions describe the computations performed on the input to produce a desired output.

> Fundamental to CS; will look at more theory in later modules.


Pseudocode is independent of programming language but used to unambiguously define the algorithm with I/O data.

There is no formal specification for pseudocode: there is no standard but it may look similar to some programming language - e.g. C-style or python-style pseudocode. However, it **omits details needed by programming languages** for simplicity.

Often contains sentences, natural language descriptions, mathematical notation.

## Sorting

Sorting is a fundamental problem - on numbers, strings etc.

The general problem includes an input of a set of elements, an output of a permutation (reordering) of these elements, and the correctness, being if the sorted output is correct depending on the requirement.

Sorting can be used when solving other (more complex) problems

## Merge sort

![[Pasted image 20241203142430.png]]
### Complexities
In terms of time complexity, merge sort is O(n log n) or loglinear for all worst, average and best cases.
For space complexity, the merge sort as implemented as an array is O(n) and O(log n) as a linked list implementation.

## Insertion sort

![[Pasted image 20241203142405.png]]
### Complexities
In terms of time complexity, insertion srt is O(n^2^) for worst and average and O(n) for best case.
it is, however, constant in terms for space (memory) complexity, O(1).

# Note: make sure to always free when calling his libraries, free the pointer data that pass into e.g. push_queue (as this uses memcpy)

# Parsing 

## Shunting yard

**Infix** notation: operators are written between their operands:, e.g. `2+3`.

> (2*(3+2))/2

**Postfix** notation: operators are written after their operands, e.g. `2 3 +`

> 3 2 + 2 * 2 /

In postfix or reverse Polish notation, the key is that **numbers (operands) are written in the order they are used, and operators are written immediately after their operands.**


### Example: Quadratic formula
$$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$
```

b - b + - ^2 a c * 4 * - a 2 * /

wrong.
```



To convert it from infix to postfix, we use Djikstra's Shunting-yard algorithm. (and then can evaluate it separately).

We pass elements from the inpur infix list into two different output lists: one being the 

Starting from the first element:
- if the element is an operand, we move it to the output list.
- if it is an operator, we peek at the operator stack. If the element at the top of the stack is greater than the input element, then we "perform" the operation of the greater precedence, i.e. popping it from the operator stack and appending it to the output list and repeat. Once we peek at the same or lower precedence, we move the input element to the operator stack.
- Once the input list is empty, we pop the elements from the operator stack and into the output list.

![[Pasted image 20241130155417.png]]


A token may be a number, operator or bracket. We can read numbers as strings and the others as single characters, and write a function to test what a token is (`is_number(char c)`, `is_operator(char c)`)
We can also use `while is_number(c)` to build strings of the number.

#### Operators
We can give operators integer values with greater precedence values having greater integers.
We could then have a function to get an `operator_precendence`, `test_precedence(a, b)` an check associativity for left/right associative.

![[Pasted image 20241130221246.png]]


# Recursion

### Program Memory Layout Recap

High address
- Command-line args
- Stack (automatic variables & function return addresses; grows downwards)
- Heap (dynamically allocated memory; grows upwards)
- Uninitialised data (of statics `exec` initialises this to 0)
- Initialised data (global and static variables)
- Text (compiled executable code)
Low address

# Recursion examples
Recursion involves stack frames with each function call, meaning there is typically higher resource usage to compute, e.g. the factorial function. There is also a risk for segmentation faults if the function does not have an accessible base case, as it will fill the stack entirely.

> Strings have an extra null byte! When allocating memory, get the size of the characters and add 1 for this.

Tip for CW: 
- look at makefile contents, run 1/2 smaller versions of test cases that are one line
- write sanity checks as early as possible 
- use debug printf statements 
Command-line secrets:
- use `gcc ... && taskX [cli]` - compile AND run
- compile code with -g and Valgrind 
- `./fileexec | head` - get first 10 lines


# CW 6 notes
- Use `strlen` function instead of arbitrary data to allocate size of a user-inputted string
- if there is an error, free dynamically alloc’d stuff first *before* returning `Null`.
- implement a bunch of functions and test independently (did this)
- no help lol

# exam
- 1 hour exam
- 25% of grade
- Tests knowledge, comprehension and application of anything covered in lectures or coursework
- In room with desktop PC
- Recommendation for revision: go back over lecture slides and coursework, look at the sample exam
	- Spot mistake in code examples, ask question about code examples in technical language
- straight forward, not designed to catch out, designed to 
- 


