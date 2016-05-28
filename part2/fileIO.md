# File I/O

> ## Learning Objectives
>
> *   Python text file IO
> *   Tabular data Numpy and common gotchas
> *   Look ahead to Pandas

##What is IO?

Typing strings and numbers into an IPython Notebook are great ways to learn basics, but sooner or later you will have to learn how to read data from a file, perform some analysis on that data and ideally save the analysis.

File is a named location on disk to store related information. It is used to permanently store data in a non-volatile memory (e.g. hard disk). Since, random access memory (RAM) is volatile which loses its data when computer is turned off, we use files for future use of the data.

When we want to read from or write to a file we need to open it first. When we are done, it needs to be closed, so that resources that are tied with the file are freed. Hence, in Python, a file operation takes place in the following order.

* Open a file
* Read or write (perform operation)
* Close the file

##IO for text files


`open()` returns a file object, and is most commonly used with two arguments: `open(filename, mode)`. mode can be `r` when the file will only be read, `w` for only writing (an existing file with the same name will be erased), and `a` opens the file for appending; any data written to the file is automatically added to the end.

To read a file’s contents, call `f.read(size)`, which reads some quantity of data and returns it as a string.

##Encoding 

When working with files in text mode, it is recommended to specify the encoding type. Files are stored in bytes in the disk, we need to decode them when we read into Python. Similarly, encoding is performed while writing texts to the file. The default encoding is platform dependent. In windows, it is 'cp1252' but 'utf-8' in Linux. Hence, we must not rely on the default encoding otherwise, our code will behave differently in different platforms. Thus, this is the preferred way to open a file for reading in text mode.

```python
f = open("test.txt",mode = 'r',encoding = 'utf-8')
```

##Read a file line-by-line 

##Closing a File

When we are done with operations to the file, we need to properly close it. Python has a garbage collector to clean up unreferenced objects. But we must not rely on it to close the file. Closing a file will free up the resources that were tied with the file and is done using the `close()` method. 

However, this method is not entirely safe. If an exception occurs when we are performing some operation with the file, the code exits without closing the file. The best way to do this is using the  `with` statement. This ensures that the file is closed when the block inside with is exited. We don't need to explicitly call the `close()` method. It is done internally.

```python
with open("test.txt",encoding = 'utf-8') as f:
   # perform file operations
```

##Tabular date with Numpy 

##Non-numeric data with Pandas

While we don't use the Pandas library in this course, it's useful to get a feel for what Pandas is, what types of data it can handle, and show how easy it is to read these in...
