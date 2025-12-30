# Debugging Strategies

<!-- **Author:** Jeremy Koch -->

## Motivation

I think developing an eye for code (including debugging) is a really valuable skill to have! But I'll admit, AI seems to be pretty good at debugging, and it is really nice to have that tedium reduced. But...
:::{warning}
You may not be able to post proprietary code to a LLM, as it effectively becomes public (part of the training data) the moment you type it in.
:::
And if you are writing something brand new, AI might not know what you are going for anyway! How will you debug? 

Debugging has basically two flavors:
- The code is producing an error.
- The code is NOT producing an error, but is behaving unexpectedly.

The strategies mentioned here can often be used in either case. 

## The code is producing an error

it usually will tell you the line number where things are going wrong. "Run-time error" means it is running for infinite time... probably it is stuck in an infinite loop. "Array indices must be positive integers or logical values" means you are somewhere calling an array with something like x(1.5), but there is no "one-point-fifth index". Since MATLAB calls functions with the same syntax, e.g. f(1.5) give a value of 1.5 to a function f (which is legal), it might take some thoughtfulness.


## The code is behaving unexpectedly/giving unexpected results

### Rubber-duck debugging

... is a classic tool used by code writers. The mere act of explaining a code in natural language is often enough to reveal where the mistake is.

### Check that a line of code does what you expect

An example: you are trying to generate a list of numbers 1, 2, 3, ... , 30. Your code includes x=[1,30], but is not working. Paste x=[1,30] into the Command Window, don't suppress with ;, and see that the output is actually: 1 30. Amend your code as necessary!


### Using pencil and paper

We will be completing problems in class. An example: you might be asked to compute, by hand, the result after one iteration of an algorithm. You will then be able to compare that against your code, e.g. by using a debug mode to pause at the end of each loop, or perhaps with a bit of code like 
::::{tab-set}
:::{tab-item} MATLAB
```MATLAB
k=2;
N=50;
S=0;
for n=1:N
    S=S+1/n^k;
    if n==1:
        print(S)
    end
end
print(S)
```
:::
:::{tab-item} python
```python
f=
```
:::
:::{tab-item} julia
```julia
f=
```
:::

::::











Plot the function to make sure things make sense. Basic plotting is illuminating. Maybe you are trying to find a root for f(x) = cos(x)+3. Do this:
x=0:0.01:8*pi;
y=cos(x)+3;
plot(x,y)
... will get you a quick plot, and you will see that the function does not have any zeros. 
Print something every time through a loop.
Don't suppress the error value. Is it Inf? Is it 0? It probably shouldn't be.
Add a counter to the while loop to see how many times it goes through. If it is just once, probably there is an issue. If it reaches 99999, also probably an issue.
If you call another function, print the value (i.e., don't suppress the output of the line with a ;). If it is giving you the same value each time, maybe there is an issue.
Print the output of an iterative scheme. It should probably be converging, so you might see: 0.9951, 0.9231, 0.9132, 0.9101, ... . If you see 0.9951, -11.9541, 31.1192, -55.2901, you are in danger.
If you are trying to generate a location for a zero or of a maximum, or whatever... you've got your output and you know the function. In your Command Window, See if f(x_out) is close to zero (if that is what you are trying to find). If you are hoping for a max, see if f(x_max+0.001)< f(x_max) and f(x_max-0.001)< f(x_max). (And, no, you don't have to worry about the logicals <>, just read the outputs.
To access MATLAB's debug mode, click the line number in your function/script that you would like to stop at. Then call the function as normal. If you'd like to keep going, click "Continue" in the top menu. Debug mode is maybe most useful when trying to see what is happening each time through a loop (so, you would choose the "end" of the loop as your stopping points). Some things to look out for:
Are your variables expected to be scalars or arrays? Are they actually scalars or arrays? Are your values expected to be positive? Are they positive?
Are your values even updating? Maybe you forgot to reset something's value each time through!
Did a variable find its way to infinity, zero, or an inappropriate negative number within a few times through the loop? Is that concerning?
We might expect a convergence metric to get smaller each time through the loop. Is it actually getting smaller?