# Newton-Raphson Method (1D)

**Author:** Jeremy Koch<sup>1,2</sup> \

## Motivation

The Newton-Raphson Method is another root-finding algorithm, though this one is called an "open" method because the search is not confined to a specific range. This has it's positives -- most notably, it converges more quickly than the bisection method -- and negatives -- it is not guaranteed to find a solution, even if one exists, and also might find the "wrong" solution.

## Idea

The idea is this: we start with a guess for the root, called the seed value, have some function $f(x)$ which we can linearize near a point $x=x_0$. We trace that line back to the $x$-axis (where $y=0$). As long 

The idea of the 
A function may be linearized by

$$ f(x) \approx f(x_0)




<!-- :::{aside}
https://en.wikipedia.org/wiki/Magnetic-core_memory
::: -->


<!-- ::::{tab-set}
:::{tab-item} MATLAB
```MATLAB
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
f=lambda x: x**2
```
:::

:::: -->