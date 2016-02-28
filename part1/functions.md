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

Let's try running our function.Calling our own function is no different from calling any other function:

```python
fibonacci(10)
```
```
`10`
```

Let's try writing another function `fahr_to_kelvin` that converts temperatures from Fahrenheit to Kelvin:

```python
def fahr_to_kelvin(temp):
    return ((temp - 32) * (5/9)) + 273.15```


When we _call_ the function, the values we pass to it are assigned to those variables so that we can use them inside the function. Inside the function, we use a [return statement](reference.html#return-statement) to send a result back to whoever asked for it.

Let's try running our function.


~~~ {.python}
print('freezing point of water:', fahr_to_kelvin(32))
print('boiling point of water:', fahr_to_kelvin(212))
~~~
~~~ {.output}
freezing point of water: 273.15
boiling point of water: 373.15
~~~

We've successfully called the function that we defined,
and we have access to the value that we returned.


<!--
> ## Integer division
>
> We are using Python 3, where division always returns a floating point number:
>
> ~~~ {.python}
> $ python3 -c "print(5/9)"
> ~~~
> ~~~ {.output}
> 0.5555555555555556
> ~~~
>
> Unfortunately, this wasn't the case in Python 2:
>
> ~~~ {.python}
> 5/9
> ~~~
> ~~~ {.output}
> 0
> ~~~
>
> If you are using Python 2 and want to keep the fractional part of division
> you need to convert one or the other number to floating point:
>
> ~~~ {.python}
> float(5)/9
> ~~~
> ~~~ {.output}
> 0.555555555556
> ~~~
> ~~~ {.python}
> 5/float(9)
> ~~~
> ~~~ {.output}
> 0.555555555556
> ~~~
> ~~~ {.python}
> 5.0/9
> ~~~
> ~~~ {.output}
> 0.555555555556
> ~~~
> ~~~ {.python}
> 5/9.0
> ~~~
> ~~~ {.output}
> 0.555555555556
> ~~~
>
> And if you want an integer result from division in Python 3,
> use a double-slash:
>
> ~~~ {.python}
> 4//2
> ~~~
> ~~~ {.output}
> 2
> ~~~
> ~~~ {.python}
> 3//2
> ~~~
> ~~~ {.output}
> 1
> ~~~

-->

## Composing Functions

Now that we've seen how to turn Fahrenheit into Kelvin,
it's easy to turn Kelvin into Celsius:

~~~ {.python}
def kelvin_to_celsius(temp_k):
    return temp_k - 273.15

print('absolute zero in Celsius:', kelvin_to_celsius(0.0))
~~~
~~~ {.output}
absolute zero in Celsius: -273.15
~~~

What about converting Fahrenheit to Celsius?
We could write out the formula,
but we don't need to.
Instead,
we can [compose](reference.html#compose) the two functions we have already created:

~~~ {.python}
def fahr_to_celsius(temp_f):
    temp_k = fahr_to_kelvin(temp_f)
    result = kelvin_to_celsius(temp_k)
    return result

print('freezing point of water in Celsius:', fahr_to_celsius(32.0))
~~~
~~~ {.output}
freezing point of water in Celsius: 0.0
~~~

This is our first taste of how larger programs are built:
we define basic operations,
then combine them in ever-large chunks to get the effect we want.
Real-life functions will usually be larger than the ones shown here --- typically half a dozen to a few dozen lines --- but
they shouldn't ever be much longer than that,
or the next person who reads it won't be able to understand what's going on.