# numpy2

> ## Learning Objectives
> *   Create useful numpy arrays 
> *   Perform operations on arrays of data.
> *  Plot data with matplotlib and seaborn 

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

