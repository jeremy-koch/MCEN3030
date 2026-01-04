# Necessary Coding Elements -- Python

Python has become the most popular language for scientists (and for machine learning), likely because of its ease with higher. However

We are using NumPy for everything in this class. "Native Python" lists like ```x=[1,2,3,4]``` do not cooperate well with mathematical operations -- instead, we are going to turn everything into NumPy arrays.

Many of the tools we will build -- differential equation solvers, numerical integrators, ... -- are part of the SciPy package. I would recommend installing that package as well. However, remember that we are building our own tools this semester -- if you start some code with ```from scipy.optimize import curve_fit```, you are doing it wrong!

## Functions

Rules for Python functions:
- Functions must be defined earlier than they are used -- e.g., the function definition cannot occur on lines 13-17 and be called on line 5.
- You can include as many 
- If your ```return``` includes more than one variable, you must have more than one variable defined in your function call line. It will complain about expecting a different-sized output.
- 


Here is a file with a couple functions in it:
```python
import numpy as np
k=2
m=np.sin(2)
print(m)
```


### Optional Arguments

```python
def Newton_Raphson1(f,x_0,err_accept=10^-3,max_iter=1000)
    ...
    # NR method where the function terminates when the error reaches 10^-3 or 1000 iterations have occurred.
    ...
    return x_R
```


## Creating vectors/matrices/arrays


```matlab
x1=0:0.1:2;                 % start:step:stop
x2=linspace(0,10,500);      % 500 points between 0 and 10
x3=logspace(4,7,500);       % 500 log-spaced points between 10^4 and 10^7
A=[[1,2,3];[4,5,6]];        % a matrix is an array of arrays with rows separated by ;

y=zeros(1,length(x2));      % a row vector full of zeros with the same length as x2
z=ones(1,length(x2));       % same, but full of ones
A=zeros(4,4);               % a 4x4 matrix of zeros
B=eye(4);                   % diagonal is full of ones, rest zero
D=diag([5,3,1]);            % diagonal is 5,3,1, rest zero
D2=diag([5,3,1],1);         % the first diagonal above the main is [5,3,1]... so this is a 4x4 matrix

r=rand(1,5);                % a row vector with 5 random numbers, uniformly spaced between 0 and 1
R=rand(4,4);                % same, but a 4x4 matrix
```



```python
f=lambda x: x**2
```



## Indexing: Accessing and Modifying Elements

The focus on many debates: should arrays be indexed starting with zero or one? Python indexes starting with 0, MATLAB and Julia index starting with 1.


```matlab

x(i)                        % accesses the ith element of x
x(3:)                       % elements 3 to the end
x(:5)                       % the first through fifth elements
x(2:4)                      % the second, third, and fourth elements

A(4,1)=5;                   % change the fourth element in column 1
A(:,5)                      % the fifth column is a vector... 
A(4,:)                      % the fourth row
```
:::
<!-- :::{tab-item} python
```python
f=lambda x: x**2
```
:::
:::{tab-item} julia
```julia
f=lambda x: x**2
```
::: -->
::::

## Doing math with them






## Conditional Statements


## Loops


## Miscellaneous


A very useful package in Python is "pandas".

## Some common motifs

Don't "hard-code" in numbers if you can avoid it! It will make your code more flexible, readable, and easier to debug. For example:
::::{tab-set}
:::{tab-item} MATLAB
```matlab
x=1:100;
y=1:100;
for i=1:100          
    % are we iterating through x or y?
    % If we have to change whichever of them to 1:500, we'd have to change our "for" line above
end

% this is better
for i=1:length(y)
    % now we know it is iterating through y
    % and if we change to y=1:500, it automatically is ready to go!
end
```
:::
<!-- :::{tab-item} python
```python
f=lambda x: x**2
```
:::
:::{tab-item} julia
```julia
f=lambda x: x**2
```
::: -->
::::

If you need something to happen if a number is even:
::::{tab-set}
:::{tab-item} MATLAB
```matlab
if mod(x,2)==0  % even!
    % do something
else            % odd!
    % do something else
end
```
:::
<!-- :::{tab-item} python
```python
f=lambda x: x**2
```
:::
:::{tab-item} julia
```julia
f=lambda x: x**2
```
::: -->
::::

To calculation a summation, initialize the sum at zero:
::::{tab-set}
:::{tab-item} MATLAB
```matlab
N=15;       % how many terms to include
S=0;        % initialize the sum at zero
for n=1:N
    S=S+sin(n);
end
```
:::
<!-- :::{tab-item} python
```python
f=lambda x: x**2
```
:::
:::{tab-item} julia
```julia
f=lambda x: x**2
```
::: -->
::::

See also: [functions](functions.md).

https://github.com/brenhinkeller/JuliaAdviceForMatlabProgrammers