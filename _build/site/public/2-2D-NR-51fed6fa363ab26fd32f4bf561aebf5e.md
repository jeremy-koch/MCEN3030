# Newton-Raphson Method (2D)

**Author:** Jeremy Koch<sup>1,2</sup> \

## Motivation

We may have a situation in which a system of two variables needs solving:

\begin{equation}
a=b
\end{equation}

## Idea

The idea is this: we have a function for which we are seeking the location where $f(x)=0$, and we have a guess for the solution $x_0$, called the seed. We linearize the function around $x_0$ and trace the resulting line back to $y=0$. If our guess is decent and the function is not too erratic, it is likely that the associated $x$-location (call it $x_1$) is a better estimate of the root than our initial guess. We repeat the process, now linearizing around $x=x_1$ and tracing the line back to find an even better estimate, $x_2$, and then maybe we use that too get an even better estimate, etc.~etc.~etc., until we have acceptably converged. 

## Derivative

With our linearized function $f(x) \approx f(x_0)+ f'(x_0)(x-x_0)$, we can set $f(x) =0$ and rearrange to solve for $x$, the better guess for the root. Generalizing the algorithm:

$$ x_{i+1} = x_{i} - \frac{f(x_i)}{f'(x_i)} $$

where, during our first iteration, $i=0$.





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