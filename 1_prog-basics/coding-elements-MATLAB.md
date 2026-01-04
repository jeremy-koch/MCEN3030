# Necessary Coding Elements -- MATLAB

MATLAB is the default option for MCEN 3030 and has been the (one) language used for this class since well-before my time. We are opening the door to other languages, but I still expect MATLAB, which is tightly intertwined with engineering education, will have the greatest number of users in this class.

MATLAB is made for math, so, for example, the solution to "the linear algebra problem" $\mathbf{A}\cdot\mathbf{x}=\mathbf{b}$ is ```b=A\x``` (```A\``` is under-divide by A, a nice shorthand for ```inv(A)``` and a little faster than actually calculating the inverse).

A couple examples that epitomize this:
- If you have a line in your function that is just ```x``` (not suppressed with ```;```), it will print the value of ```x```. Sloppy, annoying if you don't mean to do that, but I do it all the time when developing a program just to quickly see what is going on.
- 
For example, having an "unsuppressed" line (without ```;``` at the end) prints the value produced by the line, and so a ```x``` will tell you what ```x``` is.

## Functions

Let's just give an example and talk about it. Here are the contents of one file:
```matlab
function [out1,out2]=my_fxn(in1,in2)
    out1=(in1+in2)/2;
    out2=sqrt(in1*in2);
end

function 
```
... and here is a separate file, a script, that would call this function.
```matlab

```

The Rules:
- The first file must be named ```my_fxn.m``` and must be in the same directory as the script. The script could be called anything.
- Calling ```local_fxn(...)``` from the script would cause an error. Local functions are only known within their own ```.m``` file
- The output variables are named in the function declaration (```out1``` and ```out2```).
- In order to retrieve outputs 2, 3, ... when calling a function, you must allocate space for them in the call. By default, MATLAB only returns the first output. (However, if you want to be a bit sleek, you can use ~ as one or more of the variable names, and MATLAB won't bother storing those numbers anywhere.)
- In order for a function to be available outside the ```*.m``` in which it is written, the ```*.m``` file name must match the function name and the first line of the *.m file must be the function definition.
- Functions can be called from other functions/scripts/the command window when they are in the current working directory, or if the "path" has been added.
- "Local" functions are "known" only within . These are sometimes useful to handle some work that would make the main function messy. The definition must occur below the "main" function.
- A consequence of the above: there is only one "main" function per *.m file. This is one of the most annoying things about MATLAB.

A function file, with a local function below it:

Note that:


### Optional Arguments

Optional arguments do not have to be included in the function call. If they are included, the associated variable uses the value given in your function call; if they are not, they will default to the value included in the function definition.

For MCEN 3030, a common use is to define a standard error or a maximum number of iterations. Here is how that would look:
```matlab
function x_R=Newton_Raphson1(f,x_0,err_accept=10^-3,max_iter=1000)
    ...
    % code implementing the NR method where the function terminates
    % when the error reaches 10^-3 or 1000 iterations have occurred
    ...
end
```

and if you want to use the non-default values, you could call with, e.g.: ```x_root=Newton_Raphson1(f,x_0,max_iter=2000)```.




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

MATLAB indexes from ```1``` and can use ```end```


```matlab
x(i)=5;                     % accesses the ith element of x
x(3:)                       % elements 3 to the end
x(:5)                       % the first through fifth elements
x(2:4)                      % the second, third, and fourth elements

A(4,1)=5;                   % change the fourth element in column 1
A(:,5)                      % the fifth column is a vector... 
A(4,:)                      % the fourth row
```

## Doing math with them






## Conditional Statements


## Loops


## Miscellaneous

To load in data from a csv. (You may be able to load from other data types, but csv will be our standard because of the predictability. of the formatting.)


## Some common motifs

Don't "hard-code" in numbers if you can avoid it! It will make your code more flexible, readable, and easier to debug. For example:

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

