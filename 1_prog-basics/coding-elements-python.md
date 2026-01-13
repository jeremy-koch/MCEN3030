# Necessary Coding Elements -- Python

"Native Python" lists like ```x=[1,2,3,4]``` do not cooperate well with mathematical operations. Instead, we are going to turn everything into NumPy arrays, and so the first line in almost every code you write will be ```import numpy as np```. (The standard alias is ```np```, I would encourage that use.)

Many of the tools we will build -- differential equation solvers, numerical integrators, ... -- are part of the SciPy package. I would recommend installing that package as well. However, remember that we are building our own tools this semester: if you start some code with ```from scipy.optimize import curve_fit```, you are doing it wrong!

## Functions

Rules for Python functions:
- Functions must be defined earlier than they are used -- e.g., the function definition cannot occur on lines 13-17 and be called on line 5.
- You can include as many 
- If your ```return``` includes more than one variable, you must have more than one variable defined in your function call line. It will complain about expecting a different-sized output.
- 


Here is a file with a couple functions in it, and a couple function calls:
```python
import numpy as np
def my_first_fxn(a,b):
    c=a+b
    return c

def my_second_fxn(a,b):
    c=a-b
    d=2*a
    return c,d

C_1=my_first_fxn(3,2)
C_2,D_2=my_second_fxn(3,2)
```

The Rules:
- Functions begin with ```def```, a function name, and the input variables(/arguments). (Optional arguments are easy to do in Python -- see below.)
- The output of the function is whatever follows the ```return```. Could but one number or one array or multiple numbers.
- If there are multiple outputs, you must "prepare" your script for them, as I did above with the ```C_2,D_2=```.
- Many functions can be included in the same file, and they can be imported into another file in the working directory -- this is what is going on with the ```import numpy``` stuff! The way to do it: if the file is called ```some_fxns.py``` you could do: ```import some_fxns as sf``` and then the call would look like ```C_1=sf.my_first_fxn(3,2)```.



### Optional Arguments

Python allows for easy use of optional arguments -- an idea that is technically possible in MATLAB, but very clumsy. (Julia does optional arguments well too.)

Optional arguments are really neat and relevant to MCEN 3030: in most cases the answers we get will be approximate, and we have to make a judgment about what is close enough; or we have to put our foot down and say our iterations need to stop because we are not going to get the answer. Two metrics that would help us here are an acceptable convergence -- as in, if our last two iterations were basically the same, let's call it good -- and a maximum number of iterations -- as in, we've gone through this algorithm 1000 times, if we aren't there yet we aren't going to get there.



In Python it would look something like this:
```python
def Newton_Raphson1(f,x_0,con_accept=10^-3,max_iter=1000)
    ...
    # NR method where the function terminates when the error reaches 10^-3 or 1000 iterations have occurred.
    ...
    return x_R
```
... and the idea is: you can call this function using just two input arguments, ```f``` and ```x_0```, and it will assume the default values for the other two arguments. If you'd like to adjust those, you can by calling with, e.g. ```Newton_Raphson1(g,0,err_accept=10^-2)``` or ```Newton_Raphson1(g,0,max_iter=9000)``` or ```Newton_Raphson1(g,0,err_accept=10^-2,max_iter=9000)```.

## Creating vectors/matrices/arrays


```python
import numpy as np                      # almost all your code will need this at the top of the file

x0 = np.array([1, 2, 3])                # a numpy array from a python list
x1 = np.arange(0, 2.1, 0.1)             # start,stop (EXCLUSIVE!),step
x2 = np.linspace(0, 10, 500)            # 500 points between 0 and 10
x3 = np.logspace(4, 7, 500)             # 500 log-spaced points between 10^4 and 10^7
A  = np.array([[1, 2, 3], [4, 5, 6]])   # a matrix is made up of lists as rows

y  = np.zeros(len(x2))                   # a row vector full of zeros with the same length as x2
z  = np.ones(len(x2))                    # same, but full of ones
A  = np.zeros((4, 4))                    # a 4x4 matrix of zeros (note the argument is a "tuple")
B  = np.eye(4)                           # diagonal is full of ones, rest zero
D  = np.diag([5,3,1])                    # diagonal is 5,3,1, rest zero
D2 = np.diag([5,3,1],k=1)                # the first diagonal above the main is [5,3,1]... so this is a 4x4 matrix

r  = np.random.rand(5)                   # a row vector with 5 random numbers, uniformly spaced between 0 and 1 (exclusive!)
R  = np.random.rand(4,4)                 # same, but a 4x4 matrix
```


## Indexing: Accessing and Modifying Elements

Python indexes from ```0```. I like to say that the initial element in an array is the "zeroth" element... be careful when talking to MATLAB/Julia folks about the "first" element, it might be your "zeroth".

```python
x[i]=5             # changes the ith element of x (x would need to exist already)
x[3:]=0            # elements 3 to the end all become 9 (could have done e.g. [9,10,11]... changes elements 3,4,5)
x[2:5]=-88         # the second, third, and fourth elements become -88, python excludes the stop index (exclusive!)
x[-1]=999          # the last element can be indexed as -1 (and the second to last, -2)

A[4,1]=5;          # change the fourth element in column 1
A[:,5]=5;          # the fifth column is a vector... this makes all elements in that vector =5
A[4,:]=-9;         # the fourth row is now full of -9s
```

## Doing math with them

Python assumes element-by-element math (mostly what we will be doing in this class) by default, so addition, multiplication, and division of arrays is just ```x+y```, ```x*y```, and ```x/y```. Raising to powers is, controversially ```x**2``` (i.e., that is how we square a number). 

NumPy has many built-in mathematical functions that work on arrays: ```np.exp(x)``` for the exponential function, ```np.log(x)``` is the natural log, ```np.log10(x)``` is the base-10 log, ```np.sqrt(x)``` gets a square root. ```np.sin```, ```np.cos```, ```np.tan```, etc.



## Conditional Statements
Here is the ```if```-```elif```-```else``` structure:

```python:
if x<5:
    y=10
elif x>9:
    y=15
else:
    y=-99
```

Python looks like natural language here: we literally write ```if x>5 and x<10```, and similar with ```or```. ```>=``` and ```<=``` work as you'd expect!


## Loops
A ```while``` loop looks like this:
```python
counter=0;
while counter<5:
    print('hi')
    counter=counter+1
```
note that no ```end``` is needed! Whitespace!

A ```for``` reads like natural language:
```python
x=np.array([1,2,3]);
S=0
for i in range(x):
    S=S+x[i]
```



## Reading/Writing Spreadsheets

It is common to use ```*.csv``` files: comma-separated values. You may be able to load from other sources, but csv will be our standard because of the predictability of the formatting.

To read in a csv and store the data as a matrix: ```data = np.loadtxt('my_data.csv', delimiter=',')```. (From there you can get individual columns via ```x_data=data[:,1]``` etc.)

To write a new csv: ```np.savetxt('data.csv', [x_data,y_data], delimiter=',')``` creates a new file in your current directory called "data.csv".

## Anonymous Functions

In our root-finding algorithms, we will input a (mathematical) function into a (programming) function, e.g.: find the root of $f(x)=\sin(x)-0.85$. This can be achieved via an anonymous function, sometimes called a "lambda" function: ```f=lambda x: np.sin(x)-0.85```. 

If two inputs are needed: ```f=lambda x,y: x+y```.


## Some common motifs

If you need something to happen if a number is even:

```python 
if x % 2 ==0: # even!
    # do something
else:            # odd!
   # do something else
```


To calculation a summation, initialize the sum at zero:

```python
N=15       # how many terms to include
S=0       # initialize the sum at zero
for n in range(N):
    S=S+np.sin(n)

```

