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

So far the `numpy.ndarray` looks pretty much like a Python list (or nested list). Why not simply use Python lists for computations instead of creating a new array type? Basically, it all boils down to speed. As we will see later in this lesson, numpy arrays are good at maths, and more to the point, they are fast.


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
random = np.random.rand(3,2)
print(random
```
```
[[ 0.95642119  0.82504981]
 [ 0.01412624  0.00413452]
 [ 0.37054704  0.55093531]]
```
(For example)

In order to have a more visually appealing array to work with,  let's read in an image from the Scipy sample data:

```python
from scipy import misc
face = misc.face()
```

```python       
plt.imshow(f)
```



docker pull lmoresi/uom-vieps-intro2-python:2016.i

## Maths with arrays


```python
ess_file = '../../data/essendon_airport_temps.csv'
array = np.genfromtxt(ess_file, delimiter=',')
data = array[:,2:-2]
years = array[:,0]
years.astype(int)
```

Arrays also know how to perform common mathematical operations on their values. The simplest operations with data are arithmetic:
add, subtract, multiply, and divide. When you do such operations on arrays, the operation is done on each individual element of the array.

```python
doubledata = data * 2.0
```

will create a new array `doubledata` whose elements have the value of two times the value of the corresponding elements in `data`:

```python
print('original:')
print(data)
print('doubledata:')
print(doubledata[0:5,]) 
```
```
original:
[[  nan   nan   nan   nan   nan   nan   nan   nan   nan   nan   nan]
 [  nan   nan   nan   nan   nan   nan   nan   nan   nan   nan   nan]
 [  nan   nan   nan  19.3  16.7  13.3  12.   13.2  15.9  18.4  20.7]
 [ 26.   25.2  29.2  19.7  16.   14.   13.8  16.   18.2  23.2  20.8]
 [ 23.2  25.7  22.   21.4  16.7  13.6  13.1  14.6  16.4  17.5  22.3]]
doubledata:
[[  nan   nan   nan   nan   nan   nan   nan   nan   nan   nan   nan]
 [  nan   nan   nan   nan   nan   nan   nan   nan   nan   nan   nan]
 [  nan   nan   nan  38.6  33.4  26.6  24.   26.4  31.8  36.8  41.4]
 [ 52.   50.4  58.4  39.4  32.   28.   27.6  32.   36.4  46.4  41.6]
 [ 46.4  51.4  44.   42.8  33.4  27.2  26.2  29.2  32.8  35.   44.6]]
```

If, instead of taking an array and doing arithmetic with a single value (as above) you did the arithmetic operation with another array of the same shape, the operation will be done on 
corresponding elements of the two arrays.

Thus:

```python
tripledata = doubledata + data
```

will give you an array where `tripledata[0,0]` will equal `doubledata[0,0]` plus `data[0,0]`,
and so on for all other elements of the arrays.

Often, we want to do more than add, subtract, multiply, and divide values of data. Arrays also know how to do more complex operations on their values. If we want to find the average value of all elements in an array, for example, we can just ask the array for its mean value

```python
print(data.mean())
```
```
nan
```
Numpy finds that the mean of ut array, whicch contains 'NaNs' ot missing values, is NaN. Not a great result.

Luckily, there are a range of Numpy library functions to deal with NaNs (i.e. ignore them in producing summary statistices)

```python
numpy.nanmean(data)
```
```
19.230588235294118
```

For an array without NaNs, we have the easier option:

```python
random.mean()
```

`mean` is a [method](reference.html#method) of the array,
i.e., a function that belongs to it in the same way that the member `shape` does. If variables are nouns, methods are verbs: they are what the thing in question knows how to do. We need empty parentheses for `data.mean()`, even when we're not passing in any parameters, to tell Python to go and do something for us. `data.shape` doesn't need `()` because it is just a description but `data.mean()` requires the `()` because it is an action.

Numpy arrays have lots of useful methods:

~~~ {.python}
print('maximum monthly avg. temperature:', numpy.nanmax(data))
print('minimum monthly avg.temperature:', numpy.nanmin(data))
print('mean monthly avg. temp:', numpy.nanmean(data))
~~~
```python
maximum monthly avg. temperature: 29.7
minimum monthly avg.temperature: 11.2
mean monthly avg. temp: 19.6661666667
```

When analyzing data, though, we often want to look at partial statistics, such as the maximum value per patient or the average value per day.One way to do this is to create a new temporary array of the data we want, then ask it to do the calculation:

To simplify things (avoid messy data with NaNs) lets create some dummy data.

```python
data = np.random.rand(10,10)
```



```python
row0 = data[0, :] # 0 on the first axis, everything on the second
print('maximum for row 0:', row0.max())
```

We don't actually need to store the row in a variable of its own.
Instead, we can combine the selection and the method call:

```python
print('maximum value for row 2:', data[2, :].max())
```

What if we need the maximum inflammation for *all* rows (as in the next diagram on the left), or the average for each day (as in the diagram on the right)? As the diagram below shows, we want to perform the operation across an axis:


![Operations Across Axes](fig/python-operations-across-axes.png)



To support this, most array methods allow us to specify the axis we want to work on. If we ask for the average across axis 0 (rows in our 2D example),
we get:

```python
print(data.mean(axis=0))
```


As a quick check, we can ask this array what its shape is:

```python
print(data.mean(axis=0).shape)
```

The expression `(10,)` tells us we have an N&times;1 vector, so this is the average __row__ for all patients.
If we average across axis 1 (columns in our 2D example), we get:

```python
print(data.mean(axis=1))
```


which is the average across all __columns__.

The mathematician Richard Hamming once said,"The purpose of computing is insight, not numbers," and the best way to develop insight is often to visualize data. Visualization deserves an entire lecture (or course) of its own, but we can explore a few features of Python's `matplotlib` library here.

##Looping through arrays

There are a number of ways of looping through `np.arrays`.

```python
#for x in np.nditer(data):
#    print(x)
```

```python

for index, x in np.ndenumerate(data):
    print(index, x)
```



> ##_challenge:_  dreaded greyscale
>
> Now we know we know a little about doing maths with arrays, we can define a function a to convert a colour (RGB) image to grayscale.
> 
> The equivalent Matlab function uses the following formula:
>$$gray = 0.2989 \times red + 0.5870 \times green+ 0.1140 \times blue$$
> 
> 
>Write a python function that will compute the grayscale representation of our `face` array.

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


