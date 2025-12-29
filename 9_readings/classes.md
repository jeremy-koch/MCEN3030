# Classes/Methods

**Author:** Jeremy Koch

## Motivation

For those 

This will mostly be written through the prism of Python, though it should be understandable regardless of your 

## What is object-oriented programming?

It's a paradigm 






This seems really mundane, bordering on obvious: ```x``` is a list, a list is an object, we are all part of this universe, fine. The neat thing is that classes of objects can carry with them special properties called "methods" that are succinct ways.

## Methods

In base Python there is a "class" known as a list. An example: ```x=[5, 9, 'red']```... it's just a collection of data, not necessarily of the same type. Lists have associated with them [several methods](https://www.w3schools.com/python/python_ref_list.asp), e.g. ```.pop()```, in which the last element of the list is dropped:
```python
x=[5, 9, 'red']
print(x)
x.pop()
print(x)
```
... will show you that ```x``` has been changed from its original definition: it is now just ```[5,9]```.

## Defining new classes



## Everything is an object

Python makes more sense now that I learned this, even if practically it did not change much in how I write. As an example: we can create an anonymous function in python with
```python
f_line=lambda x,a,b: a+b*x
```
and then can pass that function into another function, e.g. the ```curve_fit``` function from ```scipy.optimize```:
```python
fits, _ = curve_fit(f_line, x_data, y_data)
```
I knew this already, I did it during my PhD research. However, newly wise me: "Oh, that is because an anonymous function is an object." Roll your eyes if you want, it was satisfying to have this deeper understanding!

## Just Python?

MATLAB

Julia is the outlier and is not thought of as a "OOP" language, though it does have features of OOP and [ObjectOriented.jl](https://github.com/Suzhou-Tongyuan/ObjectOriented.jl) brings more Python-like features into it. I haven't tried it though... to be honest, not always a useful thing to be worried about!





## A few useful examples

### fas

A neat thing: you and I can create new object types -- we don't just have to use the built-in ones. I'll give an example: there was a project in which I wanted to keep a record of when a variable was initialized. There are clumsy ways to do this, but an elegant way is to create a new "class" of objects that includes within it a "method" that records the start time. Here is a slightly simpler version of how I defined the class:
:::{aside}
A clumsy way: create a dictionary of initialization times, where the keys are the variable names. But then you have to carry around the dictionary...
:::
```python
class controller():  
    def __init__(self,T_target):
        self.start_time=time.time() # the time package was imported
        
    def time_elapsed(self):
        return time.time()-self.start_time

```
and then I could create a variable ```T=controller(T_target)``` such that the method ```time_elapsed()```, as in ```T.time_elapsed()```, would return the time elapsed since the variable was created. And the really cool thing: ```T``` was just another variable at this point: it could be passed into functions, it could be ...