#Numpy 1

> ## Learning Objectives
>
> *   Load a Python library and use the things it contains.
> *   Read tabular data from a file into a program.
> *   Select individual values and subsections from data.


ftp://ftp.ncdc.noaa.gov/pub/data/paleo/historical/europe-seasonal.txt

In order to load our climate data, we need to [import](reference.html#import) a library called NumPy.
In general you should use this library if you want to do fancy things with numbers, especially if you have matrices or arrays.
We can load NumPy using:

```python
import numpy as np
```

Importing a library is like getting a piece of lab equipment out of a storage locker and setting it up on the bench. Libraries provide additional functionality to the basic Python package, much like a new piece of equipment adds functionality to a lab space. Once you've loaded the library, we can ask the library to read our data file for us:

```python
np.genfromtxt(filepath, skip_header=119)
```
```
array([[  1.50000000e+03,  -9.45000000e-01,   7.15700000e+00,
          1.74830000e+01,   8.99000000e+00,   8.16600000e+00],
       [  1.50100000e+03,  -8.50000000e-01,   7.43500000e+00,
          1.74010000e+01,   8.68700000e+00,   8.16300000e+00],
       [  1.50200000e+03,  -1.05300000e+00,   6.87200000e+00,
          1.79060000e+01,   9.07100000e+00,   8.19400000e+00],
       ..., 
       [  2.00200000e+03,   2.07000000e-01,   9.21400000e+00,
          1.89050000e+01,   9.30100000e+00,   9.50800000e+00],
       [  2.00300000e+03,  -1.10100000e+00,   8.52100000e+00,
          1.96150000e+01,   9.83800000e+00,   9.37400000e+00],
       [  2.00400000e+03,   1.87000000e-01,   8.29700000e+00,
          1.83250000e+01,   1.00730000e+01,   9.23500000e+00]])
```

The expression `numpy.genfromtxt(...)` is a [function call](reference.html#function-call) that asks Python to run the function `loadtxt` that belongs to the `numpy` library.
This [dotted notation](reference.html#dotted-notation) is used everywhere in Python to refer to the parts of things as `thing.component`.

`numpy.loadtxt` has two [parameters](reference.html#parameter):
the name of the file we want to read, and the [delimiter](reference.html#delimiter) that separates values on a line. These both need to be character strings (or [strings](reference.html#string) for short), so we put them in quotes.

By default, only a few rows and columns are shown (with `...` to omit elements when displaying big arrays). To save space, Python displays numbers as `1.` instead of `1.0` when there's nothing interesting after the decimal point.

Our call to `numpy.loadtxt` read our file, but didn't save the data in memory. To do that, we need to [assign](reference.html#assignment) the array to a [variable](reference.html#variable).

Just as we can assign a single value to a integer,or list, or string (native data types) we can also assign an numpy array 
to a variable using the same syntax.  Let's re-run `numpy.loadtxt` and save its result:

```python
filepath = "../../data/europe-seasonal.txt"
data = np.genfromtxt(filepath, skip_header=119)
```

We also put the file path into a variable called`filepath`, which can help make the call to `np.genfromtxt` a bit simpler. Also, notice we supplied a function argument `skiprows=119`. This file has a lot of `metadata`, which you can see if you run a shell command from the Jupyter notebook:

```python
!head -20 $filepath
```
```
European Seasonal Temperature Reconstructions
-----------------------------------------------------------------------
               World Data Center for Paleoclimatology, Boulder
                                  and
                     NOAA Paleoclimatology Program
-----------------------------------------------------------------------
NOTE: PLEASE CITE CONTRIBUTORS WHEN USING THIS DATA!!!!!


NAME OF DATA SET: European Seasonal Temperature Reconstructions
LAST UPDATE: 6/2006 (Original receipt by WDC Paleo)
CONTRIBUTOR: Juerg Luterbacher, University of Bern
IGBP PAGES/WDCA CONTRIBUTION SERIES NUMBER: 2006-060

SUGGESTED DATA CITATION: Luterbacher, J., et al.  2006. 
European Seasonal Temperature Reconstructions.
IGBP PAGES/World Data Center for Paleoclimatology 
Data Contribution Series # 2006-060.
NOAA/NCDC Paleoclimatology Program, Boulder CO, USA.

```
##Accessing our data

Now that our data is in memory,
we can start doing things with it.
First,
let's ask what [type](reference.html#type) of thing `data` refers to:

~~~ {.python}
print(type(data))
~~~
~~~ {.output}
<class 'numpy.ndarray'>
~~~

The output tells us that `data` currently refers to an N-dimensional array created by the NumPy library. These data correspond to historical temperature records from Europe. The rows are the years and the columns are the seasons.

We can see what its [shape](reference.html#shape) is like this:

```python
print(data.shape)
```
```
(505, 6)
```

This tells us that `data` has 505 rows and 6 columns. When we created the variable `data` to store our past climate data, we didn't just create the array, we also created information about the array, called [members](reference.html#member) or attributes. This extra information describes `data` in the same way an adjective describes a noun. `data.shape` is an attribute  of `data` which described the dimensions of `data`. We use the same dotted notation for the attributes of variables that we use for the functions in libraries because they have the same part-and-whole relationship.

If we want to get a single number from the array,
we must provide an [index](reference.html#index) in square bracket, similar to how we have worked with lists:

~~~ {.python}
print('first value in data:', data[0, 0])
~~~
~~~ {.output}
first value in data:', 1500.0
~~~

~~~ {.python}
print('random value in data:', data[250, 2])
~~~
~~~ {.output}
random value in data:', 8.2959999999999994
~~~

The expression `data[250, 2]` may not surprise you. Hopefully, `data[0, 0]` reminds you the indexing scheme we used for lists.
As a result, if we have an M&times;N array in Python, its indices go from 0 to M-1 on the first axis and 0 to N-1 on the second. It takes a bit of getting used to, but one way to remember the rule is that the index is how many steps we have to take from the start to get the item we want.


An index like `data[250, 2]` selects a single element of an array, but we can select whole sections as well. For example, we can select the first ten days (columns) of values for the first four patients (rows) like this:

```python
print(data[0:4, 0:10])
```
```
array([[  1.50000000e+03,  -9.45000000e-01,   7.15700000e+00,
          1.74830000e+01,   8.99000000e+00,   8.16600000e+00],
       [  1.50100000e+03,  -8.50000000e-01,   7.43500000e+00,
          1.74010000e+01,   8.68700000e+00,   8.16300000e+00],
       [  1.50200000e+03,  -1.05300000e+00,   6.87200000e+00,
          1.79060000e+01,   9.07100000e+00,   8.19400000e+00],
       [  1.50300000e+03,  -2.13400000e+00,   7.21000000e+00,
          1.83310000e+01,   8.92200000e+00,   8.07700000e+00]])
```

The [slice](reference.html#slice) `0:4` means, "Start at index 0 and go up to, but not including, index 4." Again, the up-to-but-not-including takes a bit of getting used to, but the rule is that the difference between the upper and lower bounds is the number of values in the slice.

We don't have to start slices at 0:

```python
print(data[5:10, 0:5])
```
```python
[[  1.50500000e+03   4.80000000e-02   7.32300000e+00   1.73410000e+01
    9.28600000e+00]
 [  1.50600000e+03   6.40000000e-02   7.11600000e+00   1.75720000e+01
    8.95800000e+00]
 [  1.50700000e+03   6.12000000e-01   6.22900000e+00   1.75100000e+01
    9.07100000e+00]
 [  1.50800000e+03  -2.09900000e+00   6.81800000e+00   1.73100000e+01
    9.17800000e+00]
 [  1.50900000e+03  -1.44600000e+00   7.32300000e+00   1.78560000e+01
    9.07100000e+00]]
```

We also don't have to include the upper and lower bound on the slice. If we don't include the lower bound, Python uses 0 by default; if we don't include the upper, the slice runs to the end of the axis, and if we don't include either (i.e., if we just use ':' on its own),
the slice includes everything:

```python
small = data[:5, 3:]
print('small is:')
print(small)
```
```
small is:
[[ 17.483   8.99    8.166]
 [ 17.401   8.687   8.163]
 [ 17.906   9.071   8.194]
 [ 18.331   8.922   8.077]
 [ 18.223   9.075   8.163]]
``` 
 
 ## Cleaning our data
 
 At this point we should think a little bit about what our numpy array actually contains. When we used `np.genfromtxt(...)` to load our text file , we supplied the `skiprows=119` argument to exclued the non-tabular metadata which numpy couldn't handle. Now lets look at what those numeric rows and columns represent by using some bash within the notebook:
 
 ```
 !head -120 $filepath | tail -2
 ```
 ```
 Year        DJF         MAM        JJA         SON        Annual
1500      -0.945       7.157      17.483       8.990       8.166
 ```
 And here's the first (120th in the original .txt file) row of our numpy array:
 
 ```python
 print(data[0,:])
 ```
 ```
 [  1.50000000e+03  -9.45000000e-01   7.15700000e+00   1.74830000e+01
   8.99000000e+00   8.16600000e+00]
   ```
   
 What's happened here? Fistly, why all that scienctific notation? When our array contains both large and small values, numpy defaults to printing this way. In this case, there si sufficient variation in the magnitude of our values to have triggered this prinitng option,
 
 If you'd like to learn about overidding this behavior, have a search for examples of setting `np.set_printoptions` on [](http://stackoverflow.com/).


Okay, what about the first column? 

```print
print(data[0:10,0])
```
```
[ 1500.  1501.  1502.  1503.  1504.  1505.  1506.  1507. 1508.  1509.]
```
These values represent years. One thing you may notice is that these values look like floats (floating point numbers). Unlike lists, Numpy arrays can only contain numbers. Even more restrictive, each instance of an array can only have ony type or number...e.g. float, int, complex. To find out which type of data out array contains, we can write
 
```python
data.dtype
```
```
dtype('float64')
```
We cannot change the data type of a sub-array, only the entire array.

```python
data[0,0] = int(1500)
print(data[0,0])
``` 
```
1500.0
```
As this code block shows, numpy will always coerce _numbers_ into the correct (i.e current) data type. Strings and other non-numeric objects, however, will fail:

```python
data[0,0] = "hello"
```
```
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-12-a09d72434238> in <module>()
----> 1 data[0,0] = "hello"
```

## Plotting our data

Matplotlib is an excellent 2D and 3D graphics library for generating scientific figures. One of the key features of matplotlib, that I think makes matplotlib highly suitable for generating figures for scientific publications is that all aspects of the figure can be controlled programmatically.

```python
fig, axes = plt.subplots(figsize=(12,3)) #use the subplots axis layout managers in matplotlib.

axes.plot(data[:,0], data[:,2], 'r', label = 'MAM - Autumn')

axes.set_xlabel('year')
axes.set_ylabel('temperature')
axes.set_title('European Seasonal Temperature Reconstructions')

axes.legend()
```

> ## The matplotlib object-oriented API
> The main idea with object-oriented programming is to have objects that one can apply functions and actions on. The real advantage of this approach becomes apparent when more than one figure is created, or when a figure contains more than one subplot.

> To use the object-oriented API store a reference to the figure instance in the fig variable, and from it we create a new axis instance axes using the add_axes method in the Figure class instance fig:

 
