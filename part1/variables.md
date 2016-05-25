
# Variables

> ## Learning Objectives

> *   Assign values to variables
> *   Changing variables


An important concept in programming is variables. A variable is nothing more than a name for something so you can use it later. Programmers use these variables to store data, make their code more readable and so they don't have to keep remembering what things are.

Let's say we want to create a new variable called `name`:

```python
name = "Ola"
```

You see? It's easy! It's simply: name equals Ola.

As you've noticed, your program didn't return anything like it did before. So how do we know that the variable actually exists? Simply enter `name` and hit `enter`:

```python
name
```
```
'Ola'
```

Yippee! Your first variable :)! You can always change what it refers to:

```python
name = "Sonja"
```
```python
name
```
```
'Sonja'
```

You can use it in functions too:

```python
len(name)
```
```
5
```

But what if we used the wrong name? Can you guess what would happen? Let's try!

```python
city = "Tokyo"
```
```python
ctiy
```
```
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    NameError: name 'ctiy' is not defined
```
An error! As you can see, Python has different types of errors and this one is called a **NameError**. Python will give you this error if you try to use a variable that hasn't been defined yet. If you encounter this error later, check your code to see if you've mistyped any names.


So a Python variable is just a name for a value. Python's variables must begin with a letter and are [case sensitive](reference.html#case-sensitive).
We create a new variable by assigning a value to it using `=`. Note that `=` means assignment in Python.
Let's consider the simplest "collection" of data, a single value. The line below assigns the value `55` to a variable `weight_kg`:


```python
weight_kg = 55
```

Just like with the string assigned to `name`, our numeric (integer) variable can be printed to the screen:

```python
print(weight_kg)
```
```
55
```

We can also do arithmetic with it:

```python
print('weight in pounds:', 2.2 * weight_kg)
```
```python
weight in pounds: 121.0
```

We can also change a variable's value by assigning it a new one:

```python
weight_kg = 57.5
```
```python
print('weight in kilograms is now:', weight_kg)
```
```
weight in kilograms is now: 57.5
```

As the example above shows,
we can print several things at once by separating them with commas.

If we imagine the variable as a sticky note with a name written on it,
assignment is like putting the sticky note on a particular value:

![Variables as Sticky Notes](../fig/python-sticky-note-variables-01.svg)

This means that assigning a value to one variable does *not* change the values of other variables.
For example,
let's store the subject's weight in pounds in a variable:

```python
weight_lb = 2.2 * weight_kg
```
```python
print('weight in kilograms:', weight_kg, 'and in pounds:', weight_lb)
```
```
weight in kilograms: 57.5 and in pounds: 126.5
```

![Creating Another Variable](../fig/python-sticky-note-variables-02.svg)

and then change `weight_kg`:

```python
weight_kg = 100.0
print('weight in kilograms is now:', weight_kg, 'and weight in pounds is still:', weight_lb)
```
```
weight in kilograms is now: 100.0 and weight in pounds is still: 126.5
```

![Updating a Variable](../fig/python-sticky-note-variables-03.svg)

Since `weight_lb` doesn't "remember" where its value came from,
it isn't automatically updated when `weight_kg` changes.
This is different from the way spreadsheets work.


## The print function

Try this:

```python
name = 'Maria'
name
```
```
'Maria'
```

```python
print(name)
```
```
Maria
```

When you just type `name`, the Python interpreter responds with the string *representation* of the variable 'name', which is the letters M-a-r-i-a, surrounded by single quotes, ''. When you say `print(name)`, Python will "print" the contents of the variable to the screen, without the quotes, which is neater.

As we'll see later, `print()` is also useful when we want to print things from inside functions, or when we want to print things on multiple lines.

> ## Who's who in the memory
>
>You can use the `whos` command at any time to see what variables you have created and what modules you have loaded into the computers memory. As this is an IPython command, it will only work if you are in an IPython terminal or the Jupyter Notebook.
>
>~~~ {.python}
>whos
>~~~
>~~~ {.output}
>Variable    Type       Data/Info
>--------------------------------
>weight_kg   float      100.0
>weight_lb   float      126.5
>~~~


> ## _challenge:_  Exchanges
>
> Explain what the overall effect of this code is:
>
> ~~~ {.python}
> left = 'L'
> right = 'R'
>
> temp = left
> left = right
> right = temp
> ~~~
>
> Compare it to:
>
> ~~~ {.python}
> left, right = right, left
> ~~~
>
> Do they always do the same thing?
> Which do you find easier to read?
