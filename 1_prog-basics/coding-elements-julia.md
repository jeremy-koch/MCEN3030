# Necessary Coding Elements -- Julia

If you are interested in computational science, you might find Julia to be an interesting language. Maybe you'd like to read this: [Julia: A Fresh Approach to Numerical Computing](https://arxiv.org/abs/1411.1607).

The considerations outlined in that paper are not important to MCEN 3030, but, if you have the appetite for it, you could spend MCEN 3030 building up some relevant experience in some basic tasks, and then can expand to more cutting-edge things on the side or after the course has concluded.

There are a lot of extra considerations with Julia that will make it challenging for those who are unfamiliar with the vocabulary of computer science -- you will need to be more careful with data types and variable scope, as examples. For this reason, I think I'd like to chat with you before you commit to this language. Everyone in the class could use it and would be fine, but I just want to make sure the juice is worth the squeeze (for your situation). That being said, I would be really interested to get some more experience myself with a handful of brave students.

Julia is famous for "multiple dispatch" which is something we will not really have an opportunity to explore in this class. However, you may independently explore this, and tell me about it!






## Creating vectors/matrices/arrays


```julia
x1 = 0:0.1:2                      # start:step:stop (creates a range object)
x2 = range(0, 10, length=500)     # 500 points between 0 and 10
x3 = 10 .^range(4, 7, length=500) # 500 log-spaced points between 10^4 and 10^7
A = [1 2 3; 4 5 6]                # a matrix is built with spaces separating columns and semicolons separating rows

y = zeros(1, length(x2))    # a row vector full of zeros with the same length as x2
z = ones(1, length(x2))     # same, but full of ones
A = zeros(4, 4)             # a 4x4 matrix of zeros

using LinearAlgebra         # Required for eye (I) and diag functions
B = Matrix(1.0I, 4, 4)      # diagonal is full of ones, rest zero
D = diagm(0 => [5, 3, 1])   # diagonal is 5,3,1, rest zero
D2 = diagm(1 => [5, 3, 1])  # the first diagonal above the main is [5,3,1]... so this is a 4x4 matrix

r = rand(1, 5)              # 1x5 row matrix of random numbers
R = rand(4, 4)              # same, but a 4x4 matrix
```


## Indexing and Modifying Elements

Julia indexes from ```1``` and can use ```end``` to refer to the last index. Be careful when talking to Python folks, your "first" element might be their "zeroth". (MATLAB indexes from 1.)

Julia is consistent with the following rule: if it applies to multiple elements, the operation is "dot something". Both MATLAB and Julia have the ```.^``` and ```.*``` for element-by-element math, but Julia has the peculiar ```.=``` when setting multiple values of an array. It makes sense, if you think about it, but also I am not sure if ```x[3:end]=0``` (which is how MATLAB would do it) is actually that ambiguous!

```julia
x[i] = 5                    # changes the ith element of x (x would need to exist already)
x[3:end] .= 0               # elements 3 to the end become 0
x[2:4] .= -88               # elements 2, 3, and 4 becomes -88

A[4, 1] = 5                 # changes the fourth element in column 1
A[:, 5] .= 6                # the fifth column is a vector... this makes all of those elements equal 6
A[4, :] .= -9               # the fourth row is now full of -9s
```




## Doing math with them


<!-- 
```julia
# x=[1, 2, 3]         # with commas... this creates a column vector
# y=[4 5 6]           # no commas... this creates a row vector
# z=x.*y;
```
From the above code, we would find ```z=[4, 10, 18]```. To square all elements, ```.^2```, to divide element-by-element, ```x./y```. No dot is needed for addition and subtraction.

Common mathematical functions work element-by-element on arrays: ```sin(x)```, ```exp(x)```, ```log(x)``` is the natural log, ```log10(x)``` is the base-10 log, ```sqrt(x)``` for square root. sin, cos, tan, etc.


## Conditional Statements
Here is the ```if```-```elseif```-```else``` structure:

```matlab
if x<5
    y=10;
elseif x>9
    y=15;
else
    y=-99;
end
```

The "logical equals" is ```==``` (as in, ```x==5``` checks to see if ```x``` is equal to ```5```, evaluating that as True/False or 1/0). The logical and is ```&&```, the logical or is ```||```, and ```>=``` and ```<=``` work as you'd expect!

## Loops
A ```while``` loop looks like this:
```matlab
counter=0;
while counter<5
    display('hi')
    counter=counter+1;
end
```

and a ```for``` loop looks like this:
```matlab
x=[1,2,3];
S=0;
for i=1:length(x)
    S=S+x(i);
end
```

## Reading/Writing Spreadsheets

It is common to use ```*.csv``` files: comma-separated values. You may be able to load from other sources, but csv will be our standard because of the predictability of the formatting.

To read in a csv and store the data as a matrix: ```data = readmatrix('my_data.csv');```. (From there you can get individual columns via ```x_data=data(:,1)``` etc.)

To write a new csv: ```writematrix([x_data, y_data], 'data.csv');``` creates a new file in your current directory called "data.csv".

## Anonymous Functions

In our root-finding algorithms, we will input a (mathematical) function into a (programming) function, e.g.: find the root of $f(x)=\sin(x)-0.85$. This can be achieved via an anonymous function: ```f=@(x) sin(x)-0.85;```. 

If two inputs are needed: ```f=@(x,y) x+y;```.


## Some common motifs

If you need something to happen if a number is even:

```matlab
if mod(x,2)==0  % even!
    % do something
else            % odd!
    % do something else
end
```


To calculation a summation, initialize the sum at zero:

```matlab
N=15;       % how many terms to include
S=0;        % initialize the sum at zero
for n=1:N
    S=S+sin(n);
end
```
 -->
















## A few frustrations

A few frustrations I have encountered (and most of these are likely just because I am more used to MATLAB/Python, which are more user-friendly):
- ```y = x``` will assign ```y``` to the same memory location as ```x```, which means that changing ```x[1]``` also changes ```y[1]```. If you need to make a genuine copy that can be independently modified: ```y=copy(x)```.
- Meanwhile, slicing an array makes a copy automatically. ```z=x[2:end]``` creates an independent array, ```z``` that is not tied to ```x```.
- 





## Additional resources/readings

https://github.com/brenhinkeller/JuliaAdviceForMatlabProgrammers



<!-- 
## Functions

Rules for Julia functions:
- Definition looks like 
- Instead of a ```return``` statement, one can use the "implicit output": the last variable given a value in the function. I am suspicous of this and recommend a ```return out1,out2``` before the ```end```. It is kind of clumsy-looking to have both though. -->

<!-- ## Creating vectors/matrices/arrays

## Indexing: Accessing and Modifying Elements

## Doing math with them






## Conditional Statements


## Loops


## Miscellaneous


## Some common motifs






## Functions -->

