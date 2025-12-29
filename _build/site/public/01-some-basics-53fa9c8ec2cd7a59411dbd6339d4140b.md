# Some Coding Basics

**Author:** Jeremy Koch<sup>1,2</sup> \

## Binary


The code contained on this page is, to a large extent, all that will be needed for the core assignments in this course.
:::{aside}
The machine learning project will, of course, require a ton more code, though that project will be more practical. There is an entire course devoted to it.
:::
Remember that, in general, we are not using built-in packages! Yes, there is an ODE solver built-in to MATLAB and scipy and julia. No, you may not use them when writing your Runge-Kutta code

## Creating vectors/matrices/arrays and doing math with them

::::{tab-set}
:::{tab-item} MATLAB
```matlab
x1=0:0.1:2;                 % start:step:stop
x2=linspace(0,10,500);      % 500 points between 0 and 10
x3=logspace(4,7,500);       % 500 log-spaced points between 10^4 and 10^7
A=[[1,2,3];[4,5,6]];        % a matrix is an array of arrays, rows separated by ;
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
:::
:::{tab-item} C++
```cpp
f=lambda x: x**2
```
::: -->
::::



## Doing math with them

## Indexing/Accessing Elements


<!-- :::{aside}
https://en.wikipedia.org/wiki/Magnetic-core_memory
::: -->


<!-- ::::{tab-set}
:::{tab-item} MATLAB
```MATLAB
f=@(x) x^2
```
:::
:::{tab-item} python
```python
f=lambda x: x**2
```
:::
:::{tab-item} julia
```julia
f=lambda x: x**2
```
:::

:::: -->