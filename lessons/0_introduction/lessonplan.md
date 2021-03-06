# A small Introduction to C Programming

As students to this workshop might not be programmers, this short lesson would
serve as a primer to understanding how x86 assembly works. Here, we will go through
the basics of C programming, and data types. This should serve as a short primer for
the upcoming lesson.


## Data Types

Before we talk about C programs, we need to mention the specific data types that are
present in computing languages. In a computer, data exists as bits (Binary digITS) 
of 1s and 0s. These are grouped into chunks of 4 bits called a `nibble`, or into chunks
of 8 bits called a `byte`. This should be a familiar measure of size for the
non-technical person.

During this workshop, you will see various data types being used. We will go through
two of the most basic data types that will be used.

- - - -

### `int`

An `int` is the most basic numerical unit. It represents an **int**eger that has 32
bits. The value of the integer is given by the binary value of the bits that it is
made up of. E.g. 00001010 = value 10


### Side note on binary counting

Suppose we are counting in our decimal world, and we are at 90. We will go

90... 91... 92... 93... 94... 95... 96... 97... 98... 99...

What comes next though? We have ran out of symbols after going through all of
`0123456789`. Hence we add one to the previous digit (in this case, the tens digit),
and reset the symbol we are counting on back to the symbol `0`.

That makes sense, but now in the tens digit, we are adding one to the symbol `9`!
Once again, we are out of symbols! So once again, we therefore have to add one to the
previous digit (in this case, the hundreds digit), and reset the symbol we are
counting back to the symbol `0`.

But wait! There is no "hundreds digit" present! In this case, we simply add one to
nothing to end up with the symbol `1` in the hundred digits place.

Therefore we end up with the final number... `100`. Give yourself a pat on the back,
because counting in binary is the same idea. In binary, we only have the symbols `0`
and `1`. So how would we count in binary?

0... 1... 

We cannot add one to the symbol `1`, so we reset it, and add one to the tens digit.

0... 1... 10... 11...

We cannot add one to the symbol `1`, so we reset it, and add one to the tens digit.
BUT we cannot add one to the tens digits too, so we reset it, and add one to the
hundreds digit to get:

0... 1... 10... 11... 100... 101... 110... 111... 1000... 1001... 1010...

- - - -

Remember how in the world we count number by adding 10 to each successive digit?

For example: 6789 = **6** \* 1000 + **7** \* 100 + **8** \* 10 + **9** \* 1

Why did we choose the numbers 1000, 100, 10 and 1? It is because those are the
powers of 10. Why 10? Because that's the number of symbols we have!

Therefore, suppose we have only two symbols, then what is the value of `0b1011`. 
Well, using the same idea as above, we get the following:

**1** \* 8 + **0** \* 4 + **1** \* 2 + **1** \* 1 = 11 (in decimal).

Commonly to represent that a certain number is in binary, we will add the prefix
`0b` to the start of the number. Hence the following equation holds:

`0b1011 = 11`

Now what if we want to go in the reverse direction? Given a decimal number, we want
to get the binary.

Note that we can ask ourselves what is the biggest power of 2 that will subtract
from the given decimal number without it going negative. We write the symbol `1` in
the location of that power of 2, and subtract it away. We can keep doing this, and
once we are done, we can fill in the gaps with the symbol `0`. Lets try:

Given the number `42`, what is the binary representation?

Note that the biggest power of 2 that will subtract from `42` is `32` (which is
2 multiplied to itself 5 times). We can go to the place represented by 2^5 and write
the symbol `1` there:

|2^5|2^4|2^3|2^2|2^1|2^0|
|---|---|---|---|---|---|
| 1 | ? | ? | ? | ? | ? |

Now we need to figure out what is the biggest power of 2 that will subtract from
`42-32 = 10`. With a bit of testing we realise it is `8`, which is represented by 2^3.
We go over to the 2^3 section and write the symbol `1` there.

|2^5|2^4|2^3|2^2|2^1|2^0|
|---|---|---|---|---|---|
| 1 | ? | 1 | ? | ? | ? |

Lastly, we are left with `2`, which is just 2^1. So we can write the symbol `1` in
that location as well. Since what we are left with is `0`, we can simply fill in the
?s with `0`s as well:

|2^5|2^4|2^3|2^2|2^1|2^0|
|---|---|---|---|---|---|
| 1 | 0 | 1 | 0 | 1 | 0 |

And hence we conclude that `42 = 0b101010`.

- - - -

There is also one more number system that you will be encountering. It is called
the hexadecimal system. Hexa stands for 6 (as in hexagon), and decimal for 10. 
Why the hexadecimal system is important: How many different nibbles are there?
There are 4 bits in a nibble, and each can be either `0` or `1`. Hence there are
a total of 2 \* 2 \* 2 \* 2 = 16 different nibbles! Perhaps we can represent 
each nibble with a different symbol, from the hexadecimal system.

The hexadecimal system has 16 symbols: `0123456789ABCDEF`. Note that we cannot
have a symbol `10` in hexadecimal, because it is made of two symbols! Hence once
we have finished using the 10 numerical symbols, we need to start using letters.
In this case, the symbol `A` represents the value 10, `B` represents the value
11 and so on. The prefix for the hexadecimal system is `0x`.

Suppose we have the value `0xAF`. What is the value in decimal?

Well, we know that the symbol `A` has a value of 10, and the symbol `F` has a
value of 15. So in total, the value of `0xAF` is simply:

**10** \* 16 + **15** \* 1 = 175.

- - - -

### `char`

A `char` is an ASCII **char**acter. Remember that strings of text are really just
a bunch of characters put together. Note however, that there is a special character
to demarcate the end of the string -- the `NULL` byte. It is a character whose bits
are all 0s.

In C, each `char` character has a value that corresponds to an 8 bit integer.
Since we have just learn the hexadecimal system, we can also use 2 hexadecimal
symbols to represent a character.

The English capital letters come from the range `0x41` to `0x5A`, and the small
letters come from the range `0x61` to `0x7A`. The numerical symbols come from the
range `0x30` to `0x39`. In fact, let me just link a picture from the website
[https://www.asciitable.com/](https://www.asciitable.com/) that probably took it
from lookuptables.com:

![ascii Table][ascii]

- - - -

### `boolean` and others

However, in C, there is no such thing as a definite `true`/`false` value (these values
are called `boolean` values btw). In C, only the number 0 returns `false`, every
other number would return `true`. Keep this in mind as we go through the reversing
C programs segment later.

Note that there are other types such as `long`, `float`, `double`, etc. These will
not be covered in this workshop. Arrays and the like would also not be covered in
this session. The assembly instructions regarding these other data types are also
more involved. Perhaps these would be covered in future workshops (Sprout 2019?).


## Structure of a C program

In a C program, there would be functions, statements and expressions.

### Statements and Expressions

Here are some examples of statements and expressions: 

```
int x = 5;  // Statement
x + 5; // Expression

// An if-else statement
if (x == 5){ 
    printf ("The value of x is 5.\n"); // Expression
}
else{
    printf ("The value of x is not 5.\n");
}
```

Statements are code that do not return a value. An example of a statement would be
an if-else statement. These are _conditional_ statements that allow for the computer
to make decision based on fulfilled or unfulfilled conditions.

Another example would be a variable declaration statement. These statements can be
identified beginning with a type and followed by a string of characters that
represent the name of the variable. This can be thought of in the same was as
algebra. From that point on, you would be able to use the variable with its name.


Expressions are lines of code that return a specific value. For example, `4 + 2`
is an expression, because it returns the value `6`. Note that things which return
the value of `void` is also considered an expression. As a rule of thumb, as long as
there is a return value, it would be considered an expression.

Consider these lines of code:

```
int x = 5;
x = x + 1;
```

What is `x`'s final value? You can think of it in terms of algebra, working from the
right side to the left. In the first line, you said the value of `x` is 5. Then in the
next line, you are saying that the variable `x` gets the value of `x + 1`, which in
this case is equal to `5 + 1 = 6`. Hence after this piece of code runs, `x` has the
value of 6.

- - - -

### Functions

Functions are chunks of code that have been grouped together. The reasons
for doing so are many: First it could be because the program needs to call the same
piece of code multiple times, hence it makes sense to put every thing away. It could
also be used for code grouping.

Functions are identified by a function declaration. This tells the compiler about a
function's name, return type, and parameters. A function definition provides the 
code the program is supposed to run when the function is called. For example:

```
void example1(int x, char y){...}
```

In this case, the function is called `example1`, and takes in two arguments. The first
of the arguements should be and `int` and the second should be a `char`. After this
function runs, it would return no value, and hence we denote that as `void`.

Calling a function is simple: you take the function's name, and append parenthesis
(`()`) to it. Within the parenthesis, you will input any parameters that the
function takes, in the correct type. Suppose we want to call the function as above.
Then an example proper call to that function would be `example1(1, 'a');`.

- - - -

Let's look at another example:

```
int add(int x, int y){
    return x + y;
}

int a = 3;
int b = 6;
int z = add(a, b);
```

In the above example, the name of the function is add, and the return type is `int`.
It takes in two `int`s, and within the function, the names of the passed in values
are called x and y. Once the function has finished running, we can expect it to
return an `int` value.

When the function is called, the values of 3 and 6 are assigned to the variables
a and b respectively. The function `add` is then called with the value in a and b,
i.e. we will have `add(3, 6)`. 
In the function `x` and `y` will therefore values `3` and `6` respectively. Then the
function would then return x + y = 3 + 6 = 9. This is then assigned to the value z.

The most important function in a C program would be the main function. It tells
the computer that the lines of code within it starts the program. The program would
run until the end of the main function, after which the program would end.

### Comments

One last thing that you would see me use often in codes which I provide is comments.
In C, comments are lines which begin with two slashes (`//`). In x86 assembly, they
would begin with a semicolon (`;`). For those lines with those comments, you will
ignore everything that comes after the comment markers.

```
// This is a comment
int x = 5; // A comment to say that x has a value of 5
```

## Operations

Now, several different operations are allowed in C code. However, we will focus on
the few most basic operations we can do in C programming language.

### Addition and Subtraction

Simply take two numbers and add or subtract them. That is easy.
Note that as we mentioned above, `char`s are really just integers, we are able to
actually add and subtract them!

Consider the following piece of code, what value would the variable `x` have?

```
int x = 'a' - 'A';
```

Remember the value of `'a'` is `0x61`, and the value of `'A'` is `0x41`. So what is
the value of `0x61 - 0x41`? Just like normal math, we get the answer of `0x20`,
which, converted into decimal, gives us 32.


### Bitwise AND (&) OR (|) and XOR (^)

These are the three most common bitwise operations you will face. The reason why
they are called _bitwise_ operations is because they operate on a bit by bit basis.
They are functions which take in two pieces of data, and for each bit between the
data points, will do its operation and output a bit. Lets explore:

### Bitwise AND (&) 

As the name suggests, when given two bits, the bitwise AND operator will return
`1` if and only if the two input bits are both `1`s. In all other cases, the output
bit will be a `0`. We can draw a logic table that expresses the inputs and the
outputs as such:

|`AND`| 0 | 1 |
|-----|---|---|
|  0  | 0 | 0 |
|  1  | 0 | 1 |


### Bitwise OR (|)

Similarly, the bitwise OR operator will return a `1` if and only if either one of
the two inputs is a `1`. It will only be a `0` if both the input bits are `0`s. The
logic table is given below.

|`OR`| 0 | 1 |
|----|---|---|
|  0 | 0 | 1 |
|  1 | 1 | 1 |

### Bitwise XOR (^)

This is called the eXclusive OR operator. Although the symbol used for the XOR
operator is the carat, do not mistake it for exponentiation! In computer science
there is no symbol for exponentiation (except in a couple of languages. Python for
example uses `x**y` to mean `x` to the power of `y`).

Now the XOR operator will return a `1` if only one of the inputs is a `1`. If both
of the inputs are `0`s or if both the inputs are `1`s, the XOR operator would return
a `0`. We can draw the truth table as such

|`XOR`| 0 | 1 |
|-----|---|---|
|  0  | 0 | 1 |
|  1  | 1 | 0 |

Now, you might realise that the XOR operator is really just a combination of the OR
and the AND operator, and you are right! It is, however, one of the most important
bitwise operations in computing.

- - - -

Now, lets see the bitwise operations in practice. Suppose I have the following piece
of code. Without running the program, what would the values of OR, AND, and XOR be:

```
int x = 22;
int y = 10;
int OR = x | y;
int AND = x & y;
int XOR = x ^ y;
```

We can try to analyse this. First we need to figure out the binary values of x and y:

```
x = 0b10110
y = 0b01010
```

Then look at each bit. We can calulate the final values of each bit 

```
 x = 0b10110
 y = 0b01010
OR = 0b11110 (30)

  x = 0b10110
  y = 0b01010
AND = 0b00010 (2)

  x = 0b10110
  y = 0b01010
XOR = 0b11100 (28)
```

### Bitshifting Operators (>> and <<)

The last operator that you will be facing are the bitshifting operators. These
essentially tell the program to scoot the bits of the given number by a couple of
places.

Suppose you do the code `x << 5`. That tells the compiler to move each bit in
x a total of 5 places to the left. What happens to the 5 new places on the right?
They get filled with 0s.

```
int x = 6;  // 0b110
x << 5;     // 0b11000000 = 192
            //      ^^^^^ 5 new 0s appear on the right of the number.
```

In the same way a right bitshift scoots the number towards the right by that number
of places. But wait, what if there are 1s in the bits on the right of the number?
Well, they disappear! You don't really care about them!

```
             //      vvvv These 4 bitss disappear!
int x = 99;  // 0b1100011
x >> 4;      // 0b110
```

The last point to take note of is that `int`s are only 32 bits in length. If you do
a left shift on an `int` and the bits gets scooted out of range, your compiler might
not be kind enough to tell you! The program will silently fail!

```
int x = 31;
int y = 6 << x; // 6 << 31
```

In this example, the 2 `1`s in y has been pushed outside of the 32 bit range that an
`int` can hold. Hence the value of `y` is therefore 0.

[ascii]: ./asciifull.gif
