# Defining Functions (language specifics)

<!-- **Author:** Jeremy Koch<sup>1,2</sup> \ -->

## Some vocabulary

Script
: We will take this to mean a coding file with simple instructions that don't require much overhead, e.g.: make a list of numbers between 0 and 50, use them in a function, and print the results. This takes three lines of code in a ```*.m```, ```*.py```, or ```*.jl``` file, no need for any formal declarations, just go through the steps in that script, in order.
:::{aside}
For our purposes, MATLAB, Python, and Julia are all "scripting languages", though that title is controversial for Julia because it is technically compiled. 
:::



Function
: These turn inputs into outputs according to a set of rules. Functions require a formal declaration, the structure of which is basically the same in all languages: somewhere you declare the function name, input variables, and how to return the outputs. Specifics of each language are discussed below.

(Input) Arguments
: The 

Call
: We "call" functions from other functions or scripts, providing the necessary input arguments and allocating space for the outputs. In no language do the variable names in the call need to match the variable names in the function definition. After all, we sometimes will call a function twice, getting two (sets of) outputs.

Anonymous Function
: MATLAB, Python, and Julia all have a way of writing small functions that are not stored under a traditional function name (hence the moniker "anonymous"). They are still stored under a variable name... I am sure there are some subtleties I am missing. When part of a project's foundational architecture, this type of function definition is discouraged (one reason: it makes tracing errors difficult because the functions are not named in the error messages). However, within scripting languages, it is often a really nice tool to create an equation function for use in our algorithms like $f(x) = \ln{\sin(x)}$. As an example: ```f=@(x) log(sin(x))``` (in MATLAB).




### A note about the exam format

The questions will be akin to writing scripts: think about what function(s) might be relevant, set up the necessary inputs, handle the outputs, post-process, etc. 


## Functions 

Functions are slightly different than scripts -- you can "call" a function from a script or another function, even another file (provided it is in an appropriate location). Each language has slightly different rules:

::::{tab-set}
:::{tab-item} MATLAB
Rules for MATLAB functions:
- The output variables must be named in the function declaration (```out1``` and ```out2``` in the function defined below).
- In order to retrieve outputs 2, 3, ... when calling a function, you must allocate space for them in the call. By default, MATLAB only returns the first output. (However, if you want to be a bit sleek, you can use ~ as one or more of the variable names, and MATLAB won't bother storing those numbers anywhere.)
- In order for a function to be available outside the ```*.m``` in which it is written, the ```*.m``` file name must match the function name and the first line of the *.m file must be the function definition.
- Functions can be called from other functions/scripts/the command window when they are in the current working directory, or if the "path" has been added.
- "Local" functions are "known" only within . These are sometimes useful to handle some work that would make the main function messy. The definition must occur below the "main" function.
- A consequence of the above: there is only one "main" function per *.m file. This is one of the most annoying things about MATLAB.

A function file, with a local function below it:
```matlab
function [out1,out2]=my_fxn(in1,in2)
    out1=(in1+in2)/2;
    out2=sqrt(in1*in2);
end
```
... and a script that would call this function.
```matlab
function [out1,out2]=my_fxn(in1,in2)
    out1=(in1+in2)/2;
    out2=sqrt(in1*in2);
end
```
Note that:
- The function file must be named ```my_fxn.m``` and must be in the same directory as the script. The script could be called anything.
- Calling ```local_fxn(...)``` from the script would cause an error.
:::





:::{tab-item} python
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
:::


:::{tab-item} Julia
Rules for Julia functions:
- Definition looks like 
- Instead of a ```return``` statement, one can use the "implicit output": the last variable given a value in the function. I am suspicous of this and recommend a ```return out1,out2``` before the ```end```. It is kind of clumsy-looking to have both though.
:::
::::






## What can be passed to functions?


## Optional Arguments

All the languages have an option to include optional arguments. These do not have to be included in the function call, and if not, they will default to the value included in the function definition.

For MCEN 3030, a common use is to define a standard error or a maximum number of iterations. Here is how that would look:

::::{tab-set}
:::{tab-item} MATLAB
```matlab
function x_R=Newton_Raphson1(f,x_0,err_accept=10^-3,max_iter=1000)
    ...
    % NR method where the function terminates when the error reaches 10^-3 or 1000 iterations have occurred.
    ...
end
```

:::


:::{tab-item} python
```python
def Newton_Raphson1(f,x_0,err_accept=10^-3,max_iter=1000)
    ...
    # NR method where the function terminates when the error reaches 10^-3 or 1000 iterations have occurred.
    ...
    return x_R
```
:::


:::{tab-item} Julia
```julia

```
:::
::::