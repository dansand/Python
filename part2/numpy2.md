# numpy2

> ## Learning Objectives
> *   Create useful numpy arrays 
> *   Perform operations on arrays of data.

## Creating arrays

We have see an example of creating an array from an existing data file using `np.genfromtxt()`. We start with this approach because as researchers, and often want to dive straigt into our data.There are a number of more formulaic ways to initialise new numpy arrays, for example:

* from a Python list or tuples
* using functions that are dedicated to generating numpy arrays, such as `arange`, `linspace`, etc.

To create a new 1D  array (sometimes called a vector) from Python lists we can use the np.array function.

```python 
v = array([1,2,3,4])
print(v)
```
```
[1 2 3 4]
```

A 2D array (sometimes called a matrix) can be created from a nested list:

```python 
M = array([[1, 2], [3, 4]])
print(M)
```
```
[[1 2]
 [3 4]]
```

Like all variables in Python, we should be interested in their type:

```python
print(type(v), type(M))
```
```
<class 'numpy.ndarray'> <class 'numpy.ndarray'>
```

And as numpt arrays, we should be concerned about their size and shape:

```python
print(v.shape, M.shape)
```
```
(4,) (2, 2)
```
```python
print(v.size, M.size)
```
```
4 4
```

So far the numpy.ndarray looks pretty much like a Python list (or nested list). Why not simply use Python lists for computations instead of creating a new array type? Basically, it all boils down to speed. As we will see later in this lesson, numpy arrays are good at maths, and more to the point, they are fast.


For larger arrays it is inpractical to initialize the data manually, using explicit python lists. Instead we can use one of the many _array-generating functions_ in numpy that generate arrays of different forms. 



```python
# create a vector with np.arange
x = np.arange(0, 10, 1) # arguments: start, stop, step
print(x)
```
```
[0 1 2 3 4 5 6 7 8 9]
```

```python
# create a vector with linspace, both end points ARE included
linspace(0, 10, 25) # arguments: start, end, number
```

Let's plot some point generated using `np.linspace`

```python
x = np.linspace(0, 3, 20)
y = np.linspace(0, 9, 20)
plt.plot(x, y)       # line plot
plt.plot(x, y, 'o')  # dot plot
plt.show() 
```


```python
x, y = np.mgrid[0:3, 0:3] # similar to meshgrid in MATLAB
print(x), print(y)
```
```
[[0 0 0]
 [1 1 1]
 [2 2 2]]
[[0 1 2]
 [0 1 2]
 [0 1 2]]
```

```python
#Return a new array of given shape and type, 
#filled with zeros.
z = np.zeros((3,3))
```
```
[[ 0.  0.  0.]
 [ 0.  0.  0.]
 [ 0.  0.  0.]]
```

```python
# Create an array of the given shape /
# and fill with random samples 
# from a uniform distribution over [0, 1).
rd = np.random.rand(3,2)
```

## Maths with arrays

Arrays also know how to perform common mathematical operations on their values. The simplest operations with data are arithmetic:
add, subtract, multiply, and divide. When you do such operations on arrays, the operation is done on each individual element of the array.

Thus:

~~~ {.python}
doubledata = data * 2.0
~~~

will create a new array `doubledata` whose elements have the value of two times the value of the corresponding elements in `data`:

~~~ {.python}
print('original:')
print(data[:3, 36:])
print('doubledata:')
print(doubledata[:3, 36:])
~~~
~~~ {.output}
original:
[[ 2.  3.  0.  0.]
 [ 1.  1.  0.  1.]
 [ 2.  2.  1.  1.]]
doubledata:
[[ 4.  6.  0.  0.]
 [ 2.  2.  0.  2.]
 [ 4.  4.  2.  2.]]
~~~

If,
instead of taking an array and doing arithmetic with a single value (as above)
you did the arithmetic operation with another array of the same shape,
the operation will be done on corresponding elements of the two arrays.
Thus:

~~~ {.python}
tripledata = doubledata + data
~~~

will give you an array where `tripledata[0,0]` will equal `doubledata[0,0]` plus `data[0,0]`,
and so on for all other elements of the arrays.

~~~ {.python}
print('tripledata:')
print(tripledata[:3, 36:])
~~~
~~~ {.output}
tripledata:
[[ 6.  9.  0.  0.]
 [ 3.  3.  0.  3.]
 [ 6.  6.  3.  3.]]
~~~

Often, we want to do more than add, subtract, multiply, and divide values of data.
Arrays also know how to do more complex operations on their values.
If we want to find the average inflammation for all patients on all days,
for example,
we can just ask the array for its mean value

~~~ {.python}
print(data.mean())
~~~
~~~ {.output}
6.14875
~~~

`mean` is a [method](reference.html#method) of the array,
i.e.,
a function that belongs to it
in the same way that the member `shape` does.
If variables are nouns, methods are verbs:
they are what the thing in question knows how to do.
We need empty parentheses for `data.mean()`,
even when we're not passing in any parameters,
to tell Python to go and do something for us. `data.shape` doesn't
need `()` because it is just a description but `data.mean()` requires the `()`
because it is an action.

NumPy arrays have lots of useful methods:

~~~ {.python}
print('maximum inflammation:', data.max())
print('minimum inflammation:', data.min())
print('standard deviation:', data.std())
~~~
~~~ {.output}
maximum inflammation: 20.0
minimum inflammation: 0.0
standard deviation: 4.61383319712
~~~

When analyzing data,
though,
we often want to look at partial statistics,
such as the maximum value per patient
or the average value per day.
One way to do this is to create a new temporary array of the data we want,
then ask it to do the calculation:

~~~ {.python}
patient_0 = data[0, :] # 0 on the first axis, everything on the second
print('maximum inflammation for patient 0:', patient_0.max())
~~~
~~~ {.output}
maximum inflammation for patient 0: 18.0
~~~

We don't actually need to store the row in a variable of its own.
Instead, we can combine the selection and the method call:

~~~ {.python}
print('maximum inflammation for patient 2:', data[2, :].max())
~~~
~~~ {.output}
maximum inflammation for patient 2: 19.0
~~~

What if we need the maximum inflammation for *all* patients (as in the
next diagram on the left), or the average for each day (as in the
diagram on the right)? As the diagram below shows, we want to perform the
operation across an axis:

<!--
![Operations Across Axes](fig/python-operations-across-axes.svg)
-->

To support this,
most array methods allow us to specify the axis we want to work on.
If we ask for the average across axis 0 (rows in our 2D example),
we get:

~~~ {.python}
print(data.mean(axis=0))
~~~
~~~ {.output}
[  0.           0.45         1.11666667   1.75         2.43333333   3.15
   3.8          3.88333333   5.23333333   5.51666667   5.95         5.9
   8.35         7.73333333   8.36666667   9.5          9.58333333
  10.63333333  11.56666667  12.35        13.25        11.96666667
  11.03333333  10.16666667  10.           8.66666667   9.15         7.25
   7.33333333   6.58333333   6.06666667   5.95         5.11666667   3.6
   3.3          3.56666667   2.48333333   1.5          1.13333333
   0.56666667]
~~~

As a quick check,
we can ask this array what its shape is:

~~~ {.python}
print(data.mean(axis=0).shape)
~~~
~~~ {.output}
(40,)
~~~

The expression `(40,)` tells us we have an N&times;1 vector,
so this is the average inflammation per day for all patients.
If we average across axis 1 (columns in our 2D example), we get:

~~~ {.python}
print(data.mean(axis=1))
~~~
~~~ {.output}
[ 5.45   5.425  6.1    5.9    5.55   6.225  5.975  6.65   6.625  6.525
  6.775  5.8    6.225  5.75   5.225  6.3    6.55   5.7    5.85   6.55
  5.775  5.825  6.175  6.1    5.8    6.425  6.05   6.025  6.175  6.55
  6.175  6.35   6.725  6.125  7.075  5.725  5.925  6.15   6.075  5.75
  5.975  5.725  6.3    5.9    6.75   5.925  7.225  6.15   5.95   6.275  5.7
  6.1    6.825  5.975  6.725  5.7    6.25   6.4    7.05   5.9  ]
~~~

which is the average inflammation per patient across all days.

The mathematician Richard Hamming once said,
"The purpose of computing is insight, not numbers,"
and the best way to develop insight is often to visualize data.
Visualization deserves an entire lecture (or course) of its own,
but we can explore a few features of Python's `matplotlib` library here.





>  ##_challenge:_  Interpret
> Explain the output of the following
> ```python
> Z = np.random.uniform(0,1,10)
> z = 0.5
> m = Z.flat[np.abs(Z - z).argmin()]
> print(m)
> ```

> ## _challenge:_ Checkerboard
>Create an 8x8 matrix and fill it with a checkerboard pattern

> ## _challenge:_ Normalise 
Normalise a 5x5 random matrix 


