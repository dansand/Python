#Numpy


> ## Learning Objectives
>
> *   Load a Python library and use the things it contains.
> *   Read tabular data from a file into a program.
> *   Select individual values and subsections from data.
> *   Perform operations on arrays of data.


ftp://ftp.ncdc.noaa.gov/pub/data/paleo/historical/europe-seasonal.txt



In order to load our climate data,
we need to [import](reference.html#import) a library called NumPy.
In general you should use this library if you want to do fancy things with numbers,
especially if you have matrices or arrays.
We can load NumPy using:

```python
import numpy as np
```

Importing a library is like getting a piece of lab equipment out of a storage locker and setting it up on the bench. Libraries provide additional functionality to the basic Python package, much like a new piece of equipment adds functionality to a lab space. Once you've loaded the library,
we can ask the library to read our data file for us:

```python
np.loadtxt("../../data/europe-seasonal.txt", converters=None, skiprows=119)
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

The expression `numpy.loadtxt(...)` is a [function call](reference.html#function-call)
that asks Python to run the function `loadtxt` that belongs to the `numpy` library.
This [dotted notation](reference.html#dotted-notation) is used everywhere in Python
to refer to the parts of things as `thing.component`.

`numpy.loadtxt` has two [parameters](reference.html#parameter):
the name of the file we want to read, and the [delimiter](reference.html#delimiter) that separates values on a line. These both need to be character strings (or [strings](reference.html#string) for short), so we put them in quotes.

By default, only a few rows and columns are shown (with `...` to omit elements when displaying big arrays). To save space, Python displays numbers as `1.` instead of `1.0` when there's nothing interesting after the decimal point.

Our call to `numpy.loadtxt` read our file, but didn't save the data in memory. To do that, we need to [assign](reference.html#assignment) the array to a [variable](reference.html#variable).

Just as we can assign a single value to a integer,or list, or string (native data types) we can also assign an numpy array 
to a variable using the same syntax.  Let's re-run `numpy.loadtxt` and save its result:

```python
filepath = "../../data/europe-seasonal.txt"
data = np.loadtxt(filepath, converters=None, skiprows=119))
```

We also put the file path into a variable called`filepath`, which can help make the call to `np.loadtxt` a bit simpler. Also, notice we supplied a function argument `skiprows=119`. This file has a lot of `metadata`, which you can see if you run a shell command from the Jupyter notebook:

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
##Accessing out data

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

~~~ {.python}
small = data[:5, 3:]
print('small is:')
print(small)
~~~
~~~ {.output}
small is:
[[ 17.483   8.99    8.166]
 [ 17.401   8.687   8.163]
 [ 17.906   9.071   8.194]
 [ 18.331   8.922   8.077]
 [ 18.223   9.075   8.163]]
 
 ## Cleaning our data
 
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
While there is no "official" plotting library,
this package is the de facto standard.
First,
we will import the `pyplot` module from `matplotlib`
and use two of its functions to create and display a heat map of our data:

~~~ {.python}
import matplotlib.pyplot
image  = matplotlib.pyplot.imshow(data)
matplotlib.pyplot.show()
~~~

![Heatmap of the Data](fig/01-numpy_71_0.png)

Blue regions in this heat map are low values, while red shows high values.
As we can see,
inflammation rises and falls over a 40-day period.

> ## Some IPython magic {.callout}
>
> If you're using an IPython / Jupyter notebook,
> you'll need to execute the following command
> in order for your matplotlib images to appear
> in the notebook when `show()` is called:
>
> ~~~ {.python}
> % matplotlib inline
> ~~~
>
> The `%` indicates an IPython magic function -
> a function that is only valid within the notebook environment.
> Note that you only have to execute this function once per notebook.

Let's take a look at the average inflammation over time:

~~~ {.python}
ave_inflammation = data.mean(axis=0)
ave_plot = matplotlib.pyplot.plot(ave_inflammation)
matplotlib.pyplot.show()
~~~

![Average Inflammation Over Time](fig/01-numpy_73_0.png)

Here,
we have put the average per day across all patients in the variable `ave_inflammation`,
then asked `matplotlib.pyplot` to create and display a line graph of those values.
The result is roughly a linear rise and fall,
which is suspicious:
based on other studies,
we expect a sharper rise and slower fall.
Let's have a look at two other statistics:

~~~ {.python}
max_plot = matplotlib.pyplot.plot(data.max(axis=0))
matplotlib.pyplot.show()
~~~

![Maximum Value Along The First Axis](fig/01-numpy_75_1.png)

~~~ {.python}
min_plot = matplotlib.pyplot.plot(data.min(axis=0))
matplotlib.pyplot.show()
~~~

![Minimum Value Along The First Axis](fig/01-numpy_75_3.png)

The maximum value rises and falls perfectly smoothly,
while the minimum seems to be a step function.
Neither result seems particularly likely,
so either there's a mistake in our calculations
or something is wrong with our data.

You can group similar plots in a single figure using subplots.
This script below uses a number of new commands. The function `matplotlib.pyplot.figure()`
creates a space into which we will place all of our plots. The parameter `figsize`
tells Python how big to make this space. Each subplot is placed into the figure using
its `add_subplot` method. The `add_subplot` method takes 3 parameters. The first denotes
how many total rows of subplots there are, the second parameter refers to the
total number of subplot columns, and the final parameters denotes which subplot
your variable is referencing (left-to-right, top-to-bottom). Each subplot is stored in a
different variable (`axes1`, `axes2`, `axes3`). Once a subplot is created, the axes can
be titled using the `set_xlabel()` command (or `set_ylabel()`).
Here are our three plots side by side:

~~~ {.python}
import numpy
import matplotlib.pyplot

data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')

fig = matplotlib.pyplot.figure(figsize=(10.0, 3.0))

axes1 = fig.add_subplot(1, 3, 1)
axes2 = fig.add_subplot(1, 3, 2)
axes3 = fig.add_subplot(1, 3, 3)

axes1.set_ylabel('average')
axes1.plot(data.mean(axis=0))

axes2.set_ylabel('max')
axes2.plot(data.max(axis=0))

axes3.set_ylabel('min')
axes3.plot(data.min(axis=0))

fig.tight_layout()

matplotlib.pyplot.show()
~~~

![The Previous Plots as Subplots](fig/01-numpy_80_0.png)

The [call](reference.html#function-call) to `loadtxt` reads our data,
and the rest of the program tells the plotting library
how large we want the figure to be,
that we're creating three subplots,
what to draw for each one,
and that we want a tight layout.
(Perversely,
if we leave out that call to `fig.tight_layout()`,
the graphs will actually be squeezed together more closely.)

> ## Scientists dislike typing {.callout}
>
> We will always use the syntax `import numpy` to import NumPy.
> However, in order to save typing, it is
> [often suggested](http://www.scipy.org/getting-started.html#an-example-script)
> to make a shortcut like so: `import numpy as np`.
> If you ever see Python code online using a NumPy function with `np`
> (for example, `np.loadtxt(...)`), it's because they've used this shortcut.

> ## Check your understanding {.challenge}
>
> Draw diagrams showing what variables refer to what values after each statement in the following program:
>
> ~~~ {.python}
> mass = 47.5
> age = 122
> mass = mass * 2.0
> age = age - 20
> ~~~

> ## Sorting out references {.challenge}
>
> What does the following program print out?
>
> ~~~ {.python}
> first, second = 'Grace', 'Hopper'
> third, fourth = second, first
> print(third, fourth)
> ~~~

> ## Slicing strings {.challenge}
>
> A section of an array is called a [slice](reference.html#slice).
> We can take slices of character strings as well:
>
> ~~~ {.python}
> element = 'oxygen'
> print('first three characters:', element[0:3])
> print('last three characters:', element[3:6])
> ~~~
>
> ~~~ {.output}
> first three characters: oxy
> last three characters: gen
> ~~~
>
> What is the value of `element[:4]`?
> What about `element[4:]`?
> Or `element[:]`?
>
> What is `element[-1]`?
> What is `element[-2]`?
> Given those answers,
> explain what `element[1:-1]` does.

> ## Thin slices {.challenge}
>
> The expression `element[3:3]` produces an [empty string](reference.html#empty-string),
> i.e., a string that contains no characters.
> If `data` holds our array of patient data,
> what does `data[3:3, 4:4]` produce?
> What about `data[3:3, :]`?

> ## Check your understanding: plot scaling {.challenge}
>
> Why do all of our plots stop just short of the upper end of our graph?

> ## Check your understanding: drawing straight lines {.challenge}
>
> Why are the vertical lines in our plot of the minimum inflammation per day not perfectly vertical?

> ## Make your own plot {.challenge}
>
> Create a plot showing the standard deviation (`numpy.std`) of the inflammation data for each day across all patients.

> ## Moving plots around {.challenge}
>
> Modify the program to display the three plots on top of one another instead of side by side.
