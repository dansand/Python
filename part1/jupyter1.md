# Jupyter Notebooks 1

> ## Learning Objectives
>
> *   Explain what a the Jupyter Notebook environment is.
> *   Creation / execution of code cells.
> *   Markdown and markdown cells
> *   Shortcuts


### What are they?

Notebook documents  are documents produced by the Jupyter Notebook App which contain both computer code (e.g. python) and rich text elements (paragraph, equations, figures, links, etc...). Notebook documents are both human-readable documents containing the analysis description and the results (figures, tables, etc..) as well as executable documents which can be run to perform data analysis.

The Jupyter Notebook App is a web application that allows you to create and share documents that contain live code, equations, visualizations and explanatory text.

_How will the children of the future learn about science? How will the scientists of the future expand our thinking? I think the answer is Jupyter Notebooks._ Safia Abdalla


* Jupyter Notebooks were formally called ipython notebooks...

### The notebook dashboard

The Notebook Dashboard is the component which is shown first when launching Jupyter Notebook App. The Notebook Dashboard is mainly used to open notebook documents, and to manage the running kernels (visualize and shutdown).


Make sure you have a Notebook. If you're don't have iPython/Jupyter on your computer, you can run a temporary notebook here:
[Tempnb] (https://tmpnb.org/)

###Code

Not just Python! The Notebook has support for over 40 programming languages, including those popular in Data Science such as Python, R, Julia and Scala.

### Markdown

Explanatory text can be integrating with the Jupyter Notebook using a simple formatting schema called _Markdown_. See the link for a basic description.
https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

###Keyboard Shortcuts

Shift-Enter Run current cell and move to the cell below
Ctrl-Enter Run current cell and stay in that cell
Alt-Enter Run the current cell then create and move to a new cell below.

### Literate programming 

Is an approach to programming introduced by Donald Knuth in which a program is given as an explanation of the program logic in a natural language, such as English, interspersed with snippets of macros and traditional source code, from which a compilable source code can be generated.

### What about scripts?

# Jupyter Notebooks 2

> ## Learning Objectives
>
> *   Jupyer / IPython Magics
> *   Binder
> *   More tricks

###Magics

    %load 

This magic loads a Python file from a filepath or URL and replaces the contents of the cell with the contents of the file.
    
    %matplotlib inline
This magic places matplotlib plots inline instead of opening a new window.

    %%writefile

This magic writes the contents of a cell to a file.

    %pprint

This magic toggles pretty print on/off

    %reset

This magic resets the namespace by removing all names defined by the user, if called without arguments.

    %timeit

This magic times the execution of a Python statement or expression. The CPU and clock times are printed.

    %%html

Render the cell as a block of HTML

    %%latex

Render the cell as a block of latex

### More tricks

Adding Line Numbers
One of the most annoying things about the Jupyter Notebook is the lack of line numbers. This makes it very difficult to track down lines mentioned in error messages.

Typing CTRL-M L toggles line numbers in the focus cell.

### Binder

Version control and social coding sites like GitHub make it simple to share code, and projects like the Jupyter notebook provide interactive interfaces for language-agnostic analysis. But executing that code remains a hurdle — dependencies, data, and system configuration are less portable than code, and are more difficult to specify. Binder has two primary goals: to make it easy to construct reproducible environments, even without knowledge of containerization technology; and to make these environments available for instantaneous deployment in the browser.

https://github.com/dsfaco/a-brief-peek-into-all-things-bayes

