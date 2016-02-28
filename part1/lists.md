
# Lists

> ## Learning Objectives
>
> *   Explain what a list is.
> *   Create and index lists of simple values.
> *   List slicing


A list is a way to store many values.
Lists are built into the language (so we don't have to load a library to use them).

We create a list by putting values inside square brackets:

```python
odds = [1, 3, 5, 7]
print('odds are:', odds)
```
```
odds are: [1, 3, 5, 7]
```

We select individual elements from lists by indexing them:

```python
print('first and last:', odds[0], odds[-1])
```
```
first and last: 1 7
```

Programming languages like Fortran and MATLAB start counting at 1, because that's what human beings have done for thousands of years.Languages in the C family (including C++, Java, Perl, and Python) count from 0 because that's simpler for computers to do.


There is one important difference between lists and strings:
we can change the values in a list,
but we cannot change the characters in a string.
For example:

```python
names = ['Newton', 'Darwing', 'Turing'] # typo in Darwin's name
print('names is originally:', names)
names[1] = 'Darwin' # correct the name
print('final value of names:', names)
```
```
names is originally: ['Newton', 'Darwing', 'Turing']
final value of names: ['Newton', 'Darwin', 'Turing']
```

works, but:

```python
name = 'Bell'
name[0] = 'b'
```
```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-8-220df48aeb2e> in <module>()
      1 name = 'Bell'
----> 2 name[0] = 'b'

TypeError: 'str' object does not support item assignment
```

does not.

> ## Ch-Ch-Ch-Changes
>
> Data which can be modified in place is called [mutable](reference.html#mutable),
> while data which cannot be modified is called [immutable](reference.html#immutable).
> Strings and numbers are immutable. This does not mean that variables with string or number values are constants,
> but when we want to change the value of a string or number variable, we can only replace the old value
> with a completely new value.
>
> Lists and arrays, on the other hand, are mutable: we can modify them after they have been created. We can
> change individual elements, append new elements, or reorder the whole list.  For some operations, like
> sorting, we can choose whether to use a function that modifies the data in place or a function that returns a
> modified copy and leaves the original unchanged.


> ## Nested Lists
> Since lists can contain any Python variable, it can even contain other lists.
>
> For example, we could represent the products in the shelves of a small grocery shop:
>
> ~~~ {.python}
> x = [['pepper', 'zucchini', 'onion'],
>      ['cabbage', 'lettuce', 'garlic'],
>      ['apple', 'pear', 'banana']]
> ~~~
>
>
> Here is a visual example of how indexing a list of lists `x` works:
>
> <a href='https://twitter.com/hadleywickham/status/643381054758363136'>
> ![The first element of a list. Adapted from @hadleywickham's tweet about R > lists.](img/indexing_lists_python.png)</a>
>
> Using the previously declared list `x`, these would be the results of the
> index operations shown in the image:
>
> ~~~ {.python}
> print([x[0]])
> ~~~
>
> ~~~ {.output}
> [['pepper', 'lettuce', 'onion']]
> ~~~
>
> ~~~ {.python}
> print(x[0])
> ~~~
>
> ~~~ {.output}
> ['pepper', 'lettuce', 'onion']
> ~~~
>
> ~~~ {.python}
> print(x[0][0])
> ~~~
>
> ~~~ {.output}
> 'pepper'
> ~~~
>
> Thanks to [Hadley Wickham](https://twitter.com/hadleywickham/status/643381054758363136)
> for the image above.

There are many ways to change the contents of lists besides assigning new values to
individual elements:

~~~ {.python}
odds.append(11)
print('odds after adding a value:', odds)
~~~
~~~ {.output}
odds after adding a value: [1, 3, 5, 7, 11]
~~~

~~~ {.python}
del odds[0]
print('odds after removing the first element:', odds)
~~~
~~~ {.output}
odds after removing the first element: [3, 5, 7, 11]
~~~

~~~ {.python}
odds.reverse()
print('odds after reversing:', odds)
~~~
~~~ {.output}
odds after reversing: [11, 7, 5, 3]
~~~

While modifying in place, it is useful to remember that Python treats lists in a slightly counterintuitive way.

If we make a list and (attempt to) copy it then modify in place, we can cause all sorts of trouble:

~~~ {.python}
odds = [1, 3, 5, 7]
primes = odds
primes += [2]
print('primes:', primes)
print('odds:', odds)
~~~
~~~ {.output}
primes: [1, 3, 5, 7, 2]
odds: [1, 3, 5, 7, 2]
~~~

This is because Python stores a list in memory, and then can use multiple names to refer to the same list.
If all we want to do is copy a (simple) list, we can use the `list` function, so we do not modify a list we did not mean to:

~~~ {.python}
odds = [1, 3, 5, 7]
primes = list(odds)
primes += [2]
print('primes:', primes)
print('odds:', odds)
~~~
~~~ {.output}
primes: [1, 3, 5, 7, 2]
odds: [1, 3, 5, 7]
~~~

This is different from how variables worked in lesson 1, and more similar to how a spreadsheet works.

##Slicing

lists, (like a variety of pythn data structures), also have a slicing operation which allows us to retrieve a slice of the sequence i.e. a part of the sequence.

> ## _challenge:_ Turn a string into a list
>
> Use a for-loop to convert the string "hello" into a list of letters:
>
> ~~~ {.python}
> ["h", "e", "l", "l", "o"]
> ~~~
> Hint: You can create an empty list like this:
>
> ~~~ {.python}
> my_list = []
> ~~~

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



