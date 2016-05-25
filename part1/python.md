# What is Python?

> ## Learning Objectives

> * Different Python environments
> * Python commands
> * Operators and expressions
> * Python Strings

## Python prompt

To start playing with Python, we need to open up a *command line* on your computer.

Once you're ready, follow the instructions below.

We want to open up a Python console, so type in `python` and hit `enter`.

```python
python
```

```
Python 2.7.9 (default, Mar  1 2015, 12:57:24)
[GCC 4.9.2] on linux2
Type "help", "copyright", "credits" or "license" for more information.
```

## Your first Python command!

After running the Python command, the prompt changed to `>>>`. For us this means that for now we may only use commands in the Python language. You don't have to type in `>>>` - Python will do that for you.

If you want to exit the Python console at any point, just type `exit()` or use the shortcut `Ctrl + Z` for Windows and `Ctrl + D` for Mac/Linux. Then you won't see `>>>` any longer.

For now, we don't want to exit the Python console. We want to learn more about it. Let's start with something really simple. For example, try typing some math, like `2 + 3` and hit `enter`.

```python
2 + 3
```
```
5
```

Nice! See how the answer popped out? Python knows math! You could try other commands like:
- `4 * 5`
- `5 - 1`
- `40 / 2`

Have fun with this for a little while and then get back here :).

As you can see, Python is a great calculator. If you're wondering what else you can do...

## Operators and Expressions {#op-exp}

Most statements (logical lines) that you write will contain _expressions_. A simple example of an expression is `2 + 3`. An expression can be broken down into _operators_ and _operands_.

_Operators_ are functionality that do something and can be represented by symbols such as `+` or by special keywords. Operators require some data to operate on and such data is called _operands_. In this case, `2` and `3` are the operands.


As we just saw, you can evaluate the expressions given in the examples using the interpreter interactively. For example, to test the expression `2 + 3`, use the interactive Python interpreter prompt:

```python
2 + 3
```
```
5
```
```python
3 * 5
```
```
15
```

Here is a quick overview of the available operators:

- `+` (plus)
    - Adds two objects
    - `3 + 5` gives `8`. `'a' + 'b'` gives `'ab'`.

- `-` (minus)
    - Gives the subtraction of one number from the other; if the first operand is absent it is assumed to be zero.
    - `-5.2` gives a negative number and `50 - 24` gives `26`.

- `*` (multiply)
    - Gives the multiplication of the two numbers or returns the string repeated that many times.
    - `2 * 3` gives `6`. `'la' * 3` gives `'lalala'`.

- `**` (power)
    - Returns x to the power of y
    - `3 ** 4` gives `81` (i.e. `3 * 3 * 3 * 3`)

- `/` (divide)
    - Divide x by y
    - `13 / 3` gives `4.333333333333333`

- `//` (divide and floor)
    - Divide x by y and round the answer _down_ to the nearest whole number
    - `13 // 3` gives `4`
    - `-13 // 3` gives `-5`

- `%` (modulo)
    - Returns the remainder of the division
    - `13 % 3` gives `1`. `-25.5 % 2.25` gives `0.75`.

## Evaluation Order

If you had an expression such as `2 + 3 * 4`, is the addition done first or the multiplication? Our high school maths tells us that the multiplication should be done first. This means that the multiplication operator has higher precedence than the addition operator.

## Numbers

We've begun using numbers in python, now it's time to consider the a fundamental dichotomy: numbers are mainly of two types - integers and floats.

An examples of an integer is `2` which is just a whole number.

Examples of floating point numbers (or _floats_ for short) are `3.23` and `52.3E-4`. The `E` notation indicates powers of 10. In this case, `52.3E-4` means `52.3 * 10^-4^`.


## Strings

How about your name? Type your first name in quotes like this:

```python
"Ola"
```
    'Ola'

You've now created your first string! It's a sequence of characters that can be processed by a computer. The string must always begin and end with the same character. This may be single (`'`) or double (`"`) quotes (there is no difference!) The quotes tell Python that what's inside of them is a string.

Strings can be strung together (or concatenated). Try this:

```python
"Hi there " + "Ola"
```
```
'Hi there Ola'
```

You can also multiply strings with a number:

```python
"Ola" * 3
```
```
'OlaOlaOla'
```
If you need to put an apostrophe inside your string, you have two ways to do it.

Using double quotes:

```python
"Runnin' down the hill"
```
```
"Runnin' down the hill"
```

or escaping the apostrophe with a backslash (`\`):

```python
'Runnin\' down the hill'
```
```
"Runnin' down the hill"
```

Nice, huh? To see your name in uppercase letters, simply type:

```python
"Ola".upper()
```
```
'OLA'
```

You just used the `upper` __method__ on your string! A method (like `upper()`) is a sequence of instructions that Python has to perform on a given object (`"Ola"`) once you call it.

> We will often discuss the concept of methods as we use them, because methods are fundamental in python.

If you want to know the number of letters contained in your name, there is a __function__ for that too!

```python
len("Ola")
```
```
3
```
Wonder why sometimes you call functions with a `.` at the end of a string (like `"Ola".upper()`) and sometimes you first call a function and place the string in parentheses? Well, in some cases, functions belong to objects, like `upper()`, which can only be performed on strings. In this case, we call the function a __method__. Other times, functions don't belong to anything specific and can be used on different types of objects, just like `len()`. That's why we're giving `"Ola"` as a parameter to the `len` function.


## Errors

Let's try something new. Can we get the length of a number the same way we could find out the length of our name? Type in `len(304023)` and hit `enter`:

```python
len(304023)
```    
```
Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
TypeError: object of type 'int' has no len()
```
We got our first error! It says that objects of type "int" (integers, whole numbers) have no length. So what can we do now? Maybe we can write our number as a string? Strings have a length, right?

```Python
len(str(304023))
```
6

It worked! We used the `str` function inside of the `len` function. `str()` converts everything to strings.

- The `str` function converts things into __strings__
- The `int` function converts things into __integers__

> Important: we can convert numbers into text, but we can't necessarily convert text into numbers - what would `int('hello')` be anyway?





<!--
## Summary

OK, enough of strings. So far you've learned about:

- __the prompt__ - typing commands (code) into the Python prompt results in answers in Python
- __numbers and strings__ - in Python numbers are used for math and strings for text objects
- __operators__ - like + and \*, combine values to produce a new one
- a little look at __functions__ - like upper() and len(), that perform actions on objects.
- __errors__
- __Jupyter notebooks__

These are the basics of every programming language you learn.

-->
