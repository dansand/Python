# Functions

> ## Learning Objectives
>
> *   Define a function that takes parameters.
> *   Return a value from a function.
> *   Test and debug a function.
> *   Set default values for function parameters.
> *   Explain why we should divide programs into small, single-purpose functions.

# Functions

We're at the point now where like a way to package our code so that it is easier to reuse, and Python provides for this by letting us define things called 'functions' - a shorthand way of re-executing longer pieces of code. 

The function concept is probably *the* most important building block of any non-trivial software (in any programming language)

Functions are defined using the `def` keyword. After this keyword comes an *identifier* name for the function, followed by a pair of parentheses which may enclose some names of variables, and by the final colon that ends the line. Next follows the block of statements that are part of this function. 
An example will show that this is actually very simple. Here is the Fibonacci algorithm we developed wrapped in a function:

## From a "regular" code to a function¶

```python
def fibonacci(n):
    """
    Takes one argument `n` and returns the `n`-th Fibonacci number.
    """
    f0 = 0
    f1 = 1
    while n > 1:
        nxt = f0 + f1
        f0 = f1
        f1 = nxt
        n -= 1
    return f1
```


The function definition opens with the word `def`, which is followed by the name of the function and a parenthesized list of parameter names. The [body](reference.html#function-body) of the function - the statements that are executed when it runs - is indented below the definition line.

Let's try running our function. Calling our own function is no different from calling any other function:

```python
fibonacci(10)
```
```
10
```


Okay, let's try writing another function `fahr_to_kelvin` that converts temperatures from Fahrenheit to Kelvin:

```python
def fahr_to_kelvin(temp):
    return ((temp - 32) * (5/9.)) + 273.15```


You might have noticed that when we _call_ the function, the values (also called _arguments_ or _paramters_) we pass to it are assigned to those variables so that we can use them inside the function. Inside the function, we use a [return statement](reference.html#return-statement) to send a result back to whoever asked for it.

Let's try running our function.

```python
print('freezing point of water:', fahr_to_kelvin(32))
print('boiling point of water:', fahr_to_kelvin(212))
```

```
freezing point of water: 273.15
boiling point of water: 373.15
```

We've successfully called the function that we defined,
and we have access to the value that we returned.


## Composing Functions

Now that we've seen how to turn Fahrenheit into Kelvin,
it's easy to turn Kelvin into Celsius:

```python
def kelvin_to_celsius(temp_k):
    return temp_k - 273.15

print('absolute zero in Celsius:', kelvin_to_celsius(0.0))
```
```
absolute zero in Celsius: -273.15
```

What about converting Fahrenheit to Celsius? We could write out the formula, but we don't need to.
Instead, we can [compose](reference.html#compose) the two functions we have already created:

```python
def fahr_to_celsius(temp_f):
    temp_k = fahr_to_kelvin(temp_f)
    result = kelvin_to_celsius(temp_k)
    return result

print('freezing point of water in Celsius:', fahr_to_celsius(32.0))
```
```python
freezing point of water in Celsius: 0.0
```

This is our first taste of how larger programs are built:
we define basic operations, then combine them in ever-large chunks to get the effect we want. Real-life functions will usually be larger than the ones shown here --- typically half a dozen to a few dozen lines --- but they shouldn't ever be much longer than that, or the next person who reads it won't be able to understand what's going on.

##Local variables

When you declare variables inside a function definition, they are not related in any way to other variables with the same names used outside the function - i.e. variable names are local to the function. This is called the scope of the variable. All variables have the scope of the block they are declared in starting from the point of definition of the name.

```python
x = 50


def func(x):
    print('x is', x)
    x = 2
    print('Changed local x to', x)


func(x)
print('x is still', x)

```
```
x is 50
Changed local x to 2
x is still 50
```

##Function defaults

For some functions, you may want to make some parameters optional and use default values in case the user does not want to provide values for them. This is done with the help of default argument values. You can specify default argument values for parameters by appending to the parameter name in the function definition the assignment operator (=) followed by the default value.

```python
def say(message, times=1):
    print(message * times)

say('Hello')
say('World', 5)
```
The function named `say` is used to print a string as many times as specified. If we don't supply a value, then by default, the string is printed just once. We achieve this by specifying a default argument value of 1 to the parameter times.

>CAUTION
>Only those parameters which are at the end of the parameter list can be given default argument values i.e. you cannot  have a parameter with a default argument value preceding a parameter without a default argument value in the function's parameter list. 
> This is because the values are assigned to the parameters by position. For example,def `func(a, b=5)` is valid, but def `func(a=5, b)` is not valid.

##Doc strings

Python has a nifty feature called documentation strings, usually referred to by its shorter name docstrings. DocStrings are an important tool that you should make use of since it helps to document the program better and makes it easier to understand. Amazingly, we can even get the docstring back from, say a function, when the program is actually running!

```python
def print_max(x, y):
    """Prints the maximum of two numbers. The two values must be integers."""
    # convert to integers, if possible
    x = int(x)
    y = int(y)

    if x > y:
        print(x, 'is maximum')
    else:
        print(y, 'is maximum')

print_max(3, 5)
print(print_max.__doc__)
```
```
5 is maximum
'Prints the maximum of two numbers. The two values must be integers.'
```
There is also a prettier version:

```python
help(print_max)
```
```
Help on function print_max in module __main__:

print_max(x, y)
    Prints the maximum of two numbers. The two values must be integers.
```

Doctrings are also commonly used to automatically generate a referrence manual for your code, using - for example - Sphinx.
Technically, docstrings are not required by Python and the functions will do just fine without them. However, they are a standard part of any Python code.


> ## _challenge :_ Combining strings
>
> "Adding" two strings produces their concatenation:
> `'a' + 'b'` is `'ab'`.
> Write a function called `fence` that takes two parameters called `original` and `wrapper`
> and returns a new string that has the wrapper character at the beginning and end of the original.
> A call to your function should look like this:
>
> ~~~ {.python}
> print(fence('name', '*'))
> ~~~
> ~~~ {.output}
> *name*
> ~~~

> ## _challenge :_ Selecting characters from strings
>
> If the variable `s` refers to a string,
> then `s[0]` is the string's first character
> and `s[-1]` is its last.
> Write a function called `outer`
> that returns a string made up of just the first and last characters of its input.
> A call to your function should look like this:
>
> ~~~ {.python}
> print(outer('helium'))
> ~~~
> ~~~ {.output}
> hm
> ~~~


> ## _challenge :_ Variables inside and outside functions
>
> What does the following piece of code display when run - and why?
>
> ~~~ {.python}
> f = 0
> k = 0
>
> def f2k(f):
>   k = ((f-32)*(5.0/9.0)) + 273.15
>   return k
>
> f2k(8)
> f2k(41)
> f2k(32)
>
> print(k)
> ~~~