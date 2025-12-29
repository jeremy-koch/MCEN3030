# Root-Finding Methods Intro

**Author:** Jeremy Koch<sup>1,2</sup> \

## Motivation

Most of your work in traditional lecture classes involves pushing around equations until you can settle on something like:
\begin{equation}
    F = \frac{\pi}{2}\rho U^2 R^2.
\end{equation}
That is, you can usually "explicitly" solve for the variable you are interested using algebra. In practice, it doesn't always work out so neatly. A classic example is the Colebrook Equation, which is used to determine the pressure drop in pipe flow:
\begin{equation}
    \frac{1}{\sqrt{p}} = -2 \log\left(\frac{\epsilon/D}{3.7}+\frac{2.51}{\text{Re}\sqrt{p}}\right)
\end{equation}
Notice that $p$ appears both within the logarithm argument and outside the logarithm argument. This means it can't be solved for explicitly... i.e., you cannot arrive at $p=\text{something}$ where the "something" is fundamental mathematical functions like $\exp$, $\log$, etc. To solve these problems, engineers have traditionally looked at a chart -- the Moody Diagram. But we can also use "root-finding methods" to solve algebraic equations.
:::{aside}
The Colebrook equation is usually written in terms of $f$, "the friction factor", instead of $p$, but I want to avoid confusion with the $f(x)$ below, which is just the standard "function of $x$".
:::

## Root-Finding Algorithms

This type of problem could be called "algebraic equation solving", but actually we need to use the special properties of zero in our algorithms. That is, we must examine an equation in the form $f(x)=0$.
:::{aside}
Any equation, $A(x)=B(x)$ can be turned into a root-finding problem by rearranging to $A(x)-B(x)=0$ and then working with $f(x)=A(x)-B(x)$. For example, with the Colebrook Equation, we might manipulate it to
\begin{equation}
    \frac{1}{\sqrt{p}} +2 \log\left(\frac{\epsilon/D}{3.7}+\frac{2.51}{\text{Re}\sqrt{p}}\right) =0
\end{equation}
:::

### Types of Root-Finding Methods

There are two classes of root-finding methods: 

"Bracketed" methods are called as such because you place a lower and upper limit on your search range. These have a few downsides in general:
- You must have some idea of where the root is located. (You could say it is like -999999 to 999999, but it would take a long time to arrive at the solution.)
- They tend to be slower to converge.
- 
However, at least if there is only one root within the brackets, it is guaranteed to find it.


"Open" methods are called as such because their search range is not limited. The downsides are:
- Not guaranteed to 

However, they can converge more quickly than bracketed methods. Additionally, the main one we will discuss (Newton-Raphson) can be implemented in higher dimensions -- it does not only work for $f(x)=0$, it also works for $f(x,y)=0$ with $g(x,y)=0$, and further, with $f(x,y,z)=0,g(x,y,z)=0,h(x,y,z)=0$.

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