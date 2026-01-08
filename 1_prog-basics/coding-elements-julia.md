# Necessary Coding Elements -- Julia

If you are interested in computational science, you might find Julia to be an interesting language. Maybe you'd like to read this: [Julia: A Fresh Approach to Numerical Computing](https://arxiv.org/abs/1411.1607).

The considerations outlined in that paper are not important to MCEN 3030, but, if you have the appetite for it, you could spend MCEN 3030 building up some relevant experience in some basic tasks, and then can expand to more cutting-edge things on the side or after the course has concluded.

There are a lot of extra considerations with Julia that will make it challenging for those who are unfamiliar with the vocabulary -- you will need to be more careful with data types and variable scope, as examples. For this reason, I think I'd like to chat with you before you commit to this language. Everyone in the class could use it and would be fine, but I just want to make sure the juice is worth the squeeze (for your situation). That being said, I would be really interested to get some more experience in this langauge with a handful of brave students.

I will create the same collection of ideas here but want to make sure SOMEONE chooses Julia before I spend the time to do it!


<!-- A few frustrations I have encountered (and most of these are likely just because I am more used to MATLAB/Python, which are more user-friendly):
- ```y = x``` will assign ```y``` to the same memory location as ```x```, which means that changing ```x[1]``` also changes ```y[1]```. If you need to make a genuine copy that can be independently modified: ```y=copy(x)```.
- Meanwhile, slicing an array makes a copy automatically. ```z=x[2:end]``` creates an independent array, ```z``` that is not tied to ```x```. -->


<!-- - Julia is famous for "multiple dispatch" which is something we will not really be concerned about in this class. However, you may independently explore this. -->


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

