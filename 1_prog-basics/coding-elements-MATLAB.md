# Necessary Coding Elements -- MATLAB

MATLAB is the default option for MCEN 3030 and has been the (one) language used for this class since before my time. We are opening the door to other languages, but I still expect MATLAB, which is tightly intertwined with engineering education, will have the greatest number of users in this class.

MATLAB is made for math, so, for example, the solution to "the linear algebra problem" $\mathbf{A}\cdot\mathbf{x}=\mathbf{b}$ is ```b=inv(A)*x``` or ```b=A\x```.

## Functions

Let's just give an example and talk about it. Here are the contents of one file, with a "local function" included below it (described below).
```matlab
function [out1,out2]=my_fxn(in1,in2)
    x=[in1,in2];
    out1=my_local_fxn(x);
    out2=in2+3;
end

function b=my_local_fxn(x)
    b=mean(x);
end
```
And here are a few things that you might try in a separate script file, or as an input in the command window:
```matlab
my_fxn(4,5)

a=my_fxn(4,5)

[a,b]=my_fxn(4,5)

my_local_fxn([4,5,6])

```

Some things you will notice:
- ```my_fxn(4,5)``` works, but produces only one output. ```a=my_fxn(4,5)``` works, but you only get the first output (saved as ```a```).
- To get both outputs, you must "warn" MATLAB that two are coming. So the second command, ```[a,b]=my_fxn(4,5)``` is how to get both outputs.
- ```my_local_fxn([4,5,6])``` produces an error: ```Unrecognized function or variable 'my_local_function'.```
- When calling a function, the output variables don't need to be the same as those in the function declaration. Here: ```a``` and ```b``` are perfectly fine names -- we don't need to save them as ```out1``` and ```out2```.

The Rules:
- Callable functions must have, as their first line, ```[output variables] = function_name(input variables)```, and the file must be called ```function name.m```.
- Such functions can be called as long as you are in the same working directory -- if that ```*.m``` file is in the folder you currently have open in MATLAB.
- The local function ```my_local_fxn``` cannot be called outside of the file. We can't call it from a script or other function or the command window -- it is only known "locally" within the main function file ```my_fxn.m```. Local functions are useful if there is a little side quest you need to do within a main function that gets rid of some clutter.
- A consequence of the above: there is only one "main" function per ```*.m``` file. This is one of the most annoying things about MATLAB.
- By default, MATLAB only returns the first output if you simply call the function. In order to retrieve the other output variables, you need to "warn" MATLAB that more are coming by defining variables where they will be stored.

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


## Indexing and Modifying Elements

MATLAB indexes from ```1``` and can use ```end``` to refer to the last index. Be careful when talking to Python folks, your "first" element might be their "zeroth".

```matlab
x(i)=5;                     % changes the ith element of x (x would need to exist already)
x(3:end)=0;                 % elements 3 to the end all become 0
x(2:4)=-88;                 % the second, third, and fourth elements become -88

A(4,1)=5;                   % change the fourth element in column 1
A(:,5)=6;                   % the fifth column is a vector... this makes all those elements equal 6
A(4,:)=-9;                  % the fourth row is now full of -9s
```

## Doing math with them

MATLAB uses "dot star" ```.*``` and similar to do element-by-element math, which is mostly what we will be doing in this class.

```matlab
x=[1, 2, 3];
y=[4, 5, 6];
z=x.*y;
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

The "logical equals" is ```==``` (as in, ```x==5``` checks to see if ```x``` is equal to ```5```, evaluating that as True/False or 1/0). The logical and is ```&&```, the logical or is ```||```, and ```>=``` and ```<=``` work as you'd expect! "Not equals" is ```~=```.

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

