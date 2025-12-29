# Necessary Coding Elements

**Author:** Jeremy Koch<sup>1,2</sup> \

This course is less about using built-in functions like ```fsolve``` and more about understanding the algorithms. Truthfully, nearly all of the necessary coding elements to write all the functions in this course appear on this page -- indexing, ```if```, ```for```, ```while```. You'll need to do some space preallocation, maybe with something built-in called ```zeros```; might need to use the modulus function to determine if a number is odd or even... not much else.

:::{caution}
I think staring at this list in hopes of memorizing it is a terrible use of your time. Instead, treat this as a reference list early in the semester. It is perfectly reasonable to recognize that you will need a list of 500 numbers between 100 and 200, and you open this page to figure it out. Before long many of these will will become second nature to you.

Big picture: the best way to learn is to do it. No amount of reading my code is going to make you a skilled programmer.
:::

## Creating vectors/matrices/arrays

::::{tab-set}
:::{tab-item} MATLAB
```matlab
x1=0:0.1:2;                 % start:step:stop
x2=linspace(0,10,500);      % 500 points between 0 and 10
x3=logspace(4,7,500);       % 500 log-spaced points between 10^4 and 10^7
A=[[1,2,3];[4,5,6]];        % a matrix is an array of arrays, rows separated by ;

y=zeros(1,length(x2));      % a row vector full of zeros with the same length as x2
z=ones(1,length(x2));       % same, but full of ones
A=zeros(4,4);               % a 4x4 matrix of zeros
B=eye(4);                   % diagonal is full of ones, rest zero
D=diag([5,3,1]);            % diagonal is 5,3,1, rest zero
D2=diag([5,3,1],1);         % the first diagonal above the main is [5,3,1]... so this is a 4x4 matrix

r=rand(1,5);                % a row vector with 5 random numbers, uniformly spaced between 0 and 1
R=rand(4,4);                % same, but a 4x4 matrix
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

## Indexing: Accessing and Modifying Elements

The focus on many debates: should arrays be indexed starting with zero or one? Python indexes starting with 0, MATLAB and Julia index starting with 1.

::::{tab-set}
:::{tab-item} MATLAB
```matlab

x(i)                        % accesses the ith element of x
x(3:)                       % elements 3 to the end
x(:5)                       % the first through fifth elements
x(2:4)                      % the second, third, and fourth elements

A(4,1)                      % fourth element in column 1
A(:,5)                      % the fifth column... a vector
A(4,:)                      % the fourth row

% for all of the above, you can reassign values with =, e.g.
x(3)=5;                     % changes the third element to 5
A(:,5)=0;                   % changes the entire fifth column to 0
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

To calculation a summation
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

<!-- :::{aside}
https://en.wikipedia.org/wiki/Magnetic-core_memory
::: -->

## Functions
::::{tab-set}
:::{tab-item} MATLAB
MATLAB has a lot of restrictive rules about functions. Function files must be named the same as the top function in the file. Local functions must appear at the bottom of the main function file or script, and are not "known" outside the file.
```matlab
function [out1,out2]=my_fxn(in1,in2)


```
"Anonymous" functions (I don't know why they are called that), are written like
```matlab
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
f= x -> x^2
```
:::

::::