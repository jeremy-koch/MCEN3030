# Necessary Coding Elements -- Overview

<!-- **Author:** Jeremy Koch<sup>1,2</sup> \ -->

This course is less about using built-in functions like ```fsolve``` and more about understanding the algorithms. Truthfully, nearly all of the necessary coding elements to write all the functions in this course appear on these pages -- indexing ```x[i]``` or ```x(i)```; ```if```, ```for```, ```while```; you'll need to do some space preallocation, maybe with something built-in called ```zeros```; might need to use the modulus function, e.g. to determine if a number is odd or even, maybe a little random-number generation... not much else.

:::{caution}
Don't stare at any of these lists in hopes of memorizing them. Instead, treat them as reference lists early in the semester, and after putting these commands into action a few times you will find that you indeed memorized a lot of them.
:::

Don't forget that you have the AI green-light for homework... asking "how do I make a for loop in julia" is a really reasonable prompt for Google or an LLM, akin to just looking it up on a reference list like this! (Much more [responsible](../0_details/responsible-AI.md) than just pasting the problem description and copying the result!)


[Necessary Coding Elements -- MATLAB](coding-elements-MATLAB.md)

[Necessary Coding Elements -- Python](coding-elements-python.md)

[Necessary Coding Elements -- Julia](coding-elements-julia.md)

In addition to basic commands like how to create an array, each of the above links describes scripts, functions, and "anonymous functions".

Script
: We will take this to mean a coding file with simple instructions that don't require much overhead. For example: make a list of numbers between 0 and 50, use them in a function, and print the results. This takes three lines of code in a ```*.m```, ```*.py```, or ```*.jl``` file... no need for any formal "main function" declarations, just go through the steps in that script, in order. For our purposes, MATLAB, Python, and Julia are scripting languages, though that label is controversial for Julia because it is compiled.


Function
: These turn inputs into outputs according to a set of rules. Functions require a formal declaration, the structure of which is basically the same in all languages: give a function name, input variables, and return the outputs. We "call" functions from scripts or other functions.


Anonymous Function
: MATLAB, Python, and Julia all have a way of writing small functions that are not stored under a traditional function name (hence the moniker "anonymous"). They are still stored under a variable name. When part of a project's foundational architecture, this type of function definition is discouraged (one reason: it makes tracing errors difficult because the functions are not named in the error messages). However, within scripting languages, it is often a really nice tool to create an equation function for use in our algorithms like $f(x) = \ln{(\sin(x))}$. As an example: ```f=@(x) log(sin(x))``` (in MATLAB). You can then pass ```f``` as an argument into a function!




## Some common motifs

Don't "hard-code" in numbers if you can avoid it! It will make your code more flexible, readable, and easier to debug. For example, in MATLAB:

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