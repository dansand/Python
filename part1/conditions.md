# Conditions

> ## Learning Objectives {.objectives}
>
> *   Explain the similarities and differences between tuples and lists.
> *   Write conditional statements including `if`, `elif`, and `else` branches.
> *   Correctly evaluate expressions containing `and` and `or`.

##Comparing things


> This part is covered in The DjangoGirls [Python Basics: Comparisons](https://www.youtube.com/watch?v=7bzxqIKYgf4) video.

In the first lesson, we saw some mathematical operators. Python is also equipped with comparison operators. All comparison operators return `True` or `False`. Note the capitalization of these names.

A big part of programming includes comparing things. What's the easiest thing to compare? Numbers, of course. Let's see how that works:

```python
print(5 > 2)
print(3 < 1)
print(5 > 2 * 2)
print(1 == 1)
print(5 != 2)
```    
```
True
False
True
True
True
```

We gave Python some numbers to compare. As you can see, Python can compare not only numbers, but it can also compare method results. Nice, huh?

Give Python two more tasks:

```python
print(6 >= 12 / 2)
print(3 <= 2)
```
```    
True
False
```

`>` and `<` are easy, but what do `>=` and `<=` mean? Read them like this:

- x `>` y means: x is greater than y
- x `<` y means: x is less than y
- x `<=` y means: x is less than or equal to y
- x `>=` y means: x is greater than or equal to y



## Control flow

We can ask Python to take different actions, depending on a condition, with an `if` statement:

```python
num = 37
if num > 100:
    print('greater')
else:
    print('not greater')
print('done')
```
```
not greater
done
```

The second line of this code uses the keyword `if` to tell Python that we want to make a choice.
If the test that follows the `if` statement is true,
the body of the `if`
(i.e., the lines indented underneath it) are executed.
If the test is false,
the body of the `else` is executed instead.
Only one or the other is ever executed:

<!--
![Executing a Conditional](fig/python-flowchart-conditional.svg)\
-->


Conditional statements don't have to include an `else`.
If there isn't one,
Python simply does nothing if the test is false:

```python
num = 53
print('before conditional...')
if num > 100:
    print('53 is greater than 100')
print('...after conditional')
```

```
before conditional...
...after conditional
```

We can also chain several tests together using `elif`,
which is short for "else if".
The following Python code uses `elif` to print the sign of a number.

```python
num = -3
```

```python
if num > 0:
    print(num, "is positive")
elif num == 0:
    print(num, "is zero")
else:
    print(num, "is negative")
```

```
"-3 is negative"
```

One important thing to notice in the code above is that we use a double equals sign `==` to test for equality
rather than a single equals sign
because the latter is used to mean assignment.

We can also combine tests using `and` and `or`.
`and` is only true if both parts are true:

```python
if (1 > 0) and (-1 > 0):
    print('both parts are true')
else:
    print('at least one part is false')
```

```python
at least one part is false
```

while `or` is true if at least one part is true:
```python
if (1 < 0) or (-1 < 0):
    print('at least one test is true')
```

```
at least one test is true
```

##While loops
Now we have a little bit of experience using comparison operators to control the flow of our code, we can take a look at another very common form of loop.

The `while` statement allows you to repeatedly execute a block of statements as long as a condition is true. A while statement is an example of what is called a looping statement. A while statement can have an optional else clause.

We begin by looking at one of the simplest dynamic programming algorithms, generating a fibonacci sequence. 


```python
n = int(input("n = "))
f0 = 0
f1 = 1
while n > 1:
    nxt = f0 + f1
    f0 = f1
    f1 = nxt
    n -= 1
print("Fn =", f1)
```

This code inputs an integer n for which it computes and prints the _nth_ Fibonacci number.

>Here is how the algorithm works in a bit more detail:

>* We first initialize (set to their starting values) variables `f0` and `f1` to 0 and 1 respectively.
 
>* Then we run a loop as long as n > 1. In that loop, we

>    * Compute the sum `f0` + `f1` and save it for later in the variable nxt (short of "next", which we don't use because next is a built-in Python function).
    
>    * We assign `f0` = `f1` and `f1` = `nxt`.
>    In other words, the new value of `f0` is equal to the old >value of `f1` and the new value is equal to the sum of old >values of `f0` and `f1`.
    
>    * We reduce `n` by 1.


Note that the `int()` function here converts a string into a an integer. 

<!--

## Checking our Data

Now that we've seen how conditionals work,
we can use them to check for the suspicious features we saw in our inflammation data.
In the first couple of plots, the maximum inflammation per day
seemed to rise like a straight line, one unit per day.
We can check for this inside the `for` loop we wrote with the following conditional:

~~~ {.python}
if data.max(axis=0)[0] == 0 and data.max(axis=0)[20] == 20:
    print('Suspicious looking maxima!')
~~~

We also saw a different problem in the third dataset;
the minima per day were all zero (looks like a healthy person snuck into our study).
We can also check for this with an `elif` condition:

~~~{.python}
elif data.min(axis=0).sum() == 0:
    print('Minima add up to zero!')
~~~

And if neither of these conditions are true, we can use `else` to give the all-clear:

~~~ {.python}
else:
    print('Seems OK!')
~~~

Let's test that out:

~~~ {.python}
data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
if data.max(axis=0)[0] == 0 and data.max(axis=0)[20] == 20:
    print('Suspicious looking maxima!')
elif data.min(axis=0).sum() == 0:
    print('Minima add up to zero!')
else:
    print('Seems OK!')
~~~

~~~ {.output}
Suspicious looking maxima!
~~~

~~~ {.python}
data = numpy.loadtxt(fname='inflammation-03.csv', delimiter=',')
if data.max(axis=0)[0] == 0 and data.max(axis=0)[20] == 20:
    print('Suspicious looking maxima!')
elif data.min(axis=0).sum() == 0:
    print('Minima add up to zero!')
else:
    print('Seems OK!')
~~~

~~~ {.output}
Minima add up to zero!
~~~

In this way,
we have asked Python to do something different depending on the condition of our data.
Here we printed messages in all cases,
but we could also imagine not using the `else` catch-all
so that messages are only printed when something is wrong,
freeing us from having to manually examine every plot for features we've seen before.

-->

> ## _challenge_: How many paths?
>
> Which of the following would be printed if you were to run this code? Why did you pick this answer?
>
> 1.  A
> 2.  B
> 3.  C
> 4.  B and C
>
>```python
> if 4 > 5:
>     print('A')
> elif 4 == 5:
>     print('B')
> elif 4 < 5:
>     print('C')
> ```

> ## _challenge_: What is truth?
>
>
>Incidentally, you just learned about a new type of object in Python. It's called a __Boolean__ -- and it probably is the easiest type there is.
>
>There are only two Boolean objects:`True` and `False`. In python expressions `True` and `False` are special words in which represent true and false statements. 

>However, they aren't the only values in Python that are true and false. After reading and running the following `if` statements, explain what the rule is for which values are considered true and which are considered false.
>
> ```python
> if '':
>     print('empty string is true')
> if 'word':
>     print('word is true')
> if []:
>     print('empty list is true')
> if [1, 2, 3]:
>     print('non-empty list is true')
> if 0:
>     print('zero is true')
> if 1:
>     print('one is true')
> ```

> ## _challenge_: Close enough
>
> Write some conditions that print `True` if the variable `a` is within 10% of the variable `b`
> and `False` otherwise.
> Compare your implementation with your partner's:
> do you get the same answer for all possible pairs of numbers?


> ## _challenge_: In-place operators
>
> Python (and most other languages in the C family) provides [in-place operators](reference.html#in-place-operator)
> that work like this:
>
> ```python
> x = 1  # original value
> x += 1 # add one to x, assigning result back to x
> x *= 3 # multiply x by 3
> print(x)
> ```
> ```python
> 6
> ```
>
> Write some code that sums the positive and negative numbers in a list separately,
> using in-place operators.
> Do you think the result is more or less readable than writing the same without in-place operators?


