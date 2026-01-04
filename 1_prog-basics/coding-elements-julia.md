# Necessary Coding Elements -- Julia

If you are interested in computational science, you might find Julia to be an interesting language. It looks like MATLAB but... well maybe you'd like to read this: [Julia: A Fresh Approach to Numerical Computing](https://arxiv.org/abs/1411.1607).

The considerations outlined in that paper are not important to MCEN 3030, but 



I only recommend Julia if you are genuinely interested in computer programming and can see yourself having a career in computational science. I think that anyone could succeed with this language, but a student who is less interested in computational science will probably be more inclined to find it frustrating and may find direct practice with MATLAB/Python, which are more common languages, more valuable.

However, if you understand why compiled languages are going to run faster


A few frustrations I have encountered (and most of these are likely just because I am more used to MATLAB/Python, which are more user-friendly):
- ```y = x``` will assign ```y``` to the same memory location as ```x```, which means that changing ```x[1]``` also changes ```y[1]```. If you need to make a genuine copy that can be independently modified: ```y=copy(x)```.
- Meanwhile, slicing an array makes a copy automatically. ```z=x[2:end]``` creates an independent array, ```z``` that is not tied to ```x```.


- Julia is famous for "multiple dispatch" which is something we will not really be concerned about in this class. However, you may independently explore this.


## Additional resources/readings

https://github.com/brenhinkeller/JuliaAdviceForMatlabProgrammers


[Julia: A Fresh Approach to Numerical Computing](https://arxiv.org/abs/1411.1607)


## Functions

Rules for Julia functions:
- Definition looks like 
- Instead of a ```return``` statement, one can use the "implicit output": the last variable given a value in the function. I am suspicous of this and recommend a ```return out1,out2``` before the ```end```. It is kind of clumsy-looking to have both though.

## Creating vectors/matrices/arrays

## Indexing: Accessing and Modifying Elements

## Doing math with them






## Conditional Statements


## Loops


## Miscellaneous


## Some common motifs






## Functions

