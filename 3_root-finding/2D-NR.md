# Newton-Raphson Method (2+D)

**Author:** Jeremy Koch<sup>1,2</sup> \

## Motivation

We may have a situation in which a system of two variables needs solving:
\begin{align}
f(x,y)&=0\\
g(x,y)&=0.
\end{align}

## Idea

It is the same story as 1D Newton-Raphson.

## Derivative

With our linearized function $f(x) \approx f(x_0)+ f'(x_0)(x-x_0)$, we can set $f(x) =0$ and rearrange to solve for $x$, the better guess for the root. Generalizing the algorithm:

$$ x_{i+1} = x_{i} - \frac{f(x_i)}{f'(x_i)} $$

where, during our first iteration, $i=0$.



## Looking Forward

The process of finding a matrix inverse is not mathematically trivial, though with the convenience of modern programming it sure seems to be that way. The next unit of the class will focus on problems that can be frames via matrix equations.

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